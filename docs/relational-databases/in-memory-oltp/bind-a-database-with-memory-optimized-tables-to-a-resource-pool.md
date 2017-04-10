---
title: "Binden einer Datenbank mit speicheroptimierten Tabellen an einen Ressourcenpool | Microsoft Docs"
ms.custom: ""
ms.date: "08/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f222b1d5-d2fa-4269-8294-4575a0e78636
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Binden einer Datenbank mit speicheroptimierten Tabellen an einen Ressourcenpool
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Ein Ressourcenpool stellt eine Teilmenge der physischen Ressourcen dar, die kontrolliert werden können. Standardmäßig sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken an den Standardressourcenpool gebunden und nutzen dessen Ressourcen. Um die Auslastung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressourcen durch eine oder mehrere speicheroptimierte Tabellen und die Auslastung des für speicheroptimierte Tabellen erforderlichen Arbeitsspeichers durch andere Prozesse zu verhindern, wird empfohlen, einen eigenen Ressourcenpool zu erstellen, der die Arbeitsspeichernutzung für die Datenbank mit speicheroptimierten Tabellen verwaltet.  
  
 Eine Datenbank kann nur an einen Ressourcenpool gebunden werden. Sie können jedoch mehrere Datenbanken an denselben Pool binden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt das Binden einer Datenbank ohne speicheroptimierte Tabellen an einen Ressourcenpool, dies hat jedoch keine Auswirkungen. Sie sollten eine Datenbank an einen benannten Ressourcenpool binden, wenn Sie zu einem späteren Zeitpunkt möglicherweise speicheroptimierte Tabellen in der Datenbank erstellen möchten.  
  
 Bevor Sie eine Datenbank an einen Ressourcenpool binden können, müssen die Datenbank und der Ressourcenpool vorhanden sein. Die Bindung wird wirksam, wenn die Datenbank das nächste Mal online geschaltet wird. Weitere Informationen finden Sie unter [Database States](../../relational-databases/databases/database-states.md) .  
  
 Weitere Informationen zu Ressourcenpools finden Sie unter [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
## Schritte zum Binden einer Datenbank an einen Ressourcenpool  
  
1.  [Erstellen der Datenbank und des Ressourcenpools](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreatePool)  
  
    1.  [Erstellen der Datenbank](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreateDatabase)  
  
    2.  [Bestimmen des Mindestwerts für MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_DeterminePercent)  
  
    3.  [Erstellen eines Ressourcenpools und Konfigurieren des Arbeitsspeichers](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreateResourcePool)  
  
2.  [Binden der Datenbank an den Pool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_DefineBinding)  
  
3.  [Bestätigen der Bindung](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ConfirmBinding)  
  
4.  [Inkraftsetzen der Bindung](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_MakeBindingEffective)  
  
 Weitere Inhalte in diesem Thema  
  
-   [Ändern von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT für einen vorhandenen Pool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)  
  
-   [Prozentsatz des für speicheroptimierte Tabellen und Indizes verfügbaren Arbeitsspeichers](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)  
  
##  <a name="bkmk_CreatePool"></a> Erstellen der Datenbank und des Ressourcenpools  
 Sie können die Datenbank und den Ressourcenpool in beliebiger Reihenfolge erstellen. Wichtig ist, dass beide vor dem Binden der Datenbank an den Ressourcenpool bereits vorhanden sind.  
  
###  <a name="bkmk_CreateDatabase"></a> Erstellen der Datenbank  
 Durch folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] wird eine Datenbank mit dem Namen "IMOLTP_DB" erstellt, die mindestens eine speicheroptimierte Tabelle enthält. Der Pfad \<Laufwerk_und_Pfad> muss vor dem Ausführen dieses Befehls vorhanden sein.  
  
```tsql  
CREATE DATABASE IMOLTP_DB  
GO  
ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_fg CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_fg' , FILENAME = 'c:\data\IMOLTP_DB_fg') TO FILEGROUP IMOLTP_DB_fg;  
GO  
```  
  
###  <a name="bkmk_DeterminePercent"></a> Bestimmen des Mindestwerts für MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT  
 Sobald Sie die Arbeitsspeicheranforderungen für die speicheroptimierten Tabellen bestimmt haben, müssen Sie den erforderlichen Prozentsatz des verfügbaren Arbeitsspeichers bestimmen und die Arbeitsspeicherprozentsätze auf diesen oder einen höheren Wert festlegen.  
  
 **Beispiel:**   
