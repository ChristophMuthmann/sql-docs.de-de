---
title: Erstellen eines benutzerdefinierten Ereignisses | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fc8bcece9829388988751effd53207eb2e72830
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="create-a-user-defined-event"></a>Erstellen eines benutzerdefinierten Ereignisses
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Sie können benutzerdefinierte Ereignisse erstellen, wenn Sie zusätzlich zu den von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] vordefinierten Ereignissen weitere Ereignisse überwachen möchten. Sie können allen benutzerdefinierten Ereignissen auch einen Schweregrad zuweisen.  
  
> [!NOTE]  
> In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]sollten Sie für die Meldungen aller benutzerdefinierten Ereignisse die Option **In Windows-Anwendungsereignisprotokoll schreiben** auswählen, um sicherzustellen, dass die Meldungen protokolliert werden. Benutzerdefinierte Meldungen mit einem Schweregrad kleiner als 19 werden standardmäßig nicht im [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows-Anwendungsereignisprotokoll protokolliert. Benutzerdefinierte Meldungen mit einem Schweregrad kleiner als 19 lösen daher keine Warnungen des SQL Server-Agents aus.  
  
Benutzerdefinierte Ereignisse müssen eine eindeutige Meldungsnummer besitzen. Die Meldungsnummern für ein benutzerdefiniertes Ereignis müssen größer als 50.000 sein. Meldungen für das Ereignis können in mehreren Sprachen definiert werden. Allerdings muss vor dem Hinzufügen von Meldungen in anderen Sprachen eine Fehlermeldung in **En-US** vorhanden sein.  
  
Wenn Sie eine mehrsprachige [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Umgebung verwalten, sollten Sie in allen unterstützten Sprachen benutzerdefinierte Meldungen erstellen. Wenn Sie beispielsweise eine neue Ereignismeldung erstellen, die sowohl auf einem deutschen als auch auf einem englischen Server verwendet werden soll, können Sie für beide dieselbe Meldungsnummer und denselben Schweregrad verwenden, müssen ihnen jedoch unterschiedliche Sprachen zuweisen.  
  
In den folgenden Aufgaben werden Informationen bereitgestellt, wie Sie benutzerdefinierte Ereignisse und die dazugehörigen Warnungen erstellen:  
  
**So erstellen Sie eine Warnung auf der Grundlage einer Meldungsnummer**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**So erstellen Sie eine Warnung auf der Grundlage von Schweregraden**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**So definieren Sie die Antwort auf eine Warnung**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
**So erstellen Sie eine benutzerdefinierte Ereignisfehlermeldung**  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/54746d30-f944-40e5-a707-f2d9be0fb9eb)  
  
**So ändern Sie eine benutzerdefinierte Ereignisfehlermeldung**  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/1b28f280-8ef9-48e9-bd99-ec14d79abaca)  
  
**So löschen Sie eine benutzerdefinierte Ereignisfehlermeldung**  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/17287a15-cdde-43d1-bb18-9f920bc15db8)  
  
**So deaktivieren oder reaktivieren Sie eine Warnung**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[sp_update_alert (Transact-SQL)](http://msdn.microsoft.com/en-us/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
