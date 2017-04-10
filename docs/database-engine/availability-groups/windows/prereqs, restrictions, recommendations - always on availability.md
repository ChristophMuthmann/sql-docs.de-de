---
title: "Voraussetzungen, Einschr&#228;nkungen und Empfehlungen f&#252;r Always On-Verf&#252;gbarkeitsgruppen (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server], Server-Instanz"
  - "Verfügbarkeitsgruppen [SQL Server], Bereitstellung"
  - "Verfügbarkeitsgruppen [SQL Server], WSFC-Cluster"
  - "Verfügbarkeitsgruppen [SQL Server], Infos"
  - "Verfügbarkeitsgruppen [SQL Server], Voraussetzungen und Einschränkungen"
  - "Verfügbarkeitsgruppen [SQLServer], Failoverclusterinstanzen"
  - "Verfügbarkeitsgruppen [SQL Server], Datenbanken"
  - "Verfügbarkeitsgruppen [SQL Server]"
ms.assetid: edbab896-42bb-4d17-8d75-e92ca11f7abb
caps.latest.revision: 151
ms.author: "mikeray"
manager: "jhubbard"
---
# Voraussetzungen, Einschr&#228;nkungen und Empfehlungen f&#252;r Always On-Verf&#252;gbarkeitsgruppen (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden Überlegungen zur Bereitstellung von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] beschrieben, einschließlich Voraussetzungen, Einschränkungen und Empfehlungen für Hostcomputer, Windows Server Failover Clustering (WSFC)-Cluster, Serverinstanzen und Verfügbarkeitsgruppen. Für alle Komponenten sind Überlegungen zur Sicherheit und ggf. erforderliche Berechtigungen angegeben.  
  
> [!IMPORTANT]  
>  Vor der Bereitstellung von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] wird empfohlen, dieses Thema vollständig zu lesen.  
    
##  <a name="DotNetHotfixes"></a> .NET-Hotfixes, die Always On-Verfügbarkeitsgruppen unterstützen  
 Abhängig von den [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]-Komponenten und -Funktionen, die Sie mit [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] verwenden, müssen Sie möglicherweise zusätzliche in der folgenden Tabelle angegebene .NET-Hotfixes installieren. Die Hotfixes können in beliebiger Reihenfolge installiert werden.  
  
