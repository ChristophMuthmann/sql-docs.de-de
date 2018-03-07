---
title: ALTER SERVER CONFIGURATION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SERVER CONFIGURATION
- ALTER_SERVER_CONFIGURATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER CONFIGURATION, ALTER
- process affinity, setting
- ALTER SERVER CONFIGURATION statement
- setting process affinity
ms.assetid: f3059e42-5f6f-4a64-903c-86dca212a4b4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4489934ad1bb21c79cbb0ece01e7d061fd794c2a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-server-configuration-transact-sql"></a>ALTER SERVER CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert globale Konfigurationseinstellungen für den aktuellen Server in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER SERVER CONFIGURATION  
SET <optionspec>   
[;]  
  
<optionspec> ::=  
{  
     <process_affinity>  
   | <diagnostic_log>  
   | <failover_cluster_property>  
   | <hadr_cluster_context>  
   | <buffer_pool_extension>  
   | <soft_numa>  
}  
  
<process_affinity> ::=   
   PROCESS AFFINITY   
   {  
     CPU = { AUTO | <CPU_range_spec> }   
   | NUMANODE = <NUMA_node_range_spec>   
   }  
   <CPU_range_spec> ::=   
      { CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]   
  
   <NUMA_node_range_spec> ::=   
      { NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID } [ ,...n ]  
  
<diagnostic_log> ::=   
   DIAGNOSTICS LOG   
   {   
     ON    
   | OFF    
   | PATH = { 'os_file_path' | DEFAULT }    
   | MAX_SIZE = { 'log_max_size' MB | DEFAULT }    
   | MAX_FILES = { 'max_file_count' | DEFAULT }    
   }  
  
<failover_cluster_property> ::=   
   FAILOVER CLUSTER PROPERTY <resource_property>  
   <resource_property> ::=  
      {  
        VerboseLogging = { 'logging_detail' | DEFAULT }    
      | SqlDumperDumpFlags = { 'dump_file_type' | DEFAULT }  
      | SqlDumperDumpPath = { 'os_file_path'| DEFAULT }  
      | SqlDumperDumpTimeOut = { 'dump_time-out' | DEFAULT }  
      | FailureConditionLevel = { 'failure_condition_level' | DEFAULT }  
      | HealthCheckTimeout = { 'health_check_time-out' | DEFAULT }  
      }  
  
<hadr_cluster_context> ::=  
   HADR CLUSTER CONTEXT = { 'remote_windows_cluster' | LOCAL }  
  
<buffer_pool_extension>::=  
    BUFFER POOL EXTENSION   
    { ON ( FILENAME = 'os_file_path_and_name' , SIZE = <size_spec> )   
    | OFF }  
  
    <size_spec> ::=  
        { size [ KB | MB | GB ] }  
  
<soft_numa> ::=  
    SET SOFTNUMA  
    { ON | OFF }  
