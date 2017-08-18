---
title: Bearbeiten eines Operators | Microsoft-Dokumentation
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
- SQL Server Agent jobs, operators
- modifying operators
- jobs [SQL Server Agent], operators
- operators (users) [Database Engine], modifying with Management Studio
ms.assetid: b2ba2168-ca0b-4b59-9007-4e1e4c30679e
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b8628cf736650c53493501777f79f970ff864209
ms.contentlocale: de-de
ms.lasthandoff: 08/18/2017

---
# <a name="edit-an-operator"></a>Bearbeiten eines Operators
In diesem Thema wird beschrieben, wie Sie für Operatoren die Möglichkeit zum Empfangen von Benachrichtigungen und deren E-Mail-, Pager- und NET SEND-Adressen in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]bearbeiten.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So bearbeiten Sie einen Operator mit**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   Die Pager- und **net send** -Optionen werden in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nicht mehr im [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Vermeiden Sie die Verwendung dieser Funktionen bei neuen Entwicklungsarbeiten, und planen Sie die Änderung von Anwendungen, die diese Funktionen zurzeit verwenden.  
  
-   Beachten Sie, dass E-Mail- und Pagerbenachrichtigungen an Operatoren nur versendet werden können, wenn der SQL Server-Agent für die Verwendung von Datenbank-E-Mail konfiguriert ist. Weitere Informationen finden Sie unter [Zuweisen von Warnungen zu einem Operator](http://msdn.microsoft.com/library/ms190038.aspx).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] können Aufträge problemlos mithilfe einer grafischen Oberfläche verwaltet werden. Dies ist die empfohlene Vorgehensweise für die Erstellung und Verwaltung der Auftragsinfrastruktur.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Nur Mitglieder der festen Serverrolle **sysadmin** können Operatoren bearbeiten.  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-edit-an-operator"></a>So bearbeiten Sie einen Operator  
  
1.  Klicken Sie im Objekt-Explorer ****auf das Pluszeichen, um den Server zu erweitern, der den Operator enthält, den Sie bearbeiten möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um den Ordner **Operatoren** zu erweitern.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Operator, den Sie bearbeiten möchten, und wählen Sie **Eigenschaften**aus.  
  
    Weitere Informationen zu den verfügbaren Optionen im Dialogfeld *Operatorname***Eigenschaften** finden Sie unter:  
  
    -   [Operatoreigenschaften – Neuer Operator &#40;Seite „Allgemein“&#41;](../../ssms/agent/operator-properties-new-operator-general-page.md)  
  
    -   [Operatoreigenschaften – Neuer Operator &#40;Seite „Benachrichtigungen“&#41;](../../ssms/agent/operator-properties-new-operator-notifications-page.md)  
  
    -   [Operatoreigenschaften &#40;Seite „Verlauf“&#41;](../../ssms/agent/operator-properties-history-page.md)  
  
5.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-edit-an-operator"></a>So bearbeiten Sie einen Operator  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- updates the operator status to enabled, and sets the days   
    -- (from Monday through Friday, from 8 A.M. through 5 P.M.)
    --  when the operator can be paged.   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'François Ajenstat',  
        @enabled = 1,  
        @email_address = N'françoisa',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 64 ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_update_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/231750a6-4828-4d03-afe6-b91d38c42ed3).  
  

