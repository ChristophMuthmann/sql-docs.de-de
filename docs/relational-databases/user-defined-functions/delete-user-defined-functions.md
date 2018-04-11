---
title: Löschen von benutzerdefinierten Funktionen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: udf
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-udf
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: db1d668a-23b7-4757-a9c5-1bd848ba7f6d
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3db20508f239f3b57d3793a254526ff6eb2b68b
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="delete-user-defined-functions"></a>Löschen von benutzerdefinierten Funktionen
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Sie können benutzerdefinierte Funktionen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] löschen mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So löschen Sie eine benutzerdefinierte Funktion mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Sie können die Funktion nicht löschen, wenn Transact-SQL-Funktionen oder -Sichten in der Datenbank vorhanden sind, die auf diese Funktion verweisen und mithilfe von SCHEMABINDING erstellt wurden, oder wenn berechnete Spalten, CHECK-Einschränkungen oder DEFAULT-Einschränkungen vorhanden sind, die auf die Funktion verweisen.  
  
-   Sie können die Funktion nicht löschen, wenn berechnete Spalten vorhanden sind, die auf diese Funktion verweisen und indiziert wurden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung im Schema, zu der die Funktion gehört, oder die CONTROL-Berechtigung für die Funktion.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-delete-a-user-defined-function"></a>So löschen Sie eine benutzerdefinierte Funktion  
  
1.  Klicken Sie neben der Datenbank, die die Funktion enthält, die Sie ändern möchten, auf das Pluszeichen.  
  
2.  Klicken Sie neben dem Ordner **Programmierbarkeit** auf das Pluszeichen.  
  
3.  Klicken Sie neben dem Ordner, der die Funktion enthält, die Sie ändern möchten, auf das Pluszeichen:  
  
    -   Table-valued Function  
  
    -   Skalarwertfunktion  
  
    -   Aggregatfunktion  
  
4.  Klicken Sie mit der rechten Maustaste auf die Funktion, die Sie löschen möchten, und klicken Sie dann auf **Löschen**.  
  
5.  Klicken Sie im Dialogfeld **Objekt löschen** auf **OK**.  
  
    > [!IMPORTANT]  
    >  Klicken Sie im Dialogfeld **Objekt löschen** auf **Abhängigkeiten anzeigen**, um das Dialogfeld *Funktionsname*-**Abhängigkeiten** zu öffnen. Es werden alle Objekte angezeigt, die von der Funktion abhängig sind, und alle Objekte, von denen die Funktion abhängig ist.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-delete-a-user-defined-function"></a>So löschen Sie eine benutzerdefinierte Funktion  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- creates function called “Sales.ufn_SalesByStore”  
    USE AdventureWorks2012;  
    GO  
    CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
    RETURNS TABLE  
    AS  
    RETURN   
    (  
        SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
        FROM Production.Product AS P   
        JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
        JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
        JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
        WHERE C.StoreID = @storeid  
        GROUP BY P.ProductID, P.Name  
    );  
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- determines if function exists in database  
    IF OBJECT_ID (N'Sales.fn_SalesByStore', N'IF') IS NOT NULL  
    -- deletes function  
        DROP FUNCTION Sales.fn_SalesByStore;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md).  
  
  