```  
  
## <a name="arguments"></a>Argumente  
 **\<Process_affinity >:: =**  
  
 PROCESS AFFINITY  
 Ermöglicht das Zuordnen von Hardwarethreads zu CPUs.  
  
 CPU = {AUTOMATISCH | \<CPU_range_spec >}  
 Verteilt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Arbeitsthreads auf alle im angegebenen Bereich enthaltenen CPUs. CPUs außerhalb des angegebenen Bereichs werden keine Threads zugewiesen.  
  
 AUTO  
 Gibt an, dass einer CPU kein Thread zugewiesen ist. Das Betriebssystem kann Threads auf der Grundlage der Serverarbeitsauslastung beliebig zwischen CPUs verschieben. Dies ist die Standardeinstellung und die empfohlene Einstellung.  
  
 \<CPU_range_spec >:: =  
 Gibt die CPU oder den Bereich von CPUs an, der bzw. denen Threads zugewiesen werden sollen.  
  
 { CPU_ID | CPU_ID TO CPU_ID } [ ,...n ]  
 Eine Liste mit mindestens einer CPU. CPU-IDs beginnen bei 0 und sind **Ganzzahl** Werte.  
  
 NUMANODE = \<NUMA_node_range_spec >  
 Weist allen CPUs, die um angegebenen NUMA-Knoten oder Bereich von Konten gehören, Threads zu.  
  
 \<NUMA_node_range_spec >:: =  
 Gibt den NUMA-Knoten oder den Bereich von NUMA-Knoten an.  
  
 { NUMA_node_ID | NUMA_node_ID  TO NUMA_node_ID } [ ,...n ]  
 Eine Liste mit mindestens einem NUMA-Knoten. NUMA-Knoten-IDs beginnen bei 0 und sind **Ganzzahl** Werte.  
  
 **\<Diagnostic_log >:: =**  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 DIAGNOSTICS LOG  
 Startet oder beendet die Protokollierung von Diagnosedaten, die von der sp_server_diagnostics-Prozedur erfasst wurden, und legt SQLDIAG-Protokollkonfigurationsparameter, wie z. B. die Anzahl der Protokolldateirollover, Protokolldateigröße und den Dateispeicherort, fest. Weitere Informationen finden Sie unter [Anzeigen und Lesen des Failoverclusterinstanz-Diagnoseprotokolls](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md).  
  
 ON  
 Startet die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Protokollierung von Diagnosedaten an dem in der PATH-Dateioption angegebenen Speicherort. Dies ist die Standardeinstellung.  
  
 OFF  
 Beendet die Protokollierung von Diagnosedaten.  
  
 PATH = { 'os_file_path' | DEFAULT }  
 Pfad, der den Speicherort für die Diagnoseprotokolle angibt. Der Standardspeicherort ist \<\MSSQL\Log > im Installationsordner von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Failoverclusterinstanz.  
  
 MAX_SIZE = { 'log_max_size' MB | DEFAULT }  
 Die maximale Größe (in MB) für jedes Diagnoseprotokoll. Die Standardeinstellung ist 100 MB.  
  
 MAX_FILES = { 'max_file_count' | DEFAULT }  
 Maximale Anzahl von Diagnoseprotokolldateien, die auf dem Computer gespeichert werden können, bevor sie für neue Diagnoseprotokolle wiederverwendet werden.  
  
 **\<Failover_cluster_property >:: =**  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 FAILOVER CLUSTER PROPERTY  
 Ändert die privaten Failoverclustereigenschaften der SQL Server-Ressource.  
  
 VERBOSE LOGGING = { 'logging_detail' | DEFAULT }  
 Legt den Protokolliergrad für SQL Server-Failoverclustering fest. Diese Option kann aktiviert werden, um in den Fehlerprotokollen für die Problembehandlung weitere Details bereitzustellen.  
  
-   0 – Die Protokollierung ist deaktiviert (Standard)  
  
-   1 – Nur Fehler  
  
-   2 – Fehler und Warnungen  
  
SQLDUMPEREDUMPFLAGS  
 Bestimmt den Typ der Dumpdateien, die vom SQL Server-Hilfsprogramm SQLDumper generiert werden. Die Standardeinstellung ist 0. Weitere Informationen finden Sie unter [SQL Server Dumper-Hilfsprogramm Knowledge Base-Artikel](http://go.microsoft.com/fwlink/?LinkId=206173).  
  
 SQLDUMPERDUMPPATH = { 'os_file_path' | DEFAULT }  
 Der Speicherort, an dem das Hilfsprogramm SQLDumper die Dumpdateien speichert. Weitere Informationen finden Sie unter [SQL Server Dumper-Hilfsprogramm Knowledge Base-Artikel](http://go.microsoft.com/fwlink/?LinkId=206173).  
  
 SQLDUMPERDUMPTIMEOUT = { 'dump_time-out' | DEFAULT }  
 Der Timeoutwert in Millisekunden für die Generierung eines Dumps durch das Hilfsprogramm SQLDumper bei einem SQL Server-Fehler. Der Standardwert ist 0; das bedeutet, dass das Fertigstellen des Dumps nicht zeitlich begrenzt ist. Weitere Informationen finden Sie unter [SQL Server Dumper-Hilfsprogramm Knowledge Base-Artikel](http://go.microsoft.com/fwlink/?LinkId=206173).  
  
 FAILURECONDITIONLEVEL = { 'failure_condition_level' | DEFAULT }  
 Die Bedingungen, unter denen für die SQL Server-Failoverclusterinstanz ein Failover oder Neustart durchgeführt werden soll. Der Standardwert ist 3; das bedeutet, dass für die SQL Server-Ressource bei kritischen Serverfehlern ein Failover oder Neustart durchgeführt wird. Weitere Informationen zu diesen und anderen fehlerbedingungsebenen finden Sie unter [Configure FailureConditionLevel Property Settings](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md).  
  
 HEALTHCHECKTIMEOUT = { 'health_check_time-out' | DEFAULT }  
 Der Timeoutwert, der festlegt, wie lange die Ressourcen-DLL des SQL Server-Datenbankmoduls auf Informationen über den Serverzustand warten soll, bevor eine Instanz von SQL Server als nicht reagierend eingestuft wird. Der Timeoutwert wird in Millisekunden angegeben. Der Standardwert beträgt 60.000 Millisekunden (60 Sekunden).  
  
 **\<Hadr_cluster_context >:: =**  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 HADR-CLUSTERKONTEXT  **=**  { **"***Remote_windows_cluster***"** | LOKALE}  
 Wechselt mit dem HADR-Clusterkontext der Serverinstanz zum angegebenen Windows Server Failover Clustering-Cluster (WSFC). Die *HADR-Clusterkontext* bestimmt, welche Cluster Windows Server Failover Clustering (WSFC) die Metadaten für von der Serverinstanz gehostete verfügbarkeitsreplikate verwaltet. Verwenden Sie die SET HADR CLUSTER CONTEXT-Option nur während einer clusterübergreifenden Migration von [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] zu einer Instanz von [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] oder höher auf einem neuen WSFC-Cluster.  
  
 Sie können mit dem HADR-Clusterkontext nur vom lokalen WSFC-Cluster zu einem Remotecluster und dann zurück vom Remotecluster zum lokalen Cluster wechseln. Der HADR-Clusterkontext kann nur zu einem Remotecluster wechseln, wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Verfügbarkeitsreplikate hostet.  
  
 Ein Remote-HADR-Clusterkontext kann jederzeit zurück zum lokalen Cluster wechseln. Der Kontext kann jedoch nicht erneut gewechselt werden, solange die Serverinstanz Verfügbarkeitsreplikate hostet.  
  
 Um den Zielcluster zu identifizieren, geben Sie einen der folgenden Werte an:  
  
 *Windows-Cluster*  
 Der Clusterobjektname (CON) eines WSFC-Clusters. Sie können entweder den Kurznamen oder den vollständigen Domänennamen angeben. ALTER SERVER CONFIGURATION sucht die Ziel-IP-Adresse eines Kurznamens mithilfe einer DNS-Auflösung. In einigen Situationen könnte ein Kurzname für Verwirrung sorgen, und DNS gibt möglicherweise die falsche IP-Adresse zurück. Daher empfiehlt es sich, dass Sie den vollständigen Domänennamen angeben.  
  
 LOCAL  
 Der lokale WSFC-Cluster.  
  
 Weitere Informationen finden Sie unter [ändern die HADR Cluster Context des Server-Instanz &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md).  
  
 **\<Buffer_pool_extension >:: =**  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ON  
 Aktiviert die Pufferpoolerweiterungsoption. Diese Option erweitert die Größe des Pufferpools, indem sie nicht flüchtigen Speicher wie Solid State Drives (SSD) verwendet, um nicht modifizierte Datenseiten im Pool beizubehalten. Weitere Informationen zu diesem Feature finden Sie unter [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md). Die pufferpoolerweiterung ist nicht in jeder Edition von SQL Server verfügbar. Weitere Informationen finden Sie unter [Editionen und unterstützte Funktionen für SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 FILENAME = 'os_file_path_and_name'  
 Definiert den Verzeichnispfad und den Namen der Cachedatei der Pufferpoolerweiterung. Die Dateierweiterung muss als .BPE angegeben werden. Sie müssen BUFFER POOL EXTENSION deaktivieren, bevor Sie FILENAME ändern können.  
  
 Größe = *Größe* [ **KB** | MB | GB]  
 Definiert die Größe des Caches. Die Standardgröße wird in KB angegeben. Die Mindestgröße ist die Größe des max. Serverarbeitsspeichers. Die maximale Anzahl ist die 32fache Größe von Max. Serverarbeitsspeicher. Weitere Informationen zu max. Serverarbeitsspeicher finden Sie unter [Sp_configure &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Sie müssen BUFFER POOL EXTENSION deaktivieren, bevor Sie die Größe der Datei ändern können. Um eine Größe anzugeben, die kleiner als die aktuelle Größe ist, muss die Instanz von SQL Server neu gestartet werden, um Arbeitsspeicher freizugeben. Andernfalls muss die angegebene Größe größer oder gleich der aktuellen Größe sein.  
  
 OFF  
 Deaktiviert die Pufferpoolerweiterungsoption. Sie müssen die Pufferpoolerweiterungsoption deaktivieren, bevor Sie alle zugeordneten Parameter wie die Größe oder den Namen der Datei ändern. Wenn diese Option deaktiviert wird, werden alle zugehörigen Konfigurationsdaten aus der Registrierung entfernt.  
  
> [!WARNING]  
>  Das Deaktivieren der Pufferpoolerweiterung könnte eine negative Auswirkung auf die Serverleistung haben, da die Größe des Pufferpools erheblich reduziert wird.  
  
 **\<Soft-NUMA verwenden >**  

**Gilt für**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ON  
 Ermöglicht die automatische Partitionierung zum Aufteilen von großer Hardware-NUMA-Knoten auf kleinere NUMA-Knoten. Ändern des laufenden Werts erfordert einen Neustart des Datenbankmoduls.  
  
 OFF  
 Deaktiviert die automatische Partitionierung von großen Hardware-NUMA-Knoten in kleinere NUMA-Knoten. Ändern des laufenden Werts erfordert einen Neustart des Datenbankmoduls.  

> [!WARNING]  
> Es sind Probleme mit dem Verhalten der ALTER SERVER CONFIGURATION-Anweisung mit der SOFT-NUMA-Option und die SQL Server-Agent bezeichnet.  Im folgenden finden die empfohlenen Abfolge der Vorgänge:  
> 1) Beenden Sie die Instanz von SQL Server-Agent.  
> 2) Führen Sie die ALTER SERVER CONFGURATION SOFT-NUMA-Option.  
> 3) Starten Sie SQL Server-Instanz neu.  
> 4) Starten Sie die Instanz von SQL Server-Agent.  
  
**Weitere Informationen:** Wenn eine ALTER SERVER CONFIGURATION SET SOFTNUMA-Befehl ausgeführt wird, bevor der SQL Server-Dienst, klicken Sie dann neu gestartet wird, wenn der SQL Server-Agent-Dienst beendet wird, führen Sie einen Konfigurieren von T-SQL-Befehl, der zurückgesetzt wird die SOFTNUMA Einstellungen sichern, bevor Sie die ALTER SERVER CONFIGURATION Originalwerts. 
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Diese Anweisung erfordert keinen Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sofern nicht ausdrücklich anders angegeben. Im Fall einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterinstanz ist kein Neustart der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Clusterressource erforderlich.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Diese Anweisung unterstützt keine DDL-Trigger.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert ALTER SETTINGS-Berechtigungen für die Prozessaffinitätsoption. ALTER SETTINGS- und VIEW SERVER STATE-Berechtigungen für Diagnoseprotokoll- und Failoverclustereigenschaften-Optionen und die CONTROL SERVER-Berechtigung für die HADR-Clusterkontextoption.  
  
 Erfordert die ALTER SERVER STATE-Berechtigung für die Pufferpoolerweiterungsoption.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ressourcen-DLL, die unter dem lokalen Systemkonto ausgeführt wird. Aus diesem Grund muss das lokale Systemkonto über Lese- und Schreibzugriff auf den in der Diagnoseprotokolloption angegebenen Pfad verfügen.  
  
## <a name="examples"></a>Beispiele  
  
|Kategorie|Funktionssyntaxelemente|  
|--------------|------------------------------|  
|[Festlegen der Prozessaffinität](#Affinity)|CPU • NUMANODE • AUTO|  
|[Festlegen von diagnoseprotokolloptionen](#Diagnostic)|ON • OFF • PATH • MAX_SIZE|  
|[Festlegen der failoverclustereigenschaften](#Failover)|HealthCheckTimeout|  
|[Ändern des clusterkontexts eines verfügbarkeitsreplikats](#ChangeClusterContextExample)|**"** *Windows-Cluster* **"**|  
|[Festlegen der pufferpoolerweiterung](#BufferPoolExtension)|BUFFER POOL EXTENSION|  
  
###  <a name="Affinity"></a>Festlegen der Prozessaffinität  
 Die Beispiele in diesem Abschnitt veranschaulichen, wie die Prozessaffinität für CPUs und NUMA-Knoten festgelegt wird. In den Beispielen wird davon ausgegangen, dass der Server 256 CPUs umfasst, die in vier Gruppen von jeweils 16 NUMA-Knoten unterteilt sind. Den NUMA-Knoten oder CPUs sind keine Threads zugewiesen.  
  
-   Gruppe "0": NUMA-Knoten 0 bis 3, CPUs 0 bis 63  
-   Gruppe 1: 4 bis 7, CPUs 64 bis 127 NUMA-Knoten  
-   Gruppe 2: 8 bis 12, CPUs 128 bis 191 NUMA-Knoten  
-   Gruppe 3: NUMA-Knoten 13 bis 16, CPUs 192 bis 255  
  
#### <a name="a-setting-affinity-to-all-cpus-in-groups-0-and-2"></a>A. Festlegen der Affinität für alle CPUs in den Gruppen 0 und 2  
 Im folgenden Beispiel wird die Affinität für alle CPUs in den Gruppen 0 und 2 festgelegt.  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 63, 128 TO 191;  
```  
  
