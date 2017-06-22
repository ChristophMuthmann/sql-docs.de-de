---
title: Aktualisiert - relationale Datenbanken Docs | Microsoft Docs
description: "Aktualisierter Inhalt in zuletzt geänderten Dokumentation für relationale Datenbanken Codeausschnitte anzeigen"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 3ab051a6fd00670139bb1089dcd3f4af76b9ecef
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Neue und zuletzt aktualisiert: relationale Datenbanken Docs



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-05-01** &nbsp; - zu - &nbsp; **2017-05-23**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **relationalen Datenbanken**.




&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

Dieser Abschnitt zeigt die Auszüge von Updates, die vom Artikel, die vor kurzem eine große Aktualisierung aufgetreten sind.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sqlgraphssql-graph-samplemd"></a>1. &nbsp;[Eine Graph-Datenbank erstellen, und führen Sie einige Abfragen, die mithilfe des T-SQL-Mustervergleich](graphs/sql-graph-sample.md)

*Updated: 2017-05-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 68.  ms.author= "shkale".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ff467bf5fcf13592c796836def36e16e34f8cc31 99fcf0399006de16d0ac7cc9057564d307cb981b -->


```
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table, 
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 1), 
       (SELECT $node_id FROM Restaurant WHERE id = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 2), 
      (SELECT $node_id FROM Restaurant WHERE id = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 3), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 4), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 5), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 1),
      (SELECT $node_id FROM City WHERE id = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 2),
      (SELECT $node_id FROM City WHERE id = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 3),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 4),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 5),
      (SELECT $node_id FROM City WHERE id = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 1),
      (SELECT $node_id FROM City WHERE id =1));
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sysfngetauditfile-transact-sqlsystem-functionssys-fn-get-audit-file-transact-sqlmd"></a>2. &nbsp; [Sys. fn_get_audit_file (Transact-SQL)](system-functions/sys-fn-get-audit-file-transact-sql.md)

*Updated: 2017-05-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 046fa92ad1b7e6bb7a956493ca06cf72d45b5285 fbf55361da90663835d7e107fda697c358e0e061 -->



- **Azure SQL-Datenbank**

  Dieses Beispiel liest aus einer Datei namens `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  In diesem Beispiel liest alle Überwachungsprotokolle von Servern, die mit `Sh`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```





&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd"></a>3. &nbsp;[Verwalten der Beibehaltung von Verlaufsdaten in Temporalen Tabellen mit Systemversionsverwaltung](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b -->



**Mithilfe der zeitliche Verlauf Retention Politikansatz**

> **Hinweis:** mithilfe der zeitliche Verlauf Aufbewahrungsrichtlinie Ansatz gilt für [! INCLUDE [Sqldbesa--... /.. /Includes/sqldbesa-MD.MD)] und SQL Server-2017 CTP-Version 1.3 ab.  

Temporale verlaufsbeibehaltung möglich Ebene des einzelnen Tabelle konfiguriert, wodurch Benutzer flexible Alterungszeitraum erstellen Richtlinien. Anwenden von temporären Aufbewahrung ist einfach: Es erfordert nur einen Parameter bei Erstellung oder dem Schema einer Änderung in Tabelle festgelegt werden.

Nach der Definition Aufbewahrungsrichtlinie startet Azure SQL-Datenbank regelmäßig prüft, ob es sind Zeilen mit Verlaufsdaten, die für die automatische Bereinigung geeignet sind. Identifikation von übereinstimmenden Zeilen und deren Entfernung aus der Verlaufstabelle treten transparent, in die Hintergrundaufgabe, die geplant und vom System ausgeführt wird. Alter-Bedingung für die Verlaufszeilen für die Tabelle aktiviert ist basierend auf der Spalte, die Ende SYSTEM_TIME-Zeitraum darstellt. Tabellenzeilen, die für die Bereinigung geeignet, sofern die Beibehaltungsdauer, z. B. auf sechs Monate festgelegt ist, die folgende Bedingung erfüllen:
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
Im vorherigen Beispiel vorausgesetzt, dass die ValidTo-Spalte an das Ende der SYSTEM_TIME-Zeitraum entspricht.
**So konfigurieren Sie die Aufbewahrungsrichtlinie werden?**

Bevor Sie die Aufbewahrungsrichtlinie für eine temporale Tabelle konfigurieren, überprüfen Sie zunächst, ob temporale Verlaufsdaten Beibehaltungsdauer auf Datenbankebene aktiviert ist:
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
Datenbank-Flag **Is_temporal_history_retention_enabled** standardmäßig auf ON festgelegt ist, aber Benutzer mit ALTER DATABASE-Anweisung ändern. Es wird auch nach Point in Time Restore-Vorgang auf OFF festgelegt. Um temporale Verlaufstabellen Bereinigung während der Beibehaltung für Ihre Datenbank zu aktivieren, führen Sie die folgende Anweisung aus:
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
Aufbewahrungsrichtlinie wird beim Erstellen der Tabelle durch Angeben der Wert für den Parameter HISTORY_RETENTION_PERIOD konfiguriert:
```
CREATE TABLE dbo.WebsiteUserInfo
```





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese compact Liste enthält Links zu den aktualisierten Artikeln, die im vorherigen Abschnitt aufgeführt sind.

1. [Erstellen Sie eine Diagrammdatenbank, und führen Sie einige Abfragen, die mithilfe des T-SQL-Mustervergleich](#TitleNum_1)
2. [Sys. fn_get_audit_file (Transact-SQL)](#TitleNum_2)
3. [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](#TitleNum_3)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>Schwester Artikel

Dieser Abschnitt enthält sehr ähnlichen Artikel für zuletzt aktualisierten Artikel in anderen Themenbereichen, innerhalb der gleichen GitHub-Repository.


&nbsp;

[Microsoft /**Sql-Docs-Pr** ](https://github.com/microsoftdocs/sql-docs-pr/) -Repository auf "github.com":

- [Zuletzt aktualisiert: **relationale Datenbanken und Microsoft SQL Server** Docs](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [Zuletzt aktualisiert: **Microsoft SQL Server** Docs](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [Zuletzt aktualisiert: **Transact-SQL in SQL Server** Docs](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



