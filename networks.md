As redes no Docker são usadas para isolar contêineres, permitir que eles se comuniquem e controlar como eles se conectam à rede host ou a outras redes.

#### Tipos de Conexão

- Externa : permite a comunicação com uma API de um servidor remoto.
- Com o Host: permite a comunicação com a maquina que está executando o docker. Por default o docker usa o nome ```host.docker.internal``` para referenciar o host.
- Entre Containers : utiliza o driver bridge e permite a comunicação entre dois ou mais containers

#### Tipos de Drivers
- Bridge: default do Docker, utilizando quando containners precisam se conectar.
- Host: driver que permite a conexão entre o containner e o host (maquina que executa o docker).
- Macvlan: permite a conexão a um containner por um MAC adress.
- None: remove todas as conexão de rede de um containner.
- Pluguins: permite extensões de terceiros para criação de outras redes.

-----------------------------
Listando networks
```bash
docker network ls
```

Criando networks ( cria do tipo brigge por default)
```bash
docker network create [name]
```

Criando networks definindo o driver
```bash
docker network create -d macvlan [name] 
```

Removendo network
```bash
docker network rm [name] 
```

Removendo network  utilizadas
```bash
docker network prune+
```

Conecta um containner a uma rede
```bash
docker network connect [name] [id_containner]
```

Desconecta um containner de uma rede
```bash
docker network disconnect [name] [id_containner]
```

Inspeciona uma rede
```bash
docker network inspect [name]
```

-----------------------------

### Para conectar containners
- Executamos os containners e definimos a network que eles devem se conectar
```bash
docker run --name containner_1 --network nome_rede nome_image
```
```bash
docker run --name containner_2 --network nome_rede nome_image
```

Internamente a cada containner, para efetuar a comunicação, basta referenciar o nome do containner que se deseja conectar.



