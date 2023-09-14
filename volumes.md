Um volume no Docker é um recurso que possibilita o armazenamento e compartilhamento de dados entre contêineres e o sistema hospedeiro. Ele permite que informações sejam mantidas mesmo quando contêineres são criados ou **removidos**, sendo útil para armazenar dados como bancos de dados, arquivos de configuração e logs. Volumes proporcionam persistência de dados, compartilhamento entre contêineres, isolamento e melhor desempenho para armazenar grandes quantidades de dados. 

#### Volume Anônimo

- Os volumes anônimos são criados automaticamente pelo Docker quando você os solicita, mas não especifica um nome para eles.
- Eles são úteis para armazenar dados temporários.
- Os volumes anônimos são atribuídos a um contêiner específico e são destruídos quando o contêiner é removido.

- **Exemplo de Uso**:
  ```bash
  docker run -v /dir-volume <nome-id-imagem>

#### Bind Mount (Montagem de Vínculo)


- Bind mounts permitem que você monte um diretório ou arquivo do sistema de arquivos do host diretamente em um contêiner.
- Eles são úteis para compartilhar dados entre o host e o contêiner, e qualquer alteração feita nos arquivos é refletida em ambos os lados.
- Bind mounts são ideais para desenvolvimento e depuração, pois facilitam o acesso a código e recursos do host no contêiner.

- **Exemplo de Uso**:
  ```bash
  docker run -v /caminho/no/host:/caminho/no/contêiner imagem-do-contêiner


#### Volume Nomeado

- Volumes nomeados são volumes com um nome específico que você cria explicitamente e podem ser compartilhados entre diferentes contêineres.
- Eles persistem mesmo depois que os contêineres que os utilizam são interrompidos ou removidos, tornando-os ideais para armazenar dados persistentes.
- Volumes nomeados são criados usando o comando ```docker volume create``` ou são criados automaticamente quando você os vincula a um contêiner.

- **Exemplo de Criação de Volume Nomeado**:
  ```bash
  docker volume create nome-do-volume


- **Exemplo de Uso com um Contêiner**:
  ```bash
  docker run -v <nome-do-volume>:/dir-volume imagem-do-contêiner


------------------------------------------------------------------------------------------------------------------------------------

Listar os volumes existentes
```bash
 docker volume ls
```

Para verificar se um containner esta atrelado a algum volume, podesse usar o **docker inspect**, na chave volume estara indicando ou não o caminho do volume

  

