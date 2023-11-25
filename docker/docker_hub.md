O Docker Hub é uma plataforma em nuvem fornecida pelo Docker, que permite aos desenvolvedores compartilhar, armazenar e distribuir imagens de contêiner Docker. Ele atua como um repositório central para essas imagens, permitindo que os usuários compartilhem soluções prontas e pré-configuradas. Além disso, oferece recursos de automação para integração contínua e implantação contínua. 



#### Enviar images para o Docker Hub

### Login pelo terminal no docker hub (autenticacao)
```bash
docker login 
```
### Logout
```bash
docker logout 
```

### Envia imagem ( tem que criar o repositorio no docker hub antes do push  -> nome_usuario/nome_repositorio )
Na hora do build da imagem, devemos nomear a imagem no padrão do docker hub

```bash
docker build -t pedrojjesus/python_dask_image
```
```bash
docker push pedrojjesus/python_dask_image
```
### Download da imagem
```bash 
docker pull pedrojjesus/python_dask_image
```
### Upgrade da image ( a partir da tag ) - ( build local da imagem deve ser realizada antes, obviamente )
```bash 
docker build -t pedrojjesus/python_dask_image:v2
```
```bash 
docker push pedrojjesus/python_dask_image:v2
```
