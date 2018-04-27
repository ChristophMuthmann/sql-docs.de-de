---
title: Vollziehen des Austritts eines Zielservers aus einem Masterserver | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f9b437246d26bb4e44cfd47fe4e8a02f90d93930
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="defect-a-target-server-from-a-master-server"></a>Vollziehen des Austritts eines Zielservers aus einem Masterserver
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie den Austritt eines Zielservers aus einem Masterserver in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] oder SQL Server Management Objects (SMO) vollziehen. Führen Sie die folgenden Schritte auf dem Zielserver aus.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **Vollziehen des Austritts eines Zielservers mit:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SMO](#PowerShellProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Zum Ausführen dieser gespeicherten Prozedur muss ein Benutzer Mitglied der festen Serverrolle **sysadmin** sein.  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>So tragen Sie bei einem Masterserver einen Zielserver aus  
  
1.  Erweitern Sie in **Objekt-Explorer**einen Server, der als Zielserver konfiguriert ist.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, zeigen Sie auf **Multiserveradministration**, und klicken Sie dann auf **Austragen**.  
  
3.  Klicken Sie auf **Ja** , um zu bestätigen, dass Sie diesen Zielserver bei einem Masterserver austragen möchten.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>So tragen Sie bei einem Masterserver einen Zielserver aus  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde_md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
```  
sp_msx_defect ;  
```  
  
Weitere Informationen finden Sie unter [sp_msx_defect (Transact-SQL)](http://msdn.microsoft.com/en-us/0dfd963a-3bc5-4b58-94f7-aec976da2883).  
  
## <a name="PowerShellProcedure"></a>Verwendung von SQL Server Management Objects (SMO)  
Verwenden Sie **MsxDefect Method**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Erstellen einer Multiserverumgebung](../../ssms/agent/create-a-multiserver-environment.md)  
[Automatisierte Verwaltung in einem Unternehmen](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Vollziehen des Austritts mehrerer Zielserver aus einem Masterserver](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  