#### <a name="b-setting-affinity-to-all-cpus-in-numa-nodes-0-and-7"></a>B. Festlegen der Affinität für alle CPUs in den NUMA-Knoten 0 und 7  
 Im folgenden Beispiel wird die CPU-Affinität für Knoten `0` und `7` nur.  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY NUMANODE=0, 7;  
```  
  
#### <a name="c-setting-affinity-to-cpus-60-through-200"></a>C. Festlegen der Affinität für die CPUs 60 bis 200  
 Im folgenden Beispiel wird die Affinität für die CPUs 60 bis 200 festgelegt.  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=60 TO 200;  
```  
  
#### <a name="d-setting-affinity-to-cpu-0-on-a-system-that-has-two-cpus"></a>D. Festlegen der Affinität auf einem System, das über zwei CPUs verfügt, für CPU 0  
 Im folgenden Beispiel wird die Affinität auf einem Computer, der über zwei CPUs verfügt, auf `CPU=0` festgelegt. Vor Ausführung der folgenden Anweisung ist die interne Affinitätsbitmaske 00.  
  
```  
ALTER SERVER CONFIGURATION SET PROCESS AFFINITY CPU=0;  
```  
  
#### <a name="e-setting-affinity-to-auto"></a>E. Festlegen der Affinität auf AUTO  
 Im folgenden Beispiel wird die Affinität auf `AUTO` festgelegt.  
  
