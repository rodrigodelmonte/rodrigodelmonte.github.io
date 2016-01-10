---
layout: post
title:  "Transformando um datacenter em um único computador."
date:  2016-01-09 20:46:00
categories: cloud
---

Parece loucura mas é exatamente como o Google e o Twitter administram seus datacenters a **10 anos**, eles olham para o datacenter como se fosse um único computador. Basicamente eles aplicam um conceito chamado Warehouse Scale Machine.

**O que é Warehouse Scale Machine ou Datacenter as a Computer?**

A melhor maneira de explicar e dando exemplos então vamos lá.

Eu tenho 10 servidores bare metal com a seguinte configuração:

* 2 processadores de 6 cores,
* 64 GB de memoria.
* 1 TB de disco.

E agora se eu multiplicar a configuração a cima por 10 eu tenho a seguinte maquina:

* 20 processadores ou 120 cores !
* 640 GB de memoria.
* 10 TB de disco.

Além de unificar os recursos de hardware em um super servidor, esse modelo é responsável por distribuir as aplicações pelo cluster de servidores, garantindo que a servidor onde a tarefa irá rodar possua os requisitos de hardware que a aplicação precisa. Esse modelo é capaz de trabalhar com aplicações que tem longo tempo de vida, mais conhecidas como serviços, rs. Se um serviço deve rodar em 3 servidores do cluster e um servidor vir a falhar, o orquestrador encontra outra servidor disponivel no cluster para esse serviço.

Nós sempre escutamos ao longo dos anos que um servidor deve possuir apenas uma aplicação rodando. Esse modelo vai na contra mão e diz para colocar todos os tipos de aplicações no mesmo super servidor, porém as aplicações devem ser encapsuladas em containers assim essa camada garante o isolamento do processo.

Ter 3 aplicações consumindo 90 % da carga de um servidor é bem mais eficiente e barato do que ter, 3 servidores cada um com 1 aplicação e apenas 30% da carga sendo consumida por servidor. Porém você deve distribuir as aplicações em 2 ou mais servidores, ou seja, se usarmos mais 1 servidor para o exemplo acima nós estamos garantimos a resiliência das 3 aplicações e ainda assim economizamos um servidor.

Esse modelo faz todo o sentido quando vamos trabalhar com cloud computing uma vez que somos cobrados pelas horas de uso do hardware, ou seja, pagar 40$/mês em uma instância que usou 10% dos recursos para hospedar 1 aplicação fez você dispersar 36$/mês! Outro motivo a é lei de Murphy que diz "Qualquer coisa que possa correr mal, ocorrerá mal, no pior momento possível" e usando Cloud ou não você sempre deve se lembrar disso. Esse modelo garante que se uma instância falhar e  perder um serviço, o serviço pode ser ligado em outra instância automaticamente causando o minimo impacto possível.

As tecnologias Docker, Mesos, Kubernetes, Docker Swarm, AWS ECS, Consul e Etcd quando usadas em conjunto aplicam os conceitos acima de Datacenter as a Computer! Se for trabalhar com Cloud trabalhe com isso!

Onde buscar mais informações sobre essas tecnologias:

[Docker](https://www.docker.com/) - Projeto open-source para criação de containers.

[Mesos](http://mesos.apache.org/) - Projeto open-source mantido pela Apache Foundation para criação de clusters e orquestração de containers.

[Kubernetes](http://kubernetes.io/) - Projeto open-source criado pelo Google para criação de clusters e orquestração de containers.

[AWS ECS](https://aws.amazon.com/pt/ecs/) - Serviço da Amazon Web Services para criação de clusters e orquestração de containers.

[Consul](https://www.consul.io/) - Projeto open-source criado pela [Hashcorp](https://hashicorp.com/) para implementação de Service Discovery.

[Etcd](https://coreos.com/etcd/) - Projeto open-source criado pela [Coreos](https://coreos.com/)  para implementação de Service Discovery. [Coreos](https://coreos.com/) também criou um tipo de container chamado [rkt](https://github.com/coreos/rkt) para concorrer com o Docker.

Leituras recomendadas caso você tenha se interessado pelo o assunto:

* [Post Wired como o Google construiu seus datacenters](http://www.wired.com/2012/10/ff-inside-google-data-center/)
* [Paper The Datacenter as a Computer](http://www.morganclaypool.com/doi/pdf/10.2200/S00516ED2V01Y201306CAC024)
* [Paper Mesos](https://www.usenix.org/legacy/event/nsdi11/tech/full_papers/Hindman_new.pdf)
* [Paper Google Borg](http://static.googleusercontent.com/media/research.google.com/pt-BR//pubs/archive/43438.pdf)
* [Airbnb é um dos maiores cases ao lado do Twitter usando Mesos](https://www.youtube.com/watch?v=GfpGmhZwaoM)

A imagem abaixo representa o que aconteceu na minha cabeça quando li o post da [Wired](http://www.wired.com/2012/10/ff-inside-google-data-center/) e me fez ter interesse pelo assunto!

![Bomb](https://i.ytimg.com/vi/Z6_eXfssseo/maxresdefault.jpg)
