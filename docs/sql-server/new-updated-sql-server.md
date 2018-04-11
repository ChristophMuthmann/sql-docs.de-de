---
title: Aktualisiert – Dokumentation zu SQL Server | Microsoft-Dokumentation
description: Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: sql-server
ms.date: 02/03/2018
ms.openlocfilehash: bcbf9a579fce8d27eaa53471190dbe850774c146
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-sql-server-docs"></a>Neu und zuletzt kürzlich aktualisiert: Dokumentation zu SQL Server Data Tools



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **3.12.2017** &nbsp; bis &nbsp; **3.2.2018**
- *Themenbereich*: &nbsp; **SQL Server**




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Durchführen von Upgrades für SQL Server-Instanzen auf Windows Server 2008/2008 R2/2012-Clustern](failover-clusters/windows/upgrade-sql-server-failover-cluster-instance-2008-2012.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Offlinehilfe und Help Viewer für SQL Server](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-offline-help-and-help-viewersql-server-help-installationmd"></a>1. &nbsp; [Offlinehilfe und Help Viewer für SQL Server](sql-server-help-installation.md)

*Aktualisiert: 19.12.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 67.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ea491fdc173a54fb4cdb3dfa2e26bd206d1cc45d 22444427a48064b76088d19d1ffae0a885bfe2a7  (PR=4338  ,  Filename=sql-server-help-installation.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=f2fde1c324466530f92006561a9a29decb711e1b) -->



   Help Viewer öffnet die Registerkarte „Inhalt verwalten“.

2. Wählen Sie unter „Installationsquelle“ **Online** aus, um das neuste Paket mit Hilfeinhalten zu installieren.

   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)

   >[!NOTE]
   > Wenn Sie die Installation über einen Datenträger (Hilfe für SQL Server 2014) installieren möchten, wählen Sie unter „Installationsquelle“ **Datenträger** aus, und geben Sie den Speicherort der Datenquelle an.

   Der lokale Speicherpfad auf der Registerkarte „Inhalt verwalten“ zeigt an, wo der Inhalt auf dem lokalen Computer installiert wird. Wenn Sie den Speicherort ändern möchten, klicken Sie auf **Verschieben**, geben Sie einen anderen Ordnerpfad im Feld **Nach** ein, und klicken Sie anschließend auf **OK**.
   Wenn die Installation der Hilfe fehlschlägt, nachdem Sie den lokalen Speicherpfad geändert haben, schließen Sie Help Viewer, und öffnen Sie das Programm erneut. Vergewissern Sie sich, dass der neue Speicherort im lokalen Speicherpfad angezeigt wird, und führen Sie die Installation erneut durch.

3. Klicken Sie neben jedem Inhaltspaket (Buch), das Sie installieren möchten, auf **Hinzufügen**.
   Fügen Sie alle 13 Bücher unter „SQL Server“ hinzu, um sämtlichen Hilfeinhalt auf SQL Server zu installieren.

4. Klicken Sie im unteren rechten Bereich auf **Aktualisieren**.
   Das Inhaltsverzeichnis der Hilfe im linken Bereich wird automatisch mit den hinzugefügten Büchern aktualisiert.

   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)

> [!NOTE]
> Nicht alle Titel des höchsten Knotens im Inhaltsverzeichnis von SQL Server stimmen genau mit den Namen der jeweiligen Hilfebücher überein, die heruntergeladen werden können. Die Titel im Inhaltsverzeichnis werden den Buchnamen wie folgt zugeordnet:

| Inhaltsbereich | SQL Server-Buch |
|-----|-----|
|Analysis Services-Sprachreferenz | Analysis Services-Sprachreferenz (MDX)|
|DAX-Referenz (Data Analysis Expressions) | DAX-Referenz (Data Analysis Expressions)|
|DMX-Referenz (Data Mining-Erweiterungen) | DMX-Referenz (Data Mining-Erweiterungen)|
|Leitfäden für Entwickler für SQL Server | SQL Server Developer-Referenz|
|Hier können Sie SQL Server Management Studio herunterladen. | SQL Server Management Studio|







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


