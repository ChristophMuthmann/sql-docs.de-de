---
title: Aktualisiert - Verbindung mit SQL Server-Dokumentation | Microsoft Docs
description: "Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für die Verbindung mit Microsoft SQL Server herstellen."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: connect
ms.date: 02/03/2018
ms.openlocfilehash: cc4eb05dc4dcd74623c8ce7dfa7b7842449d79b6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-connect-to-sql-server"></a>Neue und kürzlich aktualisierte: Herstellen einer Verbindung mit SQLServer



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-12-03** &nbsp; - zu - &nbsp; **2018-02-03**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Herstellen einer Verbindung mit SQL Server**.




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

1. [Mit "immer verschlüsselt" mit dem ODBC-Treiber für SQLServer](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-using-always-encrypted-with-the-odbc-driver-for-sql-serverodbcusing-always-encrypted-with-the-odbc-drivermd"></a>1. &nbsp;[Using Always Encrypted with the Odbcdriver für SQLServer](odbc/using-always-encrypted-with-the-odbc-driver.md)

*Aktualisiert: 2018-01-22* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 524.  ms.author= "v-chojas".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a52abae2a8f27c3b5bc411ef758610116a608f9f 352368eb269b98ab5ca3a9791fae2e70bf26277a  (PR=4686  ,  Filename=using-always-encrypted-with-the-odbc-driver.md  ,  Dirpath=docs\connect\odbc\  ,  MergeCommitSha40=82c9868b5bf95e5b0c68137ba434ddd37fc61072) -->



**Abrufen von Daten in Teilen mit SQLGetData**

Bevor verschlüsselt 17 von ODBC-Treiber für SQL Server können Zeichen und binärer Spalten in Teilen mit SQLGetData abgerufen werden. Nur ein Aufruf von SQLGetData kann vorgenommen werden, mit einem Puffer, der ausreichend lang ist, um die gesamte Spalte Daten enthalten.

**Senden von Daten mit SQLPutData Teilen**

Daten einfügen oder Vergleich können nicht in Teilen mit SQLPutData gesendet werden. Nur ein Aufruf von SQLPutData kann vorgenommen werden, mit einem Puffer, die gesamten Daten enthält. Verwenden Sie zum Einfügen von long-Daten in verschlüsselten Spalten ein, API für das Massenkopieren, mit einer Eingabe-Datendatei im nächsten Abschnitt beschrieben.

**Verschlüsselte Money und smallmoney**

Verschlüsselt **Money** oder **Smallmoney** von Parametern keine Spalten angewendet werden, da es ist keine bestimmte ODBC-Datentyp die Zuordnungen für diese Typen, wodurch Fehler Operand Typ in Konflikt stehen.

**Massenkopieren von verschlüsselten Spalten**


Verwenden der [SQL-Massenkopieren Funktionen](odbc/../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) und **Bcp** -Hilfsprogramm wird seit 17 der ODBC-Treiber für SQL Server mit Always Encrypted unterstützt. Nur-Text (auf verschlüsselte und entschlüsselte auf) und Chiffretext (wörtlich übertragen) eingefügt werden kann und das Massenkopieren (Bcp_ *) APIs mit abgerufen und die **Bcp** Hilfsprogramm.

- Chiffretext varbinary(max) Format (z. B. für den Massenimport in eine andere Datenbank laden) abgerufen werden, zu verbinden, ohne die `ColumnEncryption` Option (oder legen sie den `Disabled`) und führen Sie einen BCP OUT-Vorgang.

- Zum Einfügen und Abrufen von nur-Text und den Treiber transparent Durchführen von Verschlüsselung und Entschlüsselung als Einstellung für erforderlich ist, können `ColumnEncryption` zu `Enabled` ist ausreichend. Die Funktionalität der BCP-API ist andernfalls nicht geändert.

- Einfügen von verschlüsseltem Text transformiert varbinary(max) Format (z. B. wie oben abgerufen), legen Sie die `BCPMODIFYENCRYPTED` auf "true" aus, und führen Sie einen Vorgang BCP IN. Sicherstellen Sie in der Reihenfolge für die resultierenden Daten zu entschlüsselnden, dass das Ziel Spaltenwerts CEK identisch, von dem der verschlüsselte Text ursprünglich erhalten wurde.







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


