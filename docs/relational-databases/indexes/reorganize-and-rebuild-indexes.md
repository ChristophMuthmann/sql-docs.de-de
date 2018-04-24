---
title: Neuorganisieren und Neuerstellen von Indizes | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.index.rebuild.f1
- sql13.swb.indexproperties.fragmentation.f1
- sql13.swb.index.reorg.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
caps.latest.revision: 70
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8e340dfc5c9ae6f24a98f23f2262e49fb58285bc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="reorganize-and-rebuild-indexes"></a>Neuorganisieren und Neuerstellen von Indizes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](https://msdn.microsoft.com/en-US/library/ms189858(SQL.120).aspx).

  In diesem Thema wird beschrieben, wie Sie einen fragmentierten Index in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] neu organisieren oder neu erstellen. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verwaltet Indizes automatisch, wenn Einfüge-, Update- oder Löschvorgänge an den zugrunde liegenden Daten vorgenommen werden. Im Lauf der Zeit können diese Änderungen dazu führen, dass die Informationen im Index in der Datenbank verstreut (fragmentiert) werden. Fragmentierung liegt vor, wenn Indizes über Seiten verfügen, in denen die logische Reihenfolge (basierend auf dem Schlüsselwert) nicht der physischen Reihenfolge in der Datendatei entspricht. Hochgradig fragmentierte Indizes können die Abfrageleistung beeinträchtigen und dazu führen, dass Ihre Anwendung nur langsam reagiert.  
  
 Sie können die Indexfragmentierung durch Neuorganisieren oder Neuerstellen eines Indexes beheben. Für partitionierte Indizes, die auf Grundlage eines Partitionsschemas erstellt wurden, können beide Methoden für einen vollständigen Index oder für eine einzelne Partition eines Indexes verwendet werden. Beim Neuerstellen eines Indexes wird der Index gelöscht und neu erstellt. Bei diesem Vorgang wird die Fragmentierung entfernt, Speicherplatz wird freigegeben, indem die Seiten auf der Grundlage der angegebenen oder vorhandenen Füllfaktoreinstellung komprimiert werden, und die Indexzeilen werden in aufeinanderfolgenden Seiten neu geordnet. Wenn `ALL` angegeben ist, werden alle Indizes der Tabelle in einer einzelnen Transaktion gelöscht und neu erstellt. Das Neuorganisieren eines Indexes beansprucht minimale Systemressourcen. Dabei wird die Blattebene von gruppierten und nicht gruppierten Indizes in Tabellen und Sichten defragmentiert, indem die Blattebenenseiten physisch neu geordnet werden, damit sie mit der logischen Reihenfolge der Blattknoten von links nach rechts übereinstimmen. Durch das Neuorganisieren werden die Indexseiten auch komprimiert. Die Komprimierung basiert auf dem vorhandenen Füllfaktorwert.  
   
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Fragmentation"></a> Erkennen der Fragmentierung  
 Der erste Schritt bei der Entscheidung für eine Defragmentierungsmethode besteht im Analysieren des Indexes, um den Fragmentierungsgrad zu ermitteln. Mithilfe der Systemfunktion [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)können Sie die Fragmentierung in einem bestimmten Index, allen Indizes in einer Tabelle oder indizierten Sicht, allen Indizes in einer Datenbank oder allen Indizes in allen Datenbanken erkennen. Für partitionierte Indizes stellt **sys.dm_db_index_physical_stats** außerdem Fragmentierungsinformationen für jede Partition bereit.  
  
 Das durch die Funktion **sys.dm_db_index_physical_stats** zurückgegebene Resultset enthält die folgenden Spalten.  
  
|Spalte|Description|  
|------------|-----------------|  
|**avg_fragmentation_in_percent**|Der Prozentsatz der logischen Fragmentierung (falsche Reihenfolge der Seiten in einem Index).|  
|**fragment_count**|Die Anzahl der Fragmente (physisch aufeinanderfolgende Blattseiten) im Index.|  
|**avg_fragment_size_in_pages**|Durchschnittliche Anzahl der Seiten in einem Fragment in einem Index.|  
  
 Nachdem der Grad der Fragmentierung bekannt ist, verwenden Sie die folgenden Tabelle, um die beste Methode zum Beheben der Fragmentierung zu ermitteln.  
  
|**avg_fragmentation_in_percent** -Wert|Korrigierende Anweisung|  
|-----------------------------------------------|--------------------------|  
|> 5 % und < = 30 %|ALTER INDEX REORGANIZE|  
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|  
  
