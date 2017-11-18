---
title: "JDBC Driver-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27b51025180a1c9a2463c49401589ab459e7ecaf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>JDBC Driver-Unterstützung für hohe Verfügbarkeit, Notfallwiederherstellung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In diesem Thema wird erläutert, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Unterstützung für hohe Verfügbarkeit und notfallwiederherstellung [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]. Weitere Informationen über [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]finden Sie in der [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] -Onlinedokumentation.  
  
 Ab Version 4.0 von der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], können Sie angeben, der Listener der verfügbarkeitsgruppe (hohe Verfügbarkeit und Wiederherstellung im Notfall-) verfügbarkeitsgruppe (AG) in der Verbindungseigenschaft. Wenn eine [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anwendung mit einer AlwaysOn-Datenbank, die beim Failover verbunden ist, die ursprüngliche Verbindung unterbrochen wird und die Anwendung muss eine neue Verbindung, um nach dem Failover weiterzuarbeiten öffnen. Die folgenden [Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md) in hinzugefügt wurden [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]:  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
Angeben von MultiSubnetFailover = True, wenn eine Verbindung mit dem Verfügbarkeitsgruppen-Listener einer verfügbarkeitsgruppe oder einer Failoverclusterinstanz herstellen. Beachten Sie, dass **MultiSubnetFailover** ist standardmäßig "false". Verwendung **ApplicationIntent** deklariert den Arbeitsauslastungstyp der Anwendung. Finden Sie unter Abschnitten finden Sie weitere Informationen.
 
Ab Version 6.0 des Microsoft JDBC Driver für SQL Server, eine neue Verbindungseigenschaft **TransparentNetworkIPResolution** (TNIR) wird für transparente Verbindung hinzugefügt, mit Always On-Verfügbarkeitsgruppen oder auf einem Server mit mehrere IP-Adressen zugewiesen sind. Wenn **TransparentNetworkIPResolution** ist "true", der Treiber versucht, für die Verbindung mit der ersten IP-Adresse verfügbar. Wenn der erste Versuch fehlschlägt, versucht der Treiber für die Verbindung mit allen IP-Adressen parallel, bis das Timeout abläuft, verwerfen alle ausstehenden Verbindungsversuche, wenn eine von ihnen erfolgreich abgeschlossen wurde.   

Beachten Sie Folgendes:
* TransparentNetworkIPResolution ist standardmäßig "true"
* TransparentNetworkIPResolution wird ignoriert, wenn MultiSubnetFailover "true" ist.
* TransparentNetworkIPResolution wird ignoriert, wenn die datenbankspiegelung verwendet wird
* TransparentNetworkIPResolution wird ignoriert, wenn mehr als 64 IP-Adressen vorhanden sind
* Wenn TransparentNetworkIPResolution auf "true" festgelegt ist, verwendet der erste Verbindungsversuch einen Timeoutwert von 500 ms. Restliche die Verbindungsversuche führen Sie die gleiche Logik wie die MultiSubnetFailover-Funktion. 

> [!NOTE]  
Wenn Sie Microsoft JDBC Driver 4.2 (oder niedriger) für SQL Server und **MultiSubnetFailover** lautet "false", die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] versucht, eine Verbindung mit der ersten IP-Adresse herstellen. Wenn die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] keine Verbindung mit der ersten IP-Adresse, die Verbindung nicht herstellen kann. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] wird nicht versucht, eine Verbindung mit allen nachfolgenden IP-Adressen, die dem Server zugeordnet. 

  
> [!NOTE]  
>  Das Erhöhen des Verbindungstimeouts sowie die Implementierung von Verbindungswiederholungslogik erhöhen die Wahrscheinlichkeit, dass eine Anwendung eine Verbindung zu einer Verfügbarkeitsgruppe herstellt. Da zudem eine Verbindung aufgrund eines Verfügbarkeitsgruppenfailovers fehlschlagen kann, empfiehlt sich die Implementierung von Verbindungswiederholungslogik, wodurch im Fall einer fehlgeschlagenen Verbindung bis zur erneuten Verbindung Wiederholungsversuche erfolgen.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>Verbinden mit MultiSubnetFailover  
 Geben Sie immer **MultiSubnetFailover = "true"** beim Verbinden mit dem verfügbarkeitsgruppenlistener eine [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] verfügbarkeitsgruppe oder einer [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Failoverclusterinstanz. **MultiSubnetFailover** ermöglicht ein schnelleres Failover für alle Verfügbarkeitsgruppen und Failoverclusterinstanzen in [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] und verringert erheblich die Failoverzeit für Einzel- und multisubnetz AlwaysOn-Topologien. Während eines Multisubnetzfailovers versucht der Client Verbindungen parallel. Während eines subnetzfailovers der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aggressive Wiederholungsversuche zum Herstellen die TCP-Verbindung.  
  
 Die **MultiSubnetFailover** -Verbindungseigenschaft gibt an, dass die Anwendung in einer verfügbarkeitsgruppe oder Failoverclusterinstanz und die bereitgestellt wird, wird die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] versucht, eine Verbindung mit der Datenbank auf dem primären [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz beim Herstellen der Verbindung mit allen IP-Adressen. Wenn **MultiSubnetFailover = True** ist für eine Verbindung angegeben, der Client TCP-Verbindungsversuche schneller als das Betriebssystem standardmäßig TCP-neuübertragungsintervallen wiederholt. Auf diese Weise kann die Verbindung nach einem Failover einer AlwaysOn-Verfügbarkeitsgruppe oder einer AlwaysOn-Failoverclusterinstanz schneller wiederhergestellt werden. Diese Einstellung gilt sowohl für Einzelsubnetz- als auch Multisubnetz-Verfügbarkeitsgruppen und -Failoverclusterinstanzen.  
  
 Weitere Informationen zu Schlüsselwörtern der Verbindungszeichenfolge in der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Angeben von **MultiSubnetFailover = True** beim Herstellen einer Verbindung auf einen anderen Wert als einem verfügbarkeitsgruppenlistener oder einer Failover-Clusterinstanz möglicherweise verminderter Leistung und wird nicht unterstützt.  
  
 Wenn der Sicherheits-Manager nicht installiert ist, werden virtuelle IP-Adressen (VIPs) von der Java Virtual Machine für einen begrenzten Zeitraum zwischengespeichert. Die jeweilige Dauer wird durch Ihre JDK-Implementierung und die Java-Eigenschaften networkaddress.cache.ttl und networkaddress.cache.negative.ttl bestimmt. Wenn der JDK-Sicherheits-Manager installiert ist, werden VIPs von der Java Virtual Machine zwischengespeichert, und der Cache wird standardmäßig nicht aktualisiert. Es empfiehlt sich die Gültigkeitsdauer, d. h. "time-to-live" (networkaddress.cache.ttl), für den Cache der Java Virtual Machine auf einen Tag festzulegen. Wenn Sie den Standardwert nicht auf einen Tag oder eine ähnliche Einstellung festlegen, wird der alte Wert beim Hinzufügen oder Aktualisieren einer VIP nicht aus dem Java Virtual Machine-Cache gelöscht. Weitere Informationen zu networkaddress.cache.ttl und networkaddress.cache.negative.ttl, finden Sie unter [http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html](http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html).  
  
 Befolgen Sie beim Herstellen einer Verbindung mit einem Server in einer Verfügbarkeitsgruppe oder einer Failoverclusterinstanz die folgenden Richtlinien:  
  
-   Der Treiber löst einen Fehler, wenn die **InstanceName** Connection-Eigenschaft wird verwendet, in derselben Verbindungszeichenfolge wie die **MultiSubnetFailover** Connection-Eigenschaft. Dies spiegelt den Umstand wider, dass der SQL Browser-Dienst in Verfügbarkeitsgruppen nicht verwendet wird. Jedoch, wenn die **PortNumber** -Verbindungseigenschaft ebenfalls angegeben wird, ignoriert der Treiber **InstanceName** und **PortNumber**.  
  
-   Verwenden der **MultiSubnetFailover** Verbindungseigenschaft beim Verbinden mit einer einzelnen oder mehreren Subnetzen wird dadurch die Leistung für beide verbessert.  
  
-   Um eine Verbindung mit einer Verfügbarkeitsgruppe herzustellen, geben Sie in der Verbindungszeichenfolge den Verfügbarkeitsgruppenlistener der Verfügbarkeitsgruppe als Server an. Beispiel: jdbc:sqlserver://VNN1.  
  
-   Ein Verbindungsversuch mit einer mit mehr als 64 IP-Adressen konfigurierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz verursacht einen Verbindungsfehler.  
  
-   Das Verhalten einer Anwendung, die mithilfe der **MultiSubnetFailover** Verbindungseigenschaft wird nicht beeinflusst basierend auf den Typ der Authentifizierung: [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, Kerberos-Authentifizierung oder Windows-Authentifizierung.  
  
-   Erhöhen Sie den Wert der **LoginTimeout** für Failoverzeit zu berücksichtigen und Wiederholungsversuche für anwendungsverbindungen zu reduzieren.  
  
-   Verteilte Transaktionen werden nicht unterstützt.  
  
 Wenn das schreibgeschützte Routing nicht aktiviert ist, scheitert das Herstellen der Verbindung mit einem sekundären Replikatspeicherort in einer Verfügbarkeitsgruppe in den folgenden Situationen:  
  
1.  Wenn der sekundäre Replikatspeicherort nicht zum Akzeptieren von Verbindungen konfiguriert ist.  
  
2.  Wenn eine Anwendung verwendet **ApplicationIntent = ReadWrite** (weiter unten erläutert) und der sekundäre replikatspeicherort für schreibgeschützten Zugriff konfiguriert ist.  
  
 Es kann keine Verbindung hergestellt werden, wenn ein primäres Replikat so konfiguriert ist, dass schreibgeschützte Arbeitslasten abgelehnt werden, und die Verbindungszeichenfolge **ApplicationIntent=ReadOnly**enthält.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aktualisieren zur Verwendung von Multisubnetzclustern aus Datenbankspiegelung  
 Wenn Sie ein upgrade einer [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Anwendung, die derzeit die datenbankspiegelung zu einem multisubnetz-Szenario verwendet, sollten Sie entfernen die **FailoverPartner** Verbindungseigenschaft und ersetzen es durch **MultiSubnetFailover**  festgelegt **"true"** und den Servernamen in der Verbindungszeichenfolge mit einem verfügbarkeitsgruppenlistener ersetzen. Wenn eine Verbindungszeichenfolge verwendet **FailoverPartner** und **MultiSubnetFailover = True**, generiert der Treiber einen Fehler. Jedoch, wenn eine Verbindungszeichenfolge verwendet **FailoverPartner** und **MultiSubnetFailover = "false"** (oder **ApplicationIntent = ReadWrite**), die Anwendung wird die Datenbank verwenden die Spiegelung.  
  
 Der Treiber einen Fehler zurück, wenn die datenbankspiegelung auf der primären Datenbank in der Verfügbarkeitsgruppe verwendet wird, und wenn **MultiSubnetFailover = True** wird verwendet, in der Verbindungszeichenfolge die Herstellung einer primären Datenbank nicht zu einer verfügbarkeitsgruppe der Listener.  
  
## <a name="specifying-application-intent"></a>Angeben des Anwendungszwecks  
 Wenn **ApplicationIntent = ReadOnly**, fordert der Client eine schreibgeschützte Arbeitslast aus, wenn eine Verbindung mit einer AlwaysOn-Datenbank herstellen. Der Server erzwingt den Zweck zur Verbindungszeit und während einer USE-Datenbankanweisung, jedoch lediglich für eine AlwaysOn-fähige Datenbank.  
  
 Die **ApplicationIntent** -Schlüsselwort funktioniert nicht mit älteren und schreibgeschützte Datenbanken.  
  
 Eine Datenbank kann Lesearbeitslasten auf der AlwaysOn-Zieldatenbank zulassen bzw. nicht zulassen. (Hierzu wird die **ALLOW_CONNECTIONS**Klausel der **PRIMARY_ROLE** und der **SECONDARY_ROLE**[!INCLUDE[tsql](../../includes/tsql_md.md)]-Anweisung verwendet.)  
  
 Die **ApplicationIntent** Schlüsselwort wird verwendet, um schreibgeschütztes routing zu aktivieren.  
  
## <a name="read-only-routing"></a>Schreibgeschütztes Routing  
 Das schreibgeschützte Routing ist eine Funktion, die die Verfügbarkeit des schreibgeschützten Replikats einer Datenbank sicherstellen kann. So aktivieren Sie schreibgeschütztes Routing:  
  
1.  Sie müssen eine Verbindung mit dem Verfügbarkeitsgruppen-Listener einer AlwaysOn-Verfügbarkeitsgruppe herstellen.  
  
2.  Die **ApplicationIntent** -Schlüsselwort der Verbindungszeichenfolge muss festgelegt werden, um **ReadOnly**.  
  
3.  Die Verfügbarkeitsgruppe muss vom Datenbankadministrator konfiguriert werden, um schreibgeschütztes Routing zu aktivieren.  
  
 Möglicherweise werden bei mehreren Verbindungen mithilfe von schreibgeschütztem Routing nicht alle mit demselben schreibgeschützten Replikat verbunden. Änderungen in der Datenbanksynchronisierung oder Änderungen in der Routingkonfiguration des Servers können zu Clientverbindungen mit anderen schreibgeschützten Replikaten führen. Um sicherzustellen, dass alle schreibgeschützten Anforderungen mit demselben schreibgeschützten Replikat herstellen, übergeben Sie einen verfügbarkeitsgruppenlistener oder die virtuelle IP-Adresse der **ServerName** Verbindungszeichenfolgen-Schlüsselwort. Geben Sie stattdessen den Namen der schreibgeschützten Instanz an.  
  
 Das schreibgeschützte Routing kann länger als das Herstellen einer Verbindung mit dem primären Objekt dauern, da beim schreibgeschützten Routing zunächst eine Verbindung mit dem primären Objekt hergestellt und anschließend nach dem verfügbaren am besten lesbaren sekundären Objekt gesucht wird. Deswegen sollten Sie das Anmeldetimeout vergrößern.  
  
## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>Neue Methoden, die multiSubnetFailover und applicationIntent unterstützen  
 Die folgenden Methoden ermöglichen den programmgesteuerten Zugriff auf die **MultiSubnetFailover**, **ApplicationIntent** und **TransparentNetworkIPResolution** Verbindungszeichenfolge Schlüsselwörter:  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 Die **GetMultiSubnetFailover**, **SetMultiSubnetFailover**, **GetApplicationIntent**, **SetApplicationIntent**, **GetTransparentNetworkIPResolution** und **SetTransparentNetworkIPResolution** Methoden werden auch hinzugefügt [SQLServerDataSource-Klasse](../../connect/jdbc/reference/sqlserverdatasource-class.md), [ SQLServerConnectionPoolDataSource-Klasse](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), und [SQLServerXADataSource-Klasse](../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
## <a name="ssl-certificate-validation"></a>Überprüfung des SSL-Zertifikats  
 Eine Verfügbarkeitsgruppe besteht aus mehreren physischen Servern. [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]zusätzliche Unterstützung für **alternativen Antragstellernamen** in SSL-Zertifikaten, sodass mehrere Hosts das gleiche Zertifikat zugeordnet werden können. Weitere Informationen zu SSL finden Sie unter [Grundlegendes zur SSL-Unterstützung](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen einer Verbindung mit SQLServer mit der JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md)  
  
  

