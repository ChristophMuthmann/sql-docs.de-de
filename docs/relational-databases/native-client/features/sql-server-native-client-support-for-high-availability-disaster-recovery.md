---
title: "SQL Server Native Client-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fd805562b60d37b9988b9afeb84d81e2cb2f5125
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>SQL Server Native Client-Unterstützung für hohe Verfügbarkeit, Notfallwiederherstellung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In diesem Thema wird die (in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] eingeführte) [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]Native Client-Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]erläutert. Weitere Informationen zu [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] finden Sie unter [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [Erstellung und Konfiguration von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Failoverclustering und AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) und [Aktive sekundäre Replikate: Lesbare sekundäre Replikate &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](~/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 Sie können den Verfügbarkeitsgruppenlistener einer bestimmten Verfügbarkeitsgruppe in der Verbindungszeichenfolge angeben. Wenn eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Anwendung mit einer Datenbank in einer Verfügbarkeitsgruppe verbunden ist, die ein Failover ausführt, wird die ursprüngliche Verbindung unterbrochen, und die Anwendung muss eine neue Verbindung öffnen, um die Arbeit nach dem Failover fortzusetzen.  
  
 Wenn Sie keine Verbindung mit einem Verfügbarkeitsgruppenlistener herstellen, und wenn mehrere IP-Adressen einem Hostnamen zugeordnet sind, durchläuft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client alle dem DNS-Eintrag zugeordneten IP-Adressen sequenziell. Dies kann zeitaufwändig sein, wenn die erste vom DNS-Server zurückgegebene IP-Adresse an keine Netzwerkschnittstellenkarte (NIC) gebunden ist. Wenn eine Verbindung mit einem Verfügbarkeitsgruppenlistener hergestellt wird, versucht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, Verbindungen mit allen IP-Adressen parallel herzustellen. Wenn ein Verbindungsversuch erfolgreich ist, verwirft der Treiber alle ausstehenden Verbindungsversuche.  
  
> [!NOTE]  
>  Das Erhöhen des Verbindungstimeouts sowie die Implementierung von Verbindungswiederholungslogik erhöhen die Wahrscheinlichkeit, dass eine Anwendung eine Verbindung zu einer Verfügbarkeitsgruppe herstellt. Da zudem eine Verbindung aufgrund eines Verfügbarkeitsgruppenfailovers fehlschlagen kann, empfiehlt sich die Implementierung von Verbindungswiederholungslogik, wodurch im Fall einer fehlgeschlagenen Verbindung bis zur erneuten Verbindung Wiederholungsversuche erfolgen.  
  
## <a name="connecting-with-multisubnetfailover"></a>Verbinden mit MultiSubnetFailover  
 Geben Sie immer **MultiSubnetFailover=Yes** an, wenn Sie eine Verbindung mit einem SQL Server 2012-Verfügbarkeitsgruppenlistener oder einer SQL Server 2012-Failoverclusterinstanz herstellen. **MultiSubnetFailover** ermöglicht ein schnelleres Failover für alle Verfügbarkeitsgruppen und -Failovercluster in SQL Server 2012-Instanz, und erheblich die Failoverzeit für Einzel- und multisubnetz AlwaysOn-Topologien verringert. Während eines Multisubnetzfailovers versucht der Client Verbindungen parallel. Während eines Subnetzfailovers wird der TCP-Verbindungsversuch vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Native Client aggressiv wiederholt.  
  
 Die **MultiSubnetFailover**-Verbindungseigenschaft gibt an, dass die Anwendung in einer Verfügbarkeitsgruppe oder einer Failoverclusterinstanz bereitgestellt wird und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client versucht, eine Verbindung mit der Datenbank auf der primären [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz herzustellen, indem mit allen IP-Adressen der Verfügbarkeitsgruppe Verbindungsversuche unternommen werden. Wenn **MultiSubnetFailover=Yes** für eine Verbindung angegeben wird, wiederholt der Client TCP-Verbindungsversuche schneller als dies bei den standardmäßigen TCP-Neuübertragungsintervallen des Betriebssystems der Fall ist. Dies ermöglicht eine schnellere verbindungswiederherstellung nach dem Failover einer AlwaysOn-Verfügbarkeitsgruppe oder einer immer auf Failover-Clusterinstanz und gilt für sowohl einzelne - multisubnetz - Verfügbarkeitsgruppen und Failoverclusterinstanzen.  
  
 Weitere Informationen zu Verbindungszeichenfolgeschlüsselwörtern finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Das Angeben von **MultiSubnetFailover=Yes** für ein anderes Verbindungsziel als einen Verfügbarkeitsgruppenlistener oder eine Failoverclusterinstanz kann die Leistung beeinträchtigen und wird nicht unterstützt.  
  
 Befolgen Sie beim Herstellen einer Verbindung mit einem Server in einer Verfügbarkeitsgruppe oder einer Failoverclusterinstanz die folgenden Richtlinien:  
  
-   Verwenden Sie die **MultiSubnetFailover** -Verbindungseigenschaft, wenn Sie eine Verbindung mit einem Einzelsubnetz oder Multisubnetz herstellen. Dadurch wird die Leistung für beide verbessert.  
  
-   Um eine Verbindung mit einer Verfügbarkeitsgruppe herzustellen, geben Sie in der Verbindungszeichenfolge den Verfügbarkeitsgruppenlistener der Verfügbarkeitsgruppe als Server an.  
  
-   Ein Verbindungsversuch mit einer mit mehr als 64 IP-Adressen konfigurierten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz verursacht einen Verbindungsfehler.  
  
-   Das Verhalten einer Anwendung, die die **MultiSubnetFailover**-Verbindungseigenschaft verwendet, wird durch den Authentifizierungstyp nicht beeinflusst: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung, Kerberos-Authentifizierung oder Windows-Authentifizierung.  
  
-   Sie können den Wert von **loginTimeout** erhöhen, um die Failoverzeit zu berücksichtigen und Wiederholungsversuche für Anwendungsverbindungen zu reduzieren.  
  
-   Verteilte Transaktionen werden nicht unterstützt.  
  
 Wenn das schreibgeschützte Routing nicht aktiviert ist, scheitert das Herstellen der Verbindung mit einem sekundären Replikatspeicherort in einer Verfügbarkeitsgruppe in den folgenden Situationen:  
  
1.  Wenn der sekundäre Replikatspeicherort nicht zum Akzeptieren von Verbindungen konfiguriert ist.  
  
2.  Wenn eine Anwendung **ApplicationIntent=ReadWrite** verwendet (weiter unten erläutert), und der sekundäre Replikatspeicherort für schreibgeschützten Zugriff konfiguriert ist.  
  
 Es kann keine Verbindung hergestellt werden, wenn ein primäres Replikat so konfiguriert ist, dass schreibgeschützte Arbeitslasten abgelehnt werden, und die Verbindungszeichenfolge **ApplicationIntent=ReadOnly**enthält.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aktualisieren zur Verwendung von Multisubnetzclustern aus Datenbankspiegelung  
 Ein Verbindungsfehler tritt auf, wenn die Verbindungsschlüsselwörter **MultiSubnetFailover** und **Failover_Partner** in der Verbindungszeichenfolge vorhanden sind. Es tritt auch ein Fehler auf, wenn **MultiSubnetFailover** verwendet wird und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] eine Failoverpartnerantwort zurückgibt, die angibt, dass es Teil eines Datenbankspiegelungspaars ist.  
  
 Wenn Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Anwendung aktualisieren, die derzeit Datenbankspiegelung in einem Multisubnetz-Szenario verwendet, müssen Sie die **Failover_Partner**-Verbindungseigenschaft entfernen und durch **MultiSubnetFailover**, festgelegt auf **Yes**, ersetzen sowie den Servernamen in der Verbindungszeichenfolge durch einen Verfügbarkeitsgruppenlistener ersetzen. Wenn eine Verbindungszeichenfolge **Failover_Partner** und **MultiSubnetFailover=Yes**verwendet, generiert der Treiber einen Fehler. Wenn eine Verbindungszeichenfolge jedoch **Failover_Partner** und **MultiSubnetFailover=No** (oder **ApplicationIntent=ReadWrite**) verwendet, verwendet die Anwendung Datenbankspiegelung.  
  
 Der Treiber gibt einen Fehler zurück, wenn die Datenbankspiegelung in der primären Datenbank in der Verfügbarkeitsgruppe verwendet wird, und wenn **MultiSubnetFailover=Yes** in der Verbindungszeichenfolge verwendet wird, die statt mit einem Verfügbarkeitsgruppenlistener eine Verbindung mit einer primären Datenbank herstellt.  
  
## <a name="specifying-application-intent"></a>Angeben des Anwendungszwecks  
 Wenn **ApplicationIntent = ReadOnly**, fordert der Client eine lesearbeitslast aus, wenn eine Verbindung mit einer Always On aktiviert-Datenbank herstellen. Der Server erzwingt den Versuch zur Verbindungszeit und während einer USE-Datenbankanweisung, aber nur für eine AlwaysOn-aktivierte Datenbank.  
  
 Das **ApplicationIntent** -Schlüsselwort funktioniert nicht mit schreibgeschützten Legacy-Datenbanken.  
  
 Eine Datenbank kann gestattet oder verweigert lesearbeitslasten auf die gewünschte Always On-Datenbank. (Hierzu wird die **ALLOW_CONNECTIONS**Klausel der **PRIMARY_ROLE** und der **SECONDARY_ROLE**[!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung verwendet.)  
  
 Das **ApplicationIntent** -Schlüsselwort wird verwendet, um schreibgeschütztes Routing zu aktivieren.  
  
## <a name="read-only-routing"></a>Schreibgeschütztes Routing  
 Schreibgeschütztes Routing ist eine Funktion, die die Verfügbarkeit eines schreibgeschützten Replikats einer Datenbank sicherstellen kann. So aktivieren Sie schreibgeschütztes Routing:  
  
1.  Sie müssen eine Verbindung zum Verfügbarkeitsgruppenlistener einer AlwaysOn-Verfügbarkeitsgruppe herstellen.  
  
2.  Das Schlüsselwort der **ApplicationIntent** -Verbindungszeichenfolge muss auf **ReadOnly**festgelegt werden.  
  
3.  Die Verfügbarkeitsgruppe muss vom Datenbankadministrator konfiguriert werden, um schreibgeschütztes Routing zu aktivieren.  
  
 Möglicherweise werden bei mehreren Verbindungen mithilfe von schreibgeschütztem Routing nicht alle mit demselben schreibgeschützten Replikat verbunden. Änderungen in der Datenbanksynchronisierung oder Änderungen in der Routingkonfiguration des Servers können zu Clientverbindungen mit anderen schreibgeschützten Replikaten führen. Sie gewährleisten, dass alle schreibgeschützten Anforderungen Verbindungen mit demselben schreibgeschützten Replikat herstellen, indem Sie keinen Verfügbarkeitsgruppenlistener an das Schlüsselwort der **Server** -Verbindungszeichenfolge übermitteln. Geben Sie stattdessen den Namen der schreibgeschützten Instanz an.  
  
 Schreibgeschütztes Routing dauert möglicherweise länger als das Herstellen einer primären Verbindung, da schreibgeschütztes Routing zuerst eine primäre Verbindung herstellt und dann nach der besten verfügbaren lesbaren Sekundärverbindung sucht. Deswegen sollten Sie das Anmeldetimeout vergrößern.  
  
## <a name="odbc"></a>ODBC  
 Zur Unterstützung von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] wurden in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client zwei Schlüsselwörter für ODBC-Verbindungszeichenfolgen hinzugefügt:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
 Weitere Informationen zu Schlüsselwörtern für ODBC-Verbindungszeichenfolgen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client finden Sie unter [Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Die entsprechenden Verbindungseigenschaften sind:  
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
 Weitere Informationen zu den ODBC-Verbindungseigenschaften in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client finden Sie unter [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 Die Funktionalität des **ApplicationIntent**- und des **MultiSubnetFailover**-Schlüsselworts wird ab [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] im ODBC-Datenquellen-Administrator für DSNs verfügbar gemacht, die den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Treiber verwenden.  
  
 Eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-ODBC-Anwendung kann eine von drei Funktionen verwenden, um die Verbindung herzustellen:  
  
|Funktion|Description|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)|Die Liste der Server, die von **SQLBrowseConnect** zurückgegeben wird, schließt keine VNNs ein. Sie sehen nur eine Liste von Servern ohne Angabe, ob es sich bei dem Server um einen eigenständigen Server oder einen primären oder sekundären Server in einem WSFC-Cluster (Windows Server-Failoverclustering) handelt. der zwei oder mehr [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen enthält, die für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] aktiviert wurden. Wenn Sie eine Verbindung mit einem Server herstellen, und es wird ein Fehler angezeigt, kann dies daran liegen, dass Sie eine Verbindung mit einem Server hergestellt haben und die Einstellung **ApplicationIntent** nicht mit der Serverkonfiguration kompatibel ist.<br /><br /> Da **SQLBrowseConnect** keine Server in einem WSFC-Cluster (Windows Server-Failoverclustering) erkennt, der zwei oder mehr [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen enthält, die für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] aktiviert sind, ignoriert **SQLBrowseConnect** das **MultiSubnetFailover**Schlüsselwort für Verbindungszeichenfolgen.|  
|[SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)|**SQLConnect** unterstützt sowohl **ApplicationIntent** als auch **MultiSubnetFailover** über einen Datenquellennamen (DSN) oder Verbindungseigenschaften.|  
|[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)|**SQLDriverConnect** unterstützt **ApplicationIntent** und **MultiSubnetFailover** über Schlüsselwörter für Verbindungszeichenfolgen, Verbindungseigenschaften oder DSN.|  
  
## <a name="ole-db"></a>OLE DB  
 OLE DB im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt das **MultiSubnetFailover**-Schlüsselwort nicht.  
  
 OLE DB im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt Anwendungsabsicht. Die Anwendungsabsicht verhält sich für OLE DB-Anwendungen und ODBC-Anwendungen gleiche (siehe oben).  
  
 Zur Unterstützung von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] wurde in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ein Schlüsselwort für OLE-Verbindungszeichenfolgen hinzugefügt:  
  
-   **Anwendungszweck**  
  
 Weitere Informationen zu Schlüsselwörtern für Verbindungszeichenfolgen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client finden Sie unter [Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Die entsprechenden Verbindungseigenschaften sind:  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
 Eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anwendung kann eine der folgenden Methoden zum Angeben der Anwendungsabsicht verwenden:  
  
 **IDBInitialize:: Initialize**  
 **IDBInitialize::Initialize** verwendet den zuvor konfigurierten Satz von Eigenschaften, um die Datenquelle zu initialisieren und das Datenquellenobjekt zu erstellen. Geben Sie die Anwendungsabsicht als Anbietereigenschaft oder als einen Teil der erweiterten Eigenschaftenzeichenfolge an.  
  
 **IDataInitialize:: GetDatasource**  
 **IDataInitialize::GetDataSource** verwendet eine Eingabeverbindungszeichenfolge, die das **Application Intent** -Schlüsselwort enthalten kann.  
  
 **IDBProperties::GetProperties**  
 **IDBProperties::GetProperties** ruft den Wert der Eigenschaft ab, die derzeit in der Datenquelle festgelegt wird.  Sie können den **Application Intent** -Wert über die DBPROP_INIT_PROVIDERSTRING-Eigenschaft und die SSPROP_INIT_APPLICATIONINTENT-Eigenschaft abrufen.  
  
 **IDBProperties::SetProperties**  
 Um den **ApplicationIntent** -Eigenschaftswert festzulegen, rufen Sie **IDBProperties::SetProperties** auf, indem Sie die **SSPROP_INIT_APPLICATIONINTENT** -Eigenschaft mit dem Wert "**ReadWrite**" oder "**ReadOnly**" oder die **DBPROP_INIT_PROVIDERSTRING** -Eigenschaft mit dem Wert angeben, der "**ApplicationIntent=ReadOnly**" oder "**ApplicationIntent=ReadWrite**" enthält.  
  
 Sie können die Anwendungsabsicht im Feld für die Eigenschaften der Anwendungsabsicht auf der Registerkarte Alle im Dialogfeld **Datenverknüpfungseigenschaften** angeben.  
  
 Wenn implizite Verbindungen hergestellt werden, verwendet die implizite Verbindung die Einstellung der Anwendungsabsicht der übergeordneten Verbindung. Auf ähnliche Weise erben mehrere aus der gleichen Datenquelle erstellte Sitzungen die Einstellung für die Anwendungsabsicht der Datenquelle.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Funktionen](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