<sup>1</sup> Das Neuerstellen eines Indexes kann online oder offline erfolgen. Das Neuorganisieren eines Indexes erfolgt immer online. Damit eine Verfügbarkeit ähnlich der Neuorganisierungsoption erreicht wird, sollten Indizes online neu erstellt werden.  
  
 Diese Werte dienen als grobe Richtlinie, um den Punkt zu bestimmen, an dem Sie zwischen `ALTER INDEX REORGANIZE` und `ALTER INDEX REBUILD` wechseln sollten. Die Istwerte können jedoch von Fall zu Fall unterschiedlich sein. Es ist wichtig, dass Sie experimentieren, um den besten Schwellenwert für Ihre Umgebung zu bestimmen. Bei sehr niedrigen Fragmentierungsniveaus (unter 5 Prozent) sollten diese Befehle nicht eingesetzt werden, da die Vorteile des Entfernens einer so geringen Fragmentierung die Kosten für das Neuorganisieren und Neuerstellen des Indexes nicht aufwiegen. Weitere Informationen zu `ALTER INDEX REORGANIZE` und `ALTER INDEX REBUILD` finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).   
  
> [!NOTE]
> Im Allgemeinen ist die Fragmentierung bei kleinen Indizes oft nicht steuerbar. Die Seiten kleiner Indizes werden manchmal in gemischten Blöcken gespeichert. Gemischte Blöcke sind für bis zu acht Objekte freigegeben, sodass die Fragmentierung in einem kleinen Index durch die Reorganisation oder das erneute Erstellen des Indexes möglicherweise nicht verringert wird.
  
### <a name="Restrictions"></a> Einschränkungen  
  
-   Indizes mit mehr als 128 Blöcken werden in zwei getrennten Phasen neu erstellt: der logischen und der physischen Phase. In der logischen Phase werden die vorhandenen Zuordnungseinheiten, die vom Index verwendet werden, für die Aufhebung der Zuordnung markiert, die Datenzeilen werden kopiert und sortiert und dann in neue Zuordnungseinheiten verschoben, die erstellt werden, um den neu erstellten Index zu speichern. In der physischen Phase werden die zuvor für die Aufhebung der Zuordnung markierten Zuordnungseinheiten in kurzen Transaktionen physisch gelöscht, die im Hintergrund ausgeführt werden und nicht viele Sperren benötigen. Weitere Informationen zu Blöcken finden Sie im [Handbuch zur Architektur von Seiten und Blöcken](../../relational-databases/pages-and-extents-architecture-guide.md). 
  
-   Indexoptionen können beim Neuorganisieren eines Indexes nicht angegeben werden.  
  
-   Die `ALTER INDEX REORGANIZE` -Anweisung erfordert, dass die Datendatei mit dem Index über Platz verfügt, da der Vorgang temporäre Arbeitsseiten nur in der gleichen Datei zuordnen kann, nicht in einer anderen Datei der Dateigruppe. Selbst wenn in einer Dateigruppe leere Seiten verfügbar sind, kann für den Benutzer daher trotzdem Fehler 1105 auftreten: `Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`
  
-   Das Erstellen bzw. Neuerstellen von nicht ausgerichteten Indizes für eine Tabelle mit mehr als 1.000 Partitionen ist möglich, wird aber nicht empfohlen. Dies hätte Leistungseinbußen oder eine zu hohe Speicherauslastung während der Vorgänge zur Folge.
  
> [!IMPORTANT]
> Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]werden Statistiken nicht durch das Scannen aller Zeilen in der Tabelle erstellt, wenn ein partitionierter Index erstellt oder neu erstellt wird. Der Abfrageoptimierer generiert stattdessen Statistiken mithilfe des Standardalgorithmus zur Stichprobenentnahme. Um Statistiken zu partitionierten Indizes durch das Scannen aller Zeilen in der Tabelle abzurufen, verwenden Sie `CREATE STATISTICS` oder `UPDATE STATISTICS` mit der `FULLSCAN`-Klausel.
  
### <a name="Security"></a> Sicherheit  
  
#### <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
## <a name="SSMSProcedureFrag"></a> Überprüfen der Indexfragmentierung mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>So überprüfen Sie die Fragmentierung eines Indexes  
  
1.  Erweitern Sie im Objekt-Explorer die Datenbank mit der Tabelle, in der Sie die Fragmentierung eines Indexes überprüfen möchten.  
  
2.  Erweitern Sie den Ordner **Tabellen** .  
  
3.  Erweitern Sie die Tabelle, in der Sie die Fragmentierung eines Indexes überprüfen möchten.  
  
4.  Erweitern Sie den Ordner **Indizes** .  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, für den Sie die Fragmentierung überprüfen möchten, und wählen Sie **Eigenschaften**aus.  
  
