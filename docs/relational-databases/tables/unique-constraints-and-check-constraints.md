---
title: "UNIQUE- und CHECK-Einschränkungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- constraints [SQL Server], Visual Database Tools
- Visual Database Tools [SQL Server], constraints
ms.assetid: 637098af-2567-48f8-90f4-b41df059833e
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b5596207dc1188bd9830c0993402194954737c6a
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="unique-constraints-and-check-constraints"></a>UNIQUE- und CHECK-Einschränkungen
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  UNIQUE-Einschränkungen und CHECK-Einschränkungen sind zwei Typen von Einschränkungen, mit denen die Datenintegrität in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen erzwungen werden kann. Diese sind wichtige Datenbankobjekte.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [UNIQUE-Einschränkungen](#Unique)  
  
 [CHECK-Einschränkungen](#Check)  
  
 [Verwandte Aufgaben](#Tasks)  
  
##  <a name="Unique"></a> UNIQUE-Einschränkungen  
 Einschränkungen sind Regeln, die von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] für Sie erzwungen werden. Mithilfe von UNIQUE-Einschränkungen können Sie z. B. sicherstellen, dass keine doppelten Werte in bestimmte Spalten eingegeben werden können, die nicht Teil eines Primärschlüssels sind. Obwohl sowohl eine UNIQUE-Einschränkung als auch eine PRIMARY KEY-Einschränkung Eindeutigkeit erzwingt, sollte eine UNIQUE-Einschränkung anstelle einer PRIMARY KEY-Einschränkung verwendet werden, wenn Sie die Eindeutigkeit einer Spalte bzw. einer Kombination von Spalten erzwingen möchten, die nicht den Primärschlüssel darstellt.  
  
 Im Gegensatz zu PRIMARY KEY-Einschränkungen lassen UNIQUE-Einschränkungen den Wert NULL zu. Wie bei jedem Wert, der in einer UNIQUE-Einschränkung enthalten ist, ist jedoch nur ein NULL-Wert pro Spalte zulässig. Auf eine UNIQUE-Einschränkung kann durch eine FOREIGN KEY-Einschränkung verwiesen werden.  
  
 Wenn eine UNIQUE-Einschränkung einer vorhandenen Spalte bzw. vorhandenen Spalten in der Tabelle hinzugefügt wird, überprüft [!INCLUDE[ssDE](../../includes/ssde-md.md)] die vorhandenen Daten in den Spalten, um sicherzustellen, dass alle Werte eindeutig sind. Wenn eine UNIQUE-Einschränkung zu einer Spalte hinzugefügt wird, die doppelte Werte enthält, gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler zurück und fügt die Einschränkung nicht hinzu.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] erstellt automatisch einen UNIQUE-Index, um die Anforderung an die Eindeutigkeit für die UNIQUE-Einschränkung zu erzwingen. Wenn ein Versuch unternommen wird, eine doppelte Zeile einzufügen, gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Fehlermeldung zurück, die darauf hinweist, dass die UNIQUE-Einschränkung verletzt wurde, und fügt die Zeile der Tabelle nicht hinzu. Standardmäßig wird ein eindeutiger nicht gruppierter Index erstellt, um die UNIQUE-Einschränkung zu erzwingen, es sei denn, ein gruppierter Index wird explizit angegeben.  
  
##  <a name="Check"></a> CHECK-Einschränkungen  
 CHECK-Einschränkungen erzwingen die Domänenintegrität, indem sie die Werte begrenzen, die in einer oder mehreren Spalten zulässig sind. Sie können eine CHECK-Einschränkung mit jedem logischen (booleschen) Ausdruck erstellen, der basierend auf den logischen Operatoren TRUE oder FALSE zurückgibt. Es ist z. B. möglich, den Bereich der Werte für eine **Gehalts** -Spalte zu begrenzen, indem eine CHECK-Einschränkung erstellt wird, die nur Daten zwischen 15.000 $ und 100.000 $ zulässt. Auf diese Weise wird verhindert, dass Daten eingegeben werden können, die außerhalb des normalen Einkommensbereichs liegen. Der logische Ausdruck würde wie folgt aussehen: `salary >= 15000 AND salary <= 100000`.  
  
 Sie können mehrere CHECK-Einschränkungen auf eine einzelne Spalte anwenden. Es ist auch möglich, eine einzelne CHECK-Einschränkung auf mehrere Spalten anzuwenden, indem die Einschränkung auf Tabellenebene erstellt wird. So könnte z. B. eine CHECK-Einschränkung für mehrere Spalten verwendet werden, um sicherzustellen, dass jede Zeile mit dem Wert **USA** in der **country_region** -Spalte auch einen aus zwei Zeichen bestehenden Wert in der **state** -Spalte aufweist. Auf diese Weise können mehrere Bedingungen an einer Stelle überprüft werden.  
  
 CHECK-Einschränkungen sind insofern FOREIGN KEY-Einschränkungen ähnlich, als sie die Werte kontrollieren, die in eine Spalte geschrieben werden. Sie unterscheiden sich jedoch in der Methode, mit der die gültigen Werte bestimmt werden: FOREIGN KEY-Einschränkungen rufen die Liste der gültigen Werte von einer anderen Tabelle ab, und CHECK-Einschränkungen ermitteln die gültigen Werte anhand eines logischen Ausdrucks.  
  
> [!CAUTION]  
>  Einschränkungen, die implizite oder explizite Datentypkonvertierungen einschließen, können bei bestimmten Vorgängen einen Fehler erzeugen. So können z. B. Einschränkungen, die für Tabellen definiert werden, die ihrerseits die Quellen von Partitionswechseln sind, bei einer ALTER TABLE...SWITCH-Operation zu einem Fehler führen. Vermeiden Sie deshalb die Datentypkonvertierung in Einschränkungsdefinitionen.  
  
### <a name="limitations-of-check-constraints"></a>Beschränkungen bei CHECK-Einschränkungen  
 CHECK-Einschränkungen weisen Werte zurück, die als FALSE ausgewertet werden. Da NULL-Werte als UNKNOWN ausgewertet werden, kann deren Vorhandensein in Ausdrücken zum Überschreiben einer Einschränkung führen. Angenommen, Sie platzieren z. B. eine Einschränkung für eine **int** -Spalte **MyColumn** und geben darin an, dass **MyColumn** ausschließliche den Wert 10 enthalten darf (**MyColumn=10**). Wenn Sie dann den Wert NULL in **MyColumn**einfügen, wird von [!INCLUDE[ssDE](../../includes/ssde-md.md)] der Wert NULL eingefügt, und es wird kein Fehler zurückgegeben.  
  
 Eine CHECK-Einschränkung gibt TRUE zurück, wenn die von ihr überprüfte Bedingung für alle Zeilen in der Tabelle nicht FALSE ist. CHECK-Einschränkungen werden auf Zeilenebene verwendet. Wenn eine gerade erstellte Tabelle über keinerlei Zeilen verfügt, wird jede CHECK-Einschränkung für diese Tabelle als gültig betrachtet. Dieser Umstand kann zu unerwarteten Ergebnissen führen, wie das im folgenden Beispiel gezeigt wird.  
  
```  
CREATE TABLE CheckTbl (col1 int, col2 int);  
GO  
CREATE FUNCTION CheckFnctn()  
RETURNS int  
AS   
BEGIN  
   DECLARE @retval int  
   SELECT @retval = COUNT(*) FROM CheckTbl  
   RETURN @retval  
END;  
GO  
ALTER TABLE CheckTbl  
ADD CONSTRAINT chkRowCount CHECK (dbo.CheckFnctn() >= 1 );  
GO  
```  
  
 Die hinzugefügte `CHECK` -Einschränkung gibt an, dass es mindestens eine Zeile in der `CheckTbl`-Tabelle geben muss. Da es aber in der Tabelle keine Zeilen gibt, für die die Bedingung dieser Einschränkung überprüft werden kann, wird die ALTER TABLE-Anweisung erfolgreich ausgeführt.  
  
 CHECK-Einschränkungen werden beim Ausführen von DELETE-Anweisungen nicht überprüft. Deshalb kann das Ausführen von DELETE-Anweisungen für Tabellen mit bestimmten Typen von CHECK-Einschränkungen zu unerwarteten Ergebnissen führen. Betrachten Sie beispielsweise das Ausführen der folgenden Anweisungen für die `CheckTbl`-Tabelle.  
  
```  
INSERT INTO CheckTbl VALUES (10, 10);  
GO  
DELETE CheckTbl WHERE col1 = 10;  
```  
  
 Die `DELETE` -Anweisung wird erfolgreich ausgeführt, obwohl die `CHECK` -Einschränkung angibt, dass die `CheckTbl` -Tabelle über mindestens `1` Zeile verfügen muss.  
  
##  <a name="Tasks"></a> Verwandte Aufgaben  
  
> [!NOTE]  
>  Wenn die Tabelle zur Replikation veröffentlicht ist, müssen Sie mit der Transact-SQL-Anweisung [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) oder mit SMO (SQL Server Management Objects) Schemaänderungen ausführen. Wenn die Schemaänderungen mit dem Tabellen-Designer oder dem Datenbankdiagramm-Designer ausgeführt werden, wird versucht, die Tabelle zu entfernen und erneut zu erstellen. Da veröffentlichte Objekte nicht gelöscht werden können, schlägt die Schemaänderung fehl.  
  
|Task|Thema|  
|----------|-----------|  
|Beschreibt, wie eine eindeutige Einschränkung erstellt wird.|[Erstellen von Unique-Einschränkungen](../../relational-databases/tables/create-unique-constraints.md)|  
|Beschreibt, wie eine eindeutige Einschränkung geändert wird.|[Ändern von UNIQUE-Einschränkungen](../../relational-databases/tables/modify-unique-constraints.md)|  
|Beschreibt, wie eine eindeutige Einschränkung gelöscht wird.|[Löschen von Unique-Einschränkungen](../../relational-databases/tables/delete-unique-constraints.md)|  
|Beschreibt, wie eine CHECK-Einschränkung deaktiviert wird, wenn ein Replikations-Agent Daten in die Tabelle einfügt oder darin aktualisiert.|[Deaktivieren von CHECK-Einschränkungen für die Replikation](../../relational-databases/tables/disable-check-constraints-for-replication.md)|  
|Beschreibt, wie eine CHECK-Einschränkung deaktiviert wird, wenn Sie Daten in einer Tabelle hinzufügen, aktualisieren oder löschen möchten.|[Deaktivieren von CHECK-Einschränkungen mit den Anweisungen INSERT und UPDATE](../../relational-databases/tables/disable-check-constraints-with-insert-and-update-statements.md)|  
|Beschreibt, wie der Einschränkungsausdruck oder die Optionen geändert werden, die die Einschränkung unter bestimmten Bedingungen aktivieren und deaktivieren.|[Ändern von CHECK-Einschränkungen](../../relational-databases/tables/modify-check-constraints.md)|  
|Beschreibt, wie eine CHECK-Einschränkung gelöscht wird.|[Löschen von CHECK-Einschränkungen](../../relational-databases/tables/delete-check-constraints.md)|  
|Beschreibt, wie die Eigenschaften einer CHECK-Einschränkung angezeigt werden.|[UNIQUE- und CHECK-Einschränkungen](../../relational-databases/tables/unique-constraints-and-check-constraints.md)|  
  
  
