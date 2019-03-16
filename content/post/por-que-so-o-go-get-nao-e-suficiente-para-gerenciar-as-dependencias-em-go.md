+++
date = "2016-06-21"
title = "Por que só o go get não é suficiente para gerenciar as dependências em Go?"
tags = ["golang"]
+++

A linguagem Go tem uma gama de CLIs que facilitam a vida do desenvolvedor, uma das mais usadas com toda certeza é o `get`.

```bash
go get <url do pacote sem o protocolo>
```

O `get` é responsável por baixar os pacotes, bibliotecas que nossos projetos em Go, ele utiliza controle de versão para baixar os pacotes, então para usarmos o `get` além do Go precisamos ter algum sistema de controle de versão, como por exemplo o `git`, instalado em nossa máquina.

Isso a primeira vista parece gênial, o nosso código Go que está em um github ou em qualquer outra plataforma de controle de versão já está disponível para o uso da comunidade e a recíproca é verdadeira!

Quando executamos o comando `get` em nossa máquina ele realiza o clone do repositório em nosso `$GOPATH` e quando quisermos é possível atualizar o repositório executando o mesmo commando que executamos anteriormente passando o paramêtro `-u`.

```bash
go get -u <url do pacote sem o protocolo>
```

Nosso projeto projeto não utiliza somente a biblioteca padrão do Go, usa também bibliotecas como o [Gizmo](https://github.com/NYTimes/gizmo) e também uma base de testes bem grande, por isso usamos o [Travis CI](https://travis-ci.com) para rodar nossos testes a cada commit no Github para garantir que tudo está funcionando a cada alteração que fazemos.

O Travis cria um novo container, com o Go e todas as nossas dependências a cada commit, resumindo ele faz executa o `go get` para todas as nossas dependências a cada commit, e se alguma biblioteca fizer alguma atualização que quebre compatibilidade nossos testes vão falhar, nosso build vai quebrar, e agora?

Alterar nosso código? Deixar de usar bibliotecas da comunidade e usar só a padrão fornecida pelo Go, já que o google garante a [compatibilidade na vesão 1.x](https://golang.org/doc/go1compat)?

Calma lá, não precisamos fazer nada disso, podemos usar ferramentas como o [Godep](https://github.com/tools/godep) que soluciona para nós esse tipo de problema.

Vou explicar o que o `Godep` faz em linhas gerais e entro com mais detalhes nele em um próximo post.

O Godep básicamente guarda o hash o commit que usamos de cada biblioteca que usamos e quando vamos executar um comando, como por exemplo `godep go test ./...` e lê volta o commit no repositório de cada biblioteca para o commit que usamos para depois executar o `go test`.

Espero que tenham gostado e até o próximo post.