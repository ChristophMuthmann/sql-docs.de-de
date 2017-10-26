---
title: "Anzeigen oder Ändern der Eigenschaften einer Richtlinie der richtlinienbasierten Verwaltung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 485dca1df0b2d62fb71b1c51b86fe30e449b7ccf
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>Anzeigen oder Ändern der Eigenschaften einer Richtlinie der richtlinienbasierten Verwaltung
  In diesem Thema wird beschrieben, wie Sie die Eigenschaften einer Richtlinie der richtlinienbasierten Verwaltung mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)]ändern.  
  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>So zeigen Sie die Eigenschaften aller Richtlinien für ein Objekt an  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, ein Serverobjekt, eine Datenbank oder ein Datenbankobjekt, zeigen Sie auf **Richtlinien** , und wählen Sie dann **Anzeigen**aus. Weitere Informationen zu den verfügbaren Optionen im Dialogfeld **Richtlinien anzeigen –***object_name* finden Sie unter [View Policies Dialog Box](../../relational-databases/policy-based-management/view-policies-dialog-box.md).  
  
2.  Wenn Sie fertig sind, klicken Sie auf **Schließen**.  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>So zeigen Sie die Eigenschaften einer bestimmten Richtlinie an bzw. ändern sie  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, der die Richtlinie der richtlinienbasierten Verwaltung enthält, die Sie anzeigen oder ändern möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Verwaltung** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um **Richtlinienverwaltung**zu erweitern.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Richtlinien** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf die Richtlinie, die Sie anzeigen oder ändern möchten, und wählen Sie **Eigenschaften**aus. Weitere Informationen zu den verfügbaren Optionen im Dialogfeld **Richtlinie öffnen –***policy_name* finden Sie unter [Create New Policy or Open Policy Dialog Box, General Page](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) und [Create New Policy or Open Policy Dialog Box, Description Page](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
6.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-view-a-policys-properties"></a>So zeigen Sie die Eigenschaften einer Richtlinie an  
  
1.  Stellen **Sie im Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       execution_mode,  
       description,  
       is_enabled,  
       job_id  
    FROM syspolicy_policies;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [syspolicy_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-policies-transact-sql.md).  
  
  

