---
title: "Löschen von Sichten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dropping views
- deleting views
- views [SQL Server], deleting
- removing views
ms.assetid: 6823c7f8-06ca-4bda-8482-7092f03d52a0
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c869b1e4ba7cc992687baa3236c96d25b0e63e8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="delete-views"></a>Löschen von Sichten
  Sie können Sichten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] löschen, indem Sie Folgendes verwenden: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So löschen Sie eine Sicht aus einer Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie eine Sicht löschen, werden die Definition der Sicht sowie weitere Informationen zur Sicht aus dem Systemkatalog entfernt. Alle Berechtigungen für die Sicht werden ebenfalls gelöscht.  
  
-   Eine mithilfe von `DROP TABLE` gelöschte Sicht in einer Tabelle muss explizit mit `DROP VIEW`gelöscht werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert entweder die ALTER-Berechtigung für SCHEMA oder die CONTROL-Berechtigung für OBJECT.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-delete-a-view-from-a-database"></a>So löschen Sie eine Sicht aus einer Datenbank  
  
1.  Erweitern Sie im **Objekt-Explorer**die Datenbank mit der Sicht, die Sie löschen möchten, und erweitern Sie dann den Ordner **Sichten** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Sicht, die Sie löschen möchten, und klicken Sie auf **Löschen**.  
  
3.  Klicken Sie im Dialogfeld **Objekt löschen** auf **OK**.  
  
    > [!IMPORTANT]  
    >  Klicken Sie im Dialogfeld **Objekt löschen** auf **Abhängigkeiten anzeigen** , um das Dialogfeld *view_name***-Abhängigkeiten** zu öffnen. Es werden alle Objekte angezeigt, die von der Sicht abhängig sind, und alle Objekte, von denen die Sicht abhängig ist.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-delete-a-view-from-a-database"></a>So löschen Sie eine Sicht aus einer Datenbank  
  
1.  Stellen **Sie im Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im Beispiel wird die angegebene Sicht nur gelöscht, wenn die Sicht bereits vorhanden ist.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    IF OBJECT_ID ('HumanResources.EmployeeHireDate', 'V') IS NOT NULL  
    DROP VIEW HumanResources.EmployeeHireDate;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md).  
  
  

