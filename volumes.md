Um volume no Docker é um recurso que possibilita o armazenamento e compartilhamento de dados entre contêineres e o sistema hospedeiro. Ele permite que informações sejam mantidas mesmo quando contêineres são criados ou **removidos**, sendo útil para armazenar dados como bancos de dados, arquivos de configuração e logs. Volumes proporcionam persistência de dados, compartilhamento entre contêineres, isolamento e melhor desempenho para armazenar grandes quantidades de dados. 

#### Volume Anônimo
- Os volumes anônimos são criados automaticamente pelo Docker quando você os solicita, mas não especifica um nome para eles.
- Eles são úteis para armazenar dados temporários.
- Os volumes anônimos são atribuídos a um contêiner específico e são destruídos quando o contêiner é removido.

- Exemplo de Uso:
  ```bash
  docker run -v /dir-volume [nome-id-imagem]

  
#### Volume Nomeado
- Volumes nomeados são volumes com um nome específico que você cria explicitamente e podem ser compartilhados entre diferentes contêineres.
- Eles persistem mesmo depois que os contêineres que os utilizam são interrompidos ou removidos, tornando-os ideais para armazenar dados persistentes.
- Volumes nomeados são criados usando o comando ```docker volume create``` ou são criados automaticamente quando você os vincula a um contêiner.

- Exemplo de Criação de Volume Nomeado:
  ```bash
  docker volume create [nome-do-volume]

- Exemplo de Uso com um Contêiner:
  ```bash
  docker run -v [nome-do-volume]:/dir-volume [imagem]
  

#### Bind Mount
- Bind mounts permitem que você monte um diretório do host diretamente em um containner.
- Eles são úteis para compartilhar dados entre o host e o contêiner, e qualquer alteração feita nos arquivos é refletida em ambos os lados.
- Em desenvolvimento, podemos utilizar o bind mount para atualizar em tempo real o projeto sem ter que refazer o build a cada atualização.
- Exemplo de Uso:
  ```bash
  docker run -v /dir-volume-host:/dir-volume-containner [imagem-do-containner]


------------------------------------------------------------------------------------------------------------------------------------

Listar os volumes existentes
```bash
 docker volume ls
```

- Para verificar se um containner esta atrelado a algum volume, podesse usar o **docker inspect**, na chave volume ou MOunt estara indicando ou não o caminho do volume

  

