---
title: "Datenbankdateien und Dateigruppen | Microsoft Docs"
ms.custom: ""
ms.date: "10/11/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbanken [SQL Server], Dateien"
  - "Dateigruppen [SQL Server]"
  - "Transaktionsprotokolle [SQL Server], Info"
  - "Transaktionsprotokolle [SQL Server], Dateien"
  - "MDF-Dateien"
  - "Datendateien [SQL Server]"
  - "Standarddateigruppen"
  - "Dateien [SQL Server], Informationen zu Dateien und Dateigruppen"
  - "Sekundäre Dateien [SQL Server]"
  - "Protokolldateien [SQL Server]"
  - "NDF-Dateien"
  - "Dateien [SQL Server]"
  - "LDF-Dateien"
  - "Datenbankdateien [SQL Server]"
  - "Datenbanken [SQL Server], Dateigruppen"
  - "Dateigruppen [SQL Server], Typen"
  - "Primäre Dateigruppen [SQL Server]"
  - "Benutzerdefinierte Dateigruppen [SQL Server]"
  - "Dateigruppen [SQL Server], Informationen zu Dateigruppen"
  - "Primäre Dateien [SQL Server]"
  - "Dateitypen [SQL Server]"
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Datenbankdateien und Dateigruppen
  Jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank verfügt über mindestens zwei Betriebssystemdateien: eine Datendatei und eine Protokolldatei. Datendateien enthalten Daten und Objekte wie z. B. Tabellen, Indizes, gespeicherte Prozeduren und Sichten. Protokolldateien enthalten die Informationen, die zum Wiederherstellen aller Transaktionen in der Datenbank erforderlich sind. Datendateien können für die Zuordnung und Verwaltung in Dateigruppen zusammengefasst werden.  
  
## Datenbankdateien  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken verwenden drei Arten von Dateien, wie in der folgenden Tabelle gezeigt wird.  
  
|File|Beschreibung|  
|----------|-----------------|  
|Primär|Die primäre Datendatei enthält die Startinformationen für die Datenbank und verweist auf die anderen Dateien in der Datenbank. Benutzerdaten und -objekte können in dieser Datei oder in sekundären Datendateien gespeichert werden. Jede Datenbank verfügt über eine primäre Datendatei. Die empfohlene Dateinamenerweiterung für primäre Datendateien ist MDF.|  
|Secondary|Sekundäre Datendateien sind optional, benutzerdefiniert und speichern Benutzerdaten. Sekundäre Dateien können verwendet werden, um Daten auf mehrere Datenträger zu verteilen, indem jede Datei auf einem anderen Datenträger gespeichert wird. Wenn eine Datenbank die maximal zulässige Größe für eine einzige Datei überschreitet, haben Sie zudem die Möglichkeit, sekundäre Datendateien zu verwenden, sodass die Datenbank weiter vergrößert werden kann.<br /><br /> Die empfohlene Dateinamenerweiterung für sekundäre Datendateien ist NDF.|  
|Transaktionsprotokoll|Die Transaktionsprotokolldateien speichern die Protokollinformationen, die zum Wiederherstellen der Datenbank verwendet werden. Für jede Datenbank muss mindestens eine Protokolldatei vorhanden sein. Die empfohlene Dateinamenerweiterung für Transaktionsprotokolle ist LDF.|  
  
 Sie können z. B. eine einfache Datenbank ( **Sales** ), die eine primäre Datei umfasst, die alle Daten und Objekte enthält, und eine Protokolldatei erstellen, die die Transaktionsprotokollinformationen enthält. Es kann auch eine komplexere Datenbank namens **Orders** erstellt werden, die eine primäre Datei und fünf sekundäre Dateien enthält. Die Daten und Objekte in der Datenbank verteilen sich auf alle sechs Dateien, und die vier Protokolldateien enthalten die Transaktionsprotokollinformationen.  
  
 Standardmäßig werden die Daten und Transaktionsprotokolle auf dem gleichen Laufwerk und im gleichen Pfad gespeichert. Dadurch werden auch Systeme mit nur einem Datenträger berücksichtigt. Diese Vorgehensweise ist für Produktionsumgebungen jedoch  möglicherweise nicht optimal. Es wird empfohlen, Daten und Protokolldateien auf verschiedenen Datenträgern zu speichern.  

### Logische und physische Dateinamen

SQL Server-Dateien haben zwei Namen: 

**logical_file_name:** Der logische Dateiname wird dazu verwendet, in allen Transact-SQL-Anweisungen auf die physische Datei zu verweisen. Der logische Dateiname muss den Regeln für SQL Server-Bezeichner entsprechen und innerhalb der logischen Dateinamen in der Datenbank eindeutig sein.

**os_file_name:** Der Name der Betriebssystemdatei ist der Name der physischen Datei inklusive des Verzeichnispfads. Er muss den betriebssystemspezifischen Regeln für Dateinamen entsprechen.

