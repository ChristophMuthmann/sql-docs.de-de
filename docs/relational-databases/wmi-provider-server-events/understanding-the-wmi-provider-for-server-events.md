---
title: "Grundlegendes zum WMI-Anbieter für Serverereignisse | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- architecture [WMI]
- SQL Server Agent [WMI]
- WMI Provider for Server Events, about WMI Provider for Server Events
ms.assetid: 8fd7bd18-76d0-4b28-8fee-8ad861441ab2
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d68916b90c9b8312f02f75f5911a7871d350d4d5
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>Grundlegendes zum WMI-Anbieter für Serverereignisse
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Über den WMI-Anbieter für Serverereignisse können Sie Ereignisse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mithilfe von WMI (Windows Management Instrumentation) überwachen. Der Anbieter wandelt funktioniert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in ein verwaltetes WMI-Objekt. Jedes Ereignis, das eine ereignisbenachrichtigung in generieren kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können mithilfe dieses Anbieters von WMI verwendet werden. Darüber hinaus kann der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent als eine mit WMI interagierende Verwaltungsanwendung auf diese Ereignisse reagieren. Dadurch wird der durch den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent abgedeckte Ereignisbereich im Gegensatz zu früheren Versionen erweitert.  
  
 Verwaltungsanwendungen wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent erreichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ereignisse, indem Sie in der WMI-Anbieter für Serverereignisse WMI Query Language (WQL)-Anweisungen ausgeben. WQL ist eine vereinfachte Teilmenge von Structured Query Language (SQL) mit einigen WMI-spezifischen Erweiterungen. Bei Verwendung von WQL ruft eine Anwendung einen Ereignistyp für eine bestimmte Datenbank oder ein bestimmtes Datenbankobjekt ab. Der WMI-Anbieter für Serverereignisse übersetzt die Abfrage in eine Ereignisbenachrichtigung und erstellt dadurch auf effektive Weise eine Ereignisbenachrichtigung in der Zieldatenbank. Weitere Informationen zur Funktionsweise von ereignisbenachrichtigungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [WMI Provider for Server Ereignisse Concepts](http://technet.microsoft.com/library/ms180560.aspx). Die Ereignisse, die abgefragt werden können, sind in aufgeführt [WMI-Anbieter für Server Events-Ereignisklassen und Eigenschaften](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).  
  
 Wenn ein Ereignis auftritt, das die Ereignisbenachrichtigungsfunktion zum Senden einer Meldung veranlasst, wird die Benachrichtigung an einen vordefinierten Zieldienst in **msdb** mit dem Namen **SQL/Notifications/ProcessWMIEventProviderNotification/v1.0**übermittelt. Der Zieldienst fügt das Ereignis in eine vordefinierte Warteschlange in **msdb** ein. Ihr Name ist **WMIEventProviderNotificationQueue**. (Sowohl der Dienst als auch die Warteschlange werden vom Anbieter beim Herstellen der ersten Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dynamisch erstellt.) Der Anbieter liest die Ereignisdaten aus dieser Warteschlange, wandelt sie in MOF-Daten (Managed Object Format) um und gibt sie dann an die Anwendung zurück. Die folgende Abbildung veranschaulicht diesen Prozess:  
  
 ![Flussdiagramm des WMI-Anbieters für Serverereignisse](../../relational-databases/wmi-provider-server-events/media/wmi-provider-functional-spec.gif "Flussdiagramm des WMI-Anbieters für Serverereignisse")  
  
 Betrachten Sie beispielsweise folgende WQL-Abfrage:  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS  
WHERE DatabaseName = 'AdventureWorks'  
```  
  
 Als Reaktion auf diese Abfrage erstellt der WMI-Anbieter für Serverereignisse die entsprechende Ereignisbenachrichtigung in der Zieldatenbank:  
  
```  
USE AdventureWorks ;  
GO  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE  
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',   
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 In diesem Beispiel ist `SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Bezeichner, der aus dem Präfix `SQLWEP_` und einer GUID besteht. `SQLWEP` erstellt eine neue GUID für jeden Bezeichner. Der Wert `A7E5521A-1CA6-4741-865D-826F804E5135` in der `TO SERVICE` -Klausel ist der GUID, der die Broker-Instanz in der **msdb** -Datenbank identifiziert.  
  
 Weitere Informationen zur Arbeit mit WQL finden Sie unter [Verwenden von WQL mit dem WMI-Anbieter für Serverereignisse](http://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Verwaltungsanwendungen verweisen den WMI-Anbieter für Serverereignisse an eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch Herstellen einer Verbindung mit einem WMI-Namespace, der vom Anbieter definiert ist. Der WMI-Dienst ordnet der Anbieter-DLL Sqlwep.dll diesen Namespace zu und lädt sie in den Arbeitsspeicher. Der Anbieter verwaltet einen WMI-Namespace für Serverereignisse für jede Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und das Format lautet: \\ \\.\\ *Root*\Microsoft\SqlServer\ServerEvents\\*Instance_name*, wobei *Instance_name* lautet standardmäßig MSSQLSERVER. Weitere Informationen zum Herstellen einer Verbindung mit einem WMI-Namespace für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [Verwenden von WQL mit dem WMI-Anbieter für Serverereignisse](http://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Die Anbieter-DLL Sqlwep.dll geladen wird nur ein Mal in den WMI-Hostdienst des Betriebssystems des Servers an, wie viele Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Server sind.  
  
 Ein Beispiel für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-verwaltungsanwendung, die den WMI-Anbieter für Serverereignisse, verwendet finden Sie unter [Beispiel: Erstellen einer SQL Server-Agent-Warnung mithilfe der WMI-Anbieter für Serverereignisse](http://technet.microsoft.com/library/ms186385.aspx). Ein Beispiel für eine Verwaltungsanwendung, die den WMI-Anbieter für Serverereignisse in verwaltetem Code verwendet, finden Sie unter [Beispiel: Verwenden des WMI-Ereignisanbieters in verwaltetem Code](http://technet.microsoft.com/library/ms179315.aspx). Weitere Informationen finden Sie auch über WMI in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="see-also"></a>Siehe auch  
 [Konzepte des WMI-Anbieters für Serverereignisse](http://technet.microsoft.com/library/ms180560.aspx)  
  
  
