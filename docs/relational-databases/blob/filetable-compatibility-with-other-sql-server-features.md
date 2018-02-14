---
title: "FileTable-Kompatibilität mit anderen SQL Server-Funktionen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: blob
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], using with other features
ms.assetid: f12a17e4-bd3d-42b0-b253-efc36876db37
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ba1eeb760eda46825448d3ba56bae1777c533ae
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="filetable-compatibility-with-other-sql-server-features"></a>FileTable-Kompatibilität mit anderen SQL Server-Funktionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Beschreibt, wie FileTables mit anderen Funktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]arbeiten.  
  
##  <a name="alwayson"></a> AlwaysOn-Verfügbarkeitsgruppen und FileTables  
 Wenn die Datenbank, die FILESTREAM- oder FileTable-Daten enthält, zu einer AlwaysOn-Verfügbarkeitsgruppe gehört:  
  
-   Die FileTable-Funktionalität wird teilweise von [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]unterstützt. Nach einem Failover kann auf dem primären Replikat auf FileTable-Daten zugegriffen werden, nicht jedoch auf FileTable-Daten auf lesbaren sekundären Replikaten.  
  
    > **HINWEIS:**  Beachten Sie, dass alle FILESTREAM-Funktionen nach einem Failover unterstützt werden. Sowohl auf lesbaren sekundären Replikaten als auch auf dem neuen primären Replikat kann auf FILESTREAM-Daten zugegriffen werden.  
  
-   Die FILESTREAM-Funktion und die FileTable-Funktion akzeptieren oder geben virtuelle Netzwerknamen (VNNs) statt Computernamen zurück. Weitere Informationen zu diesen Funktionen finden Sie unter [Filestream- und FileTable-Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md).  
  
