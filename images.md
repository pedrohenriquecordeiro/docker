Uma imagem Docker é um arquivo de armazenamento que contém tudo o que é necessário para executar uma aplicação, incluindo o código, as bibliotecas, as configurações e o sistema operacional.


Um contêiner Docker é uma instância de uma imagem Docker. Os contêineres são executados no kernel do sistema operacional hospedeiro, mas são isolados do sistema operacional hospedeiro e de outros contêineres.


Um containner executa uma imagem.


## Lista de Comandos Utéis

##### Cria a iamgem conforme o Dockerfile ( ja deve ter sido criado )

  

```bash  
docker build [path do dockerfile]
```
```bash  
docker build . ( se o comando estiver sendo executado dentro da pasta onde está o Dockerfile)
```



##### Rodar a imagem em um containner


```bash  
docker run [id_image]
```
```bash  
docker run [nome]:[tag]
```


##### Lista as imagens


```bash  
docker images
```


##### Nomea a image no build


```bash  
docker build -t nome_image:tag_image . 
```



##### Baixa imagem do Hub e salva no cache do pc (criar as novas imagens derivadas se torna muito mais rapidas )


```bash  
docker pull python:3
```


##### Nomea e atribui uma tag ( geralmente usado para determinar a versao) a uma image


```bash  
docker tag [id image] nome_image:tag_image
```



##### Remover images

```bash  
docker rmi [id]
```
```bash  
docker rmi nome_image:tag_image
```
```bash  
docker rmi -f [id]
```


##### Remover images e containner e networks que não estao sendo utilizados


```bash  
docker system prune
```