6.  Wählen Sie unter **Seite auswählen**die Option **Fragmentierung**aus.  
  
     Die folgenden Informationen sind auf der Seite **Fragmentierung** verfügbar:  
  
     **Seitenfüllgrad**  
     Gibt den durchschnittlichen Füllgrad der Indexseiten als Prozentwert an. 100 % bedeutet, dass die Indexseiten vollständig gefüllt sind. 50 % heißt, dass jede Indexseite im Durchschnitt zur Hälfte gefüllt ist.  
  
     **Fragmentierung gesamt**  
     Prozentwert der logischen Fragmentierung. Dieser Wert gibt die Anzahl der Seiten in einem Index an, die nicht in Reihenfolge gespeichert sind.  
  
     **Durchschnittliche Zeilengröße**  
     Durchschnittliche Größe einer Zeile auf Blattebene.  
  
     **Tiefe**  
     Anzahl der Ebenen im Index, einschließlich der Blattebene.  
  
     **Weitergeleitete Datensätze**  
     Anzahl der Datensätze in einem Heap, die Weiterleitungszeiger auf einen anderen Datenspeicherort besitzen. (Dieser Status tritt während eines Updates auf, wenn nicht genügend Speicherplatz vorhanden ist, um die neue Zeile am ursprünglichen Speicherort zu speichern.)  
  
     **Inaktive Zeilen**  
     Anzahl der Zeilen, die als gelöscht markiert sind, aber noch nicht entfernt wurden. Diese Zeilen werden von einem Bereinigungsthread entfernt, wenn der Server nicht ausgelastet ist. Dieser Wert schließt keine Zeilen ein, die aufgrund einer ausstehenden Momentaufnahme-Isolationstransaktion beibehalten werden.  
  
     **Indextyp**  
     Der Indextyp. Mögliche Werte sind **Gruppierter Index**, **Nicht gruppierter Index**und **Primär-XML**. Tabellen können auch als Heap gespeichert werden (ohne Indizes). Dann kann aber diese Seite Indexeigenschaften nicht geöffnet werden.  
  
     **Zeilen auf Blattebene**  
     Anzahl der Zeilen auf Blattebene.  
  
     **Maximale Zeilengröße**  
     Maximale Größe von Zeilen auf Blattebene.  
  
     **Minimale Zeilengröße**  
     Minimale Größe von Zeilen auf Blattebene.  
  
     **Seiten**  
     Gesamtanzahl der Datenseiten.  
  
     **Partitions-ID**  
     Partitions-ID der B-Struktur, die den Index enthält.  
  
     **Inaktive Zeilen (Version)**  
     Die Anzahl inaktiver Datensätze, die aufgrund einer ausstehenden Momentaufnahme-Isolationstransaktion beibehalten werden.  
  
