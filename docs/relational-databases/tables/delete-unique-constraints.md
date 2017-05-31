---
title: "Löschen von Unique-Einschränkungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing constraints
- UNIQUE constraints [SQL Server], deleting
- constraints [SQL Server], deleting
- deleting constraints
- constraints [SQL Server], unique
ms.assetid: 71e563fc-f5d7-4c2e-a42f-f0695a831f32
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 49169c8ac7e47e6b9d9efff891810c68372aa6c5
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="delete-unique-constraints"></a>Löschen von Unique-Einschränkungen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Sie können mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine UNIQUE-Einschränkung in [!INCLUDE[tsql](../../includes/tsql-md.md)]löschen. Wenn eine Unique-Einschränkung gelöscht wird, werden die Forderung nach Eindeutigkeit für die Werte, die in die Spalte oder Spaltenkombination im Einschränkungsausdruck eingegeben werden, und der zugehörige eindeutige index entfernt.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So löschen Sie eine Unique-Einschränkung mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-delete-a-unique-constraint-using-object-explorer"></a>So löschen Sie eine UNIQUE-Einschränkung im Objekt-Explorer  
  
1.  Erweitern Sie im Objekt-Explorer die Tabelle, die die eindeutige Einschränkung enthält, und dann erweitern Sie **Einschränkungen**.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Schlüssel, und klicken Sie dann auf **Löschen**.  
  
3.  Überprüfen Sie im Dialogfeld **Objekt löschen** , ob der richtige Schlüssel angegeben worden ist, und klicken Sie auf **OK**.  
  
#### <a name="to-delete-a-unique-constraint-using-table-designer"></a>So löschen Sie eine eindeutige Einschränkung mit dem Tabellen-Designer  
  
1.  Klicken Sie im ****Objekt-Explorer mit der rechten Maustaste auf die Tabelle mit der UNIQUE-Einschränkung, und klicken Sie dann auf **Entwerfen**.  
  
2.  Klicken Sie im Menü **Tabellen-Designer** auf **Indizes/Schlüssel**.  
  
3.  Wählen Sie im Dialogfeld **Indizes/Schlüssel** in der Liste **Ausgewählter Primärschlüssel/eindeutiger Schlüssel und Index** den eindeutigen Schlüssel aus.  
  
4.  Klicken Sie auf **Löschen**.  
  
5.  Klicken Sie im Menü **Datei** auf **Speichern** *table name*.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-delete-a-unique-constraint"></a>So löschen Sie eine Unique-Einschränkung  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Return the name of unique constraint.  
    SELECT name  
    FROM sys.objects  
    WHERE type = 'UQ' AND OBJECT_NAME(parent_object_id) = N' DocExc';  
    GO  
    -- Delete the unique constraint.  
    ALTER TABLE dbo.DocExc   
    DROP CONSTRAINT UNQ_ColumnB_DocExc;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) und [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  