||Abhängige Funktion|Hotfix|Link|  
|------|-----------------------|------------|----------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|Hotfix für .NET 3.5 SP1 fügt dem SQL-Client Unterstützung für die Always On-Funktionen „Read-intent“, „readonly“ und „multisubnetfailover“ hinzu. Der Hotfix muss auf allen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Berichtsservern installiert werden.|KB 2654347: [Hotfix für .NET 3.5 SP1 zur Unterstützung für Always On-Funktionen](http://go.microsoft.com/fwlink/?LinkId=242896)|  
  
##  <a name="SystemReqsForAOAG"></a> Windows-Systemanforderungen und -Empfehlungen  
 **In diesem Abschnitt:**  
  
-   [Prüfliste: Anforderungen](#SystemRequirements)  
  
-   [Empfehlungen für Computer, die Verfügbarkeitsreplikate (Windows-System) hosten](#ComputerRecommendations)  
  
-   [Berechtigungen](#PermissionsWindows)  
  
-   [Verwandte Aufgaben](#RelatedTasksWindows)  
  
-   [Verwandte Inhalte](#RelatedContentWS)  
  
###  <a name="SystemRequirements"></a> Prüfliste: Anforderungen (Windows-System)  
 Zur Unterstützung der Funktion [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] muss gewährleistet sein, dass jeder Computer, der an mindestens einer Verfügbarkeitsgruppe teilnehmen soll, die folgenden wesentlichen Anforderungen erfüllt:  
  
||Anforderung|Link|  
|------|-----------------|----------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Stellen Sie sicher, dass es sich bei diesem System nicht um einen Domänencontroller handelt.|Verfügbarkeitsgruppen werden nicht auf Domänencontrollern unterstützt.|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Stellen Sie sicher, dass auf jedem Computer Windows Server 2012 oder höhere Versionen ausgeführt werden.|[Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Stellen Sie sicher, dass es sich bei jedem Computer um einen Knoten in einem Windows Server Failover Clustering (WSFC)-Cluster handelt.|[Windows Server-Failoverclustering &#40;WSFC&#41; mit SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Stellen Sie sicher, dass der WSFC-Cluster ausreichend Knoten enthält, um die Verfügbarkeitsgruppenkonfigurationen zu unterstützen.|Ein WSF-Knoten kann nur ein Verfügbarkeitsreplikat für eine bestimmte Verfügbarkeitsgruppe hosten. In einem angegebenen WSFC-Knoten kann mindestens eine Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Verfügbarkeitsreplikate für viele Verfügbarkeitsgruppen hosten.<br /><br /> Fragen Sie die Datenbankadministratoren, wie viele WSFC-Knoten erforderlich sind, um die Verfügbarkeitsreplikate der geplanten Verfügbarkeitsgruppen zu unterstützen.<br /><br /> [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
  
> [!IMPORTANT]  
>  Stellen Sie zudem sicher, dass Ihre Umgebung ordnungsgemäß zum Herstellen einer Verbindung mit einer Verfügbarkeitsgruppe konfiguriert wird. Weitere Informationen finden Sie unter [Always On-Clientkonnektivität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
###  <a name="ComputerRecommendations"></a> Empfehlungen für Computer, die Verfügbarkeitsreplikate (Windows-System) hosten  
  
-   **Vergleichbare Systeme.**  Für eine bestimmte Verfügbarkeitsgruppe sollten alle Verfügbarkeitsreplikate auf vergleichbaren Systemen ausgeführt werden, die identische Arbeitslasten bewältigen können.  
  
-   **Dedizierte Netzwerkadapter:** Zur optimalen Leistung sollten Sie einen dedizierten Netzwerkadapter (NIC, Network Interface Card, Netzwerkschnittstellenkarte) für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] verwenden.  
  
-   **Ausreichender Speicherplatz:**  Jeder Computer, auf dem eine Serverinstanz ein Verfügbarkeitsreplikat hostet, muss über ausreichend Speicherplatz für alle Datenbanken in der Verfügbarkeitsgruppe verfügen. Bedenken Sie, dass sekundäre Datenbanken in gleichem Maße zunehmen wie ihre entsprechenden primären Datenbanken.  
  
###  <a name="PermissionsWindows"></a> Berechtigungen (Windows-System)  
 Zur Verwaltung eines WSFC-Clusters muss der Benutzer Systemadministrator auf jedem Clusterknoten sein.  
  
 Weitere Informationen über das Konto zum Verwalten des Clusters finden Sie unter [Anhang A: Failoverclusteranforderungen](http://technet.microsoft.com/library/dd197454.aspx).  
  
###  <a name="RelatedTasksWindows"></a> Verwandte Aufgaben (Windows-System)  
  
|Task|Link|  
|----------|----------|  
|Legen Sie den HostRecordTTL-Wert fest.|[Ändern des HostRecordTTL (Verwenden von Windows PowerShell)](#ChangeHostRecordTTLps)|  
  
####  <a name="ChangeHostRecordTTLps"></a> Ändern des HostRecordTTL (Verwenden von Windows PowerShell)  
  
1.  Öffnen Sie das PowerShell-Fenster über **Als Administrator ausführen**.  
  
2.  Importieren Sie das FailoverClusters-Modul.  
  
3.  Verwenden Sie das **Get-ClusterResource**-Cmdlet, um die Netzwerknamenressource anzuzeigen, und verwenden Sie das **Set-ClusterParameter**-Cmdlet, um den **HostRecordTTL**-Wert wie folgt festzulegen:  
  
     Get-ClusterResource „*\<Netzwerkressourcenname>*“ | Set-ClusterParameter-HostRecordTTL *\<Zeit_in_Sekunden>*  
  
     Im folgenden PowerShell-Beispiel wird der HostRecordTTL für eine Netzwerknamenressource mit dem Namen "`SQL Network Name (SQL35)`" auf 300 Sekunden festgelegt.  
  
    ```  
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  Bei jedem Öffnen eines neuen PowerShell-Fensters müssen Sie das **FailoverClusters**-Modul importieren.  
  
##### Verwandte Inhalte (PowerShell)  
  
-   [Clustering and High-Availability](http://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (Clustering und hohe Verfügbarkeit) (Failoverclustering und Netzwerklastenausgleichs-Teamblog)  
  
-   [Erste Schritte mit Windows PowerShell auf einem Failovercluster](http://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Clusterressourcenbefehle und entsprechende Windows PowerShell-Cmdlets](http://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="RelatedContentWS"></a> Verwandte Inhalte (Windows-System)  
  
-   [Konfigurieren von DNS-Einstellungen in einem Failovercluster für mehrere Standorte](http://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [DNS-Registrierung mit Netzwerknamenressource](http://blogs.msdn.com/b/clustering/archive/2009/07/17/9836756.aspx)  
  
-   [Windows 2008 R2 Failover Multisite Clustering](http://www.microsoft.com/windowsserver2008/en/us/failover-clustering-multisite.aspx)  
  
##  <a name="ServerInstance"></a> Voraussetzungen und Einschränkungen für SQL Server-Instanzen  
 Jede Verfügbarkeitsgruppe erfordert einen Satz Failoverpartner, die als *Verfügbarkeitsreplikate*bezeichnet und von Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]gehostet werden. Bei einer angegebenen Serverinstanz kann es sich um eine *eigenständige Instanz* oder eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]*Failovercluster-Instanz* (FCI) handeln.  
  
 **In diesem Abschnitt:**  
  
-   [Prüfliste: Voraussetzungen](#PrerequisitesSI)  
  
-   [Threadverwendung durch Verfügbarkeitsgruppen](#ThreadUsage)  
  
-   [Berechtigungen](#PermissionsSI)  
  
-   [Verwandte Aufgaben](#RelatedTasksSI)  
  
-   [Verwandte Inhalte](#RelatedContentSI)  
  
###  <a name="PrerequisitesSI"></a> Prüfliste: Voraussetzungen (Serverinstanz)  
  
||Voraussetzung|Links|  
|-|------------------|-----------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Beim Hostcomputer muss es sich um einen WSFC-Knoten (Windows Server Failover Clustering) handeln. Die Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], die Verfügbarkeitsreplikate für eine angegebene Verfügbarkeitsgruppe hosten, befinden sich jeweils in einem separaten Knoten eines einzelnen WSFC-Clusters . Eine Verfügbarkeitsgruppe kann sich während der Migration zu einem anderen WSFC-Cluster vorübergehend auf zwei Cluster erstrecken. SQL Server 2016 führt verteilte Verfügbarkeitsgruppen ein. In einer verteilten Verfügbarkeitsgruppe befinden sich zwei Verfügbarkeitsgruppen auf verschiedenen WSFC-Clustern.|[Windows Server-Failoverclustering &#40;WSFC&#41; mit SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [Failoverclustering und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)<br/> <br/> [Verteilte Verfügbarkeitsgruppen (Always On-Verfügbarkeitsgruppen)](../../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Wenn eine Verfügbarkeitsgruppe mit Kerberos verwendet werden soll:<br /><br /> Alle Serverinstanzen, die ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe hosten, müssen das gleiche SQL Server-Dienstkonto verwenden.<br /><br /> Der Domänenadministrator muss manuell einen Dienstprinzipalnamen (SPN) für Active Directory auf dem SQL Server-Dienstkonto beim virtuellen Netzwerknamen (VNN) des Verfügbarkeitsgruppenlisteners registrieren. Wenn der SPN auf keinem SQL Server-Dienstkonto registriert wird, treten bei der Authentifizierung Fehler auf.<br /><br /> <br /><br /> **\*\* Wichtig \*\***: Wenn Sie das SQL Server-Dienstkonto ändern, muss der Domänenadministrator den SPN erneut manuell registrieren.|[Registrieren eines Dienstprinzipalnamens für Kerberos-Verbindungen](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **Kurze Erklärung:**<br /><br /> Kerberos und SPNs erzwingen die gegenseitige Authentifizierung. Dem Windows-Konto, das die SQL Server-Dienste startet, wird der SPN zugeordnet. Wenn die Registrierung des SPNs nicht richtig erfolgt oder dabei ein Fehler aufgetreten ist, kann die Windows-Sicherheitsschicht nicht das Konto bestimmen, das dem Dienstprinzipalname zugewiesen ist. Das bedeutet, die Kerberos-Authentifizierung kann nicht verwendet werden.<br /><br /> <br /><br /> Hinweis: Bei NTLM gibt es diese Anforderung nicht.|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Wenn Sie planen, eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failoverclusterinstanz (FCI) zu verwenden, um ein Verfügbarkeitsreplikat zu hosten, muss gewährleistet sein, dass Sie die FCI-Einschränkungen verstehen und dass die FCI-Anforderungen erfüllt werden.|[Voraussetzungen und Anforderungen zum Hosten eines Verfügbarkeitsreplikats mithilfe einer SQL Server-Failoverclusterinstanz (FCI)](#FciArLimitations) (später in diesem Thema)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Auf jeder Serverinstanz muss die Enterprise Edition von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ausgeführt werden.|[Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Alle Serverinstanzen, die Verfügbarkeitsreplikate für eine Verfügbarkeitsgruppe hosten, müssen die gleiche [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sortierung verwenden.|[Festlegen oder Ändern der Serversortierung](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Aktivieren Sie die Funktion [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat für jede Verfügbarkeitsgruppe hostet. Auf einem angegebenen Computer können Sie so viele Serverinstanzen für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] aktivieren, wie Ihre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Installation unterstützt.|[Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> <br /><br /> **\*\* Wichtig \*\***: Wenn Sie einen WSFC-Cluster löschen und neu erstellen, müssen Sie die Funktion [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] auf jeder Serverinstanz, die auf dem ursprünglichen WSFC-Cluster für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] aktiviert war, deaktivieren und erneut aktivieren.|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Jede Serverinstanz erfordert einen Datenbankspiegelungs-Endpunkt. Beachten Sie, dass dieser Endpunkt von allen Verfügbarkeitsreplikaten, Datenbank-Spiegelungspartnern und Zeugen auf der Serverinstanz gemeinsam verwendet wird.<br /><br /> Wenn eine Serverinstanz, die Sie zum Hosten eines Verfügbarkeitsreplikats auswählen, unter einem Domänenbenutzerkonto ausgeführt wird und noch keinen Datenbankspiegelungs-Endpunkt aufweist, kann der [Assistent für neue Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md) (oder [Assistent zum Hinzufügen von Replikaten zu Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) den Endpunkt erstellen und dem Dienstkonto der Serverinstanz die CONNECT-Berechtigung erteilen. Wenn der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Dienst jedoch als integriertes Konto, z. B. Lokales System, Lokaler Dienst oder Netzwerkdienst, oder als Nichtdomänenkonto ausgeführt wird, müssen Sie Zertifikate zur Endpunktauthentifizierung verwenden, und der Assistent kann keinen Datenbankspiegelungs-Endpunkt auf der Serverinstanz erstellen. In diesem Fall empfiehlt es sich, dass Sie die Datenbankspiegelungs-Endpunkte manuell erstellen, bevor Sie den Assistenten starten.<br /><br /> <br /><br /> **\*\* Sicherheitshinweis \*\***: Die Transportsicherheit für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] entspricht derjenigen der Datenbankspiegelung.|[Der Datenbankspiegelungs-Endpunkt &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [Transportsicherheit für Datenbankspiegelung und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/database-mirroring/transport security - database mirroring - always on availability.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Bevor Datenbanken, die FILESTREAM verwenden, zu einer Verfügbarkeitsgruppe hinzugefügt werden, stellen Sie sicher, dass FILESTREAM auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe hostet, aktiviert worden ist.|[Aktivieren und Konfigurieren von FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Bevor eigenständige Datenbanken einer Verfügbarkeitsgruppe hinzugefügt werden, muss gewährleistet sein, dass die Serveroption **eigenständige Datenbankauthentifizierung** auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe hostet, auf **1** festgelegt wurde.|[Contained Database Authentication (Serverkonfigurationsoption)](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="ThreadUsage"></a> Threadverwendung durch Verfügbarkeitsgruppen  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] stellt die folgenden Anforderungen an Arbeitsthreads:  
  
-   Auf einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz im Leerlauf verwendet [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 0 Threads.  
  
-   Die maximale Anzahl der von Verfügbarkeitsgruppen verwendeten Threads entspricht der Einstellung, die als maximale Anzahl von Serverthreads ('**maximale Anzahl von Workerthreads**') minus 40 konfiguriert wurde.  
  
-   Die auf einer bestimmten Serverinstanz gehosteten Verfügbarkeitsreplikate verwenden einen gemeinsamen Threadpool.  
  
     Threads werden bedarfsgesteuert wie folgt freigegeben:  
  
    -   In der Regel gibt es 3 bis 10 freigegebene Threads, aber diese Zahl kann sich abhängig von der Arbeitslast des primären Replikats erhöhen.  
  
    -   Wenn ein bestimmter Thread eine Zeit lang im Leerlauf ist, wird er wieder im allgemeinen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Threadpool freigegeben. Normalerweise wird ein inaktiver Thread nach ~ 15 Sekunden Inaktivität freigegeben. Abhängig von der letzten Aktivität kann ein Thread jedoch länger im Leerlauf gehalten werden.  

    - Eine SQL Server-Instanz verwendet bis zu 100 Threads für parallele Wiederholung für sekundäre Replikate. Für jede Datenbank wird bis zur Hälfte der Gesamtzahl von CPU-Kernen, jedoch nicht mehr als 16 Threads pro Datenbank verwendet. Überschreitet die Gesamtzahl von erforderlichen Threads für eine einzelne Instanz den Wert 100, verwendet SQL Server einen einzelnes Wiederholungsthread für jede verbleibende Datenbank. Wiederholungsthreads werden nach ~ 15 Sekunden Inaktivität freigegeben. 

  
-   Darüber hinaus verwenden Verfügbarkeitsgruppen nicht freigegebene Threads wie folgt:  
  
    -   Jedes primäre Replikat verwendet einen Protokollaufzeichnungsthread für jede primäre Datenbank. Außerdem verwendet es einen Protokollsendethread für jede sekundäre Datenbank. Protokollsendethreads werden nach ~ 15 Sekunden Inaktivität freigegeben.    
  
    -   Von einer Sicherung auf einem sekundären Replikat wird ein Thread auf dem primären Replikat für die Dauer des Sicherungsvorgangs beibehalten.  
  
 Weitere Informationen finden Sie unter [Always On – HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (Always On - HADRON-Lernreihe: Nutzung des Arbeitsthreadpools für HADRON-fähige Datenbanken) (ein CSS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Technikblog).  
  
###  <a name="PermissionsSI"></a> Berechtigungen (Serverinstanz)  
  
|Task|Erforderliche Berechtigungen|  
|----------|--------------------------|  
|Erstellen des Endpunktes für die Datenbankspiegelung|Erfordert die CREATE ENDPOINT-Berechtigung oder die Mitgliedschaft in der festen Serverrolle **sysadmin** .  Erfordert zudem die CONTROL ON ENDPOINT-Berechtigung. Weitere Informationen finden Sie unter [GRANT (Endpunktberechtigungen) &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).|  
|Aktivieren von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|Erfordert auf dem lokalen Computer die Mitgliedschaft in der Gruppe **Administrator** und Vollzugriff auf den WSFC-Cluster.|  
  
###  <a name="RelatedTasksSI"></a> Verwandte Aufgaben (Serverinstanz)  
  
|Task|Thema|  
|----------|-----------|  
|Bestimmen, ob ein Datenbankspiegelungs-Endpunkt vorhanden ist|[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)|  
|Erstellen des Datenbankspiegelungs-Endpunkts (falls noch nicht vorhanden)|[Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [Verwenden von Zertifikaten für einen Datenbankspiegelungs-Endpunkt &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [Erstellen eines Datenbankspiegelungs-Endpunkts für Always On-Verfügbarkeitsgruppen &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database mirroring - always on availability groups- powershell.md)|  
|Aktivieren von Verfügbarkeitsgruppen|[Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="RelatedContentSI"></a> Verwandte Inhalte (Serverinstanz)  
  
-   [Always On – HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases (Always On – HADRON-Lernreihe: Nutzung des Arbeitsthreadpools für HADRON-fähige Datenbanken)](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
##  <a name="NetworkConnect"></a> Empfehlungen zur Netzwerkkonnektivität  
 Es wird dringend empfohlen, für die Kommunikation zwischen WSFC-Clusterelementen die gleichen Netzwerkverbindungen zu verwenden wie für die Kommunikation zwischen Verfügbarkeitsreplikaten.  Bei Verwendung separater Netzwerkverbindungen kann ein unerwartetes Verhalten auftreten, wenn einige Verbindungen (wenn auch nur vorübergehend) ausfallen.  
  
 Damit eine Verfügbarkeitsgruppe automatisches Failover unterstützt, muss das sekundäre Replikat, das dem automatischen Failoverpartner entspricht, beispielsweise den Status SYNCHRONIZED aufweisen. Wenn bei der Netzwerkverbindung mit dem sekundären Replikat (wenn auch nur vorübergehend) ein Fehler auftritt, wechselt das Replikat in den Status UNSYNCHRONIZED und wird erst nach Wiederherstellen der Verbindung erneut synchronisiert. Wenn der WSFC-Cluster ein automatisches Failover anfordert, während das sekundäre Replikat nicht synchronisiert ist, findet kein automatisches Failover statt.  
  
##  <a name="ClientConnSupport"></a> Unterstützung für Clientkonnektivität  
 Weitere Informationen zur [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]-Unterstützung für Clientkonnektivität finden Sie unter [Always On-Clientkonnektivität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
##  <a name="FciArLimitations"></a> Voraussetzungen und Einschränkungen zum Hosten eines Verfügbarkeitsreplikats mithilfe einer SQL Server-Failoverclusterinstanz (FCI)  
 **In diesem Abschnitt:**  
  
-   [Einschränkungen](#RestrictionsFCI)  
  
-   [Prüfliste: Voraussetzungen](#PrerequisitesFCI)  
  
-   [Verwandte Aufgaben](#RelatedTasksFCIs)  
  
-   [Verwandte Inhalte](#RelatedContentFCIs)  
  
###  <a name="RestrictionsFCI"></a> Einschränkungen (FCIs)  
  
> [!NOTE]  
> Failoverclusterinstanzen unterstützen freigegebene Clustervolumes (Cluster Shared Volumes, CSVs). Weitere Informationen zu CSVs finden Sie unter [Grundlegendes zu freigegebenen Clustervolumes in einem Failovercluster](http://technet.microsoft.com/library/dd759255.aspx).  
  
-   **Die Clusterknoten einer FCI können für eine angegebene Verfügbarkeitsgruppe nur ein Replikat hosten:**  Wenn Sie ein Verfügbarkeitsreplikat auf einer FCI hinzufügen, können die WSFC-Clusterknoten, die mögliche FCI-Besitzer sind, kein anderes Replikat für dieselbe Verfügbarkeitsgruppe hosten.  
  
     Weiter muss jedes andere Replikat von einer SQL Server 2016-Instanz gehostet werden, die sich unter einem anderen WSFC-Knoten des gleichen WSFC-Clusters befindet. Die einzige Ausnahme besteht darin, dass sich eine Verfügbarkeitsgruppe während der Migration zu einem anderen WSFC-Cluster vorübergehend auf zwei Cluster erstrecken kann.  
  
-   **Failoverclusterinstanzen (FCIs) unterstützen kein automatisches Failover durch Verfügbarkeitsgruppen:**  Da FCIs kein automatisches Failover durch Verfügbarkeitsgruppen unterstützen, können die Verfügbarkeitsreplikate, die von einer FCI gehostet werden, nur für manuelles Failover konfiguriert werden.  
  
-   **Ändern des FCI-Netzwerknamens:**  Falls Sie den Netzwerknamen einer FCI ändern müssen, die ein Verfügbarkeitsreplikat hostet, müssen Sie das Replikat aus seiner Verfügbarkeitsgruppe entfernen und das Replikat dann wieder der Verfügbarkeitsgruppe hinzufügen. Sie können das primäre Replikat nicht entfernen. Wenn Sie daher eine FCI umbenennen, die das primäre Replikat hostet, sollten Sie ein Failover zu einem sekundären Replikat ausführen und dann das vorherige primäre Replikat entfernen und wieder hinzufügen. Beachten Sie, dass durch Umbenennen einer FCI möglicherweise die URL ihres Datenbankspiegelungs-Endpunkts geändert wird. Stellen Sie beim Hinzufügen des Replikats sicher, dass Sie die aktuelle Endpunkt-URL angeben.  
  
###  <a name="PrerequisitesFCI"></a> Prüfliste: Voraussetzungen (FCIs)  
  
||Voraussetzung|Link|  
|-|------------------|----------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Stellen Sie sicher, dass jede SQL Server-Failoverclusterinstanz (FCI) den erforderlichen gemeinsam verwendeten Speicher laut Standardinstallation der SQL Server-Failoverclusterinstanz besitzt.||  
  
###  <a name="RelatedTasksFCIs"></a> Verwandte Aufgaben (FCIs)  
  
|Task|Thema|  
|----------|-----------|  
|Installieren eines SQL Server-Failoverclusters|[Erstellen eines neuen SQL Server-Failoverclusters &#40;Setup&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Direktes Upgrade des vorhandenen SQL Server-Failoverclusters|[Aktualisieren einer SQL Server-Failoverclusterinstanz &#40;Setup&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|Beibehalten des vorhandenen SQL Server-Failoverclusters|[Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="RelatedContentFCIs"></a> Verwandte Inhalte (FCIs)  
  
-   [Failoverclustering und Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [Always On-Architekturhandbuch: Erstellen einer Lösung für hohe Verfügbarkeit und Notfallwiederherstellung unter Verwendung von Failoverclusterinstanzen und Verfügbarkeitsgruppen](http://technet.microsoft.com/library/jj215886.aspx)  
  
##  <a name="PrerequisitesForAGs"></a> Voraussetzungen und Einschränkungen für Verfügbarkeitsdatenbanken  
 **In diesem Abschnitt:**  
  
-   [Einschränkungen](#RestrictionsAG)  
  
-   [Anforderungen](#RequirementsAG)  
  
-   [Sicherheit](#SecurityAG)  
  
-   [Verwandte Aufgaben](#RelatedTasksAGs)  
  
###  <a name="RestrictionsAG"></a> Einschränkungen (Verfügbarkeitsgruppen)  
  
-   **Verfügbarkeitsreplikate müssen von verschiedenen Knoten eines WSFC-Clusters gehostet werden:**  Für eine angegebene Verfügbarkeitsgruppe müssen Verfügbarkeitsreplikate von Serverinstanzen gehostet werden, die auf verschiedenen Knoten desselben WSFC-Clusters ausgeführt werden. Die einzige Ausnahme besteht darin, dass sich eine Verfügbarkeitsgruppe während der Migration zu einem anderen WSFC-Cluster vorübergehend auf zwei Cluster erstrecken kann.  
  
    > [!NOTE]  
    >  Virtuelle Computer können auf demselben physischen Computer jeweils ein Verfügbarkeitsreplikat für dieselbe Verfügbarkeitsgruppe hosten, da jeder virtuelle Computer als separater Computer fungiert.  
  
-   **Eindeutiger Verfügbarkeitsgruppenname:**  Jeder Verfügbarkeitsgruppenname muss auf dem WSFC-Failovercluster eindeutig sein. Die maximale Länge eines Verfügbarkeitsgruppennamens beträgt 128 Zeichen.  
  
-   **Verfügbarkeitsreplikate:**  Jede Verfügbarkeitsgruppe unterstützt ein primäres Replikat und bis zu acht sekundäre Replikate. Alle Replikate können im Modus für asynchrone Commits ausgeführt werden. Alternativ können bis zu drei Replikate im Modus für synchrone Commits ausgeführt werden (ein primäres Replikat mit zwei synchronen sekundären Replikaten).  
  
-   **Maximale Anzahl von Verfügbarkeitsgruppen und Verfügbarkeitsdatenbanken pro Computer:** Die tatsächliche Anzahl der auf einem Computer (VM oder physischer Computer) ausführbaren Datenbanken und Verfügbarkeitsgruppen richtet sich nach der Hardware und Arbeitsauslastung, es gibt jedoch keine maximale Vorgabe. Microsoft hat umfangreiche Testreihen mit 10 Verfügbarkeitsgruppen und 100 Datenbanken pro physischem Computer durchgeführt. Anzeichen für eine Systemüberlastung könnten u.a. zu wenige Arbeitsthreads, langsame Antwortzeiten für Verfügbarkeitsgruppen-Systemsichten und DMVs und/oder Systemspeicherabbilder bei angehaltenem Verteiler sein. Es wird empfohlen, die Umgebung unter produktionsähnlichen Bedingungen eingehend zu testen, um zu gewährleisten, dass das System maximale Arbeitsauslastungen im Rahmen Ihrer Anwendungs-SLAs bewältigen kann. Im Hinblick auf SLAs sollten sowohl die Auslastung unter Fehlerbedingungen als auch die erwarteten Antwortzeiten abgewogen werden.  
  
-   **Verwenden Sie den Failovercluster-Manager nicht, um Verfügbarkeitsgruppen zu bearbeiten:**  
  
     Beispiel:  
  
    -   Ändern Sie keine Verfügbarkeitsgruppeneigenschaften, z. B. die möglichen Besitzer.  
  
    -   Verwenden Sie den Failovercluster-Manager nicht, um Failover für Verfügbarkeitsgruppen auszuführen. Sie müssen [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] verwenden.  
  
###  <a name="RequirementsAG"></a> Voraussetzungen (Verfügbarkeitsgruppen)  
 Beim Erstellen oder Neukonfigurieren einer Verfügbarkeitsgruppenkonfiguration müssen Sie folgende Anforderungen einhalten.  
  
||Voraussetzung|Beschreibung|  
|-|------------------|-----------------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Wenn Sie planen, eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failoverclusterinstanz (FCI) zu verwenden, um ein Verfügbarkeitsreplikat zu hosten, muss gewährleistet sein, dass Sie die FCI-Einschränkungen verstehen und dass die FCI-Anforderungen erfüllt werden.|[Voraussetzungen und Einschränkungen zum Hosten eines Verfügbarkeitsreplikats mithilfe einer SQL Server-Failoverclusterinstanz (FCI)](#FciArLimitations) (früher in diesem Thema)|  
  
###  <a name="SecurityAG"></a> Sicherheit (Verfügbarkeitsgruppen)  
  
-   Die Sicherheit wird vom Windows Server-Failoverclustering (WSFC)-Cluster geerbt. WSFC stellt zwei Benutzersicherheitsebenen mit der Granularität gesamter WSFC-Cluster-APIs bereit:  
  
    -   Schreibgeschützter Zugriff  
  
    -   Vollzugriff  
  
         [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] benötigt Vollzugriff. Durch Aktivieren von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] auf einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] wird der Vollzugriff auf den WSFC-Cluster erteilt (über Dienst-SID).  
  
         Sie können im WSFC-Failovercluster-Manager die Sicherheit für eine Serverinstanz nicht direkt hinzufügen oder entfernen. Um WSFC-Sicherheitssitzungen zu verwalten, verwenden Sie den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfigurations-Manager oder die WMI-Entsprechung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Jede Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] muss über Berechtigungen zum Zugreifen auf die Registrierung, den Cluster usw. verfügen.  
  
-   Es wird empfohlen, dass Sie eine Verschlüsselung für Verbindungen zwischen Serverinstanzen verwenden, die [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]-Verfügbarkeitsreplikate hosten.  
  
#### Berechtigungen (Verfügbarkeitsgruppen)  
  
|Task|Erforderliche Berechtigungen|  
|----------|--------------------------|  
|Erstellen einer Verfügbarkeitsgruppe|Erfordert die Mitgliedschaft in der festen **sysadmin** -Serverrolle und die CREATE AVAILABILITY GROUP-Serverberechtigung, ALTER ANY AVAILABILITY GROUP-Berechtigung oder CONTROL SERVER-Berechtigung.|  
|Ändern einer Verfügbarkeitsgruppe|Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.<br /><br /> Außerdem erfordert das Verknüpfen einer Datenbank mit einer Verfügbarkeitsgruppe die Mitgliedschaft in der festen **db_owner**-Datenbankrolle.|  
|Löschen einer Verfügbarkeitsgruppe|Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung. Um eine Verfügbarkeitsgruppe zu löschen, die nicht am lokalen Replikatspeicherort gehostet wird, benötigen Sie die CONTROL SERVER-Berechtigung oder die CONTROL-Berechtigung für diese Verfügbarkeitsgruppe.|  
  
###  <a name="RelatedTasksAGs"></a> Verwandte Aufgaben (Verfügbarkeitsgruppen)  
  
|Task|Thema|  
|----------|-----------|  
|Erstellen einer Verfügbarkeitsgruppe|[Verwenden der Verfügbarkeitsgruppe (Assistent für neue Verfügbarkeitsgruppen)](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Erstellen einer Verfügbarkeitsgruppe (Transact-SQL)](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)<br /><br /> [Erstellen einer Verfügbarkeitsgruppe (SQL Server PowerShell)](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)<br /><br /> [Angeben der Endpunkt-URL beim Hinzufügen oder Ändern eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify endpoint url - adding or modifying availability replica.md)|  
|Ändern der Anzahl der Verfügbarkeitsreplikate|[Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Entfernen eines sekundären Replikats aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|Erstellen eines Verfügbarkeitsgruppenlisteners|[Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
|Löschen einer Verfügbarkeitsgruppe|[Entfernen einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)|  
  
##  <a name="PrerequisitesForDbs"></a> Voraussetzungen und Einschränkungen für Verfügbarkeitsdatenbanken  
 Damit einer Verfügbarkeitsgruppe eine Datenbank hinzugefügt werden kann, muss sie folgenden Voraussetzungen und Einschränkungen entsprechen:  
  
 **In diesem Abschnitt:**  
  
-   [Anforderungen](#RequirementsDb)  
  
-   [Einschränkungen](#RestrictionsDb)  
  
-   [Empfehlungen für Computer, die Verfügbarkeitsreplikate (Windows-System) hosten](#TDEdbs)  
  
-   [Berechtigungen](#PermissionsDbs)  
  
-   [Verwandte Aufgaben](#RelatedTasksADb)  
  
###  <a name="RequirementsDb"></a> Prüfliste: Anforderungen (Verfügbarkeitsdatenbanken)  
 Damit eine Datenbank einer Verfügbarkeitsgruppe hinzugefügt zu werden, müssen folgende Bedingungen für die Datenbank zutreffen:  
  
||Anforderungen|Link|  
|-|------------------|----------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Die Datenbank muss eine Benutzerdatenbank sein. Systemdatenbanken können nicht zu einer Verfügbarkeitsgruppe gehören.||  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Die Datenbank muss sich auf der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], auf der Sie die Verfügbarkeitsgruppe erstellen, und die Serverinstanz muss darauf zugreifen können.||  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Die Datenbank muss eine Datenbank mit Lese-/Schreibzugriff sein. Schreibgeschützte Datenbanken können nicht zu einer Verfügbarkeitsgruppe hinzugefügt werden.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**is_read_only** = 0)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Die Datenbank muss eine Mehrbenutzerdatenbank sein.|[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**user_access** = 0)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verwenden Sie nicht AUTO_CLOSE.|[sys.Databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**is_auto_close_on** = 0)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verwenden Sie das vollständige Wiederherstellungsmodell (auch bekannt als der vollständige Wiederherstellungsmodus).|[sys.Databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**recovery_model** = 1)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Die Datenbank muss mindestens über eine vollständige Datenbanksicherung verfügen.<br /><br /> Hinweis: Eine vollständige Sicherung ist erforderlich, um die volle-Wiederherstellungs-Protokollkette zu initiieren, nachdem seine Datenbank auf den vollständigen Wiederherstellungsmodus festgelegt wurde.|[Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Sie darf zu keiner vorhandenen Verfügbarkeitsgruppe gehören.|[sys.Databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) (**group_database_id** = NULL)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Die Datenbank darf nicht für die Datenbankspiegelung konfiguriert sein.|[sys.database_mirroring](../../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md) (Wenn die Datenbank nicht an der Spiegelung beteiligt ist, haben alle Spalten mit dem Präfix „mirroring_“ den Wert NULL.)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Bevor Sie eine Datenbank, die FILESTREAM verwendet, zu einer Verfügbarkeitsgruppe hinzufügen, muss gewährleistet sein, dass FILESTREAM auf jeder Serverinstanz aktiviert ist, die ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe hostet oder hosten wird.|[Aktivieren und Konfigurieren von FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Vor dem Hinzufügen einer enthaltenen Datenbank zu einer Verfügbarkeitsgruppe muss gewährleistet sein, dass die Serveroption **eigenständige Datenbankauthentifizierung** auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe hostet oder hosten wird, auf **1** gesetzt ist.|[Contained Database Authentication (Serverkonfigurationsoption)](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] funktioniert mit jedem unterstützten Datenbank-Kompatibilitätsgrad.  
  
###  <a name="RestrictionsDb"></a> Einschränkungen (Verfügbarkeitsdatenbanken)  
  
-   Falls sich der Dateipfad (einschließlich des Laufwerkbuchstabens) einer sekundären Datenbank vom Pfad der entsprechenden primären Datenbank unterscheidet, gelten folgende Einschränkungen.  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]:** Die Option **Vollständig** wird nicht unterstützt (auf der Seite [Anfängliche Datensynchonisierung auswählen](../../../database-engine/availability-groups/windows/select-initial-data-synchronization-page-always-on-availability-group-wizards.md)),  
  
    -   **RESTORE WITH MOVE:**  Zum Erstellen der sekundären Datenbanken müssen die Datenbankdateien auf jeder Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die ein sekundäres Replikat hostet, auf RESTORED WITH MOVE gesetzt sein.  
  
    -   **Auswirkungen auf Dateihinzufügungsvorgänge:** Bei einer späteren Dateihinzufügung auf dem primären Replikat tritt in den sekundären Datenbanken möglicherweise ein Fehler auf. Dieser Fehler kann bewirken, dass die sekundären Datenbanken angehalten werden. Dies bewirkt dann, dass die sekundären Replikate den Status NOT SYNCHRONIZING erhalten.  
  
        > [!NOTE]  
        >  Informationen zum Reagieren auf einen Dateihinzufügungsvorgang, bei dem ein Fehler aufgetreten ist, finden Sie unter [Problembehandlung bei einem fehlgeschlagenen Vorgang zum Hinzufügen einer Datei &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md).  
  
-   Sie können keine Datenbank löschen, die aktuell einer Verfügbarkeitsgruppe angehört.  
  
###  <a name="TDEdbs"></a> Nachverfolgung für TDE-geschützte Datenbanken  
 Wenn Sie die transparente Datenverschlüsselung (TDE) verwenden, muss das Zertifikat oder der asymmetrische Schlüssel zum Erstellen und Entschlüsseln weiterer Schlüssel auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe hostet, identisch sein. Weitere Informationen finden Sie unter [Verschieben einer TDE-geschützten Datenbank auf einen anderen SQL-Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
###  <a name="PermissionsDbs"></a> Berechtigungen (Verfügbarkeitsdatenbanken)  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
###  <a name="RelatedTasksADb"></a> Verwandte Aufgaben (Verfügbarkeitsdatenbanken)  
  
|Task|Thema|  
|----------|-----------|  
|Vorbereiten einer sekundären Datenbank (manuell)|[Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe (manuell)|[Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|Ändern der Anzahl der Verfügbarkeitsdatenbanken|[Hinzufügen einer Datenbank zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-database-to-an-availability-group-sql-server.md)<br /><br /> [Entfernen einer sekundären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [Entfernen einer primären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Microsoft SQL Server Always On Solutions Guide for High Availability and Disaster Recovery (Microsoft SQL Server Always On-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung)](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server Always On Team Blogs: The official SQL Server Always On Team Blog (SQL Server Always On-Teamblogs: Der offizielle SQL Server Always On-Teamblog)](http://blogs.msdn.com/b/sqlAlways%20On/)  
  
-   [Always On – HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases (Always On – HADRON-Lernreihe: Nutzung des Arbeitsthreadpools für HADRON-fähige Datenbanken)](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
## Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Failoverclustering und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Always On-Clientkonnektivität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
    
  
--------------------------------------------------  
