# devops-microsservicos

# Traefik como um Proxy Reverso para Containers do Docker

## Introdução

Um proxy reverso pode ser utilizado para executar vários containers no mesmo host do Docker mantendo um apenas um ponto de entrada para o mundo exterior (por exemplo, na porta 80 ou 443), ocultando a complexidade dos diferentes serviços por trás dele.

O [Traefik](https://traefik.io/) é um proxy reverso compatível com o Docker e possui um painel de monitoramento ou dashboard. Neste cenário o Traefik será utilizado para rotear solicitações para dois containers de aplicação web diferentes: um blog em um container [Wordpress](http://wordpress.org/) e seu banco de dados [MySQL](https://www.mysql.com/), e um container [Adminer](https://www.adminer.org/) para gerenciar o banco de dados. 

## Requisitos

Para aplicar o cenário proposto, é necessário o seguinte:

-   Um servidor Linux ou WSL2 no Windows.
- Git Instalado no servidor.
-  O Docker e Docker Compose instalados no servidor.
    

## 1 - Clonando o repositório

1.  Altere o diretório de trabalho atual para o local em que deseja ter o diretório clonado.
2. Clone o repostório.
```bash
$ git clone https://github.com/joederfmoura/devops-microsservicos.git
```

## 2 - Preparando e Executando o Traefik
Será criada uma rede do Docker para o proxy encaminhar o tráfego para os containers. A rede do Docker será necessária para conectar o traefik com aplicações que são executadas usando o Docker Compose. A rede será chamada de `web`.

````bash
$ docker network create web
````

Crie o container Traefik com este comando:

````bash
$ docker run -d \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $PWD/traefik.toml:/traefik.toml \
  -p 80:80 \
  -p 443:443 \
  -l traefik.frontend.rule=Host:monitor.localhost \
  -l traefik.port=8080 \
  --network web \
  --name traefik \
  traefik:1.7.2-alpine
````

Acesse o endereço http://monitor.localhost e explore o Dashboard. Use as credenciais u:`admin` p:`admin`


## 2 - Executando os containers

Execute o comando abaixo para executar os containers.
````bash
$ docker compose up -d
````

Pode levar alguns segundos para que as aplicações fiquem disponíveis para acesso. Seja paciente!

## 3 - Acessando as aplicaçoes

Use os endereços abaixo para acessar as aplicações pelo proxy

|Aplicação                |Endereço                          |Credenciais de Acesso                       |
|----------------|-------------------------------|-----------------------------|
|Dashboard do Traefik|http://monitor.localhost            |u: admin p: admin             |
|Blog          |http://blog.localhost            |         		   |
| DB Admin          |http://db-admin.localhost/|			servidor: `mysql` usuário: `root` senha: `password`		|


## Conclusão