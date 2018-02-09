---
title: "Aktualisiert - Analyseplattformsystem für SQL Server-Dokumentation | Microsoft Docs"
description: "Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation, Analytics Platform System für Microsoft SQL Server."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: aps-pdw
ms.date: 02/03/2018
ms.openlocfilehash: 2ae6339897b52cd16ad3417cc218afe1df95ba2a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-analytics-platform-system-for-sql-server"></a>Neue und kürzlich aktualisierte: Analyseplattformsystem für SQLServer



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-12-03** &nbsp; - zu - &nbsp; **2018-02-03**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Analyseplattformsystem für SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


***Dieses Mal sind keine neuen Artikel aufgeführt.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Konfigurieren Sie PolyBase-Verbindungen zu externen Daten](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-polybase-connectivity-to-external-dataconfigure-polybase-connectivity-to-external-datamd"></a>1. &nbsp;[Konfigurieren Sie PolyBase-Verbindungen zu externen Daten](configure-polybase-connectivity-to-external-data.md)

*Aktualisiert: 2018-01-29* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 132.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 947f789480da66b9f636f39b30caec6be60d8c4d d4d4d45fbbb8e10ed6f26fe12f9a25d2e8e4f068  (PR=4741  ,  Filename=configure-polybase-connectivity-to-external-data.md  ,  Dirpath=docs\analytics-platform-system\  ,  MergeCommitSha40=0a44ce9993ebf61f86e409255a1d58d47993951a) -->



**Kerberos-Konfiguration**

Beachten Sie, dass bei PolyBase zu einem Kerberos-gesicherte Cluster authentifiziert hat, muss die hadoop.rpc.protection-Einstellung auf Authentifizierung festgelegt werden. Dadurch verbleibt die Datenkommunikation zwischen Hadoop-Knoten, die unverschlüsselt.

 Die Verbindung zu einem Kerberos-gesicherte Hadoop-Cluster [using MIT KDC]:


1.  Suchen Sie das Hadoop-Konfigurationsverzeichnis im Installationspfad auf dem Knoten "Zugriffssteuerung":

    ```
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```

2.  Suchen Sie den hadoopseitigen Konfigurationswert der in dieser Tabelle aufgelisteten Konfigurationsschlüssel. (Suchen Sie die Dateien auf dem Hadoop-Computer im Hadoop-Konfigurationsverzeichnis.)

3.  Kopieren Sie die Konfigurationswerte in der Value-Eigenschaft in den entsprechenden Dateien auf den Knoten "Zugriffssteuerung".

    |**#**|**Konfigurationsdatei**|**Konfigurationsschlüssel**|**Aktion**|
    |------------|----------------|---------------------|----------|
    |1|core-site.xml|polybase.kerberos.kdchost|Geben Sie den KDC-Hostnamen an. Zum Beispiel: kerberos.ihr-bereich.de.|
    |2|core-site.xml|polybase.kerberos.realm|Geben Sie den Kerberos-Bereich an. Zum Beispiel: IHR-BEREICH.DE|
    |3|core-site.xml|hadoop.security.authentication|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: KERBEROS<br></br>**Sicherheitshinweis:** KERBEROS muss in Großbuchstaben geschrieben werden. Bei Kleinschreibung ist die Funktionalität nicht gewährleistet.|
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: hdfs/_HOST@YOUR-REALM.COM|
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: mapred/_HOST@YOUR-REALM.COM|
    |6|mapred-site.xml|mapreduce.jobhistory.address|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Zum Beispiel: 10.193.26.174:10020|
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: yarn/_HOST@YOUR-REALM.COM|







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel Informationen zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Bereiche für die Themenbereichsdatenbank, *führen* wurden neue oder vor kurzem aktualisiert Artikel


- [Neue und aktualisierte (1 + 3):&nbsp; **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **Analyseplattformsystem für SQL** Docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (12 + 1): **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (6 + 2):&nbsp; **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (15 + 0): **PowerShell für SQL** Docs](../powershell/new-updated-powershell.md)
- [Neue und aktualisierte (2 + 9):&nbsp; **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (1 + 0):&nbsp; **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (1 + 1):&nbsp; **SQL Operations Studio** Docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neue und aktualisierte (1 + 1):&nbsp; **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (0 + 2):&nbsp; **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Bereiche, die für die Themenbereichsdatenbank *nicht* haben eine neue oder vor kurzem aktualisiert Artikel


- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [Neue und aktualisierte (0 + 0): **ActiveX Data Objects (ADO) für SQL** Docs](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (0 + 0): **Samples for SQL** Docs](../sample/new-updated-sample.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)


