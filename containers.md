**Docker** é uma plataforma que permite criar e executar aplicativos em **containers** isolados. Um container é uma espécie de caixa autônoma que contém todos os componentes necessários para um aplicativo funcionar, como código, bibliotecas e configurações. A **imagem** é um modelo pré-fabricado que serve como base para criar os containers, como um plano de construção que especifica os materiais e as instruções necessárias. Dessa forma, é possível ter várias instâncias do mesmo aplicativo, cada uma em seu próprio container, garantindo isolamento e portabilidade.

  

## Lista de Comandos Utéis

 ##### Executa uma imagem chamada whalesay e chama o método cowsay passando uma string como parametro

  

> docker run docker/whalesay cowsay HelloWorld

  

##### O docker run executa a imagem e criar um novo container

  

##### Executa a imagem ubuntu em mode iterativo

> docker run -it ubuntu

  

#####  Executa uma imagem em background (detached)

docker run -d nginx

  

#####  Executa uma imagem e expoe uma porta (porta exposta para o localhost : porta do container)

> docker run -d -p 80:80 nginx

  

#####  Define um nome para container ( recebe um nome aleatorio se não passar )

> docker run -d -p 80:80 --name nginx_server nginx

  

#####  Para a execução de uma imagem

> docker stop [id  ou  nome  do  container]

  

#####  Remove containners

> docker -rm [id]

  

#####  Remove containners que estao em execução ( force )

> docker -rm [id] -f

  

#####  reiniciar container que foi parado

#####  o docker start reinicia o container com todos os paramentros passados na sua criacao (reinicia no modo detache)

> docker start [id]


> docker start -i [id]  ( reinicia no modo iterativo - no detache)


#####  mostra os containner que estão executando

> docker ps

> docker container ls

  

#####  Mostra os containner que estao executando e os que ja foram executados

> docker ps -a

  

#####  Acessar logs de um container

> docker logs [id]

  

#####  Acessar logs de um container em modo continuo ( follow ) 
###### control+C to exit

> docker logs -f [id]



##### Remove o containner apos o comando stop ( eh removido apos o docker stop )


> docker run --rm ubuntu



##### Copiar doc do containner

> docker cp [nome_containner]:/app/main.py ./local/copy    ( do containner para o host)



##### Inspeciona o container

> docker inspect [id_container]



##### Verificar os containers que estão sendo executados na maquina, mostrando uso de memoria, espaço, processamento ...

> docker stats

