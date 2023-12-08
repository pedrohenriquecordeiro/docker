# Imagem Docker

Uma imagem Docker é um arquivo de armazenamento que contém tudo o que é necessário para executar uma aplicação, incluindo o código, as bibliotecas, as configurações e o sistema operacional.

Um contêiner Docker é uma instância de uma imagem Docker. Os contêineres são executados no kernel do sistema operacional hospedeiro, mas são isolados do sistema operacional hospedeiro e de outros contêineres.

Um containner executa uma imagem.

*  Dockerfile
Um Dockerfile é um script de texto que contém uma série de instruções que são usadas para construir uma imagem Docker. 
Essa imagem é então usada para criar contêineres, que são instâncias executáveis de uma aplicação junto com seu ambiente e dependências. 
O Dockerfile descreve passo a passo como a imagem deve ser configurada, quais pacotes instalar, quais comandos executar e como configurar o ambiente de execução.

```DockerFile

# Usamos uma imagem base do Ubuntu 20.04
FROM ubuntu:20.04

# Autor do Dockerfile (opcional)
LABEL maintainer="Seu Nome <seu@email.com>"

# Atualiza os repositórios e instala algumas dependências
RUN apt-get update && \
    apt-get install -y \
        python3 \
        python3-pip

# Define o diretório de trabalho dentro do contêiner
WORKDIR /app

# Copia o conteúdo do diretório local para o diretório de trabalho
COPY . /app

# Instala as dependências do projeto usando o pip
RUN pip3 install -r requirements.txt

# Expõe a porta 80 para o mundo externo
EXPOSE 80

# Define a variável de ambiente de execução
ENV APP_ENV production

# Comando a ser executado quando o contêiner iniciar
CMD ["python3", "app.py"]

```



## Lista de Comandos

*  Cria a imagem conforme o Dockerfile ( ja deve ter sido criado )
```bash  
docker build -t nome_image:tag_image [path_projeto]
```
```bash  
docker build -t nome_image:tag_image . ( se o comando estiver sendo executado dentro da pasta onde está o Dockerfile)
```

*  Rodar a imagem em um containner
```bash  
docker run [id_image]
```
```bash  
docker run [nome]:[tag]
```

*  Lista as imagens
```bash  
docker images
```

*  Baixa imagem do Hub e salva no cache do pc (criar as novas imagens derivadas se torna muito mais rapidas )

```bash  
docker pull python:3
```

*  Nomea e atribui uma tag ( geralmente usado para determinar a versao) a uma image

```bash  
docker tag [id_image] nome_image:tag_image
```

*  Remover images
```bash  
docker rmi [id_image]
```
```bash  
docker rmi [nome_image:tag_image]
```
```bash  
docker rmi -f [id_image]
```

*  Remover images e containner e networks que não estao sendo utilizados

```bash  
docker system prune
```








---------------------------------------------------------------------------------------------------------------------------
# Container
**Docker** é uma plataforma que permite criar e executar aplicativos em **containers** isolados. 
Um container é uma espécie de caixa autônoma que contém todos os componentes necessários para um aplicativo funcionar, como código, bibliotecas e configurações. 
A **imagem** é um modelo pré-fabricado que serve como base para criar os containers, como um plano de construção que especifica os materiais e as instruções necessárias. 
Dessa forma, é possível ter várias instâncias do mesmo aplicativo, cada uma em seu próprio container, garantindo isolamento e portabilidade.

  

## Lista de Comandos Utéis

*  Executa uma imagem chamada whalesay e chama o método cowsay passando uma string como parametro

```bash  
docker run docker/whalesay cowsay HelloWorld
```
O docker run executa a imagem e criar um novo container

  

*  Executa a imagem ubuntu em mode iterativo
```bash
docker run -it  ubuntu
```
  

*   Executa uma imagem em background (detached)
```bash
docker run -d nginx
```
  