In diesem Beispiel wird davon ausgegangen, dass Sie Ihre Berechnungen ergeben haben, dass die speicheroptimierten Tabellen und Indizes 16 GB Arbeitsspeicher benötigen. Weiter wird davon ausgegangen, dass Sie über 32 GB Arbeitsspeicher verfügen, der für Ihre Verwendung reserviert ist.  
  
 Auf den ersten Blick müssen Sie MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT scheinbar auf 50 festlegen (50 % von 32 ist 16).  Allerdings würde das Ihren speicheroptimierten Tabellen nicht genügend Arbeitsspeicher zur Verfügung stellen. In der folgenden Tabelle ([Prozentsatz des für speicheroptimierte Tabellen und Indizes verfügbaren Arbeitsspeichers](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)) sehen Sie, dass 32GB Arbeitsspeicher zugesichert sind, wovon jedoch nur 80% für speicheroptimierte Tabellen und Indizes zur Verfügung stehen.  Daher werden die Mindest- und Höchstprozentsätze auf Grundlage des verfügbaren Arbeitsspeichers und nicht des reservierten Arbeitsspeichers berechnet.  
  
 `memoryNeedeed = 16`   
 `memoryCommitted = 32`   
 `availablePercent = 0.8`   
 `memoryAvailable = memoryCommitted * availablePercent`   
 `percentNeeded = memoryNeeded / memoryAvailable`  
  
 Unter Verwendung der tatsächlichen Zahlen:   
`percentNeeded = 16 / (32 * 0.8) = 16 / 25.6 = 0.625`  
  
 Daher benötigen Sie mindestens 62,5 % des verfügbaren Arbeitsspeichers, um die Anforderung von 16 GB für die speicheroptimierten Tabellen und Indizes zu erfüllen.  Da die Werte für MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT ganze Zahlen sein müssen, werden sie auf mindestens 63 % festgelegt.  
  
###  <a name="bkmk_CreateResourcePool"></a> Erstellen eines Ressourcenpools und Konfigurieren des Arbeitsspeichers  
 Beim Konfigurieren des Arbeitsspeichers für speicheroptimierte Tabellen sollte die Kapazitätsplanung auf MIN_MEMORY_PERCENT und nicht auf MAX_MEMORY_PERCENT beruhen.  Weitere Informationen über MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT finden Sie unter [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md). Auf diese Weise ist die Speicherverfügbarkeit für speicheroptimierte Tabellen besser vorhersagbar, da MIN_MEMORY_PERCENT Arbeitsspeichermangel für andere Ressourcenpools verursacht, um die Verfügbarkeit zu gewährleisten. Um sicherzustellen, dass Arbeitsspeicher verfügbar ist, und um OOM-Bedingungen (Out of Memory, nicht genügend Arbeitsspeicher) zu vermeiden, sollten die Werte für MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT identisch sein. Unter [Prozentsatz des für speicheroptimierte Tabellen und Indizes verfügbaren Arbeitsspeichers](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable) unten finden Sie den Prozentsatz des verfügbaren Arbeitsspeichers für speicheroptimierte Tabellen basierend auf der Menge an zugesichertem Arbeitsspeicher.  
  
 Weitere Informationen zum Arbeiten in einer VM-Umgebung finden Sie unter [Bewährte Methoden: Verwenden von In-Memory OLTP in einer Umgebung mit virtuellen Computern](../Topic/Using%20In-Memory%20OLTP%20in%20a%20VM%20Environment.md).  
  
 Durch folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Code wird ein Ressourcenpool mit dem Namen "Pool_IMOLTP" erstellt. Die Hälfte des verfügbaren Arbeitsspeichers wird dem Pool zur Verfügung gestellt.  Nachdem der Pool erstellt wurde, wird die Ressourcenkontrolle neu konfiguriert, um "Pool_IMOLTP" einzuschließen.  
  