SQL Server-Daten und -Protokolldateien können sowohl auf FAT- als auch auf NTFS-Dateisystemen platziert werden. Es wird empfohlen, dass Sie das NTFS-Dateisystem aufgrund seiner Sicherheitsaspekte verwenden. Datendateigruppen und Protokolldateien für Lese-/Schreibvorgänge können nicht auf einem mit NTFS komprimierten Dateisystem platziert werden. Nur schreibgeschützte Datenbanken und schreibgeschützte sekundäre Dateigruppen können auf einem mit NTFS komprimierten Dateisystem platziert werden.

Wenn mehrere SQL Server-Instanzen auf einem einzelnen Computer ausgeführt werden, erhält jede Instanz ein anderes Standardverzeichnis, um die Dateien für die in der Instanz erstellten Datenbanken zu speichern. Weitere Informationen finden Sie unter [Dateispeicherorte für Standard- und benannte Instanzen von SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).

### Datendateiseiten

Die Seiten in einer SQL Server-Datendatei erhalten aufeinander folgende Seitennummern, beginnend mit null (0) für die erste Seite in der Datei. Jede Datei in einer Datenbank verfügt über eine eindeutige ID-Nummer. Um eine Seite in einer Datenbank eindeutig zu identifizieren, ist sowohl die Datei-ID als auch die Seitennummer erforderlich. Im folgenden Beispiel werden die Seitennummern in einer Datenbank dargestellt, die über eine 4 MB umfassende primäre Datendatei und eine 1 MB umfassende sekundäre Datendatei verfügt.

![Datendateiseiten](../../relational-databases/databases/media/data-file-pages.gif)

Die erste Seite in jeder Datei ist eine Dateiheaderseite, die Informationen zu den Attributen der Datei enthält. Viele der anderen Seiten am Anfang der Datei enthalten ebenfalls Systeminformationen, wie z. B. Zuordnungstabellen. Eine der Systemseiten, die sowohl in der primären Datendatei als auch in der ersten Protokolldatei gespeichert ist, ist eine Datenbank-Startseite, die Informationen zu den Attributen der Datenbank enthält. Weitere Informationen zu Seiten und Seitentypen finden Sie unter „Grundlegendes zu Seiten und Blöcken“.

### Dateigröße

SQL Server-Dateien können ausgehend von ihrer ursprünglich angegebenen Größe automatisch wachsen. Wenn Sie eine Datei definieren, können Sie eine bestimmte Schrittweite für die Vergrößerung angeben. Sobald die Datei vollständig aufgefüllt ist, wird sie um den als Schrittweite festgelegten Wert vergrößert. Wenn eine Dateigruppe mehrere Dateien enthält, beginnt die automatische Vergrößerung erst dann, wenn alle Dateien vollständig gefüllt sind. Die Vergrößerung wird dann nach dem Round-Robin-Schema vorgenommen.

Für jede Datei kann zudem eine Maximalgröße angegeben werden. Wenn keine Maximalgröße angegeben wird, kann die Datei so lange vergrößert werden, bis der gesamte verfügbare Speicherplatz auf dem Datenträger verbraucht ist. Diese Funktion ist insbesondere dann hilfreich, wenn SQL Server als in eine Anwendung eingebettete Datenbank verwendet wird und der Benutzer sich nicht ohne Weiteres mit einem Systemadministrator in Verbindung setzen kann. Der Benutzer kann festlegen, dass die Dateien nach Bedarf automatisch vergrößert werden, sodass die administrative Arbeit reduziert werden kann, die mit der Überwachung des freien Speicherplatzes in der Datenbank und der manuellen Zuordnung von zusätzlichem Speicherplatz verbunden ist. 


## Datenbank-Momentaufnahmedateien

Das von einer Datenbankmomentaufnahme zum Speichern der Kopie-bei-Schreibvorgang-Daten verwendete Dateiformat hängt davon ab, ob die Momentaufnahme von einem Benutzer erstellt oder intern verwendet wird:

* Eine von einem Benutzer erstellte Datenbankmomentaufnahme speichert die Daten in mindestens einer Datei mit geringer Dichte. Die Technologie von Dateien mit geringer Dichte ist eine Funktion des NTFS-Dateisystems. Anfangs enthält eine Datei mit geringer Dichte keine Benutzerdaten. Zudem ist dieser Datei kein Speicherplatz für Benutzerdaten zugeordnet. Allgemeine Informationen zum Verwenden von Dateien mit geringer Dichte in Datenbankmomentaufnahmen sowie zum Wachstum von Datenbankmomentaufnahmen finden Sie unter [Anzeigen der Größe der Datei mit geringer Dichte einer Datenbank-Momentaufnahme (Transact-SQL)](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md). 
* Datenbankmomentaufnahmen werden intern von bestimmten DBCC-Befehlen verwendet. Zu diesen Befehlen zählen DBCC CHECKDB, DBCC CHECKTABLE, DBCC CHECKALLOC und DBCC CHECKFILEGROUP. Eine interne Datenbankaufnahme verwendet alternative Datenströme mit geringer Dichte der ursprünglichen Datenbankdateien. So wie Dateien mit geringer Dichte stellen auch alternative Datenströme eine Funktion des NTFS-Dateisystems dar. Die Verwendung alternativer Datenströme mit geringer Dichte ermöglicht das Zuordnen mehrerer Datenzuweisungen zu einer einzelnen Datei bzw. zu einem einzelnen Ordner, ohne Auswirkung auf die Dateigröße oder -umfangstatistiken. 


  
## Dateigruppen  
 Jede Datenbank besitzt eine primäre Dateigruppe. Diese Dateigruppe enthält die primäre Datendatei sowie ggf. alle sekundären Dateien, die nicht in anderen Dateigruppen gespeichert werden. Benutzerdefinierte Dateigruppen können erstellt werden, um Datendateien zum Zweck der Verwaltung, Datenzuordnung und -verteilung zu Gruppen zusammenzufassen.  
  
 Es können z. B. drei Dateien (Data1.ndf, Data2.ndf und Data3.ndf) auf drei unterschiedlichen Datenträgern erstellt und der **fgroup1**-Dateigruppe zugewiesen werden. Anschließend kann eine Tabelle speziell für die **fgroup1**-Dateigruppe erstellt werden. Abfragen nach Daten in der Tabelle werden über alle drei Datenträger verteilt, wodurch die Leistung gesteigert wird. Dieselbe Leistungssteigerung kann auch durch die Verwendung einer einzigen Datei erzielt werden, wenn diese auf einem RAID-Stripeset (Redundant Array of Independent Disks; redundantes Datenträgerarray) erstellt wird. Dateien und Dateigruppen ermöglichen Ihnen jedoch das problemlose Hinzufügen neuer Dateien zu neuen Datenträgern.  
  
 Alle Datendateien werden in den Dateigruppen gespeichert, die in der folgenden Tabelle aufgeführt werden.  
  
|Dateigruppe|Beschreibung|  
|---------------|-----------------|  
|Primär|Die Dateigruppe, die die primäre Datei enthält. Alle Systemtabellen werden der primären Dateigruppe zugewiesen.|  
|Benutzerdefinierte Dateigruppe|Jede Dateigruppe, die eigens durch den Benutzer erstellt wird, wenn dieser die Datenbank erstmals erstellt oder zu einem späteren Zeitpunkt ändert.|  
  
### Standarddateigruppe  
 Wenn Objekte in der Datenbank ohne Angabe einer Dateigruppe erstellt werden, werden sie der Standarddateigruppe zugewiesen. Zu jedem Zeitpunkt wird genau eine Dateigruppe zur Standarddateigruppe erklärt. Die Dateien in der Standarddateigruppe müssen groß genug sein, um alle neuen Objekte aufnehmen zu können, die nicht anderen Dateigruppen zugeordnet werden.  
  
 Die PRIMARY-Dateigruppe stellt die Standarddateigruppe dar, sofern diese nicht mithilfe der ALTER DATABASE-Anweisung geändert wird. Systemobjekte und -tabellen sind weiterhin der Dateigruppe PRIMARY (primäre Dateigruppe) und nicht der neuen Standarddateigruppe zugeordnet.  

### Datei- und Dateigruppenbeispiel

Im folgenden Beispiel wird eine Datenbank auf einer SQL Server-Instanz erstellt. Die Datenbank verfügt über eine primäre Datendatei, eine benutzerdefinierte Dateigruppe und eine Protokolldatei. Die primäre Datendatei befindet sich in der primären Dateigruppe, und die benutzerdefinierte Dateigruppe verfügt über zwei sekundäre Datendateien. Durch die ALTER DATABASE-Anweisung wird die benutzerdefinierte Dateigruppe als Standarddateigruppe festgelegt. Anschließend wird eine Tabelle unter Angabe der benutzerdefinierten Dateigruppe erstellt. (Dieses Beispiel verwendet einen generischen Pfad, `c:\Program Files\Microsoft SQL Server\MSSQL.1`, um die Angabe einer SQL Server-Version zu vermeiden.)

```
USE master;
GO
-- Create the database with the default data
-- filegroup and a log file. Specify the
-- growth increment and the max size for the
-- primary data file.
CREATE DATABASE MyDB
ON PRIMARY
  ( NAME='MyDB_Primary',
    FILENAME=
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_Prm.mdf',
    SIZE=4MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP MyDB_FG1
  ( NAME = 'MyDB_FG1_Dat1',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_1.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
  ( NAME = 'MyDB_FG1_Dat2',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_2.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB)
LOG ON
  ( NAME='MyDB_log',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB.ldf',
    SIZE=1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB);
GO
ALTER DATABASE MyDB 
  MODIFY FILEGROUP MyDB_FG1 DEFAULT;
GO

-- Create a table in the user-defined filegroup.
USE MyDB;
CREATE TABLE MyTable
  ( cola int PRIMARY KEY,
    colb char(8) )
ON MyDB_FG1;
GO
```

In der folgenden Abbildung werden die Ergebnisse des vorherigen Beispiels zusammengefasst.

![Beispiel einer Dateigruppe](../../relational-databases/databases/media/filegroup-example.gif)
  
## Verwandte Inhalte  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
 [ALTER DATABASE-Optionen für Dateien und Dateigruppen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20File%20and%20Filegroup%20Options%20\(Transact-SQL\).md)  
  
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  