```  
ALTER SERVER CONFIGURATION  
SET PROCESS AFFINITY CPU=AUTO;  
```  
  
###  <a name="Diagnostic"></a> Setting diagnostic log options  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Die Beispiele in diesem Abschnitt veranschaulichen, wie die Werte für die Diagnoseprotokolloption festgelegt werden.  
  
#### <a name="a-starting-diagnostic-logging"></a>A. Starten der Diagnoseprotokollierung  
 Im folgenden Beispiel wird die Protokollierung von Diagnosedaten gestartet.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
#### <a name="b-stopping-diagnostic-logging"></a>B. Beenden der Diagnoseprotokollierung  
 Im folgenden Beispiel wird die Protokollierung von Diagnosedaten beendet.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
#### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. Angeben des Speicherorts für die Diagnoseprotokolle  
 Im folgenden Beispiel wird der Speicherort für die Diagnoseprotokolle auf den angegebenen Dateipfad festgelegt.  
  
```  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
#### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. Angeben der maximalen Größe jedes Diagnoseprotokolls  
 Im folgenden Beispiel wird die maximale Größe jedes Diagnoseprotokolls auf 10 Megabytes festgelegt.  
  
```  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
###  <a name="Failover"></a>Festlegen der failoverclustereigenschaften  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel wird veranschaulicht, wie die Werte für die Ressourceneigenschaften des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusters festgelegt werden.  
  
