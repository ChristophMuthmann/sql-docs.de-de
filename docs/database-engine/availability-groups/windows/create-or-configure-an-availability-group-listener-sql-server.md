---
title: Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.availabilitygroup.newaglistener.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], client connectivity
ms.assetid: 2bc294f6-2312-4b6b-9478-2fb8a656e645
caps.latest.revision: 52
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.workload: Active
ms.openlocfilehash: 746cdda3b75aee4f15f7c03f9754614f15c68434
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-or-configure-an-availability-group-listener-sql-server"></a>Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird die Erstellung oder Konfiguration eines einzelnen *Verfügbarkeitsgruppenlisteners* für eine Always On-Verfügbarkeitsgruppe beschrieben. Dazu wird [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]verwendet.  
  
> [!IMPORTANT]  
>  Für die Erstellung des ersten Verfügbarkeitsgruppenlisteners einer Verfügbarkeitsgruppe empfehlen wir dringend die Verwendung von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Vermeiden Sie, einen Listener direkt im WSFC-Cluster zu erstellen, sofern dies nicht unbedingt notwendig ist (z. B. bei der Erstellung eines zusätzlichen Listeners).  
  
-   **Vorbereitungen:**  
  
     [Ist bereits ein Listener für diese Verfügbarkeitsgruppe vorhanden?](#DoesListenerExist)  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Voraussetzungen](#Prerequisites)  
  
     [Anforderungen für den DNS-Namen eines Verfügbarkeitsgruppenlisteners](#DNSnameReqs)  
  
     [Windows-Berechtigungen](#WinPermissions)  
  
     [SQL Server-Berechtigungen](#SqlPermissions)  
  
-   **Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Problembehandlung**  
  
     [Fehler beim Erstellen eines Verfügbarkeitsgruppenlisteners wegen Active Directory-Kontingenten](#ADQuotas)  
  
-   **Nachverfolgung: Nach dem Erstellen eines Verfügbarkeitsgruppenlisteners**  
  
     [MultiSubnetFailover-Schlüsselwort und zugehörige Funktionen](#MultiSubnetFailover)  
  
     [Einstellung RegisterAllProvidersIP](#RegisterAllProvidersIP)  
  
     [Einstellung HostRecordTTL](#HostRecordTTL)  
  
     [Beispiel-PowerShell-Skript zur Deaktivierung von RegisterAllProvidersIP und zur Reduzierung der Gültigkeitsdauer (TTL)](#SampleScript)  
  
     [Empfehlungen für anschließende Aufgaben](#FollowUpRecommendations)  
  
     [Erstellen eines zusätzlichen Listeners für eine Verfügbarkeitsgruppe (optional)](#CreateAdditionalListener)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="DoesListenerExist"></a> Ist bereits ein Listener für diese Verfügbarkeitsgruppe vorhanden?  
 **So ermitteln Sie, ob bereits ein Listener für die Verfügbarkeitsgruppe vorhanden ist**  
  
-   [Anzeigen von Eigenschaften des Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
> [!NOTE]  
>  Wenn ein Listener bereits vorhanden ist und Sie einen zusätzlichen Listener erstellen möchten, siehe [So erstellen Sie einen zusätzlichen Listener für eine Verfügbarkeitsgruppe (Optional)](#CreateAdditionalListener)weiter unten in diesem Thema.  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Sie können anhand von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]nur einen Listener pro Verfügbarkeitsgruppe erstellen. In der Regel erfordert jede Verfügbarkeitsgruppe nur einen Listener. Einige Kundenszenarien erfordern jedoch mehrere Listener für eine Verfügbarkeitsgruppe.   Nachdem Sie mit SQL Server einen Listener erstellt haben, können Sie Windows PowerShell für Failovercluster oder den WSFC Failovercluster-Manager verwenden, um zusätzliche Listener zu erstellen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [So erstellen Sie einen zusätzlichen Listener für eine Verfügbarkeitsgruppe (optional)](#CreateAdditionalListener).  
  
###  <a name="Recommendations"></a> Empfehlungen  
 Die Verwendung einer statischen IP-Adresse wird zwar empfohlen, ist für Multisubnetz-Konfigurationen jedoch nicht unbedingt erforderlich.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen mit der Serverinstanz verbunden sein, die das primäre Replikat hostet.  
  
-   Wenn Sie einen Verfügbarkeitsgruppenlistener für mehrere Subnetze einrichten und beabsichtigen, statische IP-Adressen zu verwenden, müssen Sie die statische IP-Adresse jedes Subnetzes abrufen, von dem ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe gehostet wird, für die Sie den Listener erstellen. Normalerweise müssen Sie die Netzwerkadministratoren um die statischen IP-Adressen bitten.  
  
> [!IMPORTANT]  
>  Vor dem Erstellen des ersten Listeners empfiehlt es sich, den Artikel [Always On-Clientkonnektivität (SQL Server)](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md) zu lesen.  
  
###  <a name="DNSnameReqs"></a> Anforderungen für den DNS-Namen eines Verfügbarkeitsgruppenlisteners  
 Für jeden Verfügbarkeitsgruppenlistener ist ein DNS-Hostname erforderlich, der in der Domäne und in NetBIOS eindeutig ist. Der DNS-Name ist ein Zeichenfolgenwert. Dieser Name darf nur alphanumerische Zeichen, Bindestriche (-) und Unterstriche (_) enthalten (in beliebiger Reihenfolge). Bei DNS-Hostnamen muss die Groß-/Kleinschreibung beachtet werden. Die maximale Länge beträgt 63 Zeichen, die maximale Länge, die in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]angegeben werden kann, ist jedoch 15 Zeichen.  
  
 Wir empfehlen, dass Sie eine sinnvolle Zeichenfolge angeben. Für eine Verfügbarkeitsgruppe mit dem Namen `AG1`wäre ein sinnvoller DNS-Hostname z. B. `ag1-listener`.  
  
> [!IMPORTANT]  
>  NetBIOS erkennt nur die ersten 15 Zeichen im dns_name. Wenn Sie zwei WSFC-Cluster verwenden, die vom gleichen Active Directory gesteuert werden, und Sie versuchen, Verfügbarkeitsgruppenlistener in beiden Clustern mit Namen mit mehr als 15 Zeichen und einem identischen 15-Zeichen-Präfix zu erstellen, erhalten Sie eine Fehlermeldung mit dem Hinweis, dass die VNN-Ressource nicht online geschaltet werden konnte. Informationen zu Präfix-Benennungsregeln für DNS-Namen finden Sie unter [Zuweisen von Domänennamen](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx).  
  
###  <a name="WinPermissions"></a> Windows-Berechtigungen  
  
|Berechtigungen|Link|  
|-----------------|----------|  
|Das Clusternamenobjekt (CNO) des WSFC-Clusters, der die Verfügbarkeitsgruppe hostet, muss über die Berechtigung zum **Erstellen von Computerobjekten** verfügen.<br /><br /> Standardmäßig weist ein CNO in Active Directory die Berechtigung zum **Erstellen von Computerobjekten** nicht explizit auf und kann 10 virtuelle Computerobjekte (Virtual Computer Objects, VCOs) erstellen. Nach der Erstellung von 10 VCOs können keine weiteren VCOs erstellt werden. Sie können das vermeiden, indem Sie dem CNO des WSFC-Clusters die Berechtigung explizit erteilen. Beachten Sie, dass VCOs gelöschter Verfügbarkeitsgruppen in Active Directory nicht automatisch gelöscht werden. Sie werden auf die Standardbeschränkung von 10 VCOs angerechnet, sofern sie nicht manuell gelöscht werden.<br /><br /> Hinweis: In einigen Organisationen verhindert die Sicherheitsrichtlinie, dass einzelnen Benutzerkonten die Berechtigung zum **Erstellen von Computerobjekten** erteilt wird.|*Schritte für die Konfiguration des Kontos für den Benutzer, der den Cluster installiert* in [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_installer)<br /><br /> *Schritte für die Vorabbereitstellung des Clusternamenkontos* in [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_precreating)|  
|Falls in der Organisation erforderlich ist, dass das Computerkonto für den Namen eines virtuellen Listenernetzwerks vorab bereitgestellt wird, müssen Sie Mitglied der Gruppe **Account Operator** sein oder den Domänenadministrator um Unterstützung bitten.|*Schritte für die Vorabbereitstellung eines Kontos für einen gruppierten Dienst oder eine gruppierte Anwendung* in [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_precreating2)(Schritt-für-Schritt-Anleitung für Failover Cluster: Konfigurieren von Konten in Active Directory).|  
  
> [!TIP]  
>  Im Allgemeinen ist es am einfachsten, das Computerkonto für den Namen eines virtuellen Listenernetzwerks nicht vorab bereitzustellen. Lassen Sie bei der Ausführung des Assistenten für die hohe WSFC-Verfügbarkeit nach Möglichkeit die automatische Erstellung und Konfiguration des Kontos zu.  
  
###  <a name="SqlPermissions"></a> SQL Server-Berechtigungen  
  
|Task|Berechtigungen|  
|----------|-----------------|  
|So erstellen Sie einen Verfügbarkeitsgruppenlistener|Erfordert die Mitgliedschaft in der festen **sysadmin** -Serverrolle und die CREATE AVAILABILITY GROUP-Serverberechtigung, ALTER ANY AVAILABILITY GROUP-Berechtigung oder CONTROL SERVER-Berechtigung.|  
|So ändern Sie einen vorhandenen Verfügbarkeitsgruppenlistener|Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.|  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
> [!TIP]  
>  Der [Assistent für neue Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) unterstützt Sie bei der Erstellung eines Listeners für eine neue Verfügbarkeitsgruppe.  
  
 **So erstellen oder konfigurieren Sie einen Verfügbarkeitsgruppenlistener**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Replikat der Verfügbarkeitsgruppe hostet, und klicken Sie zum Erweitern der Serverstruktur auf den Servernamen.  
  
2.  Erweitern Sie die Knoten **Always On High Availability** (Always On Hochverfügbarkeit) und **Verfügbarkeitsgruppen** .  
  
3.  Klicken Sie auf die Verfügbarkeitsgruppe, deren Listener Sie konfigurieren möchten, und wählen Sie eine der folgenden Alternativen aus:  
  
    -   Klicken Sie zum Erstellen eines Listeners mit der rechten Maustaste auf den Knoten **Verfügbarkeitsgruppenlistener** , und wählen Sie den Befehl **Neuer Listener** aus. Das Dialogfeld **Neuer Verfügbarkeitsgruppenlistener** wird geöffnet. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Verfügbarkeitsgruppenlistener hinzufügen (Dialogfeld)](#AddAgListenerDialog).  
  
    -   Erweitern Sie zum Ändern der Portnummer eines vorhanden Listeners den Knoten **Verfügbarkeitsgruppenlistener** , klicken Sie mit der rechten Maustaste auf den Listener, und wählen Sie den Befehl **Eigenschaften** aus. Geben Sie die neue Portnummer in das Feld **Port** ein, und klicken Sie auf **OK**.  
  
###  <a name="AddAgListenerDialog"></a> Neuer Verfügbarkeitsgruppenlistener (Dialogfeld)  
 **DNS-Name des Listeners**  
 Gibt den DNS-Hostnamen des Verfügbarkeitsgruppenlisteners an. Der DNS-Name ist eine Zeichenfolge, die in der Domäne und in NetBIOS eindeutig sein muss. Dieser Name darf nur alphanumerische Zeichen, Bindestriche (-) und Unterstriche (_) enthalten (in beliebiger Reihenfolge). Bei DNS-Hostnamen muss die Groß-/Kleinschreibung beachtet werden. Die maximale Länge beträgt 15 Zeichen.  
  
 Weitere Informationen finden Sie weiter oben in diesem Thema unter [Anforderungen für den DNS-Namen eines Verfügbarkeitsgruppenlisteners](#DNSnameReqs).  
  
 **Port**  
 Der von diesem Listener verwendete TPC-Port.  
  
 **Netzwerkmodus**  
 Gibt das vom Listener verwendete TCP-Protokoll an. Folgende Werte sind möglich:  
  
 **DHCP**  
 Der Listener verwendet eine dynamische IP-Adresse, die von einem Server mit dem Dynamic Host Configuration-Protokoll (DHCP) zugewiesen wird. DHCP ist auf ein einzelnes Subnetz beschränkt.  
  
> [!IMPORTANT]  
>  DHCP wird in einer Produktionsumgebung nicht empfohlen. Wenn die DHCP-IP-Leasedauer bei einer Downtime abläuft, ist eine Verlängerung erforderlich, um die neue IP-Adresse des DHCP-Netzwerks zu registrieren, die dem DNS-Namen des Listeners zugeordnet ist, was sich auf die Clientkonnektivität auswirkt. DHCP eignet sich jedoch gut zum Einrichten der Entwicklungs- und Testumgebung, um grundlegende Funktionen von Verfügbarkeitsgruppen und die Integration in Ihre Anwendungen zu überprüfen.  
  
 **Statische IP**  
 Der Listener verwendet mindestens eine statische IP-Adresse. Zusätzliche IP-Adressen sind optional. Sie müssen zum Erstellen eines Verfügbarkeitsgruppenlisteners für mehrere Subnetze für alle Subnetze eine statische IP-Adresse in der Listenerkonfiguration angeben. Wenden Sie sich an Ihren Netzwerkadministrator, um diese statischen IP-Adressen abzurufen.  
  
 Wenn Sie **Statische IP** auswählen, wird unter dem Feld **Netzwerkmodus** ein Subnetzraster angezeigt. Dieses Raster enthält Informationen zu allen Subnetzen, auf die von diesem Verfügbarkeitsgruppenlistener zugegriffen werden kann. Dieses Raster ist leer, bis Sie eine statische IP-Adresse hinzufügen, indem Sie auf **Hinzufügen**klicken.  
  
 Es gibt folgende Spalten:  
  
 **Subnetz**  
 Zeigt den Bezeichner aller Subnetze an, die Sie dem Verfügbarkeitsgruppenlistener hinzufügen.  
  
 **IP-Adresse**  
 Zeigt die IP-Adresse eines bestimmten Subnetzes an.  Für ein bestimmtes Subnetz ist die IP-Adresse entweder eine IPv4-Adresse oder eine IPv6-Adresse.  
  
 **Hinzufügen**  
 Klicken Sie zum Hinzufügen einer statischen IP-Adresse zu einem ausgewählten Subnetz oder einem anderen Subnetz für diesen Listener auf diese Option. Das Dialogfeld **IP-Adresse hinzufügen** wird geöffnet. Weitere Informationen finden Sie im Hilfethema [Dialogfeld IP-Adresse hinzufügen&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/add-ip-address-dialog-box-sql-server-management-studio.md).  
  
 **Entfernen**  
 Klicken Sie, um das ausgewählte Subnetz von diesem Listener zu entfernen.  
  
 **OK**  
 Klicken Sie, um den angegebenen Verfügbarkeitsgruppenlistener zu erstellen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So erstellen oder konfigurieren Sie einen Verfügbarkeitsgruppenlistener**  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet.  
  
2.  Verwenden Sie die LISTENER-Option der [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md) -Anweisung oder die ADD LISTENER-Option der [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) -Anweisung.  
  
     Im folgenden Beispiel wird einer vorhandenen Verfügbarkeitsgruppe namens `MyAg2`ein Verfügbarkeitsgruppenlistener hinzugefügt. Der eindeutige DNS-Name `MyAg2ListenerIvP6`wird für diesen Listener angegeben. Da sich zwei Replikate in unterschiedlichen Subnetzen befinden, verwendet der Listener entsprechend der Empfehlung statische IP-Adressen. Für die beiden Verfügbarkeitsreplikate gibt die WITH IP-Klausel jeweils die statische IP-Adresse `2001:4898:f0:f00f::cf3c and 2001:4898:e0:f213::4ce2`an, die das IPv6-Format verwendet. In diesem Beispiel wird zudem das optionale PORT-Argument verwendet, um Port `60173` als Listenerport anzugeben.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAg2   
          ADD LISTENER ‘MyAg2ListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
    GO  
  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So erstellen oder konfigurieren Sie einen Verfügbarkeitsgruppenlistener**  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, die das primäre Replikat hostet.  
  
2.  Erstellen oder ändern Sie einen Verfügbarkeitsgruppenlistener mit einem der folgenden Cmdlets:  
  
     **New-SqlAvailabilityGroupListener**  
     Erstellt einen neuen Verfügbarkeitsgruppenlistener und fügt ihn einer vorhandenen Verfügbarkeitsgruppe hinzu.  
  
     Beispielsweise wird durch den folgenden **New-SqlAvailabilityGroupListener** -Befehl ein Verfügbarkeitsgruppenlistener namens `MyListener` für die Verfügbarkeitsgruppe `MyAg`erstellt. Dieser Listener verwendet die an den **-StaticIp** -Parameter übergebene IPv4-Adresse als seine virtuelle IP-Adresse.  
  
    ```  
    New-SqlAvailabilityGroupListener -Name MyListener `   
    -StaticIp '192.168.3.1/255.255.252.0' `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
  
    ```  
  
     **Set-SqlAvailabilityGroupListener**  
     Ändert die Porteinstellung eines vorhandenen Verfügbarkeitsgruppenlisteners.  
  
     Beispielsweise wird die Portnummer durch den folgenden **Set-SqlAvailabilityGroupListener** -Befehl für den Verfügbarkeitsgruppenlistener `MyListener` auf `1535`festgelegt. Dieser Port wird zum Lauschen auf Verbindungen mit dem Listener verwendet.  
  
    ```  
    Set-SqlAvailabilityGroupListener -Port 1535 `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
  
    ```  
  
     **Add-SqlAGListenerstaticIp**  
     Fügt der vorhandenen Konfiguration eines Verfügbarkeitsgruppenlisteners eine statische IP-Adresse hinzu. Die IP-Adresse kann eine IPv4-Adresse mit Subnetz oder eine IPv6-Adresse sein.  
  
     Durch den folgenden **Add-SqlAGListenerstaticIp** -Befehl wird dem Verfügbarkeitsgruppenlistener `MyListener` in der Verfügbarkeitsgruppe `MyAg`beispielsweise eine statische IPv4-Adresse hinzugefügt. Diese IPv6-Adresse stellt die virtuelle IP-Adresse des Listeners im Subnetz `255.255.252.0`dar. Wenn sich die Verfügbarkeitsgruppe über mehrere Subnetze erstreckt, sollten Sie dem Listener eine statische IP-Adresse für jedes Subnetz hinzufügen.  
  
    ```  
    $path = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\ MyListener" `   
    Add-SqlAGListenerstaticIp -Path $path `   
    -StaticIp "2001:0db8:85a3:0000:0000:8a2e:0370:7334"  
    ```  
  
    > [!NOTE]  
    >  Verwenden Sie das Cmdlet **Get-Help**  in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -PowerShell-Umgebung, um die Syntax eines Cmdlets anzuzeigen. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="troubleshooting"></a>Problembehandlung  
  
###  <a name="ADQuotas"></a> Fehler beim Erstellen eines Verfügbarkeitsgruppenlisteners wegen Active Directory-Kontingenten  
 Die Erstellung eines neuen Verfügbarkeitsgruppenlisteners schlägt möglicherweise beim Erstellen fehl, da Sie ein Active Directory-Kontingent für das teilnehmende Clusterknoten-Computerkonto erreicht haben.  Weitere Informationen finden Sie in den folgenden Artikeln:  
  
-   [Problembehandlung für das Clusterdienstkonto bei Änderung von Computerobjekten](http://support.microsoft.com/kb/307532)  
  
-   [Active Directory-Kontingente](http://technet.microsoft.com/library/cc904295\(WS.10\).aspx)  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erstellen eines Verfügbarkeitsgruppenlisteners  
  
###  <a name="MultiSubnetFailover"></a> MultiSubnetFailover-Schlüsselwort und zugehörige Funktionen  
 **MultiSubnetFailover** ist ein neues Schlüsselwort für Verbindungszeichenfolgen, das ein schnelleres Failover bei Always On-Verfügbarkeitsgruppen und Always On-Failoverclusterinstanzen in SQL Server 2012 ermöglicht. Wenn in der Verbindungszeichenfolge `MultiSubnetFailover=True` festgelegt wird, werden die folgenden drei Teilfunktionen aktiviert:  
  
-   Schnelleres Multisubnetz-Failover auf einen Multisubnetzlistener für eine Always On-Verfügbarkeitsgruppe oder Failoverclusterinstanzen.  
  
-   Schnelleres Einzelsubnetz-Failover auf einen Einzelsubnetzlistener für eine Always On-Verfügbarkeitsgruppe oder Failoverclusterinstanzen.  
  
    -   Diese Funktion wird für Verbindungen mit einem Listener verwendet, der über eine einzelne IP in einem einzelnen Subnetz verfügt. Dadurch werden TCP-Verbindungsversuche aggressiver wiederholt, um Failovervorgänge einzelner Subnetze zu beschleunigen.  
  
-   Auflösung benannter Instanzen in eine Multisubnetz-Always On-Failoverclusterinstanz.  
  
    -   Wird verwendet, um die Auflösung benannter Instanzen für Always On-Failoverclusterinstanzen mit mehreren Subnetzendpunkten zu unterstützen.  
  
 **"MultiSubnetFailover=True" wird von NET Framework 3.5 oder OLE DB nicht unterstützt.**  
  
 **Problem:** Wenn die Verfügbarkeitsgruppe oder Failoverclusterinstanz über einen Listenernamen (wird im WSFC-Cluster-Manager als Netzwerkname oder Clientzugriffspunkt bezeichnet) verfügt, der von mehreren IP-Adressen aus unterschiedlichen Subnetzen abhängig ist, und Sie entweder ADO.NET mit .NET Framework 3.5 SP1 oder SQL Native Client 11.0 OLE DB verwenden, tritt bei bis zu 50 % der Clientverbindungsanforderungen an den Listener der Verfügbarkeitsgruppe ein Verbindungstimeout auf.  
  
 **Problemumgehungen:** Eine der folgenden Lösungen wird empfohlen.  
  
-   Wenn Sie nicht über die Berechtigung zur Bearbeitung von Clusterressourcen verfügen, ändern Sie den Wert für das Verbindungstimeout in 30 Sekunden (20-sekündiger TCP-Timeoutzeitraum plus Puffer von 10 Sekunden).  
  
     **Vorteile:**Beim Eintreten eines subnetzübergreifenden Failovers ist die Clientwiederherstellungszeit nur kurz.  
  
     **Nachteile:**Für die Hälfte der Clientverbindungen sind mehr als 20 Sekunden erforderlich.  
  
-   Wenn Sie über die notwendigen Berechtigungen zum Bearbeiten der Clusterressourcen verfügen, sollten Sie den Netzwerknamen des Verfügbarkeitsgruppenlisteners auf `RegisterAllProvidersIP=0`festlegen. Weitere Informationen finden Sie weiter unten in diesem Abschnitt unter "Einstellung RegisterAllProvidersIP".  
  
     **Vorteile:** Sie müssen den Clientverbindungs-Timeoutwert nicht erhöhen.  
  
     **Nachteile:** Beim Auftreten eines subnetzübergreifenden Failovers kann die Clientwiederherstellungszeit 15 Minuten oder länger betragen, je nach **HostRecordTTL** -Einstellung bzw. der Einstellung Ihres siteübergreifenden DNS/AD-Replikationszeitplans.  
  
###  <a name="RegisterAllProvidersIP"></a> Einstellung RegisterAllProvidersIP  
 Bei der Erstellung eines Verfügbarkeitsgruppenlisteners über [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder PowerShell, wird der Client Access Point in WSFC mit Festlegung der Eigenschaft **RegisterAllProvidersIP** auf 1 (TRUE) erstellt. Der Effekt dieses Eigenschaftswerts hängt gemäß den folgenden Angaben von der Clientverbindungszeichenfolge ab:  
  
-   Verbindungszeichenfolgen, die **MultiSubnetFailover** auf „true“ festlegen  
  
     [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] legt die  **RegisterAllProvidersIP** -Eigenschaft auf 1 fest, um die Wiederverbindungszeit nach einem Failover für Clients zu reduzieren, deren Verbindungszeichenfolgen wie empfohlen `MultiSubnetFailover = True`angeben. Beachten Sie, dass Ihre Clients zur Verwendung der Multisubnetzfunktion des Listeners möglicherweise einen Datenanbieter, der das **MultiSubnetFailover** -Schlüsselwort unterstützt, benötigen. Weitere Informationen zur Treiberunterstützung für Multisubnetzfailover finden Sie unter [Always On-Clientkonnektivität (SQL Server)](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
     Informationen zu Multisubnetzclustering finden Sie unter [SQL Server-Multisubnetzclustering &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)verwendet.  
  
    > [!TIP]  
    >  Ist `RegisterAllProvidersIP = 1`, wird beim Ausführen des WSFC-Konfigurationsüberprüfungs-Assistenten im WSFC-Cluster die folgende Warnmeldung generiert:  
    >   
    >  „Die RegisterAllProviderIP-Eigenschaft für Netzwerkname 'Name:&lt;Netzwerkname' ist auf 1 festgelegt. Für die aktuelle Clusterkonfiguration muss dieser Wert auf 0 festgelegt werden.“  
    >   
    >  Ignorieren Sie diese Meldung.  
  
-   Verbindungszeichenfolgen, die **MultiSubnetFailover** auf „true“ festlegen  
  
     Bei `RegisterAllProvidersIP = 1`treten bei Clients, deren Verbindungszeichenfolgen nicht `MultiSubnetFailover = True`verwenden, Verbindungen mit hoher Latenzzeit auf. Dies liegt daran, dass diese Clients versuchen, sequenziell Verbindungen zu allen IPs herzustellen. Wird dagegen **RegisterAllProvidersIP** in 0 geändert, wird die aktive IP-Adresse im Clientzugriffspunkt im WSFC-Cluster registriert und so die Latenzzeit für Legacyclients reduziert. Es empfiehlt sich daher, **RegisterAllProvidersIP** auf „0“ zu ändern, wenn Sie Legacyclients haben, die eine Verbindung zu einem Verfügbarkeitsgruppenlistener herstellen müssen und die **MultiSubnetFailover** -Eigenschaft nicht verwenden können.  
  
    > [!IMPORTANT]  
    >  Wenn Sie über den WSFC-Cluster (Failovercluster-Manager-GUI) einen Verfügbarkeitsgruppenlistener erstellen, ist **RegisterAllProvidersIP** standardmäßig 0 (FALSE).  
  
###  <a name="HostRecordTTL"></a> Einstellung HostRecordTTL  
 Standardmäßig werden von Clients DNS-Clustereinträge 20 Minuten zwischengespeichert.  Durch das Reduzieren von **HostRecordTTL**, d.h. der Gültigkeitsdauer (Time to Live, TTL) für den zwischengespeicherten Eintrag, können Legacyclients schneller wieder Verbindungen herstellen.  Durch das Reduzieren von **HostRecordTTL** kann jedoch auch ein stärkerer Datenverkehr zu den DN-Servern bewirkt werden.  
  
###  <a name="SampleScript"></a> Beispiel-PowerShell-Skript zur Deaktivierung von RegisterAllProvidersIP und zur Reduzierung der Gültigkeitsdauer (TTL)  
 Im folgenden PowerShell-Beispiel wird veranschaulicht, wie der **RegisterAllProvidersIP** -Clusterparameter und der **HostRecordTTL** -Clusterparameter für die Listenerressource konfiguriert werden.  Der DNS-Eintrag wird statt der standardmäßigen 20 Minuten nur 5 Minuten zwischengespeichert.  Durch das Ändern beider Clusterparameter kann die Zeit zum Herstellen der Verbindung mit der richtigen IP-Adresse nach einem Failover für Legacyclients, die den **MultiSubnetFailover** -Parameter nicht verwenden können, reduziert werden.  Ersetzen Sie `yourListenerName` durch den Namen des Listeners, den Sie ändern.  
  
```  
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName | Set-ClusterParameter RegisterAllProvidersIP 0   
Get-ClusterResource yourListenerName|Set-ClusterParameter HostRecordTTL 300  
Stop-ClusterResource yourListenerName  
Start-ClusterResource yourListenerName  
```  
  
 Weitere Informationen zu Wiederherstellungszeiten während des Failovers finden Sie unter [Client Recovery Latency During Failover](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md#DNS).  
  
###  <a name="FollowUpRecommendations"></a> Empfehlungen für anschließende Aufgaben  
 Nach dem Erstellen eines Verfügbarkeitsgruppenlisteners:  
  
-   Bitten Sie den Netzwerkadministrator, die IP-Adresse des Listeners zur exklusiven Verwendung zu reservieren.  
  
-   Geben Sie den DNS-Hostnamen des Listeners an Anwendungsentwickler weiter, damit diese den Namen in Verbindungszeichenfolgen zum Anfordern von Clientverbindungen mit dieser Verfügbarkeitsgruppe verwenden.  
  
-   Ermutigen Sie Entwickler, Clientverbindungszeichenfolgen wenn möglich auf `MultiSubnetFailover = True` zu aktualisieren. Weitere Informationen zur Treiberunterstützung für Multisubnetzfailover finden Sie unter [Always On-Clientkonnektivität (SQL Server)](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
###  <a name="CreateAdditionalListener"></a> Erstellen eines zusätzlichen Listeners für eine Verfügbarkeitsgruppe (optional)  
 Nachdem Sie mit SQL Server einen Listener erstellt haben, können Sie wie folgt einen zusätzlichen Listener hinzufügen:  
  
1.  Erstellen Sie den Listener mit einem der folgenden Tools:  
  
    -   **WSFC Failovercluster-Manager:**  
  
        1.  Fügen Sie einen Clientzugriffspunkt hinzu, und konfigurieren Sie die IP-Adresse.  
  
        2.  Schalten Sie den Listener online.  
  
        3.  Fügen Sie der WSCF-Verfügbarkeitsgruppenressource eine Abhängigkeit hinzu.  
  
         Informationen zu den Dialogfeldern und Registerkarten im Failovercluster-Manager finden Sie unter [Benutzeroberfläche: Failovercluster-Manager (Snap-In)](http://technet.microsoft.com/library/cc772502.aspx).  
  
    -   **Windows PowerShell für Failovercluster:**  
  
        1.  Verwenden Sie [Add-ClusterResource](http://technet.microsoft.com/library/ee460983.aspx) , um einen Netzwerknamen und die IP-Adressressourcen zu erstellen.  
  
        2.  Verwenden Sie [Start-ClusterResource](http://technet.microsoft.com/library/ee461056.aspx) , um die Netzwerknamenressource zu starten.  
  
        3.  Verwenden Sie [Add-ClusterResourceDependency](http://technet.microsoft.com/library/ee461014.aspx) , um die Abhängigkeit zwischen dem Netzwerknamen und der vorhandenen SQL Server-Verfügbarkeitsgruppenressource festzulegen.  
  
         Informationen zur Verwendung von Windows PowerShell für Failovercluster finden Sie unter [Übersicht über Server-Manager-Befehle](http://technet.microsoft.com/library/cc732757.aspx#BKMK_wps).  
  
2.  Starten Sie in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] das Lauschen am neuen Listener. Stellen Sie nach dem Erstellen des zusätzlichen Listeners eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] her, die das primäre Replikat der Verfügbarkeitsgruppe hostet, und ändern Sie den Listenerport mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder PowerShell.  
  
 Weitere Informationen finden Sie unter [How to create multiple listeners for same availability group](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/how-to-create-multiple-listeners-for-same-availability-group-goden-yao/) (So werden mehrere Listener für die gleiche Verfügbarkeitsgruppe erstellt, SQL Server Always On-Teamblog).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Anzeigen von Eigenschaften des Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Entfernen eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [How to create multiple listeners for same availability group](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/how-to-create-multiple-listeners-for-same-availability-group-goden-yao/)  
  
-   [SQL Server Always On-Teamblog: Der offizielle SQL Server Always On-Teamblog](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [SQL Server-Multisubnetzclustering &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)  
  
  
