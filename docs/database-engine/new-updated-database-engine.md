---
title: Aktualisierte Dokumentation zu Datenbankmodulen | Microsoft-Dokumentation
description: Anzeigen von Codeausschnitten aktualisierter Inhalte in der zuletzt geänderten Dokumentation für Datenbankmodule.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: database-engine
ms.date: 02/03/2018
ms.openlocfilehash: 41c188fd99e273c475e2cc1c2335f59ba710f083
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-database-engine-docs"></a>Neue und kürzlich aktualisierte Dokumentation zu Datenbankmodulen



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **3.12.2017** &nbsp; bis &nbsp; **3.2.2018**
- *Themenbereich:* &nbsp; **Datenbankmodul**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


***Dieses Mal sind keine neuen Artikel aufgeführt.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Durchführen eines Upgrades von Always On-Verfügbarkeitsgruppen-Replikatinstanzen](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-upgrading-always-on-availability-group-replica-instancesavailability-groupswindowsupgrading-always-on-availability-group-replica-instancesmd"></a>1. &nbsp; [Durchführen eines Upgrades von Always On-Verfügbarkeitsgruppen-Replikatinstanzen](availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)

*Aktualisiert: 29.1.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 174.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 20ca282e8965889a7a530fb67e125cc876410e41 9f27d0f9a74333b291c1cdc1529edc13960fae29  (PR=4741  ,  Filename=upgrading-always-on-availability-group-replica-instances.md  ,  Dirpath=docs\database-engine\availability-groups\windows\  ,  MergeCommitSha40=0a44ce9993ebf61f86e409255a1d58d47993951a) -->



**Spezielle Schritte für Change Data Capture oder Replikation**


Abhängig vom angewendeten Update können zusätzliche Schritte für Replikatdatenbanken von Verfügbarkeitsgruppen erforderlich sein, die für Change Data Capture oder die Replikation aktiviert sind. Lesen Sie die Anmerkungen zu dieser Version des Updates, um zu bestimmen, ob folgende Schritte erforderlich sind:

1. Upgraden Sie jedes sekundäre Replikat.

1. Führen Sie ein Failover der Verfügbarkeitsgruppe auf eine upgegradete Instanz durch, nachdem alle sekundären Replikate upgegradet wurden.

1. Führen Sie folgenden Transact-SQL-Befehl auf der Instanz aus, die das primäre Replikat hostet:

   ```
   EXECUTE [master].[sys].[sp_vupgrade_replication];
   ```

   >[!NOTE]
   >Die Ausführung dieses Befehls kann einige Minuten in Anspruch nehmen.

1. Führen Sie ein Upgrade für die Instanz aus, bei der es sich um das ursprüngliche primäre Replikat handelt.

Weitere Informationen finden Sie unter [CDC functionality may break after upgrading to the latest CU (Die CDC-Funktion funktioniert nach dem Upgrade auf das aktuelle kumulative Update nicht mehr)](http://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/).









## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die *über* neue oder kürzlich aktualisierte Artikel verfügen


- [Neu und aktualisiert (1+3):&nbsp;Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Analytics Platform System für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zur **Datenbank-Engine für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu und aktualisiert (12+1): Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu und aktualisiert (6+2):&nbsp;Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu und aktualisiert (15+0): Dokumente zu **PowerShell für SQL**](../powershell/new-updated-powershell.md)
- [Neu und aktualisiert (2+9):&nbsp;Dokumente zu **relationalen Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu und aktualisiert (1+0):&nbsp;Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zu **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Neu und aktualisiert (1+2):&nbsp;Dokumente zu **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Neu und aktualisiert (0+2):&nbsp;Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Themenbereiche, die *nicht* über neue oder kürzlich aktualisierte Artikel verfügen


- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../samples/new-updated-samples.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