##  <a name="TsqlProcedureFrag"></a> Überprüfen der Indexfragmentierung mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>So überprüfen Sie die Fragmentierung eines Indexes  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Find the average fragmentation percentage of all indexes  
    -- in the HumanResources.Employee table.   
    SELECT a.index_id, name, avg_fragmentation_in_percent  
    FROM sys.dm_db_index_physical_stats (DB_ID(N'AdventureWorks2012'), 
          OBJECT_ID(N'HumanResources.Employee'), NULL, NULL, NULL) AS a  
        JOIN sys.indexes AS b 
          ON a.object_id = b.object_id AND a.index_id = b.index_id;   
    GO  
    ```  
  
     Das von der obigen Anweisung zurückgegebene Resultset kann in etwa wie folgt aussehen.  
  
    ```  
    index_id    name                                                  avg_fragmentation_in_percent  
    ----------- ----------------------------------------------------- ----------------------------  
    1           PK_Employee_BusinessEntityID                          0  
    2           IX_Employee_OrganizationalNode                        0  
    3           IX_Employee_OrganizationalLevel_OrganizationalNode    0  
    5           AK_Employee_LoginID                                   66.6666666666667  
    6           AK_Employee_NationalIDNumber                          50  
    7           AK_Employee_rowguid                                   0  
  
    (6 row(s) affected)  
    ```  
  
 Weitere Informationen finden Sie unter [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).  
  
##  <a name="SSMSProcedureReorg"></a> Entfernen der Indexfragmentierung mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
#### <a name="to-reorganize-or-rebuild-an-index"></a>So organisieren oder erstellen Sie einen Index neu  
  
1.  Erweitern Sie im Objekt-Explorer die Datenbank mit der Tabelle, in der Sie einen Index neu organisieren möchten.  
  
2.  Erweitern Sie den Ordner **Tabellen** .  
  
3.  Erweitern Sie die Tabelle, in der Sie einen Index neu organisieren möchten.  
  
4.  Erweitern Sie den Ordner **Indizes** .  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, den Sie neu organisieren möchten, und wählen Sie **Neu organisieren**aus.  
  
6.  Vergewissern Sie sich im Dialogfeld **Indizes neu organisieren** , dass der richtige Index im Raster **Neu zu organisierende Indizes** ausgewählt ist, und klicken Sie auf **OK**.  
  
7.  Aktivieren Sie das Kontrollkästchen **Spaltendaten großer Objekte komprimieren** , um anzugeben, dass alle Seiten mit umfangreichen Objektdaten (Large Object, LOB) komprimiert werden sollen.  
  
8.  Klicken Sie auf **OK.**  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>So organisieren Sie alle Indizes in einer Tabelle neu  
  
1.  Erweitern Sie im Objekt-Explorer die Datenbank mit der Tabelle, in der Sie die Indizes neu organisieren möchten.  
  
2.  Erweitern Sie den Ordner **Tabellen** .  
  
3.  Erweitern Sie die Tabelle, in der Sie die Indizes neu organisieren möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Ordner **Indizes** , und wählen Sie **Alle neu organisieren**aus.  
  
5.  Vergewissern Sie sich im Dialogfeld **Index neu organisieren** , dass die richtigen Indizes im Raster **Neu zu organisierende Indizes**ausgewählt sind. Um einen Index aus dem Raster **Neu zu organisierende Indizes** zu entfernen, wählen Sie den Index aus, und drücken Sie die ENTF-Taste.  
  
6.  Aktivieren Sie das Kontrollkästchen **Spaltendaten großer Objekte komprimieren** , um anzugeben, dass alle Seiten mit umfangreichen Objektdaten (Large Object, LOB) komprimiert werden sollen.  
  
7.  Klicken Sie auf **OK.**  
  
#### <a name="to-rebuild-an-index"></a>So erstellen Sie einen Index neu  
  
1.  Erweitern Sie im Objekt-Explorer die Datenbank mit der Tabelle, in der Sie einen Index neu organisieren möchten.  
  
2.  Erweitern Sie den Ordner **Tabellen** .  
  
3.  Erweitern Sie die Tabelle, in der Sie einen Index neu organisieren möchten.  
  
4.  Erweitern Sie den Ordner **Indizes** .  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, den Sie neu organisieren möchten, und wählen Sie **Neu erstellen** aus.  
  
6.  Vergewissern Sie sich im Dialogfeld **Indizes neu erstellen** , dass der richtige Index im Raster **Erneut zu erstellende Indizes** ausgewählt ist, und klicken Sie auf **OK**.  
  
7.  Aktivieren Sie das Kontrollkästchen **Spaltendaten großer Objekte komprimieren** , um anzugeben, dass alle Seiten mit umfangreichen Objektdaten (Large Object, LOB) komprimiert werden sollen.  
  
8.  Klicken Sie auf **OK.**  
  
## <a name="TsqlProcedureReorg"></a> Entfernen der Indexfragmentierung mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)] 
  
#### <a name="to-reorganize-a-fragmented-index"></a>So organisieren Sie einen fragmentierten Index neu  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize the IX_Employee_OrganizationalLevel_OrganizationalNode 
    -- index on the HumanResources.Employee table.   
  
    ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode 
      ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>So organisieren Sie alle Indizes in einer Tabelle neu  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-rebuild-a-fragmented-index"></a>So erstellen Sie einen fragmentierten Index neu  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im folgenden Beispiel wird ein einzelner Index in der `Employee` -Tabelle neu erstellt.  
  
     [!code-sql[IndexDDL#AlterIndex1](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_1.sql)]  
  
#### <a name="to-rebuild-all-indexes-in-a-table"></a>So erstellen Sie alle Indizes in einer Tabelle neu  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel in das Abfragefenster. In diesem Beispiel wird das `ALL`-Schlüsselwort verwendet. Hier werden alle der Tabelle zugeordneten Indizes neu erstellt. Es werden drei Optionen angegeben.  
  
     [!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_2.sql)]  
  
 Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
 
#### <a name="automatic-index-and-statistics-management"></a>Automatische Verwaltung von Index und Statistiken

Nutzen Sie Lösungen wie [Adaptive Index Defrag](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag), um die Indexdefragmentierung und das Aktualisieren der Statistiken für eine oder mehrere Datenbanken automatisch zu verwalten. Dieser Vorgang entscheidet unter anderem anhand des Fragmentierungsgrads automatisch, ob ein Index neu organisiert oder neu erstellt wird und aktualisiert Statistiken mit einem linearen Schwellenwert.
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
  [Handbuch zum SQL Server Indexentwurf](../../relational-databases/sql-server-index-design-guide.md)   
  [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
  [Adaptive Indexdefragmentierung](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)   
  [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
  [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
  
