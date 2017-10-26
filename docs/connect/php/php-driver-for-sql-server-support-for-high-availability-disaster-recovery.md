---
title: "PHP-Treiber für SQL Server High Availability, Disaster Recovery | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24b65a4c4572638cff243bcf46e49a30453f0550
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="php-driver-for-sql-server-support-for-high-availability-disaster-recovery"></a>PHP-Treiber für SQL Server-Unterstützung für hohe Verfügbarkeit, Notfallwiederherstellung
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Thema wird erläutert, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Support (eingeführt in Version 3.0) für hohe Verfügbarkeit und notfallwiederherstellung [!INCLUDE[ssHADR](../../includes/sshadr_md.md)].  [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]-Support wurde in [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] hinzugefügt. Weitere Informationen über [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]finden Sie in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Onlinedokumentation.  
  
In Version 3.0 von der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], Sie können den verfügbarkeitsgruppenlistener angeben (hohe Verfügbarkeit und Wiederherstellung im Notfall-) verfügbarkeitsgruppe (AG) in der Verbindungseigenschaft. Wenn eine [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Anwendung mit einer AlwaysOn-Datenbank, die beim Failover verbunden ist, die ursprüngliche Verbindung unterbrochen wird und die Anwendung muss eine neue Verbindung, um nach dem Failover weiterzuarbeiten öffnen.  
  
Wenn Sie nicht mit einem Verfügbarkeitsgruppen-Listener herstellen und mehrere IP-Adressen einem Hostnamen zugeordnet sind die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] durchläuft nacheinander alle IP-Adressen, DNS-Eintrag zugeordnet. Dies kann zeitaufwändig sein, wenn die erste vom DNS-Server zurückgegebene IP-Adresse an keine Netzwerkschnittstellenkarte (NIC) gebunden ist. Beim Verbinden mit einem Verfügbarkeitsgruppen-Listener, der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Versuche zum Herstellen von Verbindungen mit allen IP-Adressen Parallel und wenn ein Verbindungsversuch erfolgreich ist, verwirft der Treiber alle ausstehenden Verbindungsversuche.  
  
> [!NOTE]  
> Das Erhöhen des Verbindungstimeouts sowie die Implementierung von Verbindungswiederholungslogik erhöhen die Wahrscheinlichkeit, dass eine Anwendung eine Verbindung zu einer Verfügbarkeitsgruppe herstellt. Da zudem eine Verbindung aufgrund eines Verfügbarkeitsgruppenfailovers fehlschlagen kann, empfiehlt sich die Implementierung von Verbindungswiederholungslogik, wodurch im Fall einer fehlgeschlagenen Verbindung bis zur erneuten Verbindung Wiederholungsversuche erfolgen.  
  
## <a name="connecting-with-multisubnetfailover"></a>Verbinden mit MultiSubnetFailover  
Die **MultiSubnetFailover** -Verbindungseigenschaft gibt an, dass die Anwendung in einer verfügbarkeitsgruppe oder Failoverclusterinstanz und die bereitgestellt wird, wird die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versucht, eine Verbindung mit der Datenbank auf dem primären [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz beim Herstellen der Verbindung mit allen IP-Adressen. Wenn **MultiSubnetFailover = True** ist für eine Verbindung angegeben, der Client TCP-Verbindungsversuche schneller als das Betriebssystem standardmäßig TCP-neuübertragungsintervallen wiederholt. Auf diese Weise kann die Verbindung nach einem Failover einer AlwaysOn-Verfügbarkeitsgruppe oder einer AlwaysOn-Failoverclusterinstanz schneller wiederhergestellt werden. Diese Einstellung gilt sowohl für Einzelsubnetz- als auch Multisubnetz-Verfügbarkeitsgruppen und -Failoverclusterinstanzen.  
  
Geben Sie immer **MultiSubnetFailover = True** beim Verbinden mit einer SQL Server 2012-verfügbarkeitsgruppenlistener oder die SQL Server 2012-Failoverclusterinstanz. **MultiSubnetFailover** aktiviert schnelleres Failover für alle Verfügbarkeitsgruppen und die Failoverclusterinstanz in SQL Server 2012 und reduziert die Failoverzeit für einzelne und Multisubnetz-AlwaysOn-Topologien erheblich. Während eines Multisubnetzfailovers versucht der Client Verbindungen parallel. Während eines subnetzfailovers der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] aggressive Wiederholungsversuche zum Herstellen die TCP-Verbindung.  
  
