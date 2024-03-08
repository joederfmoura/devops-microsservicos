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

## 2 - Executando os containers

Execute o compando abaixo para executar os containers.
````bash
$ docker compose up -d
````

Pode levar alguns segundos para que as aplicações fiquem disponíveis para acesso. Seja paciente!

## 3 - Acessando as aplicaçoes

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

|Aplicação                |Endereço                          |Credenciais de Acesso                       |
|----------------|-------------------------------|-----------------------------|
|Dashboard do Traefik|http://monitor.localhost            |u: admin p: admin             |
|Blog          |http://blog.localhost            |         		   |
|Dashes          |http://db-admin.localhost/|					|


## Conclusão