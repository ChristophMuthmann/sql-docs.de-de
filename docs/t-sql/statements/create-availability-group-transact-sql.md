---
title: "Erstellen der VERFÜGBARKEITSGRUPPE (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVAILABILITY GROUP
- CREATE_AVAILABILITY_TSQL
- CREATE_AVAILABILITY_GROUP_TSQL
- CREATE AVAILABILITY GROUP
- CREATE AVAILABILITY
- AVAILABILITY_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- CREATE AVAILABILITY GROUP statement
- Availability Groups [SQL Server], creating
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: a3d55df7-b4e4-43f3-a14b-056cba36ab98
caps.latest.revision: 196
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cebeb43402be1762021738096b9a0e959082d986
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-availability-group-transact-sql"></a>CREATE AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Erstellt eine neue Verfügbarkeitsgruppe, wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Funktion aktiviert wird.  
  
> [!IMPORTANT]  
>  Führen Sie CREATE AVAILABILITY GROUP auf die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus, die als ursprüngliches primäres Replikat der neuen Verfügbarkeitsgruppe verwendet werden soll. Diese Serverinstanz muss sich in einem WSFC-Knoten (Windows Server Failover Clustering) befinden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE AVAILABILITY GROUP group_name  
   WITH (<with_option_spec> [ ,...n ] )  
   FOR [ DATABASE database_name [ ,...n ] ]  
   REPLICA ON <add_replica_spec> [ ,...n ]  
   AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   [ LISTENER ‘dns_name’ ( <listener_option> ) ]  
[ ; ]  
  
<with_option_spec>::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | BASIC  
  | DISTRIBUTED
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  | CLUSTER_TYPE = { WSFC | EXTERNAL | NONE } 
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL }  
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL } ]   
        [,] [ READ_ONLY_ROUTING_URL = 'TCP://system-address:port' ]  
     } )  
     | PRIMARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { READ_WRITE | ALL } ]   
        [,] [ READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE } ]  
     } )  
     | SESSION_TIMEOUT = integer  
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’    
  
  <ip_address_option> ::=  
     {   
        ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’  
      | ‘ipv6_address’  
     }  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Gruppenname*  
 Gibt den Namen der neuen Verfügbarkeitsgruppe an. *Gruppenname* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Bezeichner](../../relational-databases/databases/database-identifiers.md), und es in allen Verfügbarkeitsgruppen im WSFC-Cluster muss eindeutig sein. Die maximale Länge eines Verfügbarkeitsgruppennamens beträgt 128 Zeichen.  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {PRIMÄREN | SECONDARY_ONLY | SEKUNDÄRE | KEINE}  
 Legt fest, wie ein Sicherungsauftrag das primäre Replikat auswerten soll, wenn ausgewählt wird, wo Sicherungen ausgeführt werden müssen. Sie können einen gegebenen Sicherungsauftrag erstellen, um die automatisierte Sicherungseinstellung zu berücksichtigen. Die Einstellung wird nicht von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erzwungen und weist deshalb keine Auswirkungen auf Ad-hoc-Sicherungen auf.  
  
 Die folgenden Werte werden unterstützt:  
  
 PRIMARY  
 Gibt an, dass die Sicherungen immer auf dem primären Replikat erfolgen müssen. Diese Option ist hilfreich, wenn Sie Sicherungsfunktionen benötigen, z. B. das Erstellen differenzieller Sicherungen, die nicht unterstützt werden, wenn die Sicherung auf einem sekundären Replikat ausgeführt wird.  
  
> [!IMPORTANT]  
>  Wenn Sie den Protokollversand verwenden möchten, um sekundäre Datenbanken auf eine Verfügbarkeitsgruppe vorzubereiten, legen Sie die Voreinstellung für automatisierte Sicherungen auf **Primär** fest, bis alle sekundären Datenbanken vorbereitet und mit der Verfügbarkeitsgruppe verknüpft worden sind.  
  
 SECONDARY_ONLY  
 Gibt an, dass Sicherungen nie auf dem primären Replikat ausgeführt werden dürfen. Wenn es sich beim primären Replikat um das einzige Onlinereplikat handelt, darf keine Sicherung erfolgen.  
  
 SECONDARY  
 Gibt an, dass Sicherungen auf einem sekundären Replikat erfolgen müssen, außer wenn es sich beim primären Replikat um das einzige Onlinereplikat handelt. In diesem Fall muss die Sicherung auf dem primären Replikat erfolgen. Dies ist das Standardverhalten.  
  
 Keine  
 Gibt an, dass Sicherungsaufträge die Rolle der Verfügbarkeitsreplikate ignorieren sollen, wenn sie das Replikat zum Durchführen der Sicherungen auswählen. Hinweis: Sicherungsaufträge können andere Faktoren auswerten, wie z. B. die Sicherungspriorität jedes Verfügbarkeitsreplikats in Verbindung mit seinem Betriebszustand und Verbindungsstatus.  
  
