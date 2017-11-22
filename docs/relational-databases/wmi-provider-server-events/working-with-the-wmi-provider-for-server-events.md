---
title: "Arbeiten mit WMI-Anbieter für Serverereignisse | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- event notifications [WMI]
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- Service Broker [WMI]
- WMI Provider for Server Events, connection strings
- WMI Provider for Server Events, Service Broker
- notifications [WMI]
- WMI Provider for Server Events, security
ms.assetid: cd974b3b-2309-4a20-b9be-7cfc93fc4389
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f1c5addea8d03f49ff2142deee06069ff0b1769
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="working-with-the-wmi-provider-for-server-events"></a>Verwenden des WMI-Anbieters für Serverereignisse
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Dieses Thema enthält Richtlinien, die Sie vor dem Programmieren mit dem WMI-Anbieter für Serverereignisse berücksichtigen sollten.  
  
## <a name="enabling-service-broker"></a>Aktivieren von Service Broker  
 Der WMI-Anbieter für Serverereignisse übersetzt WQL-Abfragen für Ereignisse in Ereignisbenachrichtigungen in der Zieldatenbank. Kenntnisse darüber, wie Ereignisbenachrichtigungen funktionieren, können bei der Programmierung mit dem Anbieter hilfreich sein. Weitere Informationen finden Sie unter [Konzepte des WMI-Anbieters für Serverereignisse](http://technet.microsoft.com/library/ms180560.aspx).  
  
 Da die vom WMI-Anbieter erstellten Ereignisbenachrichtigungen Meldungen zu Serverereignissen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senden, muss dieser Dienst aktiviert sein, wenn die Ereignisse generiert werden. Wenn Ihr Programm Ereignisse in einer Serverinstanz abfragt, muss der [!INCLUDE[ssSB](../../includes/sssb-md.md)] dieser Instanz in msdb aktiviert sein, da dies der Speicherort des [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Zieldiensts (mit dem Namen SQL/Notifications/ProcessWMIEventProviderNotification/v1.0) ist, der vom Anbieter erstellt wird. Wenn Ihr Programm Ereignisse in einer Datenbank oder in einem bestimmten Datenbankobjekt abfragt, muss der [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Dienst in dieser Zieldatenbank aktiviert sein. Wenn der entsprechende [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Dienst nach dem Bereitstellen der Anwendung nicht aktiviert wird, werden die von der zugrundeliegenden Ereignisbenachrichtigung generierten Ereignisse an die Warteschlange des von der Ereignisbenachrichtigung verwendeten Diensts gesendet, aber erst nach der Aktivierung des [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Diensts an die WMI-Verwaltungsanwendung zurückgegeben.  
  
 Mit der folgenden Abfrage wird bestimmt, welche Service Broker auf einer Serverinstanz aktiviert werden, und die GUID der Broker-Instanz wird festgelegt:  
  
```  
SELECT name, is_broker_enabled, service_broker_guid FROM sys.databases;  
```  
  
 Die Service Broker-GUID von msdb ist besonders interessant, da dies der Speicherort des Zieldiensts des Anbieters ist.  
  
 So aktivieren Sie [!INCLUDE[ssSB](../../includes/sssb-md.md)] verwenden Sie in einer Datenbank die ENABLE_BROKER SET-Option von der [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) Anweisung.  
  
## <a name="specifying-a-connection-string"></a>Angeben einer Verbindungszeichenfolge  
 Anwendungen leiten den WMI-Anbieter für Serverereignisse an eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weiter, indem sie eine Verbindung mit einem vom Anbieter definierten WMI-Namespace herstellen. Der WMI-Dienst ordnet der Anbieter-DLL Sqlwep.dll diesen Namespace zu und lädt sie in den Arbeitsspeicher. Jede Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügt über einen eigenen WMI-Namespace, dessen Standard: \\ \\.\\ *Root*\Microsoft\SqlServer\ServerEvents\\*Instance_name*. *Instanzname* in einer Standardinstallation von standardmäßig MSSQLSERVER [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions-and-server-authentication"></a>Berechtigungen und Serverauthentifizierung  
 Um auf den WMI-Anbieter für Serverereignisse zugreifen zu können, muss der Client, von dem eine WMI-Verwaltungsanwendung stammt, dem Windows-authentifizierten Benutzer- oder Gruppennamen in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entsprechen, die in der Verbindungszeichenfolge der Anwendung angegeben ist.  
  
## <a name="permissions-and-event-notification-scope"></a>Berechtigungen und Bereich der Ereignisbenachrichtigungen  
 Der WMI-Anbieter für Serverereignisse übersetzt WQL-Abfragen in Ereignisbenachrichtigungen in der Zieldatenbank. Daher muss die aufrufende Anwendung über die erforderlichen Mindestberechtigungen für den Zugriff auf den Anbieter sowie über die richtigen Berechtigungen in der Datenbank zum Erstellen der erforderlichen Ereignisbenachrichtigungen verfügen. Die folgenden Berechtigungen sind erforderlich:  
  
-   Zum Erstellen einer Ereignisbenachrichtigung, die sich auf die Datenbank bezieht, ist mindestens die CREATE DATABASE DDL EVENT NOTIFICATION-Berechtigung in der aktuellen Datenbank erforderlich.  
  
-   Zum Erstellen einer Ereignisbenachrichtigung für eine DDL-Anweisung, die sich auf den Server bezieht, ist mindestens die CREATE DDL EVENT NOTIFICATION-Berechtigung auf dem Server erforderlich.  
  
-   Zum Erstellen einer Ereignisbenachrichtigung für ein Ablaufverfolgungsereignis ist mindestens die CREATE TRACE EVENT NOTIFICATION-Berechtigung auf dem Server erforderlich.  
  
-   Zum Erstellen einer Ereignisbenachrichtigung, die sich auf eine Warteschlange bezieht, ist mindestens die ALTER-Berechtigung für die Warteschlange erforderlich.  
  
 Informationen dazu, wie WQL-Abfragen zugewiesen sind, finden Sie unter [Verwenden von WQL mit dem WMI-Anbieter für Serverereignisse](http://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Betrachten Sie zur Darstellung des Bereichs eine WMI-Anbieteranwendung, die die folgende WQL-Abfrage enthält:  
  
```  
SELECT * FROM ALTER_TABLE  
WHERE DatabaseName = "AdventureWorks2012"   
    AND SchemaName = "Person"  
    AND ObjectName = "Person"  
    AND ObjectType = "TABLE";  
```  
  
 Der WMI-Anbieter übersetzt diese Abfrage in eine Ereignisbenachrichtigung, die in der Datenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] erstellt wird. Das bedeutet, dass der Aufrufer über die erforderlichen Berechtigungen zum Erstellen einer Ereignisbenachrichtigung dieser Art, insbesondere über die CREATE DATABASE DDL EVENT NOTIFICATION-Berechtigung, in der Datenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] verfügen muss.  
  
 Wenn eine WQL-Abfrage eine auf der Serverebene zugewiesene Ereignisbenachrichtigung beispielsweise durch die Ausgabe der Abfrage SELECT * FROM ALTER_TABLE angibt, muss die aufrufende Anwendung über die Berechtigung CREATE DDL EVENT NOTIFICATION auf Serverebene verfügen. Serverbezogene Ereignisbenachrichtigungen werden in der master-Datenbank gespeichert. Sie können die [server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) Katalogsicht, um die zugehörigen Metadaten anzeigen.  
  
> [!NOTE]  
>  Der vom WMI-Anbieter (Server, Datenbank oder Objekt) erstellte Bereich der Ereignisbenachrichtigung ist letztlich von dem vom WMI-Anbieter verwendeten Ergebnis der Überprüfung der Berechtigungen abhängig. Dies wird durch die Berechtigungen des Benutzers, der den Anbieter aufruft, sowie durch die Überprüfung der abgefragten Datenbank bestimmt.  
>   
>  Im vorherigen Beispiel erstellt der Anbieter zunächst eine Ereignisbenachrichtigung, die sich auf die Datenbank bezieht (`ON DATABASE`). Wenn der Anbieter bestätigt, dass die Datenbank vorhanden ist und dass der Aufrufer über die erforderlichen Berechtigungen zum Erstellen einer Ereignisbenachrichtigung in der Datenbank verfügt, ist die Registrierung erfolgreich. Wenn die Registrierung nicht erfolgreich ist, erstellt der Anbieter eine Ereignisbenachrichtigung auf dem Server (`ON SERVER`). Wenn diese Registrierung erfolgreich ist, werden alle auf dem Server auftretenden `ALTER_TABLE`-Ereignisse vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess an den WMI-Dienstprozess gesendet. Der Anbieter filtert jedoch alle Ereignisse heraus, die nicht für die `AdventureWorks`-Datenbank bestimmt sind. Durch diesen Prozess wird der Netzwerkverkehr, der für den Bereich des Ereignisses erforderlich ist, möglicherweise erhöht. Mithilfe dieses Prozesses können Sie jedoch WQL-Abfragen bereits vor dem Erstellen von Datenbanken auf den Datenbanken registrieren und nach dem Erstellen der Datenbank Ereignisdaten empfangen und DDL-Aktivitäten starten.  
  
## <a name="permissions-and-message-verification"></a>Berechtigungen und Meldungsüberprüfung  
 Der WMI-Anbieter sendet keine Meldungen für Ereignisbenachrichtigungen, wenn die beiden folgenden Bedingungen zutreffen:  
  
-   Der Benutzer, der die Ereignisbenachrichtigung über den WMI-Anbieter erstellt hat, ist in der Datenbank nicht mehr vorhanden oder verfügt nicht mehr über die erforderliche Berechtigung zum Erstellen einer ähnlichen Ereignisbenachrichtigung.  
  
-   Die Ereignisbenachrichtigungen werden bei folgenden Ereignissen erstellt:  
  
    -   DROP_LOGIN  
  
    -   ALTER_LOGIN  
  
    -   DROP_USER  
  
    -   ALTER_USER  
  
    -   ADD_ROLE_MEMBER  
  
    -   DROP_ROLE_MEMBER  
  
    -   ADD_SERVER_ROLE_MEMBER  
  
    -   DROP_SERVER_ROLE_MEMBER  
  
    -   DENY oder REVOKE (Gilt nur für die Berechtigungen ALTER DATABASE, ALTER ANY DATABASE EVENT NOTIFICATION, CREATE DATABASE DDL EVENT NOTIFICATION, CONTROL SERVER, ALTER ANY EVENT NOTIFICATION, CREATE DDL EVENT NOTIFICATION oder CREATE TRACE EVENT NOTIFICATION.)  
  
## <a name="working-with-event-data-on-the-client-side"></a>Verwenden von Ereignisdaten auf der Clientseite  
 Nachdem der WMI-Anbieter für Serverereignisse die erforderliche ereignisbenachrichtigung in der Zieldatenbank erstellt sendet die ereignisbenachrichtigung Ereignisdaten an den Zieldienst in ' msdb ' mit dem Namen **SQL/Notifications/ProcessWMIEventProviderNotification /V1.0**. Der Zieldienst stellt das Ereignis in eine Warteschlange in **Msdb** mit der Bezeichnung **WMIEventProviderNotificationQueue**. (Der Dienst und die Warteschlange werden dynamisch erstellt vom Anbieter zunächst zum Verbindungsaufbau mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].) Der Anbieter liest die XML-Ereignisdaten aus dieser Warteschlange, wandelt sie in MOF-Daten (Managed Object Format) um und gibt sie dann an die Clientanwendung zurück. Die MOF-Daten bestehen aus den Eigenschaften des Ereignisses, das von der WQL-Abfrage als CIM-Classendefinition (Common Information Model) angefordert wird. Jede Eigenschaft verfügt über einen entsprechenden CIM-Typ. Z. B. die `SPID` Eigenschaft zurückgegeben wird, als CIM-Typ **Sint32**. Für jede Eigenschaft der CIM-Typen sind aufgeführt, unter jede Ereignisklasse in [WMI-Anbieter für Server Events-Ereignisklassen und Eigenschaften](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Konzepte des WMI-Anbieters für Serverereignisse](http://technet.microsoft.com/library/ms180560.aspx)  
  
  
