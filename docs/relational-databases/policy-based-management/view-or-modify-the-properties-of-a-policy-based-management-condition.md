---
title: "Anzeigen oder Ändern der Eigenschaften einer Bedingung der richtlinienbasierten Verwaltung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cac543a91282a6329e44c297d56a9550b18f4681
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>Anzeigen oder Ändern der Eigenschaften einer Bedingung der richtlinienbasierten Verwaltung
  In diesem Thema wird beschrieben, wie Sie die Eigenschaften einer Bedingung der richtlinienbasierten Verwaltung mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)]ändern.  
  

  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  

  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>So zeigen Sie die Eigenschaften einer Bedingung an bzw. ändern sie  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, der die Bedingungen enthält, die Sie anzeigen oder ändern möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Verwaltung** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um **Richtlinienverwaltung**zu erweitern.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Bedingungen** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf die Bedingung, die Sie anzeigen oder bearbeiten möchten, und wählen Sie **Eigenschaften** aus. Weitere Informationen zu den Optionen im Dialogfeld **Bedingung öffnen** – *Bedingungsname* finden Sie unter [Dialogfeld 'Neue Bedingung erstellen' oder 'Bedingung öffnen', Seite 'Allgemein'](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md), [Dialogfeld 'Bedingung öffnen', Seite 'Abhängige Richtlinien'](../../relational-databases/policy-based-management/open-condition-dialog-box-dependent-policies-page.md), [Dialogfeld 'Neue Bedingung erstellen' oder 'Bedingung öffnen', Seite 'Beschreibung'](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-description-page.md) und [Dialogfeld 'Erweiterte Bearbeitung &#40;Bedingung&#41;'](../../relational-databases/policy-based-management/advanced-edit-condition-dialog-box.md).  
  
6.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-view-a-conditions-properties"></a>So zeigen Sie die Eigenschaften einer Bedingung an  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 Weitere Informationen finden Sie unter [yspolicy_conditions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md).  
  
  