#### <a name="a-specifying-the-value-for-the-healthchecktimeout-property"></a>A. Angeben des Werts für die HealthCheckTimeout-Eigenschaft  
 Im folgenden Beispiel wird die Option `HealthCheckTimeout` auf 15.000 Millisekunden (15 Sekunden) festgelegt.  
  
```  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
###  <a name="ChangeClusterContextExample"></a> B. Ändern des Clusterkontexts eines Verfügbarkeitsreplikats  
 Im folgenden Beispiel wird der HADR-Clusterkontext der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geändert. Angeben des wsfc-zielclusters `clus01`, im Beispiel wird der vollständige clusterobjektname, `clus01.xyz.com`.  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
### <a name="setting-buffer-pool-extension-options"></a>Festlegen der Pufferpoolerweiterungsoptionen  
  
####  <a name="BufferPoolExtension"></a> A. Festlegen der Pufferpoolerweiterungsoption  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel wird die Pufferpoolerweiterungsoption aktiviert, und es werden Name und Größe der Datei angegeben.  
  
```  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 50 GB);  
```  
  
#### <a name="b-modifying-buffer-pool-extension-parameters"></a>B. Ändern von Pufferpoolerweiterungsparametern  
 Im folgenden Beispiel wird die Größe einer Pufferpoolerweiterungsdatei geändert. Die Pufferpoolerweiterungsoption muss deaktiviert werden, bevor einer der Parameter geändert wird.  
  
```  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION OFF;  
GO  
EXEC sp_configure 'max server memory (MB)', 12000;  
GO  
RECONFIGURE;  
GO  
ALTER SERVER CONFIGURATION  
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 60 GB);  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Soft-NUMA &#40; SQLServer &#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)   
 [Ändern des HADR-Clusterkontexts der Serverinstanz &#40; SQLServer &#41;](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)   
 [DM_OS_SCHEDULERS &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)   
 [dm_os_memory_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md)   
 [Sys.dm_os_buffer_pool_extension_configuration &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)   
 [Pufferpoolerweiterung](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  
