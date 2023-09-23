## Up
O Docker Compose é uma ferramenta que permite definir e gerenciar aplicativos Docker multi-container de forma mais fácil e eficiente. 
Ele permite que você defina, configure e execute várias imagens Docker como parte de uma única aplicação. 
Com o Docker Compose, você pode descrever a configuração de seus aplicativos em um arquivo YAML (geralmente chamado de "docker-compose.yml") e, em seguida, 
iniciar todo o aplicativo com um único comando.

```bash
docker-compose up
```

docker-compose.yml

```yaml
version: '3.3' # Versão da especificação do Docker Compose que está sendo usada.

services:
  db: # Container de MySQL
    image: mysql:5.7 # Imagem Docker a ser usada para este serviço (
                     # (Você terar que buildar e seta um nome para sua imagem, se desejar utilizar uma imagem personalizada)
    volumes:
      - db_data:/var/lib/mysql # Monta um volume chamado "db_data" no diretório do MySQL para persistir os dados do banco de dados.
    restart: always # Define que o contêiner deve ser reiniciado sempre que parar ou falhar.
    environment:
      MYSQL_ROOT_PASSWORD: wordpress # Configuração de variáveis de ambiente para a senha do usuário root do MySQL e outros detalhes do banco de dados.
      MYSQL_DATABASE: wordpress
      MYSQL_USER: matheus
      MYSQL_PASSWORD: secret

  wordpress:
    depends_on: 
      - db  # Especifica que este serviço depende do serviço "db" (MySQL) e, portanto, o MySQL deve ser iniciado antes do WordPress.
    image: wordpress:latest # Imagem Docker para o serviço WordPress, usando a versão mais recente.
    ports:
      - "8000:80" # Mapeia a porta 8000 do host para a porta 80 do contêiner WordPress.
    restart: always 
    environment: 
      WORDPRESS_DB_HOST: db:3306 # Configuração de variáveis de ambiente para o WordPress, informando como se conectar ao banco de dados.
      WORDPRESS_DB_USER: matheus
      WORDPRESS_DB_PASSWORD: secret
      WORDPRESS_DB_NAME: wordpress

volumes:
  db_data: {} # Define um volume chamado "db_data" como vazio

```

----------------------
Executar o compose no mode detach
```bash
docker-compose up -d
```

Para o compose
```bash
docker-compose down
```

--------------------------
## Variaveis de Ambiente

Devemos evitar passar credencias diretamente em codigo, para isso temos a instrução env_file, que importa a credencias necessaria automaticamente a partir de path de um arquivo .env.

./config/db.env
```yaml
MYSQL_ROOT_PASSWORD=wordpress 
MYSQL_DATABASE=wordpress
MYSQL_USER=matheus
MYSQL_PASSWORD=secret
```

./config/wordpress.env
```yaml
WORDPRESS_DB_HOST=db:3306
WORDPRESS_DB_USER=matheus
WORDPRESS_DB_PASSWORD=secret
WORDPRESS_DB_NAME=wordpress
```
docker-compose.yml
```yaml
version: '3.3' # Versão da especificação do Docker Compose que está sendo usada.

services:
  db: # Container de MySQL
    image: mysql:5.7 # Imagem Docker a ser usada para este serviço
    volumes:
      - db_data:/var/lib/mysql # Monta um volume chamado "db_data" no diretório do MySQL para persistir os dados do banco de dados.
    restart: always # Define que o contêiner deve ser reiniciado sempre que parar ou falhar.
    env_file:
      - ./config/db.env # caminho do arquivo de credenciais

  wordpress:
    depends_on: 
      - db  # Especifica que este serviço depende do serviço "db" (MySQL) e, portanto, o MySQL deve ser iniciado antes do WordPress.
    image: wordpress:latest # Imagem Docker para o serviço WordPress, usando a versão mais recente.
    ports:
      - "8000:80" # Mapeia a porta 8000 do host para a porta 80 do contêiner WordPress.
    restart: always 
    env_file:
      - ./config/wordpress.env # caminho do arquivo de credenciais

volumes:
  db_data: {} # Define um volume chamado "db_data" como vazio

```

--------------------------
## Networks

O Compose cria redes brigde automaticamente para que os containners se comuniquem entre si. Porém pode existir situações que não queiramos que isso aconteça, para isso podemos explicitar no yaml, a criação de uma rede e quais containners irão se comunicar.

docker-compose.yml
```yaml
version: '3.3' # Versão da especificação do Docker Compose que está sendo usada.

services:
  db: # Container de MySQL
    image: mysql:5.7 # Imagem Docker a ser usada para este serviço
    volumes:
      - db_data:/var/lib/mysql # Monta um volume chamado "db_data" no diretório do MySQL para persistir os dados do banco de dados.
    restart: always # Define que o contêiner deve ser reiniciado sempre que parar ou falhar.
    env_file:
      - ./config/db.env # caminho do arquivo de credenciais
    networks:
      - backend # Monta uma rede e inclui esse containner

  wordpress:
    depends_on: 
      - db  # Especifica que este serviço depende do serviço "db" (MySQL) e, portanto, o MySQL deve ser iniciado antes do WordPress.
    image: wordpress:latest # Imagem Docker para o serviço WordPress, usando a versão mais recente.
    ports:
      - "8000:80" # Mapeia a porta 8000 do host para a porta 80 do contêiner WordPress.
    restart: always 
    env_file:
      - ./config/wordpress.env # caminho do arquivo de credenciais
    networks:
      - backend # Monta uma rede e inclui esse containner
      

volumes:
  db_data: {} # Define um volume chamado "db_data" como vazio
networks:
  backend:
    driver: bridge # Define o driver da rede
```

---------------------------

## Build de Imagem no Yaml
Podemos usar a instrução build no yaml que aponta o path do projeto da imagem. Dessa forma o compose irá realizar o build para gente.

docker-compose.yml
```yaml
version: '3.3' # Versão da especificação do Docker Compose que está sendo usada.

services:
  db: # Container de MySQL
    build: ./mysql/ # Path onde se encontra o projeto da imagem e o Dockerfile
    volumes:
      - db_data:/var/lib/mysql # Monta um volume chamado "db_data" no diretório do MySQL para persistir os dados do banco de dados.
    restart: always # Define que o contêiner deve ser reiniciado sempre que parar ou falhar.
    env_file:
      - ./config/db.env # caminho do arquivo de credenciais
    networks:
      - backend # Monta uma rede e inclui esse containner

  wordpress:
    depends_on: 
      - db  # Especifica que este serviço depende do serviço "db" (MySQL) e, portanto, o MySQL deve ser iniciado antes do WordPress.
    build: ./wordpress/ # Path onde se encontra o projeto da imagem e o Dockerfile
    ports:
      - "8000:80" # Mapeia a porta 8000 do host para a porta 80 do contêiner WordPress.
    restart: always 
    env_file:
      - ./config/wordpress.env # caminho do arquivo de credenciais
    networks:
      - backend # Monta uma rede e inclui esse containner
      

volumes:
  db_data: {} # Define um volume chamado "db_data" como vazio
networks:
  backend:
    driver: bridge # Define o driver da rede


```
