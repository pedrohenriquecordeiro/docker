
 **Orquestração** é o ato de conseguir gerenciar e escalar os containers da 
nossa aplicação.
- Temos um serviço que rege sobre outros serviços, verificando se os 
mesmos estão funcionando como deveriam.
- Desta forma conseguimos garantir uma aplicação saudável e também que 
esteja sempre disponível.
- Alguns serviços: Docker Swarm, Kubernetes e Apache Mesos.


## Docker Swarm

Uma ferramenta do Docker para orquestrar containers.
- Permite escalar horizontalmente nossos projetos;
- Tem a facilidade que os comandos são muito semelhantes ao do Docker.
- Toda instalação do Docker já vem com Swarm, porém desabilitado.


### Conceitos fundamentais
- Nodes: é uma instância (máquina).
- Manager Node: Node que gerencia os demais Nodes.
- Worker Node: Nodes que trabalham em função do Manager.
- Service: Um conjunto de Tasks que o Manager Node manda o Work Node executar.
- Task: comandos que são executados nos Nodes.

### Iniciando o Swarm

Podemos iniciar o Swarm com o comando: ```docker swarm init```
- Em alguns casos precisamos declarar o IP do servidor com a flag: ```-- advertise-addr```.
- Isso fará com que a instância/máquina vire um Node.
- E também transforma o Node em um Manager.
