---

copyright:
  years: 2016,2018
lastupdated: "2018-01-03"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Prezzi
{: #pricing}

## Configurazione di base
Un servizio {{site.data.keyword.composeForRedis_full}} viene fornito con due nodi redis/sentinel, ognuno dei quali ha 256MB di memoria e 256MB di archiviazione, che equivale a 1 unità di risorse. Il servizio _include_ la replica e l'elevata disponibilità, per cui ogni unità e il prezzo per unità _include_ il costo delle risorse in entrambi i nodi.

La configurazione di base inoltre include un nodo sentinel dedicato per gestire la replica e un portale HAProxy per gestire le connessioni. Il nodo sentinel e il portale HAProxy hanno 64MB di memoria ognuno.

### Costo
La configurazione del servizio di base a un prezzo fissato. Consulta i tile del catalogo {{site.data.keyword.cloud_notm}} per i prezzi di base nella tua valuta locale. Ad esempio, il prezzo di base in dollari US è $13/mese.

## Opzioni di espansione
Se hai bisogno di ulteriore memoria per il tuo servizio, puoi aumentare le risorse assegnate in un rapporto 1:1 di archiviazione del disco per unità di memoria. Un'unità {{site.data.keyword.composeForRedis}} è composta da 256MB di archiviazione e 256MB di memoria e ogni unità e prezzo per unità _include_ il costo di incremento delle risorse su entrambi i nodi.

### Costo
Ogni unità aggiuntiva (256MB di archiviazione/256MB di memoria) ha un prezzo per unità, che viene elencato nella tua valuta corrente nel tile del catalogo {{site.data.keyword.cloud_notm}} per il servizio. In dollari US ogni unità aggiuntiva costa $13. Quando la dimensione _totale_ di tutti i tuoi servizi {{site.data.keyword.composeForRedis}} aumenta, il prezzo per unità diminuisce, come mostrato nella seguente tabella dei prezzi a livelli.

### Prezzi a livelli
Numero di unità|Prezzo per unità
----------|-----------
1 - 9 unità|prezzo per unità di base -- $13.00 USD/Unità
10 - 24 unità|10% di riduzione -- $11.70 USD/Unità
25 - 49 unità|20% di riduzione -- $10.40 USD/Unità
50 - 99 unità|30% di riduzione -- $9.10 USD/Unità
100 - 499 unità|40% di riduzione --$7.80 USD/Unità
500 - 999 unità|50% di riduzione -- $6.50 USD/Unità
1.000 - 4.999 unità|60% di riduzione -- $5.20 USD/Unità
5.000+ unità|70% di riduzione -- $3.90 USD/Unità
{: caption="Tabella 1. Prezzi a livelli di {{site.data.keyword.composeForRedis}}" caption-side="top"}

