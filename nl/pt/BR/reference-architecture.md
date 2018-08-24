---
copyright:
  years: 2016,2018
lastupdated: "2018-06-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Arquitetura 
{: #architecture}

## Replicação

Um serviço {{site.data.keyword.composeForRedis_full}} usa o [Redis Sentinel](https://redis.io/topics/sentinel) para fornecer alta disponibilidade e monitoramento para seus bancos de dados. Cada serviço consiste em três nós de dados; os três executam o processo sentinel e dois executam o processo redis. Quando você seleciona uma região na qual o serviço é implementado, os três nós são distribuídos pelas zonas de disponibilidade da região e seus dados são replicados entre eles. Se um membro de dados se tornar inacessível, seu cluster continuará a operar normalmente.

## Criptografia de Disco

Todos os serviços do {{site.data.keyword.composeForRedis}} têm criptografia em repouso. Seus dados residem em servidores que possuem criptografia em nível de volume ativada. 

Como este {{site.data.keyword.composeForRedis}} é um serviço gerenciado, é possível que os operadores do {{site.data.keyword.cloud}} Compose vejam dados. Além da criptografia de disco, recomendamos que, se você estiver armazenando informações pessoais em seu banco de dados, as criptografe antes de armazená-las ou use extensões ou recursos para ativar a criptografia no próprio banco de dados. Embora esses métodos possam afetar a usabilidade ou o desempenho, é uma boa prática assegurar-se de que as informações pessoais sejam protegidas com criptografia.

## Auto-scaling

Os recursos são escalados automaticamente com base no uso total de memória dos bancos de dados do Redis. O armazenamento baseia-se em uma razão de RAM provisionada em 1:1. Esses recursos são empacotados como unidades.

O Auto-scaling foi projetado para responder às tendências de curto a médio prazo de seu banco de dados. A cada minuto, seu serviço será verificado e, se ele estiver sendo executado com pouca RAM, mais unidades serão alocadas para a implementação. 

O Auto-scaling não reduz a capacidade de implementações em que o uso de disco/memória foi reduzido. Os recursos provisionados para seus bancos de dados permanecerão para suas necessidades futuras ou até você reduzir a capacidade de sua implementação manualmente.
{: .tip}
