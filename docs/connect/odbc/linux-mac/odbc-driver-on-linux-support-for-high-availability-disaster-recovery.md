---
title: ODBC-Treiber unter Linux und Mac OS - High Availability and Disaster Recovery | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d7b6c72d350b718a7676bffd72c261b7cfa72667
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>ODBC-Treiber unter Linux und MacOS Unterstützung für hohe Verfügbarkeit und Wiederherstellung im Notfall
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Die ODBC-Treiber für Linux und MacOS Unterstützung [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Weitere Informationen zu [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], finden Sie unter:  
  
-   [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover (SQLServer)](http://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [Erstellung und Konfiguration von Verfügbarkeitsgruppen (SQLServer)](http://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [Failoverclustering und AlwaysOn-Verfügbarkeitsgruppen (SQLServer)](http://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [Aktive sekundäre Replikate: Lesbare sekundäre Replikate (AlwaysOn-Verfügbarkeitsgruppen)](http://msdn.microsoft.com/library/ff878253.aspx)  
  
Sie können den Verfügbarkeitsgruppenlistener einer bestimmten Verfügbarkeitsgruppe in der Verbindungszeichenfolge angeben. Wenn eine ODBC-Anwendung unter Linux oder MacOS mit einer Datenbank in einer verfügbarkeitsgruppe verbunden ist, die ein Failover ausführt, die ursprüngliche Verbindung unterbrochen wird, und öffnen Sie die Anwendung muss eine neue Verbindung, um die Arbeit nach dem Failover fortzusetzen.

Die ODBC-Treiber unter Linux und MacOS durchlaufen nacheinander alle IP-Adressen, die einen DNS-Hostnamen zugeordnet sind, sofern Sie nicht eine mit einem Verfügbarkeitsgruppen-Listener Verbindung und mehrere IP-Adressen mit dem Hostnamen zugeordnet sind.

Wenn der DNS-Server der erste zurückgegebene IP-Adresse nicht verbindungsfähigen ist, können diese Iterationen zeitaufwendig sein. Beim Verbinden mit einem verfügbarkeitsgruppenlistener versucht der Treiber, Verbindungen mit allen IP-Adressen parallel herzustellen. Falls ein Verbindungsversuch erfolgreich war, bricht der Treiber alle weiteren laufenden Verbindungsversuche ab.

> [!NOTE]  
> Da eine Verbindung aufgrund eines verfügbarkeitsgruppenfailovers fehlschlagen kann, implementieren Sie verbindungswiederholungslogik; Bei einem Verbindungsfehler zu wiederholen, bis er erneut eine Verbindung herstellt. Das Erhöhen des Verbindungstimeouts sowie die Implementierung einer Verbindungswiederholungslogik erhöhen die Chance auf eine Verbindung mit der Verfügbarkeitsgruppe.

## <a name="connecting-with-multisubnetfailover"></a>Verbinden mit MultiSubnetFailover

Geben Sie immer **MultiSubnetFailover = Yes** (oder **= "true"**) beim Herstellen einer Verbindung mit einem [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] verfügbarkeitsgruppenlistener oder [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] Failoverclusterinstanz. **MultiSubnetFailover** ermöglicht ein schnelleres Failover für alle Verfügbarkeitsgruppen und Failoverclusterinstanzen in [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]. **MultiSubnetFailover** beträchtlich reduziert die Failoverzeit für Einzel- und multisubnetz AlwaysOn-Topologien. Während eines Multisubnetzfailovers versucht der Client, Verbindungen parallel herzustellen. Während eines subnetzfailovers versucht der Treiber energisch, die TCP-Verbindung.

Die **MultiSubnetFailover** -Verbindungseigenschaft zeigt an, dass die Anwendung in einer Verfügbarkeitsgruppe oder einer Failoverclusterinstanz bereitgestellt wird. Der Treiber versucht, sich mit der Datenbank auf dem primären Replikat herstellen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanz beim Herstellen der Verbindung mit allen IP-Adressen. Bei der Verbindung mit **MultiSubnetFailover = Yes**, der Client wiederholt TCP-Verbindungsversuche schneller als die standardmäßig TCP-neuübertragungsintervallen des Betriebssystems. **MultiSubnetFailover=Yes** ermöglicht eine schnellere Verbindungswiederherstellung nach dem Failover entweder einer AlwaysOn-Verfügbarkeitsgruppe oder einer AlwaysOn-Failoverclusterinstanz. **MultiSubnetFailover = Yes** gilt für sowohl einzelne - multisubnetz - Verfügbarkeitsgruppen und Failoverclusterinstanzen.  

Verwenden Sie **MultiSubnetFailover=Yes** wenn Sie eine Verbindung mit einem Verfügbarkeitsgruppenlistener oder einer Failoverclusterinstanz herstellen. Andernfalls kann die Leistung Ihrer Anwendung negativ beeinflusst werden.

Beachten Sie bei der verbindungsherstellung mit einem Server in einer verfügbarkeitsgruppe oder Failoverclusterinstanz:
  
-   Geben Sie **MultiSubnetFailover = Yes** zur Verbesserung der Leistung bei der Verbindung mit einem einzelnen Subnetz oder multisubnetz-Verfügbarkeitsgruppe.

-   Geben Sie den verfügbarkeitsgruppenlistener der verfügbarkeitsgruppe als Server in der Verbindungszeichenfolge.
  
-   Sie können keine Verbindung mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Instanz mit mehr als 64 IP-Adressen konfiguriert.

-   Beide [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Authentifizierung oder die Kerberos-Authentifizierung genutzt werden mit **MultiSubnetFailover = Yes** ohne Auswirkung auf das Verhalten der Anwendung.

-   Sie können den Wert von **loginTimeout** erhöhen, um die Failoverzeit zu berücksichtigen und die Anzahl der von der Anwendung durchgeführten Verbindungsversuche zu reduzieren.

-   Verteilte Transaktionen werden nicht unterstützt.  
  
Wenn das schreibgeschützte Routing nicht aktiviert ist, scheitert die Verbindungsherstellung mit einem sekundären Replikatspeicherort in einer Verfügbarkeitsgruppe in den folgenden Situationen:  
  
1.  Wenn der sekundäre Replikatspeicherort nicht zum Akzeptieren von Verbindungen konfiguriert ist.  
  
2.  Wenn eine Anwendung **ApplicationIntent=ReadWrite** verwendet wird und der sekundäre Replikatspeicherort für den schreibgeschützten Zugriff konfiguriert ist.  
  
Es kann keine Verbindung hergestellt werden, wenn ein primäres Replikat so konfiguriert ist, dass schreibgeschützte Arbeitsauslastungen abgelehnt werden und die Verbindungszeichenfolge **ApplicationIntent=ReadOnly**enthält.  
  
## <a name="specifying-application-intent"></a>Angeben des Anwendungszwecks  
Im Fall von **ApplicationIntent=ReadOnly**fordert der Client eine Lesearbeitslast an, wenn eine Verbindung mit einer AlwaysOn-aktivierten Datenbank hergestellt wird. Der Server erzwingt den Zweck zur Verbindungszeit und während einer USE-datenbankanweisung, aber nur für eine AlwaysOn-aktivierten Datenbank.

Das **ApplicationIntent** -Schlüsselwort funktioniert nicht mit schreibgeschützten Legacy-Datenbanken.  

Eine Datenbank kann Lesearbeitslasten auf der AlwaysOn-Zieldatenbank zulassen bzw. nicht zulassen. (Verwenden der **ALLOW_CONNECTIONS** -Klausel der **PRIMARY_ROLE** und **SECONDARY_ROLE** [!INCLUDE[tsql](../../../includes/tsql_md.md)] Anweisungen.)  
  
Das Schlüsselwort **ApplicationIntent** wird verwendet, um das schreibgeschützte Routing zu aktivieren.  
  
## <a name="read-only-routing"></a>Schreibgeschütztes Routing  
Das schreibgeschützte Routing ist eine Funktion, die die Verfügbarkeit des schreibgeschützten Replikats einer Datenbank sicherstellen kann. So aktivieren Sie schreibgeschütztes Routing:  
  
1.  Stellen Sie eine Verbindung zum Verfügbarkeitsgruppenlistener einer AlwaysOn-Verfügbarkeitsgruppe her.  
  
2.  Das Verbindungszeichenfolge-Schlüsselwort **ApplicationIntent** - muss auf **ReadOnly**eingerichtet sein.  
  
3.  Der Datenbankadministrator muss die Verfügbarkeitsgruppe entsprechend konfigurieren, um schreibgeschütztes Routing zu aktivieren.  
  
Es ist möglich das mehrere Verbindungen die schreibgeschütztes Routing verwenden, mit verschiedenen schreibgeschützten Replikaten verbunden werden. Änderungen in der Datenbanksynchronisierung oder Änderungen in der Routingkonfiguration des Servers können zu Clientverbindungen mit anderen schreibgeschützten Replikaten führen. Sie gewährleisten, dass alle schreibgeschützten Anforderungen Verbindungen mit demselben schreibgeschützten Replikat herstellen, indem Sie keinen Verfügbarkeitsgruppenlistener an das **Server** -Verbindungsschlüsselwort übermitteln. Geben Sie stattdessen den Namen der schreibgeschützten Instanz an.  
  
Die Zeit bis zum Verbindungsaufbau ist beim schreibgeschützten Routing länger als beim Zugriff auf das primäre Replikat. Erhöhen Sie deshalb Ihr Anmeldetimout. Schreibgeschütztes Routing verbindet sich zunächst mit dem primären Replikat und sucht dann nach dem besten verfügbaren lesbaren sekundären Replikat.  
  
## <a name="odbc-syntax"></a>ODBC-Syntax

Zwei ODBC-Verbindungszeichenfolgen-Schlüsselwörter unterstützen [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
Weitere Informationen zu ODBC-Verbindungszeichenfolgen-Schlüsselwörter finden Sie unter [Schlüsselwörtern für Verbindungszeichenfolgen mit SQL Native Client verwenden](http://msdn.microsoft.com/library/ms130822.aspx).  
  
Die entsprechende Verbindungsattribute sind:
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
Weitere Informationen zu ODBC-Verbindungsattributen finden Sie unter [SQLSetConnectAttr](http://msdn.microsoft.com/library/ms131709.aspx).  
  
Eine ODBC-Anwendung, verwendet [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] kann eine von zwei Funktionen zum Herstellen die Verbindung verwenden:  
  
|Funktion|Description|  
|------------|---------------|  
|[SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect** unterstützt sowohl **ApplicationIntent** und **MultiSubnetFailover** über einen Datenquellennamen (DSN) oder das Verbindungsattribut.|  
|[SQLDriverConnect-Funktion](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect** unterstützt **ApplicationIntent** und **MultiSubnetFailover** über DSN, Verbindungszeichenfolgen-Schlüsselwort oder Verbindungsattribut.|
  
## <a name="see-also"></a>Siehe auch  

[Schlüsselwörter für Verbindungszeichenfolgen und Datenquellennamen (DSNs)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[Programmierrichtlinien](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Versionsanmerkungen](../../../connect/odbc/linux-mac/release-notes.md)  