*   Executa uma imagem e expoe uma porta (porta exposta para o localhost : porta do container)
```bash
docker run -d -p 80:80 nginx
```

*   Define um nome para container ( recebe um nome aleatorio se não passar )
```bash
docker run --name [nome-containner] [imagem]
```
  

*   Para a execução de uma imagem
```bash
docker stop [id_ou_nome_do_container]
```
  

*   Remove containners
```bash
docker -rm [id]
```
  

*   Remove containners que estao em execução ( force )
```bash
docker -rm [id] -f
```
  

*   reiniciar container que foi parado

O docker start reinicia o container com todos os paramentros passados na sua criacao (reinicia no modo detache)

```bash
docker start [id]
```

```bash
docker start -i [id]  ( reinicia no modo iterativo - no detache)
```

*   Mostra os containner que estão executando

```bash
docker ps
```

```bash
docker container ls
```
  

*   Mostra os containner que estao executando e os que ja foram executados

```bash
docker ps -a
```
  

*   Acessar logs de um container

```bash
docker logs [id]
```
  

*   Acessar logs de um container em modo continuo ( follow ) 
control + C to exit

```bash
docker logs -f [id]
```


*  Remove o containner depois do comando stop ( docker stop )


```bash
docker run --rm ubuntu
```


*  Copiar doc do containner

```bash
docker cp [nome_containner]:/app/main.py ./local/copy    ( do_containner_para_o_host)
```


*  Inspeciona o container

```bash
docker inspect [id_container]
```


*  Verificar os containers que estão sendo executados na maquina, mostrando uso de memoria, espaço, processamento ...

```bash
docker stats
```

---------------------------------------------------------------------------------------------------------------------------
# Docker HUB
O Docker Hub é uma plataforma em nuvem fornecida pelo Docker, que permite aos desenvolvedores compartilhar, armazenar e distribuir imagens de contêiner Docker. Ele atua como um repositório central para essas imagens, permitindo que os usuários compartilhem soluções prontas e pré-configuradas. Além disso, oferece recursos de automação para integração contínua e implantação contínua. 



* Enviar images para o Docker Hub

  *  Login pelo terminal no docker hub (autenticacao)
  ```bash
  docker login 
  ```* 
  *  Logout
  ```bash
  docker logout 
  ```

*  Envia imagem ( tem que criar o repositorio no docker hub antes do push  -> nome_usuario/nome_repositorio )
Na hora do build da imagem, devemos nomear a imagem no padrão do docker hub

```bash
docker build -t pedrojjesus/python_dask_image
```
```bash
docker push pedrojjesus/python_dask_image
```
*  Download da imagem
```bash 
docker pull pedrojjesus/python_dask_image
```
*  Upgrade da image ( a partir da tag ) - ( build local da imagem deve ser realizada antes, obviamente )
```bash 
docker build -t pedrojjesus/python_dask_image:v2
```
```bash 
docker push pedrojjesus/python_dask_image:v2
```


---------------------------------------------------------------------------------------------------------------------------
# Network
As redes no Docker são usadas para isolar contêineres, permitir que eles se comuniquem e controlar como eles se conectam à rede host ou a outras redes.

* # Tipos de Conexão

- Externa : permite a comunicação com uma API de um servidor remoto.
- Com o Host: permite a comunicação com a maquina que está executando o docker. Por default o docker usa o nome ```host.docker.internal``` para referenciar o host.
- Entre Containers : utiliza o driver bridge e permite a comunicação entre dois ou mais containers

* # Tipos de Drivers
- Bridge: default do Docker, utilizando quando containners precisam se conectar.
- Host: driver que permite a conexão entre o containner e o host (maquina que executa o docker).
- Macvlan: permite a conexão a um containner por um MAC adress.
- None: remove todas as conexão de rede de um containner.
- Pluguins: permite extensões de terceiros para criação de outras redes.



* Listando networks
```bash
docker network ls
```

* Criando networks ( cria do tipo brigge por default)
```bash
docker network create [name]
```

