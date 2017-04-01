---
title: "Laden von Daten f&#252;r Columnstore-Indizes | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b29850b5-5530-498d-8298-c4d4a741cdaf
caps.latest.revision: 31
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 28
---
# Laden von Daten f&#252;r Columnstore-Indizes
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Laden Sie Daten mithilfe der Funktion zum SQL-Massenladen in einen Columnstore-Index und wenden Sie Einfügemethoden an. Diese Methoden umfassen bcp, Integration Services und die merge- oder insert-Anweisung von Transact-SQL.  
  
 Neu bei Columnstore-Indizes? Informieren Sie sich über die Begriffe und Konzepte unter [Beschreibung von Columnstore-Indizes](../Topic/Columnstore%20Indexes%20Guide.md).  
  
 Ist eine ausführliche Erläuterung erforderlich? Weitere Informationen finden Sie in diesem [Blogbeitrag](http://blogs.msdn.com/b/sqlcat/archive/2015/03/11/data-loading-performance-considerations-on-tables-with-clustered-columnstore-index.aspx).  
  
##  <a name="dataload_cci"></a> Massenladen in einen gruppierten Columnstore-Index  
 Um Zeilen mittels Massenladen in einen gruppierten Columnstore-Index einzufügen, können Sie das Befehlszeilentool „bcp“ oder Integration Services verwenden oder Zeilen in einer Stagingtabelle auswählen.  
  
 ![Laden in einen gruppierten columnstore-Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-loadprocess.gif "Laden in einen gruppierten columnstore-Index")  
  
 Gemäß dem Diagramm gilt Folgendes für das Massenladen:  
  
1.  Die Daten werden nicht vorab sortiert. Daten werden in der Reihenfolge in Zeilengruppen eingefügt, in der sie empfangen werden.  
  
2.  Wenn die Batchgröße >= 102.400 ist, werden die Zeilen direkt in die komprimierten Zeilengruppen eingefügt. Es wird empfohlen, dass Sie die Batchgröße >= 102.400 für einen effizienten Massenimport auswählen, da Sie das Verschieben von Datenzeilen in eine Delta-Zeilengruppen vermeiden können, bevor die Zeilen von einem Hintergrundthread (Tupelverschiebungsvorgang) schließlich in komprimierte Zeilengruppen verschoben werden.  
  
3.  Wenn die Batchgröße < 102.400 oder die verbleibenden Zeilen < 102.400 sind, werden die Zeilen in Delta-Zeilengruppen geladen.  
  
 Beim Massenladen in gruppierte Columnstore-Indizes sind die folgenden Optimierungen verfügbar.  
  
-   Paralleles Laden: Sie können gleichzeitig mehrere Massenimporte (bcp oder Masseneinfügung) ausführen, die jeweils eine separate Datendatei laden. Im Gegensatz zu Rowstore müssen Sie TABLOCK nicht angeben, da jeder Massenimportthread Daten ausschließlich in separate Zeilengruppen lädt (komprimierte oder Delta-Zeilengruppen), die eine exklusive Sperre aufweisen.   Die Verwendung von TABLOCK erzwingt eine exklusive Sperre für die Tabelle, und Sie sind dann nicht in der Lage, Daten parallel zu importieren.  
  
-   Protokolloptimierung: Das Massenladen wird minimal protokolliert. Das gilt auch beim Laden der Daten in eine komprimierte Zeilengruppe. Es erfolgt keine minimale Protokollierung beim Laden von Daten in Delta-Zeilengruppen mit einer Batchgröße < 102.400.  
  
-   Sperrenoptimierung: Beim Laden in komprimierte Zeilengruppen wird die X-Sperre für Zeilengruppen abgerufen. Beim Massenladen in Delta-Zeilengruppen wird eine X-Sperre für die Zeilengruppe abgerufen, aber SQL Server sperrt die PAGE/EXTENT weiterhin, da die X-Zeilengruppensperre nicht Teil der Sperrhierarchie ist.  
  
 Wenn Sie über einen oder mehrere nicht gruppierte Indizes verfügen, erfolgt keine Sperren- oder Protokollierungsoptimierung für den Indext selbst, sondern die Optimierungen für den gruppierten Columnstore-Index, die oben beschrieben wurden, sind weiterhin vorhanden.  
  
## Funktionsweise des Deltastore  
 Gruppierte Columnstore-Indizes erfassen bis zu 1.048.576 Zeilen im Deltastore, bevor sie in der komprimierten Zeilengruppe komprimiert werden. Dies verbessert die Komprimierung des Columnstore-Index. Wenn eine Deltastore-Zeilengruppe 1.048.576 Zeilen enthält, wird die Zeilengruppe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als geschlossen markiert. Ein Hintergrundprozess, der als *Tupelverschiebungsvorgang* bezeichnet wird, findet jede geschlossene Zeilengruppe und komprimiert sie im Columnstore.  
  
 Für jeden gruppierten Columnstore-Index können mehrere Deltastores vorhanden sein.  
  
-   Wenn ein Deltastore gesperrt ist, versucht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eine Sperre für einen anderen Deltastore zu erhalten. Wenn keine Deltastores verfügbar sind, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen neuen Deltastore.  
  
-   Für eine partitionierte Tabelle sind für jede Partition mehrere Deltastores vorhanden.  
  
 Diese Szenarien beschreiben, in welchen Fällen geladene Zeilen direkt in den Columnstore und in welchen Fällen sie in den Deltastore aufgenommen werden.  
  
 In diesem Beispiel kann jede Zeilengruppe 102.400 bis 1.048.576 Zeilen pro Zeilengruppe enthalten. In der Praxis kann die maximale Größe einer Zeilengruppe kleiner sein als 1.048.576 Zeilen, wenn nicht ausreichend Arbeitsspeicher vorhanden ist.  
  
|Zeilen für Massenladevorgang|Zur komprimierten Zeilengruppe hinzugefügte Zeilen|Zur Delta-Zeilengruppe hinzugefügte Zeilen|  
|-----------------------|-------------------------------------------|--------------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> Zeilengruppengröße: 145.000.|0|  
|1,048,577|1,048,576<br /><br /> Zeilengruppengröße: 1.048.576.|1|  
|2,252,152|2,252,152<br /><br /> Zeilengruppengrößen: 1.048.576, 1.048.576, 155.000.|0|  
  
 Im folgenden Beispiel werden die Ergebnisse des Ladens von 1.048.577 Zeilen in eine Tabelle angezeigt. Aus den Ergebnissen wird ersichtlich, dass eine COMPRESSED-Zeilengruppe im Columnstore (in Form von komprimierten Spaltensegmenten) und eine Zeile im Deltastore vorhanden sind.  
  
```  
SELECT object_id, index_id, partition_number, row_group_id, delta_store_hobt_id, state state_desc, total_rows, deleted_rows, size_in_bytes   
FROM sys.dm_db_column_store_row_group_physical_stats  
```  
  
 ![Rowgroup and deltastore for a batch load](../../relational-databases/indexes/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup and deltastore for a batch load")  
  
## Laden aus einer Stagingtabelle  
 Ein häufiges Muster für das Laden von Daten ist das Laden der Daten in eine Stagingtabelle. Dann werden einige Transformationen ausgeführt und die Daten anschließend mithilfe des folgenden Befehls in die Zieltabelle geladen:  
  
```  
INSERT INTO <columnstore index>  SELECT <list of columns> FROM <Staging Table>  
  
```  
  
 Dieser Befehl lädt die Daten auf ähnliche Weise wie BCP oder der Masseneinfügungsvorgang in den Columnstore-Index, jedoch in einem einzelnen Batch. Wenn die Anzahl der Zeilen in der Stagingtabelle kleiner als 102.400 ist, werden die Zeilen in eine Delta-Zeilengruppe geladen. Andernfalls werden die Zeilen direkt in eine komprimierte Zeilengruppe geladen.  Eine wichtige Einschränkung war, dass dieser Einfügungsvorgang einen einzelnen Thread umfasste. Zum parallelen Laden der Daten könnten Sie mehrere Stagingtabelle erstellen, oder INSERT/SELECT mit nicht überlappenden Bereiche von Zeilen aus der Stagingtabelle ausgeben.  Diese Einschränkung gilt ab SQL Server 2016 nicht mehr. Der nachfolgende Befehl lädt die Daten aus einer Stagingtabelle parallel, aber Sie müssen TABLOCK angegeben.  
  
```  
INSERT INTO <columnstore index>  WITH (TABLOCK)  SELECT <list of columns> FROM <Staging Table>  
```  
  
 Beim Laden in gruppierte Columnstore-Indizes aus Stagingtabellen sind die folgenden Optimierungen verfügbar.  
  
-   Protokolloptimierung: Minimale Protokollerung. Das gilt auch beim Laden der Daten in eine komprimierte Zeilengruppe. Es erfolgt keine minimale Protokollierung beim Laden von Daten in Delta-Zeilengruppen.  
  
-   Sperrenoptimierung: Beim Laden in komprimierte Zeilengruppen wird die X-Sperre für Zeilengruppen abgerufen. Bei der Delta-Zeilengruppe wird eine X-Sperre für die Zeilengruppe abgerufen, aber SQL Server sperrt die PAGE/EXTENT weiterhin, da die X-Zeilengruppensperre nicht Teil der Sperrhierarchie ist.  
  
 Wenn Sie über einen oder mehrere nicht gruppierte Indizes verfügen, erfolgt keine Sperren- oder Protokollierungsoptimierung für den Indext selbst, sondern die Optimierungen für den gruppierten Columnstore-Index, die oben beschrieben wurden, sind weiterhin vorhanden.  
  
## Laden durch Anwenden der Einfügung  
 *Einfügung anwenden* bezieht sich auf die Möglichkeit, die Zeilen mithilfe von INSERT INTO in den Columnstore zu laden. Jede Zeile wird zu einer Delta-Zeilengruppe hinzugefügt. Durch Einfügung angewendete Zeilen gelangen direkt in die Deltastore-Zeilengruppe, wo sie gesammelt werden, bis die Zeilengruppe nach Erreichen von 1.048.576 Zeilen oder der Neuerstellung des Columnstore-Index geschlossen wird.  
  
```  
INSERT INTO <table-name> VALUES (<set of values>)  
```  
  
 Beachten Sie, dass parallele Threads, die INSERT INTO zum Einfügen von Werten in einen gruppierten Columnstore-Index verwenden, Zeilen in dieselbe Delta-Zeilengruppe einfügen können.  
  
 Sobald die Zeilengruppe 1.048.576 Zeilen enthält, wird die Delta-Zeilengruppe als CLOSED markiert, ist aber weiterhin für Abfragen und Aktualisierungs-/Löschvorgänge verfügbar. Die neu eingefügten Zeilen gelangen jedoch in eine vorhandene oder neu erstellte Deltastore-Zeilengruppe. Es gibt einen Hintergrundthread, den *Tupelverschiebungsvorgang*, der die geschlossenen Deltazeilengruppen in regelmäßigen Abständen komprimiert, z.B. alle fünf Minuten. Sie können den folgenden Befehl explizit aufrufen, um die geschlossenen Delta-Zeilengruppen zu komprimieren.  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE  
```  
  
 Wenn Sie erzwingen möchten, dass eine Delta-Zeilengruppe geschlossen und komprimiert wird, können Sie den folgenden Befehl ausführen. Sie können diesen Befehl ausführen, wenn Sie das Laden der Zeilen abgeschlossen haben und keine weiteren neuen Zeilen erwarten. Durch explizites Schließen und Komprimieren der Delta-Zeilengruppe können Sie weiteren Speicherplatz sparen und die Abfrageleistung für Analysen verbessern. Eine bewährte Methode ist das Aufrufen dieses Befehls, wenn Sie nicht erwarten, dass weitere neue Zeilen eingefügt werden.  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE with (COMPRESS_ALL_ROW_GROUPS = ON)  
```  
  
## Laden von Daten in eine partitionierte Tabelle  
 Bei partitionierten Daten weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zuerst jede Zeile einer Partition zu und führt dann Columnstore-Vorgänge für die Daten innerhalb der Partition aus. Jede Partition verfügt über eigene Zeilengruppen und mindestens einen Deltastore.  
  
## Laden von Daten in einen nicht gruppierten Columnstore-Index  
 Für eine Rowstore-Tabelle mit nicht gruppierten Columnstore-Indexdaten fügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Daten immer in die Basistabelle ein. Die Daten werden nie direkt in den Columnstore-Index eingefügt.  
  
## Siehe auch  
 [Beschreibung von Columnstore-Indizes](../Topic/Columnstore%20Indexes%20Guide.md)   
 [Columnstore-Indizes, Zusammenfassung der Funktionen nach Version](../Topic/Columnstore%20Indexes%20Versioned%20Feature%20Summary.md)   
 [Abfrageleistung für Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Columnstore-Indizes für Data Warehousing](../Topic/Columnstore%20Indexes%20for%20Data%20Warehousing.md)   
 [Columnstore-Index-Defragmentierung](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  