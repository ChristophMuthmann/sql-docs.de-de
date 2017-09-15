---
title: "Aktualisiert - SSMA für die SQL Server-Dokumentation | Microsoft Docs"
description: "Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für SQL Server Migration Assistant (SSMA) for Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssma-sql-server-migration-assistant
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 68df82bc7da6d7ef5aed3522c06704fb92bb0982
ms.contentlocale: de-de
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-migration-assistant-ssma"></a>Neue und kürzlich aktualisierte: SQL Server Migration Assistant (SSMA)



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-07-18** &nbsp; - zu - &nbsp; **2017-09-11**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **SQL Server Migration Assistant**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links führen zu neue Artikel, die vor kurzem hinzugefügt wurden.


***Dieses Mal sind keine neuen Artikel aufgeführt.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

Dieser Abschnitt zeigt die Auszüge von Updates, die vom Artikel, die vor kurzem eine große Aktualisierung aufgetreten sind.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese compact Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Welche &#39; s in SSMA für DB2 (DB2ToSQL)](#TitleNum_1)
2. [SQL Server Migration Assistant](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-what39s-new-in-ssma-for-db2-db2tosqldb2what-s-new-in-ssma-for-db2-db2tosqlmd"></a>1. &nbsp;[Was &#39; s in SSMA für DB2 (DB2ToSQL)](db2/what-s-new-in-ssma-for-db2-db2tosql.md)

*Aktualisiert: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 24.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5dfb378ac578f54935a8a1fa7194398f3631017 f4427d1857894ad348cef5c92fbf6b51d00ee652  (PR=3070  ,  Filename=what-s-new-in-ssma-for-db2-db2tosql.md  ,  Dirpath=docs\ssma\db2\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**SSMA v7.4**

Die v7.4-Version von SSMA für DB2 enthält die folgenden Änderungen:
- Die **Abfragetimeout** Option ist während der Ermittlung an Quelle und Ziel Schema verfügbar.
! [Option Timeout für Remoteabfragen--... /Media/Query-timeout_red.PNG)

- Die Qualität und Konvertierung Metrik wurde mit targeted Fehlerbehebungen, aufgrund von Kundenfeedback verbessert.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA v7.4. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.

**SSMA V7. 3**

Die V7. 3-Version von SSMA für DB2 enthält die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- SSMA Extensibility Framework verfügbar gemacht werden, über die folgenden Elemente:
  - Exportieren Sie zu einem SQL Server Data Tools (SSDT)-Projekt bereit.
    -   Sie können jetzt Schemaskripts von SSMA in ein SSDT-Projekt exportieren. Die Schemaskripts können Sie zusätzliche Schemas ändern und Bereitstellen der Datenbank.
! [Als SSDT-Befehl "Projekt"--speichern... /Media/Export-Schema-scripts_red.PNG)
  - Bibliotheken, die zum Ausführen von benutzerdefinierter Konvertierungen von SSMA genutzt werden können.
    - Jetzt können Sie Code erstellen, die benutzerdefinierte Syntax Konvertierungen und Konvertierungen, die zuvor vom SSMA verarbeitet wurden nicht verarbeiten kann.
      - Anweisungen zum Erstellen eines benutzerdefinierten Konverters stehen in diesem Blogbeitrag [Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Beispielprojekt für die Konvertierung herunterladen dies [Blogbeitrag](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

**SSMA V7. 2**

Die V7. 2-Version von SSMA für DB2 enthält die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- Telemetrie-Erweiterungen bieten eine bessere Datenpunkte, um Kundenprobleme zu beheben und zu verbessern SSMAs-Wechselkurse.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-migration-assistantsql-server-migration-assistantmd"></a>2. &nbsp;[SQL Server Migration Assistant](sql-server-migration-assistant.md)

*Aktualisiert: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1))

<!-- Source markdown line 36.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 340d718e85fa73c6722862a0a7ba90239b247389 b29f4be2b6d208fd6038c2f9e1c7f0b7bd6b9ed7  (PR=3070  ,  Filename=sql-server-migration-assistant.md  ,  Dirpath=docs\ssma\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**Unterstützte Quellen und Zielversionen**

Überprüfen Sie die Informationen im Download Center für den Download SSMA, für unterstützte Datenquellen.

Die folgende Zielversionen werden für SSMA unterstützt.

- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Azure SQL-Datenbank
- SQLServer 2017 unter Windows und Linux (Vorschau)
- ** Azure SQL Datawarehouse

** Dieses Ziel wird nur von SSMA für Oracle unterstützt.









## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Dieser Abschnitt enthält sehr ähnlich Artikel für die zuletzt aktualisierten Artikel in anderen Bereichen in unserer öffentlichen Repositorys für "github.com" Betreff: [MicrosoftDocs/Sql-Docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (3 + 12): **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (5 + 0): **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (5 + 1): **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (19 + 82): **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (1 + 8): **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (12 + 1): **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (0 + 1): **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (7 + 1): **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (1 + 1): **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (0 + 2): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (1 + 4): **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (4 + 1): **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)
- [Neue und aktualisierte (0 + 1): **-Tools für SQL** Docs](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [Neue und aktualisierte (0 + 0): **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [Neue und aktualisierte (0 + 0): **Master Data Services (MDS) für SQL** Docs](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)