* Criando networks definindo o driver
```bash
docker network create -d macvlan [name] 
```

* Removendo network
```bash
docker network rm [name] 
```

* Removendo network  utilizadas
```bash
docker network prune+
```

* Conecta um containner a uma rede
```bash
docker network connect [name] [id_containner]
```

* Desconecta um containner de uma rede
```bash
docker network disconnect [name] [id_containner]
```

* Inspeciona uma rede
```bash
docker network inspect [name]
```





*  Para conectar containners
  - Executamos os containners e definimos a network que eles devem se conectar
  ```bash
  docker run --name containner_1 --network nome_rede nome_image
  ```
  ```bash
  docker run --name containner_2 --network nome_rede nome_image
  ```

Internamente a cada containner, para efetuar a comunicação, basta referenciar o nome do containner que se deseja conectar.





---------------------------------------------------------------------------------------------------------------------------
# Volume

Um volume no Docker é um recurso que possibilita o armazenamento e compartilhamento de dados entre contêineres e o sistema hospedeiro. 
Ele permite que informações sejam mantidas mesmo quando contêineres são criados ou **removidos**, sendo útil para armazenar dados como bancos de dados, arquivos de configuração e logs. 
Volumes proporcionam persistência de dados, compartilhamento entre contêineres, isolamento e melhor desempenho para armazenar grandes quantidades de dados. 

* # Volume Anônimo
- Os volumes anônimos são criados automaticamente pelo Docker quando você os solicita, mas não especifica um nome para eles.
- Eles são úteis para armazenar dados temporários.
- Os volumes anônimos são atribuídos a um contêiner específico e são destruídos quando o contêiner é removido.

- Exemplo de Uso:
  ```bash
  docker run -v /dir-volume [nome-id-imagem]

  
* # Volume Nomeado
- Volumes nomeados são volumes com um nome específico que você cria explicitamente e podem ser compartilhados entre diferentes contêineres.
- Eles persistem mesmo depois que os contêineres que os utilizam são interrompidos ou removidos, tornando-os ideais para armazenar dados persistentes.
- Volumes nomeados são criados usando o comando ```docker volume create``` ou são criados automaticamente quando você os vincula a um contêiner.

- Exemplo de Criação de Volume Nomeado:
  ```bash
  docker volume create [nome-do-volume]

- Exemplo de Uso com um Contêiner:
  ```bash
  docker run -v [nome-do-volume]:/dir-volume [imagem]
  

* # Bind Mount
- Bind mounts permitem que você monte um **diretório do host** diretamente em um containner.
- Eles são úteis para compartilhar dados entre o host e o contêiner, e qualquer alteração feita nos arquivos é refletida em ambos os lados.
- Em desenvolvimento, podemos utilizar o bind mount para atualizar em tempo real o projeto sem ter que refazer o build a cada atualização, bastando a gente colocar os arquivos do projeto no bind mount.
- Exemplo de Uso:
  ```bash
  docker run -v /dir-volume-host:/dir-volume-containner [imagem-do-containner]



* Podemos criar um volume também no Dockerfile
```Dockerfile
VOLUME ["/backup"]
```

* Listar os volumes nomeados e anônimos existentes
```bash
 docker volume ls
```

* Verifica os detalhes de um volume
```bash
 docker volume inspect [nome-volume]
```

* Remove um volume
```bash
 docker volume rm [nome-volume]
```
Se um volume estiver em uso por um containner, será gerado um erro.

* Remove todos os volumes que não estão sendo utilizados
```bash
 docker volume prune
```
- Para verificar se um containner esta atrelado a algum volume, podesse usar o **docker inspect**, na chave volume ou MOunt estara indicando ou não o caminho do volume


* # Volume de apenas Leitura
```bash
 docker run -v [nome-do-volume]:/dir-volume:ro [imagem]
```
```bash
 docker volume create [nome-do-volume]:ro 
```
(:ro read only)