Weitere Informationen zu Schlüsselwörtern der Verbindungszeichenfolge in [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], finden Sie unter [Verbindungsoptionen](../../connect/php/connection-options.md).  
  
Angeben von **MultiSubnetFailover = True** beim Herstellen einer Verbindung auf einen anderen Wert als einem verfügbarkeitsgruppenlistener oder einer Failover-Clusterinstanz möglicherweise verminderter Leistung und wird nicht unterstützt.  
  
Stellen Sie mithilfe der folgenden Richtlinien eine Verbindung mit einem Server in einer Verfügbarkeitsgruppe her:  
  
-   Verwenden Sie die **MultiSubnetFailover** -Verbindungseigenschaft, wenn Sie eine Verbindung mit einem Einzelsubnetz oder Multisubnetz herstellen. Dadurch wird die Leistung für beide verbessert.  
  
-   Um eine Verbindung mit einer Verfügbarkeitsgruppe herzustellen, geben Sie in der Verbindungszeichenfolge den Verfügbarkeitsgruppenlistener der Verfügbarkeitsgruppe als Server an.  
  
-   Ein Verbindungsversuch mit einer mit mehr als 64 IP-Adressen konfigurierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz verursacht einen Verbindungsfehler.  
  
-   Das Verhalten einer Anwendung, die die **MultiSubnetFailover**-Verbindungseigenschaft verwendet, wird durch den Authentifizierungstyp nicht beeinflusst: [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Authentifizierung, Kerberos-Authentifizierung oder Windows-Authentifizierung.  
  
-   Erhöhen Sie den Wert der **LoginTimeout** für Failoverzeit zu berücksichtigen und Wiederholungsversuche für anwendungsverbindungen zu reduzieren.  
  
-   Verteilte Transaktionen werden nicht unterstützt.  
  
Wenn das schreibgeschützte Routing nicht aktiviert ist, scheitert das Herstellen der Verbindung mit einem sekundären Replikatspeicherort in einer Verfügbarkeitsgruppe in den folgenden Situationen:  
  
1.  Wenn der sekundäre Replikatspeicherort nicht zum Akzeptieren von Verbindungen konfiguriert ist.  
  
2.  Wenn eine Anwendung **ApplicationIntent=ReadWrite** verwendet (weiter unten erläutert), und der sekundäre Replikatspeicherort für schreibgeschützten Zugriff konfiguriert ist.  
  
Es kann keine Verbindung hergestellt werden, wenn ein primäres Replikat so konfiguriert ist, dass schreibgeschützte Arbeitslasten abgelehnt werden, und die Verbindungszeichenfolge **ApplicationIntent=ReadOnly**enthält.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aktualisieren zur Verwendung von Multisubnetzclustern aus Datenbankspiegelung  
Ein Verbindungsfehler tritt auf, wenn die Verbindungsschlüsselwörter **MultiSubnetFailover** und **Failover_Partner** in der Verbindungszeichenfolge vorhanden sind. Es tritt auch ein Fehler auf, wenn **MultiSubnetFailover** verwendet wird und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eine Failoverpartnerantwort zurückgibt, die angibt, dass es Teil eines Datenbankspiegelungspaars ist.  
  
Wenn Sie ein upgrade einer [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Anwendung, die derzeit die datenbankspiegelung zu einem multisubnetz-Szenario verwendet, sollten Sie entfernen die **von Failover_Partner** Verbindungseigenschaft und ersetzen es durch **MultiSubnetFailover ** festgelegt **Ja** , und Ersetzen Sie den Servernamen in der Verbindungszeichenfolge mit einem Verfügbarkeitsgruppen-Listener. Wenn eine Verbindungszeichenfolge verwendet **von Failover_Partner** und **MultiSubnetFailover = True**, generiert der Treiber einen Fehler. Jedoch, wenn eine Verbindungszeichenfolge verwendet **von Failover_Partner** und **MultiSubnetFailover = "false"** (oder **ApplicationIntent = ReadWrite**), die Anwendung wird die Datenbank verwenden die Spiegelung.  
  
Der Treiber einen Fehler zurück, wenn die datenbankspiegelung auf der primären Datenbank in der Verfügbarkeitsgruppe verwendet wird, und wenn **MultiSubnetFailover = True** wird verwendet, in der Verbindungszeichenfolge die Herstellung einer primären Datenbank nicht zu einer verfügbarkeitsgruppe der Listener.  
  
## <a name="specifying-application-intent"></a>Angeben des Anwendungszwecks  
Im Fall von **ApplicationIntent=ReadOnly** fordert der Client eine Lesearbeitslast an, wenn eine Verbindung mit einer AlwaysOn-aktivierten Datenbank hergestellt wird. Der Server erzwingt den Versuch zur Verbindungszeit und während einer USE-Datenbankanweisung, aber nur für eine AlwaysOn-aktivierte Datenbank.  
  
Das Schlüsselwort **ApplicationIntent** funktioniert nicht mit schreibgeschützten Legacy-Datenbanken.  
  
Eine Datenbank kann Lesearbeitslasten auf der AlwaysOn-Zieldatenbank zulassen bzw. nicht zulassen. (Hierzu wird die **ALLOW_CONNECTIONS**Klausel der **PRIMARY_ROLE** und der **SECONDARY_ROLE**[!INCLUDE[tsql](../../includes/tsql_md.md)]-Anweisung verwendet.)  
  
Das **ApplicationIntent** -Schlüsselwort wird verwendet, um schreibgeschütztes Routing zu aktivieren.  
  
## <a name="read-only-routing"></a>Schreibgeschütztes Routing  
Schreibgeschütztes Routing ist eine Funktion, die die Verfügbarkeit eines schreibgeschützten Replikats einer Datenbank sicherstellen kann. So aktivieren Sie schreibgeschütztes Routing:  
  
1.  Sie müssen eine Verbindung zum Verfügbarkeitsgruppenlistener einer AlwaysOn-Verfügbarkeitsgruppe herstellen.  
  
2.  Das Schlüsselwort der **ApplicationIntent** -Verbindungszeichenfolge muss auf **ReadOnly**festgelegt werden.  
  
3.  Die Verfügbarkeitsgruppe muss vom Datenbankadministrator konfiguriert werden, um schreibgeschütztes Routing zu aktivieren.  
  
Möglicherweise werden bei mehreren Verbindungen mithilfe von schreibgeschütztem Routing nicht alle mit demselben schreibgeschützten Replikat verbunden. Änderungen in der Datenbanksynchronisierung oder Änderungen in der Routingkonfiguration des Servers können zu Clientverbindungen mit anderen schreibgeschützten Replikaten führen. Sie gewährleisten, dass alle schreibgeschützten Anforderungen Verbindungen mit demselben schreibgeschützten Replikat herstellen, indem Sie keinen Verfügbarkeitsgruppenlistener an das Schlüsselwort der **Server** -Verbindungszeichenfolge übermitteln. Geben Sie stattdessen den Namen der schreibgeschützten Instanz an.  
  
Schreibgeschütztes Routing dauert möglicherweise länger als das Herstellen einer primären Verbindung, da schreibgeschütztes Routing zuerst eine primäre Verbindung herstellt und dann nach der besten verfügbaren lesbaren Sekundärverbindung sucht. Deswegen sollten Sie das Anmeldetimeout vergrößern.  
  
## <a name="see-also"></a>Siehe auch  
[Verbinden mit dem Server](../../connect/php/connecting-to-the-server.md)  
  

