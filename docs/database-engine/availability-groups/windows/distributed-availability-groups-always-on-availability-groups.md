---
title: "Verteilte Verf&#252;gbarkeitsgruppen (Always On-Verf&#252;gbarkeitsgruppen) | Microsoft Docs"
ms.custom: ""
ms.date: "08/30/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
caps.latest.revision: 28
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 28
---
# Verteilte Verf&#252;gbarkeitsgruppen (Always On-Verf&#252;gbarkeitsgruppen)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Mithilfe von verteilten Verfügbarkeitsgruppen können Sie zwei Verfügbarkeitsgruppen einander zuordnen, die auf verschiedenen Windows Server-Failoverclustern (WSFC) ausgeführt werden. Einer der wichtigsten Einsatzzwecke von verteilten Verfügbarkeitsgruppen liegt in der Notfallwiederherstellung, wenn der primäre Standort geografisch vom DR-Standort getrennt ist. Die Daten sollen kontinuierlich auf den DR-Standort repliziert werden, jedoch soll ein mögliches Netzwerkproblem oder ein anderes Problem am DR-Standort nicht zu einem Ausfall des primären Standorts führen können.  
  
 Das folgende Diagramm veranschaulicht die Architektur einer verteilten Verfügbarkeitsgruppe.  
  
 ![AlwaysOn Distributed Availability Groups](../../../database-engine/availability-groups/windows/media/alwayson-distributed-availability-groups.png "AlwaysOn Distributed Availability Groups")  
  
 Im vorstehenden Diagramm sind zwei separate Windows Server-Failovercluster (WFSC 1 und WFSC 2) dargestellt. Jeder Cluster verfügt über eine eigene Verfügbarkeitsgruppe mit einer entsprechenden Datenbankkonfiguration. Eine verteilte Verfügbarkeitsgruppe kann man sich als eine „Verfügbarkeitsgruppe von Verfügbarkeitsgruppen“ vorstellen. AG 1 wird in diesem Beispiel zur primären Verfügbarkeitsgruppe. Einfügungen und Aktualisierungen werden alle am primären Replikat AG 1 vorgenommen und dann auf dessen sekundäre Replikate repliziert. Die Änderungen werden jedoch auch einmal über das Netzwerk zur zweiten Verfügbarkeitsgruppe auf WSFC 2 repliziert. Die Verfügbarkeitsgruppe AG 2 repliziert diese Änderungen auf ihre sekundären Replikate.  
  
> [!IMPORTANT]  
>  Wenn eine verteilte Verfügbarkeitsgruppenbeziehung zwischen zwei Verfügbarkeitsgruppen eingerichtet wird, wird die zweite Verfügbarkeitsgruppe automatisch als schreibgeschützt festgelegt. Aktualisierungen und Einfügungen können nur am primären Replikat der primären Verfügbarkeitsgruppe (in diesem Fall dem primären Replikat von AG 1) vorgenommen werden.  
  
 Verteilte Verfügbarkeitsgruppen unterscheiden sich von einer Verfügbarkeitsgruppe auf einem einzelnen Windows Server-Failovercluster in den folgenden Punkten:  
  
-   Jeder WSFC erhält seine eigene Konfiguration für Quorummodus und Knotenvotum aufrecht. Dies bedeutet, dass die Integrität des sekundären WSFC sich nicht auf den primären WSFC auswirkt.  
  
-   Die Daten werden einmalig über das Netzwerk an den sekundären WSFC gesendet und dann innerhalb dieses Clusters repliziert. In einem einzelnen WSFC werden die Daten individuell an jedes Replikat gesendet. Im Fall eines geografisch getrennten sekundären Standorts sind verteilte Verfügbarkeitsgruppen effizienter.  
  
-   Die auf dem primären und dem sekundären Cluster verwendete Betriebssystemversion darf verschieden sein. In einem einzelnen WSFC müssen alle Server die gleiche Version des Betriebssystems ausführen. Dadurch bietet sich die Möglichkeit, verteilte Verfügbarkeitsgruppen mit rollierenden Updates/Upgrades des Betriebssystems zu verwenden.  
  
