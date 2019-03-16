+++
date = "2017-02-12"
title = "Gerando chave SSH com Go"
tags = ["golang"]
+++

O post de hoje será diferente será um tutorial de como gerar uma chave SSH usando apenas Go.

O pessoal da própria linguagem Go criou um package que nos auxilia nas operações com SSH 
o `golang.org/x/crypto/ssh`, mas esse package não está na stdlib da linguagem então 
precisamos baixar usando o `go get`.

```bash
go get -u golang.org/x/crypto/ssh
```

Para gerar uma chave SSH publica, a que usamos para nos conectar em nossos servidores 
ou se conectar aos repositórios do Github, precisamos antes gerar uma chave privada, 
pois essa chave publica é gerada a partir de uma chave privada.

Essa chave privada pode ser de quantos bits quisermos, a quantidade de bits mais usada 
é `4096`, essa é a quantidade de bits recomendada pelo Github, para gerarmos a chave de 
conexão com Github.

Então vamos lá gerar nossa chave privada:

```go
func generatePrivateKey(bits int) (privateKey *rsa.PrivateKey, err error) {
	privateKey, _ = rsa.GenerateKey(rand.Reader, bits)
	privateKeyDer := x509.MarshalPKCS1PrivateKey(privateKey)
	privateKeyBlock := pem.Block{
		Type:    "RSA PRIVATE KEY",
		Headers: nil,
		Bytes:   privateKeyDer,
	}
	privateKeyPem := pem.EncodeToMemory(&privateKeyBlock)
	fmt.Println("PRIVATE KEY:", string(privateKeyPem))
	return
}
```

Agora que já temos nossa chave privada podemos gerar a publica a partir dela.

Então vamos gera-lá:

```go
func generatePublicKey(privateKey *rsa.PrivateKey) (err error) {
	publicKey := privateKey.PublicKey
	pub, _ := ssh.NewPublicKey(&publicKey)
	fmt.Println("PUBLIC KEY:", string(ssh.MarshalAuthorizedKey(pub)))
	return
}
```

A função `ssh.MarshalAuthorizedKey` coloca a nossa chave no padrão usado pelo `OpenSSH`, 
que é o padrão aceito pelo Github, Digital Ocean e muitos outros lugares que aceitam 
conexão via SSH.

A nossa chave SSH está pronta para uso. Com isso terminamos o tutorial espero que tenham 
gostado. Todo o código para este tutorial se encontra em meu [Github](https://github.com/felipeweb/blog-posts/tree/master/ssh), Abraços e até a proxima.