```tsql  
-- set MIN_MEMORY_PERCENT and MAX_MEMORY_PERCENT to the same value  
CREATE RESOURCE POOL Pool_IMOLTP   
  WITH   
    ( MIN_MEMORY_PERCENT = 63,   
    MAX_MEMORY_PERCENT = 63 );  
GO  
  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bkmk_DefineBinding"></a> Binden der Datenbank an den Pool  
 Binden Sie die Datenbank mithilfe der `sp_xtp_bind_db_resource_pool` -Systemfunktion an den Ressourcenpool. Die Funktion akzeptiert zwei Parameter: den Datenbanknamen und den Ressourcenpoolnamen.  
  
 Mit folgender [!INCLUDE[tsql](../../includes/tsql-md.md)] wird eine Bindung zwischen der IMOLTP_DB-Datenbank und dem Pool_IMOLTP-Ressourcenpool definiert. Die Bindung wird erst wirksam, nachdem die Datenbank online geschaltet wurde.  
  
```tsql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
 Die sp_xtp_bind_db_resourece_pool-Systemfunktion akzeptiert zwei Zeichenfolgenparameter: database_name und pool_name.  
  
##  <a name="bkmk_ConfirmBinding"></a> Bestätigen der Bindung  
 Bestätigen Sie die Bindung, und beachten Sie die Ressourcenpool-ID für IMOLTP_DB. Sie darf nicht NULL sein.  
  
```tsql  
SELECT d.database_id, d.name, d.resource_pool_id  
FROM sys.databases d  
GO  
```  
  
##  <a name="bkmk_MakeBindingEffective"></a> Inkraftsetzen der Bindung  
 Nachdem die Datenbank an den Ressourcenpool gebunden wurde, müssen Sie sie offline und anschließend wieder online schalten, damit die Bindung wirksam wird. Wenn die Datenbank zuvor an einen anderen Pool gebunden war, wird dadurch der zugeordnete Arbeitsspeicher aus dem vorherigen Ressourcenpool entfernt, und die Speicherbelegungen für die speicheroptimierte Tabelle und die Indizes stammen jetzt aus dem neu an die Datenbank gebundenen Ressourcenpool.  
  
```tsql  
USE master  
GO  
  
ALTER DATABASE IMOLTP_DB SET OFFLINE  
GO  
ALTER DATABASE IMOLTP_DB SET ONLINE  
GO  
  
USE IMOLTP_DB  
GO  
```  
  
 Jetzt ist die Datenbank an den Ressourcenpool gebunden.  
  
##  <a name="bkmk_ChangeAllocation"></a> Ändern von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT für einen vorhandenen Pool  
 Wenn Sie dem Server zusätzlichen Arbeitsspeicher hinzufügen oder sich die für die speicheroptimierten Tabellen erforderliche Menge an Arbeitsspeicher ändert, müssen Sie möglicherweise den Wert von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT ändern. Die folgenden Schritte veranschaulichen, wie Sie den Wert von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT für einen Ressourcenpool ändern. Richtlinien für die für MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT zu verwendenden Werte finden Sie im entsprechenden Abschnitt weiter unten.  Weitere Informationen finden Sie im Thema [Bewährte Methoden: Verwenden von In-Memory OLTP in einer Umgebung mit virtuellen Computern](../Topic/Using%20In-Memory%20OLTP%20in%20a%20VM%20Environment.md).  
  
1.  Ändern Sie den Wert von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT mithilfe von `ALTER RESOURCE POOL`.  
  
2.  Verwenden Sie `ALTER RESURCE GOVERNOR`, um die Ressourcenkontrolle mit den neuen Werten neu zu konfigurieren.  
  
 **Beispielcode**  
  
