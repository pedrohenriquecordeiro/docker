O Docker Compose é uma ferramenta que permite definir e gerenciar aplicativos Docker multi-container de forma mais fácil e eficiente. 
Ele permite que você defina, configure e execute várias imagens Docker como parte de uma única aplicação. 
Com o Docker Compose, você pode descrever a configuração de seus aplicativos em um arquivo YAML (geralmente chamado de "docker-compose.yml") e, em seguida, 
iniciar todo o aplicativo com um único comando.

```bash
docker-compose up
```

Exemplo de yaml

```yaml
version: '3.3' # Versão da especificação do Docker Compose que está sendo usada.

services:
  db: # Container de MySQL
    image: mysql:5.7 # Imagem Docker a ser usada para este serviço
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
