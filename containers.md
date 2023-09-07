**Docker** é uma plataforma que permite criar e executar aplicativos em **containers** isolados. Um container é uma espécie de caixa autônoma que contém todos os componentes necessários para um aplicativo funcionar, como código, bibliotecas e configurações. A **imagem** é um modelo pré-fabricado que serve como base para criar os containers, como um plano de construção que especifica os materiais e as instruções necessárias. Dessa forma, é possível ter várias instâncias do mesmo aplicativo, cada uma em seu próprio container, garantindo isolamento e portabilidade.

  

## Lista de Comandos Utéis

### Executa uma imagem chamada whalesay e chama o método cowsay passando uma string como parametro

```bash  
docker run docker/whalesay cowsay HelloWorld
```
O docker run executa a imagem e criar um novo container

  

### Executa a imagem ubuntu em mode iterativo

```bash
docker run -it ubuntu
```
  

###  Executa uma imagem em background (detached)

```bash
docker run -d nginx
```
  

###  Executa uma imagem e expoe uma porta (porta exposta para o localhost : porta do container)

```bash
docker run -d -p 80:80 nginx
```
  

###  Define um nome para container ( recebe um nome aleatorio se não passar )

```bash
docker run -d -p 80:80 --name nginx_server nginx
```
  

###  Para a execução de uma imagem

```bash
docker stop [id_ou_nome_do_container]
```
  

###  Remove containners

```bash
docker -rm [id]
```
  

###  Remove containners que estao em execução ( force )

```bash
docker -rm [id] -f
```
  

###  reiniciar container que foi parado

###  o docker start reinicia o container com todos os paramentros passados na sua criacao (reinicia no modo detache)

```bash
docker start [id]
```

```bash
docker start -i [id]  ( reinicia no modo iterativo - no detache)
```

###  mostra os containner que estão executando

```bash
docker ps
```

```bash
docker container ls
```
  

###  Mostra os containner que estao executando e os que ja foram executados

```bash
docker ps -a
```
  

###  Acessar logs de um container

```bash
docker logs [id]
```
  

###  Acessar logs de um container em modo continuo ( follow ) 
#### control + C to exit

```bash
docker logs -f [id]
```


### Remove o containner apos o comando stop ( eh removido apos o docker stop )


```bash
docker run --rm ubuntu
```


### Copiar doc do containner

```bash
docker cp [nome_containner]:/app/main.py ./local/copy    ( do_containner_para_o_host)
```


### Inspeciona o container

```bash
docker inspect [id_container]
```


### Verificar os containers que estão sendo executados na maquina, mostrando uso de memoria, espaço, processamento ...

```bash
docker stats
```