```tsql  
ALTER RESOURCE POOL Pool_IMOLTP  
WITH  
     ( MIN_MEMORY_PERCENT = 70,  
       MAX_MEMORY_PERCENT = 70 )   
GO  
  
-- reconfigure the Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
##  <a name="bkmk_PercentAvailable"></a> Prozentsatz des für speicheroptimierte Tabellen und Indizes verfügbaren Arbeitsspeichers  
 Wenn Sie eine Datenbank mit speicheroptimierten Tabellen und eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Arbeitsauslastung demselben Ressourcenpool zuordnen, legt die Ressourcenkontrolle einen internen Schwellenwert für [!INCLUDE[hek_2](../../includes/hek-2-md.md)] fest, damit bei der Poolverwendung keine Konflikte auftreten. Im Allgemeinen liegt der Nutzungsschwellenwert für [!INCLUDE[hek_2](../../includes/hek-2-md.md)] bei ca. 80 % des Pools. In der folgenden Tabelle sind tatsächliche Schwellenwerte für verschiedene Arbeitsspeichergrößen angegeben.  
  
 Wenn Sie einen dedizierten Ressourcenpool für die [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Datenbank erstellen, müssen Sie schätzen, wie viel physischer Arbeitsspeicher nach Berücksichtigung von Zeilenversionen und Datenzunahme für die Tabellen im Arbeitsspeicher benötigt wird. Nach dem Schätzen des benötigten Arbeitsspeichers erstellen Sie einen Ressourcenpool mit einem Prozentwert des Commit-Zielarbeitsspeichers für die SQL-Instanz, wie durch die Spalte „committed_target_kb“ im DMV `sys.dm_os_sys_info` dargestellt (siehe [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)). Sie können beispielsweise einen Ressourcenpool "P1" mit 40 % des gesamten Arbeitsspeichers erstellen, der für die Instanz verfügbar ist. Von diesen 40 % erhält das [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Modul einen kleineren Prozentsatz zum Speichern von [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Daten.  So wird sichergestellt, dass [!INCLUDE[hek_2](../../includes/hek-2-md.md)] nicht den gesamten Arbeitsspeicher aus diesem Pool beansprucht.  Der Wert des kleineren Prozentsatzes ist abhängig vom zugesicherten Zielspeicher. In der folgenden Tabelle wird der für eine [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Datenbank in einem Ressourcenpool (benannt oder Standard) verfügbare Arbeitsspeicher aufgeführt, bevor ein OOM-Fehler ausgelöst wird.  
  
|Zugesicherter Zielspeicher|Für speicherinterne Tabellen verfügbarer Prozentsatz|  
|-----------------------------|---------------------------------------------|  
|<= 8 GB|70 %|  
|<= 16 GB|75%|  
|<= 32 GB|80%|  
|\<= 96 GB|85%|  
|>96 GB|90%|  
  
 Wenn der zugesicherte Zielspeicher beispielsweise 100 GB beträgt und Sie schätzen, dass für die speicheroptimierten Tabellen und Indizes 60 GB Arbeitsspeicher benötigt werden, können Sie einen Ressourcenpool mit MAX_MEMORY_PERCENT = 67 erstellen (60 GB erforderlich/0,90 = 66,667 GB – aufgerundet auf 67 GB; 67 GB/100 GB installiert = 67 %). So wird sichergestellt, dass für die [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Objekte die erforderlichen 60 GB vorhanden sind.  
  
 Sobald eine Datenbank an einen benannten Ressourcenpool gebunden wurde, können Sie mit der folgenden Abfrage die Speicherbelegungen für unterschiedliche Ressourcenpools anzeigen.  
  
```tsql  
SELECT pool_id  
     , Name  
     , min_memory_percent  
     , max_memory_percent  
     , max_memory_kb/1024 AS max_memory_mb  
     , used_memory_kb/1024 AS used_memory_mb   
     , target_memory_kb/1024 AS target_memory_mb  
   FROM sys.dm_resource_governor_resource_pools  
```  
  
 Diese Beispielausgabe zeigt, dass speicheroptimierte Objekte 1.356 MB Arbeitsspeicher im Ressourcenpool "PoolIMOLTP" mit einer oberen Grenze von 2.307 MB belegen. Diese Obergrenze steuert, wie viel Arbeitsspeicher insgesamt von speicheroptimierten Benutzer- und Systemobjekten belegt werden kann, die dem Pool zugeordnet sind.  
  
 **Beispielausgabe**   
Diese Ausgabe stammt aus der oben erstellten Datenbank und den entsprechenden Tabellen.  
  
```  
pool_id     Name        min_memory_percent max_memory_percent max_memory_mb used_memory_mb target_memory_mb  
----------- ----------- ------------------ ------------------ ------------- -------------- ----------------   
1           internal    0                  100                3845          125            3845  
2           default     0                  100                3845          32             3845  
259         PoolIMOLTP 0                  100                3845          1356           2307  
```  
  
 Weitere Informationen finden Sie unter [sys.dm_resource_governor_resource_pools (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
 Wenn Sie die Datenbank nicht an einen benannten Ressourcenpool binden, wird sie an den Pool "default" gebunden. Da der Standardressourcenpool von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die meisten anderen Zuordnungen verwendet wird, können Sie nicht die DMV "sys.dm_resource_governor_resource_pools" verwenden, um den von speicheroptimierten Tabellen beanspruchten Arbeitsspeicher für die gewünschte Datenbank exakt zu überwachen.  
  
## Siehe auch  
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)   
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Erstellen eines Ressourcenpools](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Ändern der Einstellungen für den Ressourcenpool](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [Löschen eines Ressourcenpools](../../relational-databases/resource-governor/delete-a-resource-pool.md)  
  
  