---
title: "Listener, Clientkonnektivität, Anwendungsfailover | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: a7e5ed2cc2df42469baf3b28e36e6c1444d892a9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="listeners-client-connectivity-application-failover"></a>Listener, Clientkonnektivität, Anwendungsfailover
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Dieses Thema enthält Informationen zu Überlegungen hinsichtlich [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Clientkonnektivität und Anwendungsfailoverfunktionalität.  
  
> [!NOTE]  
>  Für den Großteil der allgemeinen Listenerkonfigurationen können Sie einfach den ersten Verfügbarkeitsgruppenlistener mit [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Anweisungen oder PowerShell-Cmdlets erstellen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Verwandte Aufgaben](#RelatedTasks).  
  
 **In diesem Thema:**  
  
-   [Verfügbarkeitsgruppenlistener](#AGlisteners)  
  
-   [Verwenden eines Listeners zum Herstellen einer Verbindung mit dem primären Replikat](#ConnectToPrimary)  
  
-   [Verwenden eines Listeners zum Herstellen einer Verbindung mit einem schreibgeschützten sekundären Replikat (schreibgeschütztes Routing)](#ConnectToSecondary)  
  
    -   [So konfigurieren Sie Verfügbarkeitsreplikate für das schreibgeschützte Routing](#ConfigureARsForROR)  
  
    -   [Schreibgeschützte Anwendungsabsicht und schreibgeschütztes Routing](#ReadOnlyAppIntent)  
  
-   [Umgehen von Verfügbarkeitsgruppenlistenern](#BypassAGl)  
  
-   [Verhalten von Clientverbindungen beim Failover](#CCBehaviorOnFailover)  
  
-   [Unterstützen von Multisubnetz-Failovern für Verfügbarkeitsgruppen](#SupportAgMultiSubnetFailover)  
  
-   [Verfügbarkeitsgruppenlistener und SSL-Zertifikate](#SSLcertificates)  
  
-   [Verfügbarkeitsgruppenlistener und Serverprinzipalnamen (SPNs)](#SPNs)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
-   [Verwandte Inhalte](#RelatedContent)  
  
##  <a name="AGlisteners"></a> Verfügbarkeitsgruppenlistener  
 Sie können Clientkonnektivität für die Datenbank einer angegebenen Verfügbarkeitsgruppe bereitstellen, indem Sie einen Verfügbarkeitsgruppenlistener erstellen. Ein Verfügbarkeitsgruppenlistener ist der Name eines virtuellen Netzwerks (Virtual Network Name, VNN), mit dem Clients eine Verbindung herstellen können, um auf eine Datenbank in einem primären oder sekundären Replikat einer AlwaysOn-Verfügbarkeitsgruppe zuzugreifen. Ein Verfügbarkeitsgruppenlistener ermöglicht es einem Client, eine Verbindung mit einem Verfügbarkeitsreplikat herzustellen, ohne dass der Name der physischen Instanz von SQL Server, mit der der Client eine Verbindung herstellt, bekannt ist.  Die Clientverbindungszeichenfolge muss nicht geändert werden, damit eine Verbindung mit dem aktuellen Ort des aktuellen primären Replikats hergestellt werden kann.  
  
 Ein Verfügbarkeitsgruppenlistener besteht aus einem DNS (Domain Name System)-Listenernamen, einer Listenerportbezeichnung und mindestens einer IP-Adresse. Nur das TCP-Protokoll wird von Verfügbarkeitsgruppenlistenern unterstützt.  Der DNS-Name des Listeners muss auch in der Domäne und NetBIOS eindeutig sein.  Wenn Sie einen neuen Verfügbarkeitsgruppenlistener erstellen, wird er zu einer Ressource in einem Cluster mit einem zugeordneten virtuellen Netzwerknamen (VNN), einer virtuellen IP (VIP) und Verfügbarkeitsgruppenabhängigkeit. Ein Client verwendet DNS, um den VNN in mehrere IP-Adressen aufzulösen, und versucht dann, eine Verbindung mit jeder einzelnen Adresse herzustellen, bis eine Verbindungsanforderung erfolgreich ist oder ein Timeout eintritt.  
  
 Wenn für mindestens ein [lesbares sekundäres Replikat](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) das schreibgeschützte Routing konfiguriert ist, werden Clientverbindungen für beabsichtigte Lesevorgänge auf dem primären Replikat an ein lesbares sekundäres Replikat umgeleitet. Auch wenn das primäre Replikat auf einer Instanz von SQL Server offline geschaltet wird und auf einer anderen Instanz von SQL Server ein neues primäres Replikat online geschaltet wird, ermöglicht der Verfügbarkeitsgruppenlistener Clients Verbindungen mit dem neuen primären Replikat.  
  
 Wichtige Informationen zu Verfügbarkeitsgruppenlistenern finden Sie unter [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
 **In diesem Abschnitt:**  
  
-   [Konfiguration des Verfügbarkeitsgruppenlisteners](#AGlConfig)  
  
-   [Auswählen eines Ports für Verfügbarkeitsgruppenlistener](#SelectListenerPort)  
  
###  <a name="AGlConfig"></a> Konfiguration des Verfügbarkeitsgruppenlisteners  
 Ein Verfügbarkeitsgruppenlistener wird definiert, indem Folgendes angegeben wird:  
  
 Eindeutiger DNS-Name  
 Dieser wird auch als virtueller Netzwerkname (Virtual Network Name, VNN) bezeichnet. Es gelten die Active Directory-Benennungsregeln für DNS-Hostnamen. Weitere Informationen finden Sie im KB-Artikel [Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten](http://support.microsoft.com/kb/909264) .  
  
 Mindestens eine virtuelle IP-Adresse (Virtual IP address, VIP)  
 VIPs werden für mindestens ein Subnetz konfiguriert, in dem ein Failover der Verfügbarkeitsgruppe erfolgen kann.  
  
 IP-Adresskonfiguration  
 Für einen gegebenen Listener der Verfügbarkeitsgruppe verwendet die IP-Adresse entweder das Dynamic Host Configuration Protocol (DHCP) oder mindestens eine statische IP-Adresse.  
  
-   Dynamic Host Configuration Protocol (DHCP)  
  
     Wenn sich eine Verfügbarkeitsgruppe in einem einzelnen Subnetz befindet, können Sie alle IP-Adressen der Verfügbarkeitsgruppenlistener konfigurieren, um das DHCP zu verwenden. Für Vorproduktionsumgebungen bietet DHCP ein einfaches Setup für eine Verfügbarkeitsgruppe, für die keine Notfallwiederherstellung an einem Remotestandort in einem separaten Subnetz erforderlich ist. Dennoch sollte DHCP nicht in Verbindung mit einem Verfügbarkeitsgruppenlistener in einer Produktionsumgebung verwendet werden. Wenn es zu einer Ausfallzeit kommt und das DHCP-IP-Leasing abläuft, ist für die erneute Registrierung der dem DNS-Listenernamen zugeordneten neuen DHCP-IP-Adresse zusätzlich Zeit erforderlich. Dies führt zu einem Ausfall der Clientverbindung.  
  
-   Statische IP-Adressen  
  
     In Produktionsumgebungen wird empfohlen, dass Verfügbarkeitsgruppenlistener statische IP-Adressen verwenden. Wenn sich die Verfügbarkeitsgruppen jedoch in Subnetzen einer Domäne mit mehreren Subnetzen befinden, muss ein Verfügbarkeitsgruppenlistener statische IP-Adressen verwenden.  
  
 Hybride Netzwerkkonfigurationen und DHCP in mehreren Subnetzen werden nicht für Verfügbarkeitsgruppenlistener unterstützt. Das liegt daran, dass im Fall eines Failovers eine dynamische IP abgelaufen sein könnte oder freigegeben wird, wodurch die hohe Verfügbarkeit insgesamt gefährdet wird.  
  
###  <a name="SelectListenerPort"></a> Auswählen eines Ports für Verfügbarkeitsgruppenlistener  
 Wenn Sie einen Verfügbarkeitsgruppenlistener konfigurieren, müssen Sie einen Port festlegen.  Sie können den Standardport auf 1433 konfigurieren, um Clientverbindungszeichenfolgen einfach zu gestalten. Wenn Sie 1433 verwenden, müssen Sie keine Portnummer in einer Verbindungszeichenfolge festlegen.   Da jeder Verfügbarkeitsgruppenlistener einen separaten virtuellen Netzwerknamen besitzt, kann außerdem jeder für einen WSFC-Cluster konfigurierte Verfügbarkeitsgruppenlistener für den Verweis auf Port 1433 konfiguriert werden.  
  
 Sie können auch einen nicht standardmäßigen Listenerport festlegen. Dies bedeutet jedoch, dass Sie auch in der Verbindungszeichenfolge immer dann explizit einen Zielport angeben müssen, wenn Sie eine Verbindung mit dem Verfügbarkeitsgruppenlistener herstellen.  Darüber hinaus müssen Sie die Berechtigung für die Firewall für den nicht standardmäßigen Port öffnen.  
  
 Wenn Sie den Standardport 1433 für die virtuellen Netzwerknamen der Verfügbarkeitsgruppenlistener verwenden, müssen Sie dennoch sicherstellen, dass keine anderen Dienste im Clusterknoten diesen Port verwenden. Andernfalls tritt ein Portkonflikt auf.  
  
 Wenn eine der Instanzen von SQL Server bereits über den Instanzlistener TCP-Port 1433 überwacht und keine anderen Dienste (einschließlich weitere Instanzen von SQL Server) auf dem Computer Port 1433 überwachen, wird kein Portkonflikt mit dem Verfügbarkeitsgruppenlistener verursacht.  Das liegt daran, dass der Verfügbarkeitsgruppenlistener den selben TCP-Port im gleichen Dienstprozess freigeben kann.  Mehrere Instanzen von SQL Server (parallel) sollten jedoch nicht für die Überwachung desselben Ports konfiguriert werden.  
  
##  <a name="ConnectToPrimary"></a> Verwenden eines Listeners zum Herstellen einer Verbindung mit dem primären Replikat  
 Um mithilfe eines Verfügbarkeitsgruppenlisteners eine Verbindung mit dem primären Replikat für Lese-/Schreibzugriff herzustellen, gibt die Verbindungszeichenfolge den DNS-Namen des Verfügbarkeitsgruppenlisteners an.  Wenn ein Verfügbarkeitsgruppenreplikat zu einem neuen Replikat wird, werden vorhandene Verbindungen, für die der Netzwerkname eines Verfügbarkeitslisteners verwendet wird, unterbrochen.  Neue Verbindungen zum Verfügbarkeitsgruppenlistener werden dann an das neue primäre Replikat weitergeleitet. Beispiel für eine einfache Verbindungszeichenfolge für den ADO.NET-Anbieter (System.Data.SqlClient):  
  
```  
Server=tcp: AGListener,1433;Database=MyDB;IntegratedSecurity=SSPI  
```  
  
 Sie können dennoch direkt auf die Instanz des SQL Server-Namens der primären oder sekundären Replikate verweisen, anstatt den Servernamen des Verfügbarkeitsgruppenlisteners zu verwenden. In diesem Fall werden neue Verbindungen jedoch nicht automatisch zum aktuellen primären Replikat weitergeleitet.  Schreibgeschütztes Routing geht ebenfalls verloren.  
  
##  <a name="ConnectToSecondary"></a> Verwenden eines Listeners zum Herstellen einer Verbindung mit einem schreibgeschützten sekundären Replikat (schreibgeschütztes Routing)  
 *Schreibgeschütztes Routing* bezieht sich auf die Möglichkeit von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , eingehende Verbindungen für einen Verfügbarkeitsgruppenlistener an ein sekundäres Replikat weiterzuleiten, das für schreibgeschützte Arbeitslasten konfiguriert ist. Eine eingehende Verbindung, die auf den Namen eines Verfügbarkeitsgruppenlisteners verweist, kann automatisch an ein schreibgeschütztes Replikat weitergeleitet werden, wenn Folgendes zutrifft:  
  
-   Mindestens ein sekundäres Replikat wird auf schreibgeschützten Zugriff festgelegt, und jedes schreibgeschützte sekundäre Replikat sowie das primäre Replikat werden konfiguriert, um schreibgeschütztes Routing zu unterstützen. Weitere Informationen finden Sie weiter unten in diesem Abschnitt unter [So konfigurieren Sie Verfügbarkeitsreplikate für das schreibgeschützte Routing](#ConfigureARsForROR).  

-   Die Verbindungszeichenfolge verweist auf eine Datenbank innerhalb der Verfügbarkeitsgruppe. Eine Alternative dazu ist es, für den Anmeldenamen, der für die Verbindung verwendet wird, die Datenbank als Standarddatenbank zu konfigurieren. Weitere Informationen dazu finden Sie in [diesem Blogbeitrag zur Funktionsweise des Algorithmus mit dem schreibgeschützten Routing](https://blogs.msdn.microsoft.com/mattn/2012/04/25/calculating-read_only_routing_url-for-alwayson/) (in englischer Sprache).

-   Die Verbindungszeichenfolge verweist auf einen Verfügbarkeitsgruppenlistener, und die Anwendungsabsicht der eingehenden Verbindung wird auf schreibgeschützt festgelegt, z. B. mithilfe des Schlüsselworts **Application Intent=ReadOnly** in den ODBC- oder OLEBD-Verbindungszeichenfolgen, -Verbindungsattributen oder -Eigenschaften. Weitere Informationen finden Sie weiter unten in diesem Abschnitt unter [Schreibgeschützte Anwendungsabsicht und schreibgeschütztes Routing](#ReadOnlyAppIntent).  
  
###  <a name="ConfigureARsForROR"></a> So konfigurieren Sie Verfügbarkeitsreplikate für das schreibgeschützte Routing  
 Ein Datenbankadministrator muss die Verfügbarkeitsreplikate wie folgt konfigurieren:  
  
1.  Für jedes Verfügbarkeitsreplikat, das Sie als lesbares sekundäres Replikat konfigurieren möchten, muss ein Datenbankadministrator die folgenden Einstellungen konfigurieren, die nur unter der sekundären Rolle wirksam werden:  
  
    -   Der Verbindungszugriff muss auf "alles" oder "schreibgeschützt" festgelegt werden.  
  
    -   Die URL für das schreibgeschützte Routing muss angegeben werden.  
  
2.  Für jede dieser Replikate muss eine schreibgeschützte Routingliste für die primäre Rolle angegeben werden. Geben Sie einen oder mehrere Servernamen als Routingziele an.  
  
####  <a name="RelatedTasksROR"></a> Verwandte Aufgaben  
  
-   [Konfigurieren des schreibgeschützten Zugriffs auf ein Verfügbarkeitsreplikat &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
###  <a name="ReadOnlyAppIntent"></a> Schreibgeschützte Anwendungsabsicht und schreibgeschütztes Routing  
 Die Eigenschaft der Verbindungszeichenfolge für die Anwendungsabsicht gibt an, dass die Anforderung der Clientanwendung direkt an die Version mit Lese-/Schreibzugriff oder die schreibgeschützte Version einer Verfügbarkeitsgruppendatenbank weitergeleitet wird. Zum Verwenden des schreibgeschützten Routings muss ein Client beim Herstellen einer Verbindung mit dem Verfügbarkeitsgruppenlistener eine schreibgeschützte Anwendungsabsicht in der Verbindungszeichenfolge verwenden. Ohne die schreibgeschützte Anwendungsabsicht werden Verbindungen zum Verfügbarkeitsgruppenlistener zur Datenbank weitergeleitet, die sich auf dem primären Replikat befindet.  
  
 Das Attribut der Anwendungsabsicht wird während der Anmeldung in der Clientsitzung gespeichert. Die Instanz von SQL Server verarbeitet dann diese Absicht und ermittelt das weitere Vorgehen entsprechend der Konfiguration der Verfügbarkeitsgruppe und dem aktuellen Lese-/Schreibstatus der Zieldatenbank im sekundären Replikat.  
  
 Beispiel für eine Verbindungszeichenfolge für den ADO.NET-Anbieter (System.Data.SqlClient) mit Festlegung einer schreibgeschützten Anwendungsabsicht:  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly  
```  
  
 In diesem Beispiel für eine Verbindungszeichenfolge versucht der Client, über den Verfügbarkeitsgruppenlistener `AGListener` an Port 1433 eine Verbindung mit der AdventureWorks-Datenbank herzustellen (Sie können den Port auch weglassen, wenn der Verfügbarkeitsgruppenlistener an Port 1433 lauscht).  In der Verbindungszeichenfolge wurde die Eigenschaft **ApplicationIntent** auf **ReadOnly**festgelegt, was diese zu einer *Verbindungszeichenfolge für beabsichtige Lesevorgänge*macht.  Ohne diese Einstellung hätte der Server kein schreibgeschütztes Routing der Verbindung versucht.  
  
 Die primäre Datenbank der Verfügbarkeitsgruppe verarbeitet die eingehende Anforderung für schreibgeschütztes Routing und versucht, ein schreibgeschütztes Online-Replikat zu suchen, das mit dem primären Replikat verknüpft und für schreibgeschütztes Routing konfiguriert ist.  Der Client empfängt Verbindungsinformationen vom primären Replikatserver und stellt eine Verbindung mit dem ermittelten schreibgeschützten Replikat her.  
  
 Hinweis: Die Anwendungsabsicht kann von einem Clienttreiber an eine Downlevelinstanz von SQL Server gesendet werden.  In diesem Fall wird die schreibgeschützte Anwendungsabsicht ignoriert, und die Verbindung bleibt normal bestehen.  
  
 Sie können schreibgeschütztes Routing umgehen, indem Sie die Verbindungseigenschaft der Anwendungsabsicht nicht auf **ReadOnly** festlegen (bei keiner Angabe während der Anmeldung lautet der Standard **ReadWrite** ), oder indem Sie direkt eine Verbindung mit der primären Replikatinstanz von SQL- Server herstellen, statt den Namen des Verfügbarkeitsgruppenlisteners zu verwenden.  Schreibgeschütztes Routing erfolgt auch dann nicht, wenn Sie eine direkte Verbindung mit einem schreibgeschützten Replikat herstellen.  
  
####  <a name="RelatedTasksApps"></a> Verwandte Aufgaben  
  
-   [SQL Server Native Client-Unterstützung für hohe Verfügbarkeit, Notfallwiederherstellung](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="BypassAGl"></a> Umgehen von Verfügbarkeitsgruppenlistenern  
 Während Verfügbarkeitsgruppenlistener Unterstützung für Failoverumleitung und schreibgeschütztes Routing ermöglichen, müssen Clientverbindungen diese nicht verwenden. Eine Clientverbindung kann auch direkt auf die Instanz von SQL Server verweisen, statt eine Verbindung mit dem Verfügbarkeitsgruppenlistener herzustellen.  
  
 Es besteht kein Unterschied zur Instanz von SQL Server, unabhängig davon, ob die Verbindung mithilfe des Verfügbarkeitslisteners oder mithilfe eines anderen Instanzendpunkts angemeldet wird.  Die Instanz von SQL Server überprüft den Status der Zieldatenbank und ermöglicht oder verweigert die Konnektivität basierend auf der Konfiguration der Verfügbarkeitsgruppe und dem aktuellen Status der Datenbank auf der Instanz.  Wenn z. B. eine Clientanwendung direkt eine Verbindung mit einer Instanz des SQL Server-Ports herstellt und eine Verbindung mit einer in einer Verfügbarkeitsgruppe gehosteten Zieldatenbank herstellt und die Zieldatenbank sich im primären Status befindet und online geschaltet ist, ist die Konnektivität erfolgreich.  Ist die Zieldatenbank offline oder in einem Übergangsstatus, schlägt die Konnektivität zur Datenbank fehl.  
  
 Alternativ können Anwendungen beim Migrieren von der Datenbankspiegelung zu [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]die Verbindungszeichenfolge für die Datenbankspiegelung angeben, sofern nur ein sekundäres Replikat vorhanden ist und Benutzerverbindungen unzulässig sind. Weitere Informationen finden Sie weiter unten in diesem Abschnitt unter [Verwenden von Verbindungszeichenfolgen für die Datenbankspiegelung mit Verfügbarkeitsgruppen](#DbmConnectionString).  
  
###  <a name="DbmConnectionString"></a> Verwenden von Verbindungszeichenfolgen für die Datenbankspiegelung mit Verfügbarkeitsgruppen  
 Wenn eine Verfügbarkeitsgruppe nur ein sekundäres Replikat besitzt und mit ALLOW_CONNECTIONS = READ_ONLY oder ALLOW_CONNECTIONS = NONE für das sekundäre Replikat konfiguriert wird, können Clients mithilfe einer Verbindungszeichenfolge für die Datenbankspiegelung eine Verbindung mit dem primären Replikat herstellen. Dieser Ansatz kann beim Migrieren einer vorhandenen Anwendung von der Datenbankspiegelung zu einer Verfügbarkeitsgruppe nützlich sein, sofern Sie die Verfügbarkeitsgruppe auf zwei Verfügbarkeitsreplikate (ein primäres und ein sekundäres Replikat) beschränken. Wenn Sie zusätzliche sekundäre Replikate hinzufügen, müssen Sie einen Verfügbarkeitsgruppenlistener für die Verfügbarkeitsgruppe erstellen und die Anwendungen aktualisieren, damit der DNS-Name des Verfügbarkeitsgruppenlisteners verwendet wird.  
  
 Wenn Sie die Verbindungszeichenfolgen der Datenbankspiegelung verwenden, kann der Client entweder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oder .NET Framework-Datenanbieter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verwenden. Die von einem Client bereitgestellte Verbindungszeichenfolge muss mindestens den Namen einer Serverinstanz, den *ursprünglichen Partnernamen*, angeben, um die Serverinstanz zu identifizieren, auf der das Verfügbarkeitsreplikat, zu dem Sie eine Verbindung herstellen möchten, ursprünglich gehostet wird. Optional kann die Verbindungszeichenfolge auch den Namen einer anderen Serverinstanz, den *Failoverpartnernamen*, enthalten, um die Serverinstanz zu identifizieren, auf der das sekundäre Replikat ursprünglich gehostet wird.  
  
 Weitere Informationen zu Verbindungszeichenfolgen für die Datenbankspiegelung finden Sie unter [Verbinden von Clients mit einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
##  <a name="CCBehaviorOnFailover"></a> Verhalten von Clientverbindungen beim Failover  
 Wenn ein Verfügbarkeitsgruppenfailover auftritt, werden vorhandene persistente Verbindungen zur Verfügbarkeitsgruppe beendet. Der Client muss eine neue Verbindung herstellen, um weiterhin dieselbe primäre Datenbank oder schreibgeschützte sekundäre Datenbank zu verwenden.  Während eines Failovers auf der Serverseite tritt bei der Verbindung zur Verfügbarkeitsgruppe möglicherweise ein Fehler auf, und die Clientanwendung wird gezwungen, erneut eine Verbindung herzustellen, bis die primäre Datenbank wieder vollständig online geschaltet ist.  
  
 Wenn die Verfügbarkeitsgruppe während des Verbindungsversuchs einer Clientanwendung, jedoch vor dem Verbindungstimeout online geschaltet wird, stellt der Clienttreiber möglicherweise während einer der internen Wiederholungsversuche erfolgreich eine Verbindung her. In diesem Fall wird kein Fehler an die Anwendung ausgegeben.  
  
##  <a name="SupportAgMultiSubnetFailover"></a> Unterstützen von Multisubnetz-Failovern für Verfügbarkeitsgruppen  
 Wenn Sie Clientbibliotheken verwenden, die die MultiSubnetFailover-Verbindungsoption in der Verbindungszeichenfolge unterstützen, können Sie das Verfügbarkeitsgruppenfailover auf ein anderes Subnetz optimieren, indem Sie MultiSubnetFailover je nach Syntax des verwendeten Anbieters auf "True" oder "Ja" festlegen.  
  
> [!NOTE]  
>  Diese Einstellung wird für Verbindungen mit einem Subnetz und mehreren Subnetzen mit den Namen von Verfügbarkeitslistenern und SQL Server-Failoverclusterinstanzen empfohlen.  Wenn Sie diese Option aktivieren, stehen auch für Szenarien mit einem Subnetz weitere Optimierungen zur Verfügung.  
  
 Die **MultiSubnetFailover** -Verbindungsoption funktioniert nur mit dem TCP-Netzwerkprotokoll und wird nur beim Herstellen einer Verbindung mit einem Verfügbarkeitsgruppenlistener und für beliebige virtuelle Netzwerknamen unterstützt, die eine Verbindung mit [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]herstellen.  
  
 Beispiel für eine Verbindungszeichenfolge des ADO.NET-Anbieters (System.Data.SqlClient) mit aktiviertem Multisubnetzfailover:  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI; MultiSubnetFailover=True  
```  
  
 Die **MultiSubnetFailover** -Verbindungsoption sollte auf **True** festgelegt werden, auch wenn die Verfügbarkeitsgruppe nur ein einzelnes Subnetz umfasst.  Dies ermöglicht es Ihnen, neue Clients vorzukonfigurieren, um künftig weitere Subnetze zu unterstützen, ohne dass die Clientverbindungszeichenfolgen geändert werden müssen. Darüber hinaus wird die Failoverleistung für Failover in einem Subnetz optimiert.  Die **MultiSubnetFailover** -Verbindungsoption ist zwar nicht erforderlich, bietet jedoch den Vorteil eines schnelleren Subnetzfailovers.  Das liegt daran, dass der Clienttreiber versucht, parallel ein TCP-Socket für alle der Verfügbarkeitsgruppe zugeordneten IP-Adressen zu öffnen.  Der Clienttreiber wartet, bis die erste IP erfolgreich antwortet, und verwendet diese dann für die Verbindung.  
  
##  <a name="SSLcertificates"></a> Verfügbarkeitsgruppenlistener und SSL-Zertifikate  
 Wenn beim Herstellen einer Verbindung mit einem Verfügbarkeitsgruppenlistener die beteiligten Instanzen von SQL Server SSL-Zertifikate zusammen mit Sitzungsverschlüsselung verwenden, muss der Clienttreiber den alternativen Antragstellernamen im SSL-Zertifikat unterstützen, um die Verschlüsselung zu erzwingen.  SQL Server-Treiberunterstützung für den alternativen Antragstellernamen des Zertifikats ist für ADO.NET (SqlClient), Microsoft JDBC und SQL Native Client (SNAC) geplant.  
  
 Ein X.509-Zertifikat muss für alle beteiligten Serverknoten im Failovercluster mit einer Liste aller im alternativen Antragstellernamen des Zertifikats festgelegten Verfügbarkeitsgruppenlistenern konfiguriert werden.  
  
 Wenn der WSFC z. B. drei Verfügbarkeitsgruppenlistener mit den Namen `AG1_listener.Adventure-Works.com`, `AG2_listener.Adventure-Works.com`und `AG3_listener.Adventure-Works.com`besitzt, sollte der alternative Antragstellername für das Zertifikat folgendermaßen festgelegt werden:  
  
```  
CN = ServerFQDN  
SAN = ServerFQDN,AG1_listener.Adventure-Works.com, AG2_listener.Adventure-Works.com, AG3_listener.Adventure-Works.com  
```  
  
##  <a name="SPNs"></a> Verfügbarkeitsgruppenlistener und Serverprinzipalnamen (SPNs)  
 Ein Serverprinzipalname (SPN) muss in Active Directory von einem Domänenadministrator für alle Verfügbarkeitsgruppenlistener-Namen konfiguriert werden, um Kerberos für die Clientverbindung mit dem Verfügbarkeitsgruppenlistener zu aktivieren. Bei der Registrierung des Serverprinzipalnamens (SPN) müssen Sie das Dienstkonto derjenigen Serverinstanz verwenden, die das Verfügbarkeitsreplikat hostet.  Damit der SPN in allen Replikaten funktioniert, muss dasselbe Dienstkonto für alle Instanzen im WSFC-Cluster verwendet werden, der die Verfügbarkeitsgruppe hostet.  
  
 Konfigurieren Sie den SPN mithilfe des **setspn** Windows-Befehlszeilentools.  Beispiel für die Konfiguration eines Serverprinzipalnamens für die Verfügbarkeitsgruppe `AG1listener.Adventure-Works.com` , die auf einer Reihe von SQL Server-Instanzen gehostet wird und zur Ausführung unter dem Domänenkonto `corp/svclogin2`konfiguriert ist:  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp/svclogin2  
```  
  
 Weitere Informationen zur manuellen Registrierung eines SPN für SQL Server finden Sie unter [Register a Service Principal Name for Kerberos Connections](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [AlwaysOn-Clientkonnektivität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Anzeigen von Eigenschaften des Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Entfernen eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Zugriffs auf ein Verfügbarkeitsreplikat &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Microsoft SQL Server AlwaysOn-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Einführung in den Verfügbarkeitsgruppenlistener](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/16/introduction-to-the-availability-group-listener/) (SQL Server AlwaysOn-Teamblog)  
  
-   [SQL Server AlwaysOn-Teamblog: Der offizielle SQL Server AlwaysOn-Teamblog](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On-Clientkonnektivität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [Informationen zum Clientverbindungszugriff auf Verfügbarkeitsreplikate &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Aktive sekundäre Replikate: Lesbare sekundäre Replikate (Always On-Verfügbarkeitsgruppen)](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Verbinden von Clients mit einer Datenbank-Spiegelungssitzung (SQL Server)](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  
