---
title: OLE DB-Treiber für SQL Server-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall | Microsoft Docs
description: OLE DB-Treiber für SQL Server-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 05275a1f770ce4a01f583dda768872a26b5e3725
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="ole-db-driver-for-sql-server-support-for-high-availability-disaster-recovery"></a>OLE DB-Treiber für SQL Server-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Artikel werden OLE DB-Treiber für SQL Server-Unterstützung (hinzugefügt [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Weitere Informationen zu [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] finden Sie unter [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [Erstellung und Konfiguration von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Failoverclustering und AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) und [Aktive sekundäre Replikate: Lesbare sekundäre Replikate &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 Sie können den Verfügbarkeitsgruppenlistener einer bestimmten Verfügbarkeitsgruppe in der Verbindungszeichenfolge angeben. Wenn ein OLE DB-Treiber für SQL Server-Anwendung mit einer Datenbank in einer verfügbarkeitsgruppe verbunden ist, die ein Failover ausführt, die ursprüngliche Verbindung unterbrochen wird, und öffnen Sie die Anwendung muss eine neue Verbindung, um die Arbeit nach dem Failover fortzusetzen.  
  
 Wenn Sie nicht mit einem verfügbarkeitsgruppenlistener herstellen, und mehrere IP-Adressen einem Hostnamen zugeordnet sind, werden alle IP-Adressen, DNS-Eintrag zugeordneten OLE DB-Treiber für SQL Server nacheinander durchlaufen. Dies kann zeitaufwändig sein, wenn die erste vom DNS-Server zurückgegebene IP-Adresse an keine Netzwerkschnittstellenkarte (NIC) gebunden ist. Beim Verbinden mit einem Verfügbarkeitsgruppen-Listener versucht, OLE DB-Treiber für SQL Server, Verbindungen mit allen IP-Adressen parallel herzustellen, und wenn ein Verbindungsversuch erfolgreich ist, verwirft der Treiber alle ausstehenden Verbindungsversuche.  
  
> [!NOTE]  
> Das Erhöhen des Verbindungstimeouts sowie die Implementierung von Verbindungswiederholungslogik erhöhen die Wahrscheinlichkeit, dass eine Anwendung eine Verbindung zu einer Verfügbarkeitsgruppe herstellt. Da zudem eine Verbindung aufgrund eines Verfügbarkeitsgruppenfailovers fehlschlagen kann, empfiehlt sich die Implementierung von Verbindungswiederholungslogik, wodurch im Fall einer fehlgeschlagenen Verbindung bis zur erneuten Verbindung Wiederholungsversuche erfolgen.  
  
## <a name="connecting-with-multisubnetfailover"></a>Verbinden mit MultiSubnetFailover  
 Geben Sie immer **MultiSubnetFailover = Yes** beim Verbinden mit SQL Server AlwaysOn-Verfügbarkeitsgruppe Listener oder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Failoverclusterinstanz. **MultiSubnetFailover** ermöglicht ein schnelleres Failover für alle AlwaysOn-Verfügbarkeitsgruppen und Failoverclusterinstanzen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], und verringert erheblich die Failoverzeit für Einzel- und multisubnetz AlwaysOn-Topologien. Während eines Multisubnetzfailovers versucht der Client Verbindungen parallel. Während eines subnetzfailovers versucht der OLE DB-Treiber für SQL Server TCP-Verbindung.  
  
 Die **MultiSubnetFailover** -Verbindungseigenschaft gibt an, dass die Anwendung in einer verfügbarkeitsgruppe oder Failoverclusterinstanz bereitgestellt wird, und diesen OLE DB-Treiber für SQL Server versucht, eine Verbindung mit der Datenbank auf der primäre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Instanz beim Herstellen der Verbindung mit allen IP-Adressen. Wenn **MultiSubnetFailover=Yes** für eine Verbindung angegeben wird, wiederholt der Client TCP-Verbindungsversuche schneller als dies bei den standardmäßigen TCP-Neuübertragungsintervallen des Betriebssystems der Fall ist. Dies ermöglicht eine schnellere verbindungswiederherstellung nach dem Failover einer AlwaysOn-Verfügbarkeitsgruppe oder einer Failoverclusterinstanz und gilt für sowohl einzelne - multisubnetz - Verfügbarkeitsgruppen und Failoverclusterinstanzen.  
  
 Weitere Informationen zu verbindungszeichenfolgeschlüsselwörtern finden Sie unter [Schlüsselwörtern für Verbindungszeichenfolgen mit OLE DB-Treiber für SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
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
  
Wenn Sie ein upgrade einer OLE DB-Treiber für SQL Server-Anwendung, die derzeit verwendet der datenbankspiegelung zu einer multisubnetz-Szenario, entfernen Sie die **von Failover_Partner** Verbindungseigenschaft und ersetzen es durch  **MultiSubnetFailover** festgelegt **Ja** , und Ersetzen Sie den Servernamen in der Verbindungszeichenfolge mit einem Verfügbarkeitsgruppen-Listener. Wenn eine Verbindungszeichenfolge **Failover_Partner** und **MultiSubnetFailover=Yes**verwendet, generiert der Treiber einen Fehler. Wenn eine Verbindungszeichenfolge jedoch **Failover_Partner** und **MultiSubnetFailover=No** (oder **ApplicationIntent=ReadWrite**) verwendet, verwendet die Anwendung Datenbankspiegelung.  
  
Der Treiber gibt einen Fehler zurück, wenn die Datenbankspiegelung in der primären Datenbank in der Verfügbarkeitsgruppe verwendet wird, und wenn **MultiSubnetFailover=Yes** in der Verbindungszeichenfolge verwendet wird, die statt mit einem Verfügbarkeitsgruppenlistener eine Verbindung mit einer primären Datenbank herstellt.  
  
## <a name="specifying-application-intent"></a>Angeben des Anwendungszwecks  
Wenn **ApplicationIntent = ReadOnly**, fordert der Client eine lesearbeitslast aus, wenn eine Verbindung mit einer Always On aktiviert-Datenbank herstellen. Der Server erzwingt den Zweck zur Verbindungszeit und während einer `USE` database-Anweisung jedoch nur an eine Datenbank Always On aktiviert.  
  
Das **ApplicationIntent** -Schlüsselwort funktioniert nicht mit schreibgeschützten Legacy-Datenbanken.  
  
Eine Datenbank kann gestattet oder verweigert lesearbeitslasten auf die gewünschte Always On-Datenbank. (Hierzu wird die **ALLOW_CONNECTIONS**Klausel der **PRIMARY_ROLE** und der **SECONDARY_ROLE**[!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung verwendet.)  
  
Das **ApplicationIntent** -Schlüsselwort wird verwendet, um schreibgeschütztes Routing zu aktivieren.  
  
## <a name="read-only-routing"></a>Schreibgeschütztes Routing  
Schreibgeschütztes Routing ist eine Funktion, die die Verfügbarkeit eines schreibgeschützten Replikats einer Datenbank sicherstellen kann. So aktivieren Sie schreibgeschütztes Routing:  
  
1.  Sie müssen eine Verbindung zum Verfügbarkeitsgruppenlistener einer AlwaysOn-Verfügbarkeitsgruppe herstellen.  
  
2.  Das Schlüsselwort der **ApplicationIntent** -Verbindungszeichenfolge muss auf **ReadOnly**festgelegt werden.  
  
3.  Die AlwaysOn-Verfügbarkeitsgruppe muss vom Datenbankadministrator So aktivieren Sie schreibgeschütztes routing konfiguriert werden.  
  
Möglicherweise werden bei mehreren Verbindungen mithilfe von schreibgeschütztem Routing nicht alle mit demselben schreibgeschützten Replikat verbunden. Änderungen in der Datenbanksynchronisierung oder Änderungen in der Routingkonfiguration des Servers können zu Clientverbindungen mit anderen schreibgeschützten Replikaten führen. Um sicherzustellen, dass alle schreibgeschützten Anforderungen mit demselben schreibgeschützten Replikat herstellen, übergeben Sie einen Listener AlwaysOn-Verfügbarkeitsgruppe die **Server** Verbindungszeichenfolgen-Schlüsselwort. Geben Sie stattdessen den Namen der schreibgeschützten Instanz an.  
  
Schreibgeschütztes Routing dauert möglicherweise länger als das Herstellen einer primären Verbindung, da schreibgeschütztes Routing zuerst eine primäre Verbindung herstellt und dann nach der besten verfügbaren lesbaren Sekundärverbindung sucht. Deswegen sollten Sie das Anmeldetimeout vergrößern.  
  
## <a name="ole-db"></a>OLE DB  
Der OLE DB-Treiber für SQL Server unterstützt sowohl die **ApplicationIntent** und **MultiSubnetFailover** Schlüsselwörter.   
  
Die zwei Schlüsselwörter für OLE DB-Verbindungszeichenfolgen hinzugefügt wurden, zur Unterstützung [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in OLE DB-Treiber für SQL Server:  
  
-   **ApplicationIntent** 
-   **MultiSubnetFailover**  
  
 Weitere Informationen zu Schlüsselwörtern der Verbindungszeichenfolge in OLE DB-Treiber für SQL Server finden Sie unter [Schlüsselwörtern für Verbindungszeichenfolgen mit OLE DB-Treiber für SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  

### <a name="application-intent"></a>Application Intent 

Die entsprechenden Verbindungseigenschaften sind:  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
Ein OLE DB-Treiber für SQL Server OLE DB-Anwendung kann eine der Methoden zum Angeben der anwendungsabsicht verwenden:  
  
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
  
### <a name="multisubnetfailover"></a>MultiSubnetFailover

Die entsprechende Verbindungseigenschaft ist:  
  
-   **SSPROP_INIT_MULTISUBNETFAILOVER**  

Die SSPROP_INIT_MULTISUBNETFAILOVER-Eigenschaft ist vom Typ Boolean auf. Die Eigenschaft akzeptiert die Werte der VARIANT_TRUE oder VARIANT_FALSE.

Rufen Sie zum Festlegen des MultiSubnetFailover-Eigenschaftswert **IDBProperties:: SetProperties** übergibt die SSPROP_INIT_MULTISUBNETFAILOVER-Eigenschaft mit dem Wert **VARIANT_TRUE** oder **VARIANT_ "False"**. 

#### <a name="example"></a>Beispiel

```
DBPROP rgPropMultisubnet;

rgPropMultisubnet.dwPropertyID = SSPROP_INIT_MULTISUBNETFAILOVER;
rgPropMultisubnet.dwOptions = DBPROPOPTIONS_REQUIRED;
rgPropMultisubnet.dwStatus = DBPROPSTATUS_OK;
rgPropMultisubnet.colid = DB_NULLID;
V_VT(&(rgPropMultisubnet.vValue)) = VT_BOOL;
V_BOOL(&(rgPropMultisubnet.vValue)) = VARIANT_TRUE;

DBPROPSET PropSet;

PropSet.rgProperties = &rgPropMultisubnet;
PropSet.cProperties = 1;
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;
IDBProperties* pIDBProperties = NULL;
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);
pIDBProperties->SetProperties(1, &PropSet);
```

## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Funktionen](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [Verwenden von Verbindungszeichenfolgen-Schlüsselwörtern mit dem OLE DB-Treiber für SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)  
  
  
