+++
date = "2019-03-17"
title = "Deployando seu site em Hugo no Github Pages com Circle CI"
tags = ["Devops"]
+++

Hoje vamos ver como automatizar o deploy de um site em Hugo no Github Pages com Circle CI, serão 2 passos o de gerar o site e o de fazer deploy.

## Definindo o workflow

```yaml
workflows:
  version: 2
  build:
    jobs:
      - build
      - deploy:
          requires:
            - build
          filters:
            branches:
              only: master
```

Além definir os 2 passos colocamos filtros para que o passo de deploy aconteça somente quando fizermos commit na branch master e se o passo de build finalizar com sucesso.

## Gerando o site

Vamos configurar o Circle CI para rodar o comando `hugo` para gerar o site no diretório `public` usando a imagem docker `cibuilds/hugo` e persista o diretório para usarmos no proximo passo.

```yaml
build:
    docker:
      - image: cibuilds/hugo
    steps:
      - checkout
      - run:
          name: Build site
          command: hugo
      - persist_to_workspace:
          root: ./
          paths: public
```

## Fazendo o deploy

Vamos configurar o Circle CI para rodar o comando `gh-pages`. Vamos instalar usando a imagem docker `circleci/node` e o `npm` e depois configurar o `git`.

```yaml
deploy:
    docker:
      - image: circleci/node
    steps:
      - checkout
      - attach_workspace:
          at: ./
      - run:
          name: Install and configure dependencies
          command: |
            sudo npm install -g gh-pages
            git config user.email "felipeweb.programador@gmail.com"
            git config user.name "felipeweb"
      - run:
          name: deploy site
          command: gh-pages --dotfiles --repo https://$GITHUB_TOKEN@github.com/felipeweb/felipeweb.dev.git --message "[skip ci] update site" --dist ./public
```

## Adicionando token do Github no Circle CI

Vamos acessar o [Circle CI](https://circleci.com/gh/felipeweb/felipeweb.dev/edit#env-vars) e adicionar a variável.

![](/img/circleci.png)

## Conclusão

No final temos o YAML abaixo:

```yaml
version: 2
jobs:
  build:
    docker:
      - image: cibuilds/hugo
    steps:
      - checkout
      - run:
          name: Build site
          command: hugo
      - persist_to_workspace:
          root: ./
          paths: public
  deploy:
    docker:
      - image: circleci/node
    steps:
      - checkout
      - attach_workspace:
          at: ./
      - run:
          name: Install and configure dependencies
          command: |
            sudo npm install -g gh-pages
            git config user.email "felipeweb.programador@gmail.com"
            git config user.name "felipeweb"
      - run:
          name: deploy site
          command: gh-pages --dotfiles --repo https://$GITHUB_TOKEN@github.com/felipeweb/felipeweb.dev.git --message "[skip ci] update site" --dist ./public
workflows:
  version: 2
  build:
    jobs:
      - build
      - deploy:
          requires:
            - build
          filters:
            branches:
              only: master
```

Espero que tenham gostado até a proxima!