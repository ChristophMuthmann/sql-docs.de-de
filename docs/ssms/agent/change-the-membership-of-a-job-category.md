---
title: "Ändern der Mitgliedschaft einer Auftragskategorie | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0fb956f7cd8fa5673cce4a3a437879d57ac8b280
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie die Mitgliedschaft der Auftragskategorie in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] oder SQL Server Management Objects ändern können.  
  
Auftragskategorien helfen Ihnen dabei, Ihre Aufträge zum einfachen Filtern und Gruppieren zu organisieren. Sie können eigene Auftragskategorien erstellen. Zudem können Sie die Mitgliedschaft von Microsoft SQL Server-Agent-Aufträgen in Auftragskategorien ändern.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So ändern Sie die Mitgliedschaft einer Auftragskategorie mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>So ändern Sie die Mitgliedschaft einer Auftragskategorie  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, auf dem Sie eine Auftragskategorie bearbeiten möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Aufträge** , und wählen Sie **Auftragskategorien verwalten**aus.  
  
4.  Wählen Sie im Dialogfeld **Auftragskategorien verwalten -***Servername* die Auftragskategorie aus, die Sie bearbeiten möchten, und klicken Sie dann auf **Aufträge anzeigen**.  
  
5.  Aktivieren Sie das Kontrollkästchen **Alle Aufträge anzeigen** .  
  
6.  Um der Kategorie einen Auftrag hinzuzufügen, aktivieren Sie im Hauptraster in der **Select** -Spalte das Kontrollkästchen, das dem Auftrag entspricht. Um einen Auftrag aus der Kategorie zu entfernen, deaktivieren Sie das Kontrollkästchen. Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
7.  Schließen Sie das Dialogfeld **Auftragskategorien verwalten -***Servername* .  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>So ändern Sie die Mitgliedschaft einer Auftragskategorie  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_update_job (Transact-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623).  
  
## <a name="SMO"></a>Verwendung von SQL Server Management Objects  
**So ändern Sie die Mitgliedschaft einer Auftragskategorie**  
  
Verwenden Sie die **JobCategory** -Klasse, indem Sie eine von Ihnen ausgewählte Programmiersprache, z. B. Visual Basic, Visual C# oder PowerShell verwenden.  
  
