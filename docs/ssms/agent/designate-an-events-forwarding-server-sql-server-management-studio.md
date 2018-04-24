---
title: Bestimmen eines Ereignisweiterleitungsserver | Microsoft-Dokumentation
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
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6a204a92259fa97fdb5324353ed3266ed3389567
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designate an Events Forwarding Server (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie einen Server bestimmen, auf den von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Ereignisse in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] . Ereignisweiterleitung gilt für Ereignisse, die zwischen Servern weitergeleitet werden, und nicht für Ereignisse, die zwischen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] weitergeleitet werden, die auf einem einzelnen Computer gehostet werden. Beachten Sie außerdem, dass zum Empfangen weitergeleiteter Ereignisse der Warnungsverwaltungsserver eine Standardinstanz von SQL Server sein muss.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So bestimmen Sie einen Ereignisweiterleitungsserver mit**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>So bestimmen Sie einen Ereignisweiterleitungsserver  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, von dem aus Sie Ereignisse an andere Server weiterleiten möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent** , und wählen Sie **Eigenschaften**aus.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften des SQL Server-Agents >***Servername* unter **Seite auswählen** auf **Erweitert**.  
  
4.  Aktivieren Sie unter **SQL Server-Ereignisweiterleitung**das Kontrollkästchen **Ereignisse an anderen Server weiterleiten** .  
  
5.  Klicken Sie in der Liste **Server** auf einen Server, und wählen Sie dann unter **Ereignisse**eine der folgenden Aktionen aus:  
  
    -   Klicken Sie auf **Ereignisse ohne Behandlung** , um nur Ereignisse weiterzuleiten, die noch nicht von lokalen Warnungen verarbeitet wurden.  
  
    -   Klicken Sie auf **Alle Ereignisse** , um alle Ereignisse unabhängig davon weiterzuleiten, ob sie von lokalen Warnungen verarbeitet wurden.  
  
6.  Klicken Sie in der Liste **Bei diesem Schweregrad des Ereignisses oder darüber** auf den Schweregrad, bei dem Ereignisse an den ausgewählten Server weitergeleitet werden.  
  
7.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