> [!IMPORTANT]  
>  Die Einstellung AUTOMATED_BACKUP_PREFERENCE wird nicht erzwungen. Die Interpretation dieser Einstellung hängt von der Logik ab, die Sie ggf. per Skript in Sicherungsaufträge für die Datenbanken in einer angegebenen Verfügbarkeitsgruppe integriert haben. Die Voreinstellung für die automatisierte Sicherung hat keine Auswirkungen auf Ad-hoc-Sicherungen. Weitere Informationen finden Sie unter [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  Um die automatisierte sicherungseinstellung einer vorhandenen verfügbarkeitsgruppe anzuzeigen, wählen Sie die **Automated_backup_preference** oder **Automated_backup_preference_desc** Spalte die [ availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) -Katalogsicht angezeigt. Darüber hinaus [Sys. fn_hadr_backup_is_preferred_replica &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) können verwendet werden, um das bevorzugte sicherungsreplikat zu bestimmen.  Diese Funktion gibt 1 für mindestens eines der Replikate, selbst wenn `AUTOMATED_BACKUP_PREFERENCE = NONE`.  
  
 FAILURE_CONDITION_LEVEL  **=**  {1 | 2 | **3** | 4 | 5}  
 Gibt an, welche fehlerbedingungen ein automatisches Failover für diese verfügbarkeitsgruppe auslösen. FAILURE_CONDITION_LEVEL wird auf Gruppenebene festgelegt, aber spielt nur auf verfügbarkeitsreplikaten, die für den Verfügbarkeitsmodus für synchrone Commits konfiguriert sind (AVAILIBILITY_MODE  **=**  SYNCHRONOUS_COMMIT). Weiterhin können fehlerbedingungen ein automatisches Failover auslösen, nur dann, wenn die primären und sekundären Replikate für den automatischen Failovermodus konfiguriert sind (FAILOVER_MODE  **=**  automatische) und das sekundäre Replikat ist. derzeit synchronisiert mit dem primären Replikat.  
  
 Die Fehlerbedingungsebenen (1-5) reichen von der Ebene 1 mit den wenigsten Einschränkungen bis zur Ebene 5 mit den meisten Einschränkungen. Jede Bedingungsebene umfasst stets auch sämtliche weniger restriktiven Ebenen. Daher schließt die strengste Bedingungsebene 5 die vier Bedingungsebenen mit weniger Einschränkungen (1-4) ein, Ebene 4 schließt die Ebenen 1-3 ein usw. In der folgenden Tabelle wird die Fehlerbedingung beschrieben, die der jeweiligen Ebene entspricht.  
  
|Ebene|Fehlerbedingung|  
|-----------|-----------------------|  
|1|Gibt an, dass in einem der folgenden Fälle ein automatisches Failover initiiert werden muss:<br /><br /> – Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ist ausgefallen.<br /><br /> -Das Leasing der verfügbarkeitsgruppe für die Verbindung mit dem wsfc-Cluster läuft ab, da keine ACK-Meldung von der Serverinstanz empfangen wird. Weitere Informationen finden Sie unter [How It Works: SQL Server AlwaysOn Lease Timeout](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-AlwaysOn-lease-timeout.aspx).|  
|2|Gibt an, dass in einem der folgenden Fälle ein automatisches Failover initiiert werden muss:<br /><br /> – Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Verbindung zum Cluster her und der verfügbarkeitsgruppe der Benutzer angegebene HEALTH_CHECK_TIMEOUT-Schwellenwert überschritten wird.<br /><br /> -Das verfügbarkeitsreplikat ist im Status "Fehler".|  
|3|Gibt an, dass ein automatisches Failover bei kritischen internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlern initiiert werden soll, z. B. verwaisten Spinlocks, schwerwiegenden Schreibzugriffsverletzungen oder zu vielen Sicherungen.<br /><br /> Dies ist das Standardverhalten.|  
|4|Gibt an, dass ein automatisches Failover bei mittelschweren internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlern initiiert werden soll, z. B. bei dauerhaft unzureichendem Arbeitsspeicher im internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressourcenpool.|  
|5|Gibt an, dass ein automatisches Failover bei sämtlichen qualifizierten Fehlerbedingungen initiiert werden soll, einschließlich:<br /><br /> -Erschöpfung der SQL Engine-Arbeitsthreads.<br /><br /> -Erkennung eines unlösbaren Deadlocks.|  
  
> [!NOTE]  
>  Fehlen einer Reaktion von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client Anforderungen ist nicht relevant für Verfügbarkeitsgruppen.  
  
 Der FAILURE_CONDITION_LEVEL- und der HEALTH_CHECK_TIMEOUT-Wert definieren eine *flexible Failoverrichtlinie für* für eine bestimmte Gruppe. Diese flexible Failoverrichtlinie bietet eine präzise Kontrolle der Bedingungen, die ein automatisches Failover verursachen müssen. Weitere Informationen finden Sie unter [Flexible Failoverrichtlinie für automatisches Failover einer Verfügbarkeitsgruppe &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *Millisekunden*  
 Gibt die Wartezeit (in Millisekunden) für die [Sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) gespeicherte Systemprozedur Serverzustand Informationen zurückgegeben werden sollen, bevor der wsfc-Cluster wird davon ausgegangen, dass die Serverinstanz langsam oder blockiert ist. HEALTH_CHECK_TIMEOUT wird auf Gruppenebene festgelegt, aber spielt nur auf verfügbarkeitsreplikaten, die für den Verfügbarkeitsmodus für synchrone Commits mit automatischem Failover konfiguriert sind (AVAILIBILITY_MODE  **=**  SYNCHRONE _COMMIT).  Darüber hinaus kann ein integritätsprüfungstimeout ein automatisches Failover auslösen, nur dann, wenn die primären und sekundären Replikate für den automatischen Failovermodus konfiguriert sind (FAILOVER_MODE  **=**  automatische) und der sekundären Datenbank Replikat ist derzeit mit dem primären Replikat synchronisiert.  
  
 Der standardmäßige HEALTH_CHECK_TIMEOUT-Wert beträgt 30.000 Millisekunden (30 Sekunden). Der minimale Wert beträgt 15.000 Millisekunden (15 Sekunden) und der maximale Wert 4.294.967.295 Millisekunden.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** führt keine Integritätsprüfungen auf Datenbankebene aus.  
  
 DB_FAILOVER  **=**  {ON | {OFF}  
 Gibt die Antwort an, die bei eine Datenbank auf dem primären Replikat offline ist. Alle Status außer ONLINE für eine Datenbank in der verfügbarkeitsgruppe auf ON festgelegt, wird ein automatisches Failover ausgelöst. Wenn diese Option auf OFF festgelegt ist, wird nur die Integrität der Instanz verwendet, auf Automatisches Failover auslösen.  
  
  Weitere Informationen zu dieser Einstellung finden Sie unter [Datenbankoption für die Erkennung von Ebene Integrität](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 
  
 DTC_SUPPORT  **=**  {PER_DB | KEINE}  
 Gibt an, ob die datenbankübergreifende Transaktionen über dem distributed Transaction Coordinator (DTC) unterstützt werden. Datenbankübergreifende Transaktionen werden nur unterstützt ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. PER_DB wird die verfügbarkeitsgruppe mit Unterstützung für diese Transaktionen erstellt. Weitere Informationen finden Sie unter [Datenbankübergreifende Transaktionen und verteilte Transaktionen für Always On-Verfügbarkeitsgruppen oder Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
 BASIC  
 Dient zum Erstellen einer Basis-verfügbarkeitsgruppe. Basis-Verfügbarkeitsgruppen auf einer Datenbank und zwei Replikate beschränkt werden: ein primäres Replikat und ein sekundäres Replikat. Diese Option ist ein Ersatz für veraltete Datenbankspiegelungsfunktion in SQL Server Standard Edition. Weitere Informationen finden Sie unter [Basis-Verfügbarkeitsgruppen &#40; Always On-Verfügbarkeitsgruppen &#41; ](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md). Basis-Verfügbarkeitsgruppen werden unterstützt ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  

 DISTRIBUTED  
 Dient zum Erstellen einer verteilten verfügbarkeitsgruppe. Diese Option wird mit dem AVAILABILITY GROUP ON-Parameter verwendet, die Verbindung zwei Verfügbarkeitsgruppen in separate Windows Server-Failovercluster.  Weitere Informationen finden Sie unter [Verteilte Verfügbarkeitsgruppen &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md). Verteilte Verfügbarkeitsgruppen werden unterstützt ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. 

 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 In SQL Server 2017 CTP 2.2 eingeführt. Dient zum Festlegen einer minimalen Anzahl von synchrone sekundäre Replikate erforderlich, um einen Commit auszuführen, bevor die primäre eine Transaktion ein Commit ausgeführt wird. Garantiert, dass SQL Server-Transaktion wartet, bis die Transaktionsprotokolle für die minimale Anzahl von sekundären Replikaten aktualisiert werden. Der Standardwert ist 0. das gleiche Verhalten wie SQL Server 2016 bietet. Der minimale Wert ist 0. Der maximale Wert ist die Anzahl der Replikate minus 1. Diese Option bezieht sich auf die Replikate im synchronen Commit-Modus. Wenn Replikate im synchronen Commit-Modus befinden, Schreibvorgänge auf dem primären Replikat warten, bis der Schreibvorgänge auf den sekundären Replikaten für synchrone Commit im Transaktionsprotokoll der Replikat-Datenbank. Wenn eine SQL-Server, die ein synchrone sekundäre Replikat hostet, nicht mehr reagiert, markiert der SQL-Server, die das primäre Replikat hostet dieses sekundäre Replikat als nicht synchronisiert, und fahren Sie fort. Wenn die nicht reagierende Datenbank wieder online geschaltet wird befindet sich in einem Zustand "nicht synchronisiert", und das Replikat als fehlerhaft markiert, bis das primäre synchronen Vorgang erleichtern kann. Diese Einstellung wird sichergestellt, dass das primäre Replikat wartet, bis die minimale Anzahl der Replikate für jede Transaktion ein Commit ausgeführt wurde. Wenn die minimale Anzahl der Replikate nicht verfügbar ist, führen Sie anschließend Commits auf dem primären Replikat. Diese Einstellung gilt für Verfügbarkeitsgruppen mit Clustertyp `WSFC` und `EXTERNAL`. Für Clustertyp `EXTERNAL` die Einstellung geändert wird, wenn die Clusterressource die verfügbarkeitsgruppe hinzugefügt wird. Finden Sie unter [hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](../../linux/sql-server-linux-availability-group-ha.md).

 CLUSTER_TYPE  
 In SQL Server 2017 CTP 2.2 eingeführt. Verwendet, um festzustellen, ob die verfügbarkeitsgruppe auf einem Windows Server Failover Cluster (WSFC) ist.  Auf WSFC festgelegt, wenn die verfügbarkeitsgruppe auf eine Failoverclusterinstanz auf einem Windows Server-Failovercluster ist. Auf EXTERNEN festgelegt, wenn der Cluster von einem Cluster-Manager verwaltet wird, die nicht auf einem Windows Server-Failovercluster, wie Linux Schrittmacher ist. Beim Gruppieren von Verfügbarkeit mithilfe von WSFC nicht für Cluster Koordinierung auf NONE festgelegt. Angenommen, wenn eine verfügbarkeitsgruppe Linux-Servern enthält. 

 Datenbank *Database_name*  
 Gibt eine Liste mit mindestens einer Benutzerdatenbank auf der lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz an (der Serverinstanz, auf der Sie die Verfügbarkeitsgruppe erstellen). Sie können mehrere Datenbanken für eine Verfügbarkeitsgruppe angeben, aber jede Datenbank kann nur zu einer Verfügbarkeitsgruppe gehören. Weitere Informationen zu den Typ von Datenbanken, die eine verfügbarkeitsgruppe unterstützt werden, finden Sie unter [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). Um herauszufinden, welche lokalen Datenbanken bereits zu einer verfügbarkeitsgruppe gehören, finden Sie unter der **Replica_id** Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.  
  
 Die DATABASE-Klausel ist optional. Wenn Sie ihn weglassen, ist die neue verfügbarkeitsgruppe leer.  
  
 Nachdem Sie die verfügbarkeitsgruppe erstellt haben, eine Verbindung mit jeder Serverinstanz, die ein sekundäres Replikat hostet und klicken Sie dann jede sekundäre Datenbank vorbereiten, und mit der verfügbarkeitsgruppe zu verknüpfen. Weitere Informationen finden Sie unter [Starten der Datenverschiebung auf einer sekundären Always On-Datenbank &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
> [!NOTE]  
>  Später können Sie berechtigte Datenbanken auf der Serverinstanz hinzufügen, die das primäre Replikat für eine Verfügbarkeitsgruppe hostet. Sie können zudem eine Datenbank aus einer Verfügbarkeitsgruppe entfernen. Weitere Informationen finden Sie unter [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)hinzugefügt wird.  
  
 REPLICA ON  
 Gibt eine bis fünf SQL Server-Instanzen als Hostverfügbarkeitsreplikate in der neuen Verfügbarkeitsgruppe an.  Jedes Replikat wird von seiner Serverinstanzadresse gefolgt von einer WITH (…)-Klausel angegeben. Sie müssen mindestens die lokale Serverinstanz angeben, die das ursprüngliche primäre Replikat wird. Optional können Sie auch bis zu vier sekundäre Replikate angeben.  
  
 Sie müssen jedes sekundäre Replikat mit der Verfügbarkeitsgruppe verknüpfen. Weitere Informationen finden Sie unter [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)hinzugefügt wird.  
  
> [!NOTE]  
>  Wenn Sie weniger als vier sekundäre Replikate angeben, wenn Sie eine verfügbarkeitsgruppe erstellen, können Sie ein zusätzliches sekundäres Replikat zu einem beliebigen Zeitpunkt mithilfe der [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung. Außerdem können Sie mit dieser Anweisung alle sekundären Replikate aus einer vorhandenen Verfügbarkeitsgruppe entfernen.  
  
 \<Server_instance > Gibt die Adresse der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die als Host für ein Replikat. Das Adressformat hängt davon ab, ob die Instanz die Standardinstanz oder eine benannte Instanz ist und ob es eine eigenständige Instanz oder eine Failoverclusterinstanz (FCI) ist, wie dies im Folgenden beschrieben ist:  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 Diese Adresse weist die folgenden Komponenten auf:  
  
 *system_name*  
 Der NetBIOS-Name des Computersystems, auf dem sich eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zielinstanz befindet. Dieser Computer muss ein WSFC-Knoten sein.  
  
 *FCI_network_name*  
 Ist der Netzwerkname, der verwendet wird, um auf einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failovercluster zuzugreifen. Verwenden Sie diesen Namen, wenn die Serverinstanz als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverpartner beteiligt ist. Zur Ausführung von SELECT- [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) auf einer FCI-Serverinstanz gibt die gesamte '*FCI_network_name*[\\*Instance_name*]' Zeichenfolge (also die vollständigen replikatnamen).  
  
 *instance_name*  
 Der Name einer Instanz von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gehostet wird *System_name* oder *FCI_network_name* und mit dem HADR-Dienst aktiviert ist. Bei einer Standardserverinstanz ist *instance_name* optional. Bei dem Instanznamen wird die Groß-/Kleinschreibung berücksichtigt. Auf einer eigenständigen Serverinstanz Name dieses Werts ist identisch mit den Rückgabewert von zur Ausführung von SELECT- [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md).  
  
 \  
 Ein Trennzeichen verwendet werden, nur bei der Angabe *Instance_name*, um sie über separate *System_name* oder *FCI_network_name*.  
  
 Informationen zu den erforderlichen Komponenten für wsfc-Knoten und Serverinstanzen finden Sie unter [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL **= "**TCP**://***Systemadresse***:***Port***"**  
 Gibt den URL-Pfad für die [datenbankspiegelungsendpunkt](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md) für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die das verfügbarkeitsreplikat hostet, die Sie in der aktuellen REPLICA ON-Klausel definieren.  
  
 Die ENDPOINT_URL-Klausel ist erforderlich. Weitere Informationen finden Sie unter [Angeben der Endpunkt-URL beim Hinzufügen oder Ändern eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)zu unterstützen.  
  
 **"**TCP**://***Systemadresse***:***Port***"**  
 Gibt eine URL zum Bestimmen einer Endpunkt-URL oder einer URL für das schreibgeschützte Routing an. Die URL-Parameter lauten wie folgt:  
  
 *system-address*  
 Ist eine Zeichenfolge, beispielsweise ein Systemname, ein vollqualifizierter Domänenname oder eine IP-Adresse, die das Zielcomputersystem eindeutig identifiziert.  
  
 *port*  
 Ist eine Portnummer, die dem Spiegelungsendpunkt der Partnerserverinstanz (für die ENDPOINT_URL-Option) oder der Portnummer, die von [!INCLUDE[ssDE](../../includes/ssde-md.md)] der Serverinstanz (für die READ_ONLY_ROUTING_URL-Option) verwendet wird, zugeordnet ist.  
  
 AVAILABILITY_MODE  **=**  {{SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT}  
 SYNCHRONOUS_COMMIT oder ASYNCHRONOUS_COMMIT gibt an, ob das primäre Replikat warten Sie, bis das sekundäre Replikat zum Bestätigen des verstärken (Schreiben), der die Protokolldatensätze auf den Datenträger, bevor das primäre Replikat die Transaktion auf einem angegebenen primären übergeben werden können die Datenbank. Die Transaktionen auf anderen Datenbanken über dasselbe primäre Replikat können unabhängig einen Commit ausführen.
  
 SYNCHRONOUS_COMMIT  
 Gibt an, dass das primäre Replikat wartet, bis sie auf diesem sekundären Replikat (Modus mit synchronem Commit) festgeschrieben wurden ein commit für Transaktionen. Sie können SYNCHRONOUS_COMMIT für bis zu drei Replikate angeben, einschließlich des primären Replikats.  
  
 ASYNCHRONOUS_COMMIT  
 Gibt an, dass das primäre Replikat einen Commit für Transaktionen ausführt, ohne zu warten, bis dieses sekundäre Replikat das Protokoll verstärkt (Verfügbarkeitsmodus mit synchronem Commit). Sie können ASYNCHRONOUS_COMMIT für bis zu fünf Verfügbarkeitsreplikate angeben, einschließlich des primären Replikats.  
  
 Die AVAILABILITY_MODE-Klausel ist erforderlich. Weitere Informationen finden Sie unter [Verfügbarkeitsmodi &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)ausgetauscht werden.  
  
 FAILOVER_MODE  **=**  {AUTOMATISCHE | MANUELLE}  
 Gibt den Failovermodus des Verfügbarkeitsreplikats an, das Sie definieren.  
  
 AUTOMATIC  
 Aktiviert das automatische Failover. Diese Option wird nur unterstützt, wenn Sie auch AVAILABILITY_MODE = SYNCHRONOUS_COMMIT angeben. Sie können AUTOMATIC für zwei Verfügbarkeitsreplikate angeben, einschließlich des primären Replikats.  
  
> [!NOTE]  
>  SQL Server-Failoverclusterinstanzen (FCIs) unterstützen kein automatisches Failover durch Verfügbarkeitsgruppen. Daher können die Verfügbarkeitsreplikate, die von einer FCI gehostet werden, nur für manuelles Failover konfiguriert werden.  
  
 MANUAL  
 Ermöglicht, Geplantes Manuelles Failover oder erzwungenes Manuelles Failover (normalerweise *erzwungenes Failover*) durch den Datenbankadministrator.  
  
 Die FAILOVER_MODE-Klausel ist erforderlich. Die beiden Typen des manuellen Failovers, manuelles Failover ohne Datenverlust und erzwungenes Failover (mit möglichem Datenverlust), werden unter unterschiedlichen Bedingungen unterstützt. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Failover und Failovermodi &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
 SEEDING_MODE  **=**  {AUTOMATISCHE | MANUELLE}  
 Gibt an, wie das sekundäre Replikat ursprünglich mit Anfangsdaten gefüllt ist.  
  
 AUTOMATIC  
 Ermöglicht direkte seeding. Diese Methode startet das sekundäre Replikat über das Netzwerk an. Diese Methode erfordert nicht das Sichern und Wiederherstellen einer Kopie der primären Datenbank auf dem Replikat.  
  
> [!NOTE]  
>  Für das direkte seeding, müssen Sie das Erstellen einer Datenbank auf jedem sekundären Replikat zulassen, durch den Aufruf **ALTER AVAILABILITY GROUP** mit der **GRANT CREATE ANY DATABASE** Option.  
  
 MANUAL  
 Gibt an, manuelle seeding (Standard). Diese Methode erfordert, dass Sie eine Sicherung der Datenbank auf dem primären Replikat zu erstellen und diese Sicherung auf dem sekundären Replikat manuell wiederherstellen.  
  
 BACKUP_PRIORITY  **=** *n*  
 Gibt die Priorität für die Ausführung von Sicherungen auf diesem Replikat in Relation zu den anderen Replikaten in derselben Verfügbarkeitsgruppe an. Der Wert liegt im Bereich von 0 bis 100 und ist eine ganze Zahl. Diese Werte haben die folgenden Bedeutungen:  
  
-   1..100 gibt an, dass das Verfügbarkeitsreplikat zum Ausführen von Sicherungen ausgewählt werden könnte. 1 gibt die niedrigste Priorität und 100 die höchste Priorität an. Wenn BACKUP_PRIORITY = 1, würde das Verfügbarkeitsreplikat nur zum Ausführungen von Sicherungen ausgewählt werden, wenn gerade keine höheren Prioritätsverfügbarkeitsreplikate verfügbar sind.  
  
-   0 gibt an, dass dieses verfügbarkeitsreplikat ist nicht zum Ausführen von Sicherungen ist. Dies ist zum Beispiel für ein Remoteverfügbarkeitsreplikat hilfreich, für das keine Failover bei Sicherungen auftreten sollen.  
  
 Weitere Informationen finden Sie unter [Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)wichtig sind.  
  
 SECONDARY_ROLE **(** ... **)**  
 Gibt rollenspezifische Einstellungen an, die wirksam, wenn dieses verfügbarkeitsreplikat die sekundäre Rolle besitzt (d. h., wenn es sich um ein sekundäres Replikat ist). Geben Sie innerhalb der Klammern eine oder beide sekundäre Rollenoptionen an. Wenn Sie beide angeben, verwenden Sie eine durch Trennzeichen getrennte Liste.  
  
 Folgende Optionen stehen für die sekundäre Rolle zur Verfügung:  
  
 ALLOW_CONNECTIONS  **=**  {NEIN | READ_ONLY | ALLE}  
 Gibt an, ob die Datenbanken eines bestimmten Verfügbarkeitsreplikats, das die sekundäre Rolle einnimmt (das heißt, als sekundäres Replikat dient), Verbindungen von Clients akzeptieren können, z. B.:  
  
 NO  
 Es werden keine Verbindungen mit sekundären Datenbanken dieses Replikats zugelassen. Sie sind für den Lesezugriff nicht verfügbar. Dies ist das Standardverhalten.  
  
 READ_ONLY  
 Nur Verbindungen mit den Datenbanken im sekundären Replikat, die die Anwendungsabsicht-Eigenschaft auf festgelegt ist, zulässig sind **ReadOnly**. Weitere Informationen zu dieser Eigenschaft finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Für alle Verbindungen mit den Datenbanken im sekundären Replikat ist der schreibgeschützte Zugriff zugelassen.  
  
 Weitere Informationen finden Sie unter [Aktive sekundäre Replikate: Lesbare sekundäre Replikate &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)wichtig sind.  
  
 READ_ONLY_ROUTING_URL **= "**TCP**://***Systemadresse***:***Port***"**  
 Gibt die URL an, die zum Weiterleiten von Verbindungsanforderungen für beabsichtigte Lesevorgänge zu diesem Verfügbarkeitsreplikat verwendet werden soll. Dies ist die URL, die das SQL Server-Datenbankmodul überwacht. In der Regel überwacht die Standardinstanz des SQL Server-Datenbankmoduls auf TCP-Port 1433.  
  
 Für eine benannte Instanz verwenden, erhalten Sie die Portnummer durch Abfragen der **Port** und **Type_desc** Spalten von der [dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md) -verwaltungssicht. Die Serverinstanz verwendet den Transact-SQL-Listener (**Type_desc = "TSQL"**).  
  
 Weitere Informationen zum Berechnen der schreibgeschützten routing-URL für ein Replikat finden Sie unter [berechnen von Read_only_routing_url für AlwaysOn-](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-AlwaysOn.aspx).  
  
> [!NOTE]  
>  Für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollte der Transact-SQL-Listener konfiguriert werden, um einen bestimmten Port zu verwenden. Weitere Informationen finden Sie unter [Konfigurieren eines Servers zur Überwachung eines bestimmten TCP-Ports &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
 PRIMARY_ROLE **(** ... **)**  
 Gibt rollenspezifische Einstellungen an, die wirksam, wenn dieses verfügbarkeitsreplikat die primäre Rolle besitzt (d. h., wenn es sich um das primäre Replikat ist). Geben Sie innerhalb der Klammern eine oder beide primäre Rollenoptionen an. Wenn Sie beide angeben, verwenden Sie eine durch Trennzeichen getrennte Liste.  
  
 Folgende Optionen stehen für die primäre Rolle zur Verfügung:  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE | ALLE}  
 Gibt den Verbindungstyp an, den die Datenbanken eines bestimmten Verfügbarkeitsreplikats, das die primäre Rolle einnimmt (das heißt, als primäres Replikat dient), von Clients akzeptieren können, z. B.:  
  
 READ_WRITE  
 Verbindungen, bei denen die Verbindungseigenschaft für die Anwendungsabsicht auf **ReadOnly** festgelegt ist, werden nicht zugelassen.  Wenn die Eigenschaft für die Anwendungsabsicht auf **ReadWrite** festgelegt ist oder keine Verbindungseigenschaft für die Anwendungsabsicht festgelegt wurde, wird die Verbindung zugelassen. Weitere Informationen zur Verbindungseigenschaft für die Anwendungsabsicht finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Für die Datenbanken im primären Replikat sind alle Verbindungen zugelassen. Dies ist das Standardverhalten.  
  
 READ_ONLY_ROUTING_LIST  **=**  { **("**\<Server_instance >**"** [ **,**... *n* ] **)** | NONE} gibt eine durch Trennzeichen getrennte Liste von Serverinstanzen, die verfügbarkeitsreplikate für diese verfügbarkeitsgruppe, die die folgenden Anforderungen erfüllen hosten, wenn unter der sekundären Rolle ausgeführt wird:  
  
-   Wird konfiguriert, um alle Verbindungen oder schreibgeschützte Verbindungen (siehe das obige ALLOW_CONNECTIONS-Argument der SECONDARY_ROLE-Option) zuzulassen.  
  
-   Die schreibgeschützte Routing-URL wurde definiert (siehe das obige READ_ONLY_ROUTING_URL-Argument der SECONDARY_ROLE-Option).  
  
 Die READ_ONLY_ROUTING_LIST-Werte lauten wie folgt:  
  
 \<Server_instance > Gibt die Adresse der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die als Host für ein Replikat, das ein lesbares sekundäres Replikat unter der sekundären Rolle ausgeführt wird.  
  
 Verwenden Sie eine durch Trennzeichen getrennte Liste, um alle Serverinstanzen anzugeben, die ein lesbares sekundäres Replikat hosten könnten. Schreibgeschütztes routing folgt die Reihenfolge, in welchem, die Server-Instanzen in der Liste angegeben sind. Wenn Sie die Hostserverinstanz eines Replikats auf der schreibgeschützten Routingliste des Replikats einschließen, ist es eine empfohlene Vorgehensweise, diese Serverinstanz am Ende der Liste zu platzieren, damit Verbindungen für beabsichtigte Lesevorgänge bei Verfügbarkeit zu einem sekundären Replikat wechseln.  
  
 Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], können Sie die Anforderungen für den Lastenausgleich mit leseabsicht über lesbare sekundäre Replikate. Dies können Sie angeben, indem Sie die Replikate in einer geschachtelten Klammern innerhalb der schreibgeschützten Routingliste platzieren. Weitere Informationen und Beispiele finden Sie unter [Konfigurieren von Lastenausgleich über schreibgeschützte Replikate hinweg](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).  
  
 Keine  
 Gibt an, wenn dieses verfügbarkeitsreplikat das primäre Replikat ist, schreibgeschütztes routing nicht unterstützt wird. Dies ist das Standardverhalten.  
  
 SESSION_TIMEOUT  **=**  *ganze Zahl*  
 Gibt den Zeitraum für das Sitzungstimeout in Sekunden an. Wenn Sie die Option nicht angeben, beträgt der Timeoutzeitraum standardmäßig 10 Sekunden. Der Wert muss mindestens 5 Sekunden betragen.  
  
> [!IMPORTANT]  
>  Es wird empfohlen, einen Timeoutzeitraum von 10 Sekunden oder mehr zu wählen.  
  
 Weitere Informationen über die Sitzungstimeout finden Sie unter [(Übersicht) der AlwaysOn-Verfügbarkeitsgruppen &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 AVAILABILITY GROUP FÜR  
 Gibt an, zwei Verfügbarkeitsgruppen, die bilden eine *verteilten verfügbarkeitsgruppe*. Jede verfügbarkeitsgruppe ist Teil des eigenen Windows Server Failover Cluster (WSFC). Wenn Sie eine verteilte verfügbarkeitsgruppe erstellen, wird die verfügbarkeitsgruppe auf das aktuelle SQL Server-Instanz der primären verfügbarkeitsgruppe. Die zweite verfügbarkeitsgruppe wird die sekundäre verfügbarkeitsgruppe.  
  
 Sie müssen die sekundäre verfügbarkeitsgruppe auf die verteilte verfügbarkeitsgruppe zu verknüpfen. Weitere Informationen finden Sie unter [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)hinzugefügt wird.  
  
 \<Ag_name > Gibt den Namen der verfügbarkeitsgruppe, die eine bildet die Hälfte der verteilten verfügbarkeitsgruppe.  
  
 LISTENER **= "**TCP**://***Systemadresse***:***Port***"**  
 Gibt den URL-Pfad für den Listener der verfügbarkeitsgruppe zugeordnet.  
  
 Die LISTENER-Klausel ist erforderlich.  
  
 **"**TCP**://***Systemadresse***:***Port***"**  
 Gibt eine URL für den Listener der verfügbarkeitsgruppe zugeordnet. Die URL-Parameter lauten wie folgt:  
  
 *system-address*  
 Ist eine Zeichenfolge, z. B. ein Systemname, einen vollqualifizierten Domänennamen oder eine IP-Adresse, die den Listener zielcomputersystem eindeutig identifiziert.  
  
 *port*  
 Ist eine Portnummer, die dem Spiegelungsendpunkt der verfügbarkeitsgruppe zugeordnet ist. Beachten Sie, dass dies nicht der Port des Listeners ist.  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT}  
 Gibt an, ob das primäre Replikat warten Sie, bis die sekundäre verfügbarkeitsgruppe bestätigen Sie das verstärken (Schreiben), der die Protokolldatensätze auf den Datenträger, bevor das primäre Replikat einen Commit die Transaktion auf eine bestimmte primäre Datenbank ausführen kann.  
  
 SYNCHRONOUS_COMMIT  
 Gibt an, dass das primäre Replikat wartet, bis sie auf die sekundäre verfügbarkeitsgruppe festgeschrieben wurden ein commit für Transaktionen. Sie können SYNCHRONOUS_COMMIT für bis zu zwei Verfügbarkeitsgruppen, einschließlich der primären verfügbarkeitsgruppe angeben.  
  
 ASYNCHRONOUS_COMMIT  
 Gibt an, dass das primäre Replikat Transaktionen ein Commit ausgeführt wird, ohne zu warten, die für diese sekundäre verfügbarkeitsgruppe auf das Protokoll festschreibt. Sie können ASYNCHRONOUS_COMMIT für bis zu zwei Verfügbarkeitsgruppen, einschließlich der primären verfügbarkeitsgruppe angeben.  
  
 Die AVAILABILITY_MODE-Klausel ist erforderlich.  
  
 FAILOVER_MODE  **=**  {MANUELLE}  
 Gibt den Failovermodus der verteilten verfügbarkeitsgruppe.  
  
 MANUAL  
 Ermöglicht, Geplantes Manuelles Failover oder erzwungenes Manuelles Failover (normalerweise *erzwungenes Failover*) durch den Datenbankadministrator.  
  
 Die FAILOVER_MODE-Klausel ist erforderlich, und die einzige Option ist manuell. Das automatische Failover auf die sekundäre Verfügbarkeitsgruppe wird nicht unterstützt.  
  
 SEEDING_MODE  **=**  {AUTOMATISCHE | MANUELLE}  
 Gibt an, wie die sekundäre verfügbarkeitsgruppe anfänglich mit Anfangsdaten gefüllt ist.  
  
 AUTOMATIC  
 Ermöglicht direkte seeding. Diese Methode startet die sekundäre verfügbarkeitsgruppe über das Netzwerk an. Diese Methode erfordert nicht das Sichern und Wiederherstellen einer Kopie der primären Datenbank auf den Replikaten der sekundären verfügbarkeitsgruppe.  
  
 MANUAL  
 Gibt an, manuelle seeding (Standard). Diese Methode müssen Sie eine Sicherung der Datenbank auf dem primären Replikat zu erstellen und diese Sicherung auf die Replikate der sekundären verfügbarkeitsgruppe manuell wiederherstellen.  
  
 LISTENER **"***Dns_name***" (** \<Listener_option > **)** definiert einen neuen verfügbarkeitsgruppenlistener für diese verfügbarkeitsgruppe. LISTENER ist ein optionales Argument.  
  
> [!IMPORTANT]  
>  Vor dem Erstellen des ersten Listeners wird dringend empfohlen, Sie lesen [erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
>   
>  Nachdem Sie einen Listener für eine Verfügbarkeitsgruppe erstellt haben, empfehlen wir dringend, folgende Schritte auszuführen:  
>   
>  -   Bitten Sie den Netzwerkadministrator, die IP-Adresse des Listeners zur exklusiven Verwendung zu reservieren.  
> -   Geben Sie den DNS-Hostnamen des Listeners an Anwendungsentwickler weiter, damit diese den Namen in Verbindungszeichenfolgen zum Anfordern von Clientverbindungen mit dieser Verfügbarkeitsgruppe verwenden.  
  
 *DNS-Name*  
 Gibt den DNS-Hostnamen des Verfügbarkeitsgruppenlisteners an. Der DNS-Name des Listeners muss in der Domäne und NetBIOS eindeutig sein.  
  
 *Dns_name* ist ein Zeichenfolgenwert. Dieser Name darf nur alphanumerische Zeichen, Bindestriche (-) und Unterstriche (_) enthalten (in beliebiger Reihenfolge). Bei DNS-Hostnamen muss die Groß-/Kleinschreibung beachtet werden. Die maximale Länge beträgt 63 Zeichen.  
  
 Wir empfehlen, dass Sie eine sinnvolle Zeichenfolge angeben. Für eine Verfügbarkeitsgruppe mit dem Namen `AG1`wäre ein sinnvoller DNS-Hostname z. B. `ag1-listener`.  
  
> [!IMPORTANT]  
>  NetBIOS erkennt nur die ersten 15 Zeichen im dns_name. Wenn Sie zwei wsfc-Cluster, die vom gleichen Active Directory gesteuert werden und Sie versuchen, verfügbarkeitsgruppenlistener in beiden Clustern mit Namen mit mehr als 15 Zeichen und einem identischen 15-Zeichen-Präfix zu erstellen, meldet einen Fehler an, dass das virtuelle Netzwerk Ressource konnte nicht online geschaltet werden. Informationen zu Präfix-Benennungsregeln für DNS-Namen finden Sie unter [Zuweisen von Domänennamen](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx).  
  
 \<Listener_option > LISTENER nimmt eine der folgenden \<Listener_option > Optionen: 
  
 MIT DHCP [ON { **("***four_part_ipv4_address***","***four_part_ipv4_mask***")** }]  
 Gibt an, dass der verfügbarkeitsgruppenlistener das Dynamic Host Configuration Protocol (DHCP) verwendet.  Verwenden Sie die ON-Klausel optional, identifizieren Sie das Netzwerk auf dem Listener erstellt wird. DHCP ist beschränkt auf ein einzelnes Subnetz, das für alle Serverinstanzen verwendet wird, das in der verfügbarkeitsgruppe ein Replikat hostet.  
  
> [!IMPORTANT]  
>  DHCP wird in einer Produktionsumgebung nicht empfohlen. Wenn die DHCP-IP-Leasedauer bei einer Downtime abläuft, ist eine Verlängerung erforderlich, um die neue IP-Adresse des DHCP-Netzwerks zu registrieren, die dem DNS-Namen des Listeners zugeordnet ist, was sich auf die Clientkonnektivität auswirkt. DHCP eignet sich jedoch gut zum Einrichten der Entwicklungs- und Testumgebung, um grundlegende Funktionen von Verfügbarkeitsgruppen und die Integration in Ihre Anwendungen zu überprüfen.  
  
 Beispiel:  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 MIT IP-Adresse **(** { **("***four_part_ipv4_address***","***four_part_ipv4_mask* **')** | **("***ipv6_address***")** } [ **,** ...  *n*  ] **)** [ **,** PORT  **=**  *Listener_port* ]  
 Gibt an, dass statt DHCP Listener der verfügbarkeitsgruppe eine oder mehrere statische IP-Adressen verwendet. Um eine Verfügbarkeitsgruppe über mehrere Subnetze zu erstellen, erfordert jedes Subnetz in der Listenerkonfiguration eine statische IP-Adresse. Für ein angegebenes Subnetz kann die statische IP-Adresse entweder eine IPv4-Adresse oder eine IPv6-Adresse sein. Wenden Sie sich an Ihren Netzwerkadministrator, um eine statische IP-Adresse für jedes Subnetz zu erhalten, die ein Replikat für die neue verfügbarkeitsgruppe hostet.  
  
 Beispiel:  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 Gibt eine vierteilige IPv4-Adresse für einen Verfügbarkeitsgruppenlistener an. Beispiel: `10.120.19.155`.  
  
 *four_part_ipv4_mask*  
 Gibt eine vierteilige IPv4-Maske für einen Verfügbarkeitsgruppenlistener an. Beispiel: `255.255.254.0`.  
  
 *ipv6_address*  
 Gibt eine IPv6-Adresse für einen Verfügbarkeitsgruppenlistener an. Beispiel: `2001::4898:23:1002:20f:1fff:feff:b3a3`.  
  
 PORT  **=**  *Listener_port*  
 Gibt die Portnummer –*Listener_port*– von einem Verfügbarkeitsgruppen-Listener verwendet werden, die von einer WITH IP-Klausel angegeben ist. PORT ist optional.  
  
 Die Standardportnummer 1433 wird unterstützt. Wenn Sie jedoch Sicherheitsbedenken hegen, empfehlen wir die Verwendung einer anderen Portnummer.  
  
 Beispiel: `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
## <a name="prerequisites-and-restrictions"></a>Voraussetzungen und Einschränkungen  
 Informationen zu den Voraussetzungen für das Erstellen einer verfügbarkeitsgruppe finden Sie unter [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 Informationen zu Einschränkungen bei den AVAILABILITY GROUP-Transact-SQL-Anweisungen finden Sie unter [Übersicht von Transact-SQL-Anweisungen für AlwaysOn-Verfügbarkeitsgruppen &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** und die CREATE AVAILABILITY GROUP-Serverberechtigung, ALTER ANY AVAILABILITY GROUP-Berechtigung oder CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-configuring-backup-on-secondary-replicas-flexible-failover-policy-and-connection-access"></a>A. Konfigurieren der Sicherung für sekundäre Replikate, flexible Failoverrichtlinien und Verbindungszugriff  
 Im folgenden Beispiel wird eine Verfügbarkeitsgruppe mit dem Namen `MyAg` für die zwei Benutzerdatenbanken `ThisDatabase` und `ThatDatabase` erstellt. In der folgenden Tabelle werden die Werte zusammengefasst, die für die Optionen angegeben wurden, die für die Verfügbarkeitsgruppe als Ganzes festgelegt sind.  
  
|Gruppenoption|Einstellung|Description|  
|------------------|-------------|-----------------|  
|AUTOMATED_BACKUP_PREFERENCE|SECONDARY|Diese automatisierte Sicherungseinstellung gibt an, dass Sicherungen auf einem sekundären Replikat erfolgen sollen, außer wenn das primäre Replikat das einzige Replikat online ist (dies ist das Standardverhalten). Damit die AUTOMATED_BACKUP_PREFERENCE-Einstellung in Kraft tritt, müssen Sicherungsaufträge in Verfügbarkeitsdatenbanken so verfasst werden, dass die automatische Sicherungseinstellung berücksichtigt wird.|  
|FAILURE_CONDITION_LEVEL|3|Diese Einstellung für die Fehlerbedingungsebene gibt an, dass ein automatisches Failover bei kritischen internen SQL Server-Fehlern initiiert werden soll, z. B. verwaisten Spinlocks, ernsten Schreibzugriffsverletzungen oder zu vielen Sicherungen.|  
|HEALTH_CHECK_TIMEOUT|600000|Diese zustandsüberprüfungs-Timeoutwert, 60 Sekunden besagt, dass der wsfc-Cluster 60.000 Millisekunden wartet der [Sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) gespeicherte Systemprozedur Serverzustand Informationen zu einer Serverinstanz zurück Hosten ein Replikat mit synchronem Commit mit automatischem, bevor der Cluster wird davon ausgegangen, dass die hostserverinstanz langsam oder blockiert ist. (Der Standardwert beträgt 30.000 Millisekunden.)|  
  
 Drei Verfügbarkeitsreplikate müssen von den Standardserverinstanzen auf Computern mit der Bezeichnung `COMPUTER01`, `COMPUTER02` und `COMPUTER03` gehostet werden. In der folgenden Tabelle werden die für die Replikatoptionen jedes Replikats angegebenen Werte zusammengefasst.  
  
|Replikatoption|Einstellung auf `COMPUTER01`|Einstellung auf `COMPUTER02`|Einstellung auf `COMPUTER03`|Description|  
|--------------------|-----------------------------|-----------------------------|-----------------------------|-----------------|  
|ENDPOINT_URL|TCP: / /*COMPUTER01:5022*|TCP: / /*COMPUTER02:5022*|TCP: / /*COMPUTER03:5022*|In diesem Beispiel weisen die Systeme dieselbe Domäne auf. Daher können die Endpunkt-URLs den Namen des Computersystems als Systemadresse verwenden.|  
|AVAILABILITY_MODE|SYNCHRONOUS_COMMIT|SYNCHRONOUS_COMMIT|ASYNCHRONOUS_COMMIT|Zwei der Replikate verwenden den Modus mit synchronem Commit. Nach der Synchronisierung unterstützen sie Failover ohne Datenverlust. Das dritte Replikat verwendet den Verfügbarkeitsmodus mit asynchronem Commit.|  
|FAILOVER_MODE|AUTOMATIC|AUTOMATIC|MANUAL|Die Replikate mit synchronem Commit unterstützen automatisches Failover und geplantes manuelles Failover. Das Verfügbarkeitsmodusreplikat mit synchronem Commit unterstützt nur erzwungenes manuelles Failover.|  
|BACKUP_PRIORITY|30|30|90|Dem Replikat mit asynchronem Commit wird eine höhere Priorität (90) als dem Replikat mit synchronem Commit zugewiesen. Sicherungen sind tendenziell auf der Serverinstanz auftreten, die das Replikat mit asynchronem Commit hostet.|  
|SECONDARY_ROLE|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' )|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' )|( ALLOW_CONNECTIONS = READ_ONLY, <br />READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' )|Nur das Replikat mit asynchronem Commit fungiert als lesbares sekundäres Replikat.<br /><br /> Gibt den Computernamen und die standardmäßige Datenbank-Modulportnummer (1433) an.<br /><br /> Dieses Argument ist optional.|  
|PRIMARY_ROLE|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = NONE )|In der primären Rolle lehnen alle Replikate Verbindungsversuche mit leseabsicht.<br /><br /> Verbindungsanforderungen für beabsichtigte Lesevorgänge werden zu COMPUTER03 weitergeleitet, wenn das lokale Replikat unter der sekundären Rolle ausgeführt wird. Wenn dieses Replikat unter der primären Rolle ausgeführt wird, wird das schreibgeschützte Routing deaktiviert.<br /><br /> Dieses Argument ist optional.|  
|SESSION_TIMEOUT|10|10|10|In diesem Beispiel wird der Timeoutwert für die Standardsitzung (10) angegeben. Dieses Argument ist optional.|  
  
 Im Beispiel wird schließlich die optionale LISTENER-Klausel angegeben, um einen Verfügbarkeitsgruppenlistener für die neue Verfügbarkeitsgruppe zu erstellen. Der eindeutige DNS-Name `MyAgListenerIvP6`wird für diesen Listener angegeben. Die zwei Replikate befinden sich auf anderen Subnetzen, daher muss der Listener statische IP-Adressen verwenden. Für die beiden Verfügbarkeitsreplikate gibt die WITH IP-Klausel jeweils eine statische IP-Adresse an, nämlich `2001:4898:f0:f00f::cf3c` und `2001:4898:e0:f213::4ce2`, die das IPv6-Format verwenden. In diesem Beispiel wird zudem das optionale PORT-Argument verwendet, um Port `60173` als Listenerport anzugeben.  
  
```  
CREATE AVAILABILITY GROUP MyAg   
   WITH (  
      AUTOMATED_BACKUP_PREFERENCE = SECONDARY,  
      FAILURE_CONDITION_LEVEL  =  3,   
      HEALTH_CHECK_TIMEOUT = 600000  
       )  
  
   FOR   
      DATABASE  ThisDatabase, ThatDatabase   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE =  MANUAL,  
         BACKUP_PRIORITY = 90,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = NONE ),  
         SESSION_TIMEOUT = 10  
         );
GO  
ALTER AVAILABIIITY GROUP [MyAg]
  ADD LISTENER ‘MyAgListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
GO  
```  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellen einer Verfügbarkeitsgruppe &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [Verwenden des Assistenten für Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Verwenden des Dialogfelds „Neue Verfügbarkeitsgruppe“ &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten für Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [DROP AVAILABILITY GROUP &#40; Transact-SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [Problembehandlung für die Always On-Verfügbarkeitsgruppenkonfiguration &#40; SQLServer &#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover (SQL Server)](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  


