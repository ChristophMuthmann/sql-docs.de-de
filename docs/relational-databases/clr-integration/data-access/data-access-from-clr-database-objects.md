---
title: Datenzugriff von CLR-Datenbankobjekten | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
caps.latest.revision: 41
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34a3fba5d3026601994d8c258ea35b87cbf5d4bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="data-access-from-clr-database-objects"></a>Data Access from CLR Database Objects
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Eine Routine der common Language Runtime (CLR) kann problemlos in der Instanz von gespeicherte Daten zugreifen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in dem er, sowie Daten in Remoteinstanzen gespeichert ausgeführt wird. Auf welche Daten die Routine zugreifen kann, wird durch den Benutzerkontext bestimmt, in dem der Code ausgeführt wird. Zugriff auf Daten aus einem CLR-Datenbankobjekt mithilfe der .NET Framework-Datenanbieter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], auch als bezeichnet **SqlClient**. Dies ist der gleiche Anbieter, den Entwickler zum Zugriff von verwalteten Clientanwendungen und Anwendungen der mittleren Ebene auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Daten verwenden. Aus diesem Grund können Sie Ihr Wissen von ADO.NET nutzen und **SqlClient** in Client-und der mittleren Ebene.  
  
> [!NOTE]  
>  Benutzerdefinierten Typmethoden und benutzerdefinierten Funktionen wird nicht ermöglicht, standardmäßig auf Daten zuzugreifen. Müssen Sie festlegen der **DataAccess** Eigenschaft **SqlMethodAttribute** oder **"SqlFunctionAttribute"** auf **DataAccessKind.Read** aktivieren Nur-Lese Datenzugriff über Methoden für den benutzerdefinierten Typ (UDT) oder benutzerdefinierte Funktionen. Datenänderungsvorgänge von UDTs oder benutzerdefinierten Funktionen ausgehend sind nicht zulässig. Ein solcher Versuch löst zur Ausführungszeit eine Ausnahme aus.  
  
 In diesem Abschnitt werden nur die spezifischen Unterschiede der Funktionen und Verhaltensweisen beim Datenzugriff von einem CLR-Datenbankobjekt ausgehend beschrieben. Weitere Informationen zu Funktionen und Funktionalität von ADO.NET finden Sie in der ADO.NET-Dokumentation im .NET Framework SDK.  
  
 In der folgenden Tabelle sind die Themen dieses Abschnitts aufgeführt.  
  
 [Kontextverbindung](../../../relational-databases/clr-integration/data-access/context-connection.md)  
 Beschreibt die Kontextverbindung zu SQL Server.  
  
 [Identitätswechsel und Anmeldeinformationen für Verbindungen](../../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
 Beschreibt die Annahme der Identität von Verbindungen und Verbindungsanmeldeinformationen.  
  
 [Von SQL Server verwendete prozessinterne spezifische Erweiterungen für ADO.NET](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 Erläutert die prozessinternen spezifischen **SqlPipe**, **SqlContext**, **SqlTriggerContext**, und **SqlDataRecord** Objekte.  
  
 [CLR-Integration und Transaktionen](../../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
 Beschreibt wie das neue vom System.Transactions-Namespace bereitgestellte Transaktionsframework in ADO.NET und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-CLRIntegration einbezogen wird.  
  
 [XML-Serialisierung auf Grundlage von CLR-Datenbankobjekten](http://msdn.microsoft.com/library/ac84339b-9384-4710-bebc-01607864a344)  
 Erklärt, wie XML-Serialisierungsszenarien von CLR-Datenbankobjekten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aktiviert werden.  
  
  