-   Bei allen Zugriffen auf FILESTREAM- oder FileTable-Daten über Dateisystem-APIs sollten VNNs statt der Computernamen verwendet werden. Weitere Informationen finden Sie unter [FILESTREAM und FileTable bei AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
##  <a name="OtherPartitioning"></a> Partitionierung und FileTables  
 Partitionierung wird in FileTables nicht unterstützt. Mit der Unterstützung für mehrere FILESTREAM-Dateigruppen können in den meisten Szenarien reine Skalierungsprobleme behandelt werden, ohne dass hierfür auf die Partitionierung zurückgegriffen werden muss (im Gegensatz zu SQL 2008-FILESTREAMs).  
  
##  <a name="OtherRepl"></a> Replikation und FileTables  
 Replikation und verwandte Funktionen (einschließlich Transaktionsreplikation, Mergereplikation, Änderungsdatenaufzeichnung und Änderungsnachverfolgung) werden in FileTables nicht unterstützt.  
  
##  <a name="OtherIsolation"></a> Transaktionssemantik und FileTables  
 **Windows-Anwendungen**  
 Windows-Anwendungen verstehen keine Datenbanktransaktionen, deshalb stellen Windows-Schreibvorgänge nicht die ACID-Eigenschaften einer Datenbanktransaktion bereit. Daher sind Transaktionsrollbacks und Wiederherstellung bei Windows-Updatevorgängen nicht möglich.  
  
 **Transact-SQL-Anwendungen**  
 Bei TSQL-Anwendungen, die in der FILESTREAM-(file_stream)-Spalte in einer FileTable arbeiten, ist die Isolationssemantik die gleiche wie beim FILESTREAM-Datentyp in einer regulären Benutzertabelle.  
  
##  <a name="OtherQueryNot"></a> Abfragebenachrichtigungen und FileTables  
 Die Abfrage kann keinen Verweis auf die FILESTREAM-Spalte in der FileTable, in der WHERE-Klausel oder in einem anderen Teil der Abfrage enthalten.  
  
##  <a name="OtherSelectInto"></a> SELECT INTO und FileTables  
 SELECT INTO-Anweisungen aus einer FileTable geben die FileTable-Semantik nicht an die erstellte Zieltabelle weiter (genau wie FILESTREAM-Spalten in einer regulären Tabelle). Alle Zieltabellenspalten verhalten sich genau wie normale Spalten. Sie weisen keine ihnen zugeordnete FileTable-Semantik auf.  
  
##  <a name="OtherTriggers"></a> Trigger und FileTables  
 **DDL-Trigger (Data Definition Language, Datendefinitionssprache)**  
 Es gibt keine besonderen Überlegungen für DDL-Trigger mit FileTables. Normale DDL-Trigger werden für CREATE DATABASE- oder ALTER DATABASE-Vorgänge sowie für CREATE TABLE- oder ALTER TABLE-Vorgänge für FileTables ausgelöst. Trigger können durch Aufrufen der EVENTDATA()-Funktion die tatsächlichen Ereignisdaten abrufen, einschließlich des DDL-Befehlstexts und sonstiger Informationen. Es gibt keine neuen Ereignisse oder Änderungen an dem vorhandenen Eventdata-Schema.  
  
 **DML-Trigger (Data Manipulation Language, Datenbearbeitungssprache)**  
 Diese Einschränkungen werden während des DDL-Vorgangs zur Erstellung von Triggern erzwungen.  
  
-   FileTables unterstützen keine INSTEAD OF-Trigger für DML-Vorgänge. Dies ist eine bestehende Einschränkung für alle Tabellen, die FILESTREAM-Spalten enthalten.  
  
-   FileTables unterstützen AFTER-Trigger für DML-Vorgänge.  
  
-   In einer FileTable definierte Trigger können keine FileTables (einschließlich der übergeordneten FileTable) aktualisieren. Diese Einschränkung verhindert hauptsächlich, dass ein Trigger in einen Sperrkonflikt mit den vom Dateisystem verhängten Sperren in derselben Transaktion gerät.  
  
 **Nicht transaktionaler Zugriff und Auswirkungen auf Trigger**  
 -   Wenn der nicht transaktionale Updatezugriff in einer Datenbank zulässig ist, können direkte Updates der FILESTREAM-Daten in beliebigen Tabellen ausgeführt werden, u. a. auch für FileTable in dieser Datenbank. Aufgrund dieser Möglichkeit ist das BEFORE-Image des FILESTREAM-Inhalts für den Trigger möglicherweise nicht verfügbar.  
  
-   Für nicht transaktionale Updatevorgänge durch das Dateisystem erstellt SQL Server eine interne Transaktion, um den CloseHandle-Vorgang aufzuzeichnen, und alle definierten DML-Trigger werden möglicherweise als Teil dieser Transaktion ausgelöst. Ein Rollback auf eine Transaktion im Triggertext wird nicht verhindert, es erfolgt jedoch kein Rollback der am FILESTREAM vorgenommenen Änderungen.  Ein solcher Rollback kann ebenfalls verhindern, dass die UPDATE-Trigger ausgelöst werden, selbst wenn der FILESTREAM-Inhalt geändert wurde.  
  
-   Zusätzlich zu diesen Auswirkungen gelten für Trigger in FileTables zwei zusätzliche Verhalten:  
  
    -   Bei nicht transaktionalen Updatevorgängen in der FileTable durch das Dateisystem ist es möglich, dass der FILESTREAM-Inhalt ausschließlich von anderen Win32-Vorgängen gesperrt wird und darauf nicht für Lese-/Schreibzugriff durch den Triggertext zugegriffen werden kann. In solchen Fällen kann durch den versuchten Zugriff auf den FILESTREAM-Inhalt im Triggertext ein Freigabeverletzungsfehler ausgegeben werden. Trigger müssen so konzipiert werden, dass solche Fehler entsprechend behandelt werden.  
  
    -   Das AFTER-Image des FILESTREAM ist möglicherweise nicht stabil, da in machen Fällen aufgrund der im Dateisystemzugriff zulässigen Freigabemodi zur selben Zeit durch andere nicht transaktionale Updates aktiv darin geschrieben werden kann.  
  
-   Bei einer unplanmäßigen Beendigung von Win32-Handles, wie beispielsweise beim expliziten Abbrechen von Win32-Handles durch einen Administrator ODER einen Datenbankabsturz, werden während der Wiederherstellungsvorgänge keine Benutzertrigger ausgeführt, obwohl der FILESTREAM von der unplanmäßig beendeten Win32-Anwendung möglicherweise geändert wurde.  
  
##  <a name="OtherViews"></a> Sichten und FileTables  
 **Sichten**  
 Eine Sicht kann in einer FileTable genau wie in einer anderen Tabelle erstellt werden. Die folgenden Überlegungen gelten jedoch für eine in einer FileTable erstellten Sicht:  
  
-   Die Sicht weist keine FileTable-Semantik auf. Die Spalten in der Sicht (einschließlich Dateiattributspalten) verhalten sich z. B. wie normale Sichtspalten ohne besondere Semantik. Das gleiche gilt für Zeilen, die Dateien/Verzeichnisse darstellen.  
  
-   Die Sicht kann möglicherweise auf Grundlage der Semantik für eine aktualisierbare Sicht aktualisiert werden, die Updates können jedoch wie in der Tabelle aufgrund der zugrunde liegenden Tabelleneinschränkungen abgelehnt werden.  
  
-   Der Dateipfad für eine Datei kann in der Sicht visuell dargestellt werden, indem er als explizite Spalte in der Sicht hinzugefügt wird. Zum Beispiel:  
  
     `CREATE VIEW MP3FILES AS SELECT column1, column2, …, GetFileNamespacePath() AS PATH, column3,…  FROM Documents`  
  
 **Indizierte Sichten**  
 Indizierte Sichten können derzeit keine FILESTREAM-Spalten oder berechnete/persistente berechnete Spalten enthalten, die von den FILESTREAM-Spalten abhängig sind. Dieses Verhalten bleibt auch bei in der FileTable definierten Sichten unverändert.  
  
##  <a name="OtherSnapshots"></a> Momentaufnahmeisolation und FileTables  
 Die Read Committed-Momentaufnahme und die Momentaufnahmeisolation basieren auf der Möglichkeit, eine Momentaufnahme der für Leser verfügbaren Daten zu erstellen, selbst wenn für die Daten Updatevorgänge ausgeführt werden. FileTables lassen jedoch nicht transaktionalen Schreibzugriff auf Filestream-Daten zu. Daher gelten die folgenden Einschränkungen für die Verwendung dieser Funktionen in Datenbanken, die FileTables enthalten:  
  
-   Eine Datenbank, die FileTables enthält, kann so geändert werden, dass RCSI/SI aktiviert wird.  
  
-   Wenn der nicht transaktionale Zugriff für die Datenbank auf FULL festgelegt wird, wird eine Transaktion unter RCSI ausgeführt, oder SI weist das folgende Verhalten auf:  
  
    -   Alle [!INCLUDE[tsql](../../includes/tsql-md.md)] -Lesevorgänge der FileTable-file_stream-Spalte sind fehlerhaft. INSERT und UPDATE für die Spalte wären immer noch erfolgreich, solange kein Lesevorgang aus der file_stream-Spalte versucht wird.  
  
    -   Wenn die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung READCOMMITTEDLOCK-Tabellenhinweise angibt, sind Lesevorgänge erfolgreich, und anstelle der Zeilenversionsverwaltung werden Sperren für die Zeilen vorgenommen.  
  
    -   Transaktive Win32 FileStream-Öffnungsanforderungen sind ebenfalls fehlerhaft.  
  
    -   Nicht transaktiver FileTable-Win32-Zugriff ist erfolgreich. Nicht alle internen von FileTable ausgeführten Abfragen sind betroffen.  
  
    -   Die Volltextindizierung ist immer erfolgreich, unabhängig von den Datenbankoptionen (READ_COMMITTED_SNAPSHOT oder ALLOW_SNAPSHOT_ISOLATION).  
  
##  <a name="readsec"></a> Lesbare sekundäre Datenbanken  
 Die gleichen Überlegungen gelten sowohl für lesbare sekundäre Datenbank als auch für Momentaufnahmen. Selbiges ist im vorherigen Abschnitt [Momentaufnahmeisolation und FileTables](#OtherSnapshots)beschrieben.  
  
##  <a name="CDB"></a> Eigenständige Datenbanken und FileTables  
 Die FILESTREAM-Funktion, von der die FileTable-Funktion abhängt, erfordert einen gewissen Konfigurationsaufwand außerhalb der Datenbank. Daher sind Datenbanken, die FILESTREAM oder FileTable verwenden, nicht vollständig eigenständig.  
  
 Sie können den Einschlusstyp der Datenbank auf PARTIAL festlegen, wenn Sie bestimmte Funktionen eigenständiger Datenbanken verwenden möchten, z. B. eigenständige Benutzer. In diesem Fall müssen Sie jedoch beachten, dass einige Datenbankeinstellungen nicht in der Datenbank enthalten sind und nicht automatisch mit der Datenbank verschoben werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
