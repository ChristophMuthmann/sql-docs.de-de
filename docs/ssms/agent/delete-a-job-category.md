---
title: Löschen einer Auftragskategorie | Microsoft-Dokumentation
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
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7b31c79c27e0221cd306b024d7c6a5bd2c7aa589
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="delete-a-job-category"></a>Löschen einer Auftragskategorie
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie eine [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftragskategorie in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] oder SQL Server Management Objects löschen können.  
  
Auftragskategorien helfen Ihnen dabei, Ihre Aufträge zum einfachen Filtern und Gruppieren zu organisieren. Sie können z. B. alle Aufträge für die Datenbanksicherung in der Datenbankwartungskategorie organisieren.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So löschen Sie eine Auftragskategorie mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
Wenn Sie eine benutzerdefinierte Auftragskategorie löschen, werden sie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] aufgefordert, die Aufträge neu zuzuweisen, die in einer anderen Auftragskategorie zugewiesen wurden. Sie können nur benutzerdefinierte Auftragskategorien löschen.  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-delete-a-job-category"></a>So löschen Sie eine Auftragskategorie  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, auf dem Sie eine Auftragskategorie löschen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Aufträge** , und wählen Sie **Auftragskategorien verwalten**aus.  
  
4.  Klicken Sie im Dialogfeld *Auftragskategorien verwalten***Servername* auf die zu löschende Auftragskategorie.  
  
5.  Klicken Sie auf **Löschen**.  
  
6.  Klicken Sie im Dialogfeld **Auftragskategorien** auf **Ja**.  
  
7.  Schließen Sie das Dialogfeld **Auftragskategorien verwalten***Servername*.  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-delete-a-job-category"></a>So löschen Sie eine Auftragskategorie  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_delete_category (Transact-SQL)](http://msdn.microsoft.com/en-us/63ea7d0d-a567-456e-a778-bee99e21d16c).  
  
## <a name="SMO"></a>Verwendung von SQL Server Management Objects  
**So löschen Sie eine Auftragskategorie**  
  
Rufen Sie die **JobCategory** -Klasse auf, indem Sie eine von Ihnen ausgewählte Programmiersprache, z. B. Visual Basic, Visual C# oder PowerShell verwenden.  
  