-   Die primäre und sekundäre Verfügbarkeitsgruppe müssen die gleiche Konfiguration der Datenbanken aufweisen.  
  
-   Das automatische Failover auf die sekundäre Verfügbarkeitsgruppe wird nicht unterstützt.  
  
## Erstellen einer verteilten Verfügbarkeitsgruppe  
 Um eine verteilte Verfügbarkeitsgruppe zu erstellen, müssen Sie eine Verfügbarkeitsgruppe und einen Listener auf jedem WSFC erstellen. Anschließend kombinieren Sie diese zu einer verteilten Verfügbarkeitsgruppe. Die folgenden Schritte stellen ein einfaches Beispiel in Transact-SQL dar. Dieses Beispiel deckt nicht alle Details zum Erstellen von Verfügbarkeitsgruppen und Listenern ab; vielmehr legt es den Schwerpunkt auf die Herausarbeitung der wichtigsten Anforderungen.  
  
### Erstellen der ersten Verfügbarkeitsgruppe auf dem ersten Cluster  
 Erstellen Sie eine Verfügbarkeitsgruppe auf dem ersten WSFC.   In diesem Beispiel heißt die Verfügbarkeitsgruppe `ag1` für die Datenbank `db1`.  
  
```tsql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
 Beachten Sie, dass in diesem Beispiel direktes Seeding zum Einsatz kommt, wobei **SEEDING_MODE** sowohl für die Replikate als auch für die verteilte Verfügbarkeitsgruppe auf **AUTOMATIC** festgelegt ist. Das bedeutet, dass die sekundären Replikate und sekundären Verfügbarkeitsgruppen nach der Einrichtung automatisch aufgefüllt werden, ohne eine manuelle Sicherung und Wiederherstellung der primären Datenbank erforderlich zu machen.  
  
### Verknüpfen der sekundären Replikate mit der primären Verfügbarkeitsgruppe  
 Alle sekundären Replikate müssen mithilfe von **ALTER AVAILABILITY GROUP** mit der Option **JOIN** mit der Verfügbarkeitsgruppe verknüpft werden. Da in diesem Beispiel direktes Seeding verwendet wird, müssen Sie außerdem **ALTER AVAILABILITY GROUP** mit der Option **GRANT CREATE ANY DATABASE** aufrufen. Dies ermöglicht der Verfügbarkeitsgruppe, die Datenbank zu erstellen und mit dem automatischen Seeding aus dem ersten Replikat zu beginnen.  
  
 In diesem Beispiel werden die folgenden Befehle auf dem sekundären Replikat `server2` ausgeführt, um die Verknüpfung mit der Verfügbarkeitsgruppe `ag1` herzustellen. Der Verfügbarkeitsgruppe ist es damit gestattet, Datenbanken auf dem sekundären Replikat zu erstellen.  
  
```tsql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  
  
