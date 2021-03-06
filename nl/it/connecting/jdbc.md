---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Connessione programmatica con JDBC
{: #con_prog_jdbc}

Definisci una connessione tra un'applicazione Java™ e il database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prerequisiti

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedura

In ogni applicazione Java, specifica l'ID utente e la password includendo il metodo **DriverManager.getConnection** e una delle seguenti stringhe URL JDBC:

- Per una connessione con SSL:

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- Per una connessione senza SSL:

  `jdbc:db2://<host_name>:50000/BLUDB`


