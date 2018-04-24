---
title: Festlegen eines SQL Server-Alias für den SQL Server-Agent-Dienst | Microsoft-Dokumentation
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
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2fac6b98904de3ae4be485dc36c6a6762e58931d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ein [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Alias für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent festgelegt wird, der für das Herstellen einer Verbindung mit [!INCLUDE[ssDE](../../includes/ssde_md.md)] verwendet wird. Standardmäßig stellt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] über Named Pipes mithilfe dynamischer Servernamen her, die keine zusätzliche Clientkonfiguration erfordern. Einen Serververbindungsalias müssen Sie nur konfigurieren, wenn Sie nicht den standardmäßigen Netzwerktransport verwenden oder wenn Sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] herstellen, die an einer alternativen Named Pipe lauscht.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   [So legen Sie einen SQL Server-Alias für den für den SQL Server-Agent-Dienst mithilfe von SQL Server Management Studio fest](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent wird nur dann ordnungsgemäß ausgeführt, wenn Sie einen Aliasnamen auswählen, der auf die lokale Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Knoten wird nur im Objekt-Explorer angezeigt, wenn Sie die Berechtigung besitzen, ihn zu verwenden.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent muss zur Verwendung der Anmeldeinformationen eines Kontos konfiguriert werden, das Mitglied der festen Serverrolle **sysadmin** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ist, um seine Funktionen ausführen zu können. Das Konto muss über die folgenden Windows-Berechtigungen verfügen:  
  
-   Anmelden als Dienst (SeServiceLogonRight)  
  
-   Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)  
  
-   Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)  
  
-   Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)  
  
Weitere Informationen zu den Windows-Berechtigungen, die für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstkonto erforderlich sind, finden Sie unter [Auswählen eines Kontos für den SQL Server-Agent-Dienst](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) und [Einrichten von Windows-Dienstkonten](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>So legen Sie einen SQL Server-Alias für den SQL Server-Agent-Dienst fest  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] her, und erweitern Sie diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften des SQL Server-Agents***Servername* unter **Seite auswählen** auf **Verbindung**, und  
  
4.  geben Sie im Feld **Aliasname für den lokalen Hostserver** den Alias des Servers ein, mit dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent verbunden werden soll.  
  
5.  Klicken Sie auf **OK**.  
  