### Erstellen eines Listeners für die primäre Verfügbarkeitsgruppe  
 Fügen Sie im nächsten Schritt einen Listener für die primäre Verfügbarkeitsgruppe auf dem ersten WSFC hinzu. In diesem Beispiel hat der Listener den Namen `ag1-listener`. Weitere Informationen zum Erstellen eines Listeners finden Sie unter [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server &#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### Erstellen der zweiten Verfügbarkeitsgruppe auf dem zweiten Cluster  
 Erstellen Sie anschließend auf dem zweiten WSFC eine zweite Verfügbarkeitsgruppe, `ag2`. Die Datenbank wird in diesem Fall nicht angegeben, da sie automatisch per Seeding aus der primären Verfügbarkeitsgruppe aufgefüllt wird.  
  
```tsql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
>  Beachten Sie, dass die sekundäre Verfügbarkeitsgruppe den gleichen Endpunkt für die Datenbankspiegelung verwenden muss (in diesem Beispiel Port 5022). Andernfalls wird die Replikation nach einem lokalen Failover beendet.  
  
### Verknüpfen der sekundären Replikate mit der sekundären Verfügbarkeitsgruppe  
 In diesem Beispiel werden die folgenden Befehle auf dem sekundären Replikat `server4` ausgeführt, um die Verknüpfung mit der Verfügbarkeitsgruppe `ag2` herzustellen. Der Verfügbarkeitsgruppe wird dann gestattet, Datenbanken auf dem sekundären Replikat zu erstellen, um das direkte Seeding zu unterstützen.  
  
```tsql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### Erstellen eines Listeners für die sekundäre Verfügbarkeitsgruppe  
 Fügen Sie im nächsten Schritt einen Listener für die sekundäre Verfügbarkeitsgruppe auf dem zweiten WSFC hinzu. In diesem Beispiel hat der Listener den Namen `ag2-listener`. Weitere Informationen zum Erstellen eines Listeners finden Sie unter [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server &#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### Erstellen der verteilten Verfügbarkeitsgruppe auf dem ersten Cluster  
 Erstellen Sie auf dem ersten WSFC eine verteilte Verfügbarkeitsgruppe (die in diesem Beispiel den Namen `distributedag` trägt). Verwenden Sie den **CREATE AVAILABILITY GROUP**-Befehl mit der **DISTRIBUTED**-Option. Der **AVAILABILITY GROUP ON**-Parameter gibt die Mitgliedsverfügbarkeitsgruppen an, `ag1` und `ag2`.  
  
```tsql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  Die **LISTENER_URL** gibt den Listener für jede Verfügbarkeitsgruppe zusammen mit dem Datenbankspiegelungs-Endpunkt der Verfügbarkeitsgruppe an. In diesem Beispiel ist das Port `5022` (nicht Port `60173`, der zum Erstellen des Listeners verwendet wurde).  
  
### Verknüpfen der verteilten Verfügbarkeitsgruppe auf dem zweiten Cluster  
 Verknüpfen Sie anschließend die verteilte Veerfügbarkeitsgruppe auf dem zweiten WSFC.  
  
```tsql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

  
## Failover auf eine sekundäre Verfügbarkeitsgruppe  
 Zurzeit wird nur manuelles Failover unterstützt. Die folgende Transact-SQL-Anweisung erzwingt das Failover auf die verteilte Verfügbarkeitsgruppe mit dem Namen `distributedag`:  


1. Legen Sie den Verfügbarkeitsmodus für die sekundäre Verfügbarkeitsgruppe auf synchronen Commit fest. 
    
      ```tsql  
      ALTER AVAILABILITY GROUP [distributedag] 
      MODIFY 
      AVAILABILITY GROUP ON
      'ag1' WITH  
         ( 
          LISTENER_URL = 'tcp://ag1-listener:5022',  
          AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = MANUAL, 
          SEEDING_MODE = MANUAL 
          ), 
      'ag2' WITH  
        ( 
        LISTENER_URL = 'tcp://ag2-listener:5022', 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
        FAILOVER_MODE = MANUAL, 
        SEEDING_MODE = MANUAL 
        );  
       
      ```  
  
1. Warten Sie, bis sich der Status der verteilten Verfügbarkeitsgruppe in `SYNCHRONIZED` geändert hat. Führen Sie die folgende Abfrage auf dem SQL-Server aus, der das primäre Replikat der primären Verfügbarkeitsgruppe hostet. 
    
      ```tsql  
      SELECT ag.name
             , drs.database_id
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.end_of_log_lsn 
        FROM sys.dm_hadr_database_replica_states drs,
        sys.availability_groups ag
          WHERE drs.group_id = ag.group_id;      
      ```  

    Führen Sie den nächsten Schritt aus, sobald **synchronization_state_desc** für die Verfügbarkeitsgruppe gleich `SYNCHRONIZED` ist. Ist **synchronization_state_desc** nicht gleich `SYNCHRONIZED`, führen Sie den Befehl alle fünf Sekunden aus, bis die Änderung erfolgt ist. Wechseln Sie erst zum nächsten Schritt, wenn **synchronization_state_desc** gleich  = `SYNCHRONIZED` ist. 

1. Legen Sie auf dem SQL-Server, der das primäre Replikat für die primäre Verfügbarkeitsgruppe hostet, die Rolle der verteilten Verfügbarkeitsgruppe auf `SECONDARY` fest. 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
      ```  

    Hinweis: Zu diesem Zeitpunkt ist die verteilte Verfügbarkeitsgruppe nicht verfügbar.

1. Testen Sie die Failoverbereitschaft. Führen Sie die folgende Abfrage aus:

      ```tsql
      SELECT ag.name, 
             drs.database_id, 
             drs.group_id, 
             drs.replica_id, 
             drs.synchronization_state_desc, 
             drs.end_of_log_lsn 
      FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
      WHERE drs.group_id = ag.group_id; 
      ```  
    Die Verfügbarkeitsgruppe ist für Failover eingerichtet, wenn für sie **ynchronization_state_desc** gleich `SYNCHRONIZED` und wenn **end_of_log_lsn** für beide Verfügbarkeitsgruppen identisch ist. 

1. Führen Sie ein Failover von der primären Verfügbarkeitsgruppe zur sekundären Verfügbarkeitsgruppe aus. Führen Sie den folgenden Befehl auf dem SQL-Server aus, der das primäre Replikat der sekundären Verfügbarkeitsgruppe hostet. 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
      ```  
      Hinweis: Nach diesem Schritt ist die verteilte Verfügbarkeitsgruppe verfügbar.
      
Nachdem Sie die obigen Schritte ausgeführt haben, erfolgt ein Failover für die verteilte Verfügbarkeitsgruppe ohne Datenverlust. Microsoft empfiehlt, den Verfügbarkeitsmodus wieder in ASYNCHRONOUS_COMMIT zu ändern, wenn zwischen den Verfügbarkeitsgruppen eine geografische Entfernung liegt, die Latenz (Wartezeit) verursacht. 
  
## Entfernen einer verteilten Verfügbarkeitsgruppe  
 Die folgende Transact-SQL-Anweisung entfernt eine verteilte Verfügbarkeitsgruppe mit dem Namen `distributedag`:  
  
```tsql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## Erstellen einer verteilten Verfügbarkeitsgruppe mit Failoverclusterinstanzen

Sie können eine verteilte Verfügbarkeitsgruppe mit einer Verfügbarkeitsgruppe auf einer Failoverclusterinstanz (FCI) erstellen. In diesem Fall benötigen Sie keinen Verfügbarkeitsgruppenlistener. Verwenden Sie den virtuellen Netzwerknamen (VNN) für das primäre Replikat der FCI-Instanz. Im folgenden Beispiel ist eine verteilte Verfügbarkeitsgruppe namens SQLFCIDAG dargestellt. Eine Verfügbarkeitsgruppe ist SQLFCIAG. SQLFCIAG hat 2 FCI-Replikate. Der VNN für das primäre FCI-Replikat ist FCI SQLFCIAG-1, und der VNN für das sekundäre FCI-Replikat ist SQLFCIAG-2. Die verteilte Verfügbarkeitsgruppe enthält außerdem SQLAG-DR zur Wiederherstellung im Notfall.

![Verteilte AlwaysOn-Verfügbarkeitsgruppe](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 Mit der folgenden DDL-Anweisung wird diese verteilte Verfügbarkeitsgruppe erstellt. 

```tsql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

Beachten Sie, dass die Listener-URL mit dem VNN der primären FCI-Instanz identisch ist.

## Ausführen eines manuellen Failovers für die FCI in der verteilten Verfügbarkeitsgruppe

Um ein manuelles Failover für die FCI-Verfügbarkeitsgruppe auszuführen, aktualisieren Sie die verteilte Verfügbarkeitsgruppe, um die Änderung der Listener-URL zu übernehmen. Führen Sie z. B. folgende DDL-Anweisung sowohl für die primäre als auch die sekundäre Verfügbarkeitsgruppe von SQLFCIAG aus:

```tsql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2:5022'
    )
```  
  
## Siehe auch  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  