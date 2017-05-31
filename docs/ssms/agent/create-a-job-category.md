---
title: Erstellen einer Auftragskategorie | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 960865a8bb263a2089dc51a75304e3e6e40b85bf
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-job-category"></a>Erstellen einer Auftragskategorie
In diesem Thema wird beschrieben, wie Sie eine Auftragskategorie in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Management Objects erstellen können.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent stellt integrierte Auftragskategorien bereit, denen Aufträge zugewiesen werden können. Sie können auch eine Auftragskategorie erstellen und diesen Aufträge zuweisen. Auftragskategorien helfen Ihnen dabei, Ihre Aufträge zum einfachen Filtern und Gruppieren zu organisieren. Sie können z. B. alle Aufträge für die Datenbanksicherung in der Datenbankwartungskategorie organisieren. Sie können zudem eigene Auftragskategorien erstellen.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So erstellen Sie eine Auftragskategorie mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
Multiserverkategorien sind nur auf einem Masterserver vorhanden. Auf einem Masterserver ist nur eine Standardauftragskategorie verfügbar: [**Nicht kategorisiert (Multiserver)**]. Beim Herunterladen eines Multiserverauftrags wird seine Kategorie auf dem Zielserver in **Aufträge vom MSX** geändert.  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-a-job-category"></a>So erstellen Sie eine Auftragskategorie  
  
1.  Klicken Sie im Objekt-Explorer **** auf das Pluszeichen, um den Server zu erweitern, auf dem Sie eine Auftragskategorie erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Aufträge** , und wählen Sie **Auftragskategorien verwalten**aus.  
  
4.  Klicken Sie im Dialogfeld **Auftragskategorien verwalten -***Servername* auf **Hinzufügen**.  
  
5.  Geben Sie im neuen Dialogfeld **Name** einen Namen für die neue Auftragskategorie ein.  
  
6.  Aktivieren Sie das Kontrollkästchen **Alle Aufträge anzeigen** . Wählen Sie für die neue Kategorie mindestens einen Auftrag aus, indem Sie die Kontrollkästchen der entsprechenden Aufträge aktivieren.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie im Dialogfeld **Auftragskategorien verwalten -***Servername* auf **Aktualisieren** , um sicherzustellen, dass die neue Auftragskategorie aktiv ist. Schließen Sie das Dialogfeld, wenn alles normal aussieht.  
  
Weitere Informationen zu diesen Dialogfeldern finden Sie unter [Auftragskategorien – Auftragskategorien verwalten](../../ssms/agent/job-categories-manage-job-categories.md) und [Eigenschaften für neue Auftragskategorie – Neue Auftragskategorie](../../ssms/agent/job-categories-properties-new-job-category.md).  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-create-a-job-category"></a>So erstellen Sie eine Auftragskategorie  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_add_category (Transact-SQL)](http://msdn.microsoft.com/en-us/6cca32cd-d941-4378-aed6-a7c90cb7520a).  
  
## <a name="SMO"></a>Verwendung von SQL Server Management Objects  
**So erstellen Sie eine Auftragskategorie**  
  
Rufen Sie die **JobCategory** -Klasse auf, indem Sie eine von Ihnen ausgewählte Programmiersprache, z. B. Visual Basic, Visual C# oder PowerShell verwenden. Beispielcode hierzu finden Sie unter [Planen von automatischen, administrativen Tasks im SQL Server-Agent](http://msdn.microsoft.com/en-us/900242ad-d6a2-48e9-8a1b-f0eea4413c16).  
  

