---
title: "Deaktivieren von Fremdschl&#252;sseleinschr&#228;nkungen mit INSERT- und UPDATE-Anweisungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Einschränkungen [SQL Server], Fremdschlüssel"
  - "Fremdschlüssel [SQL Server], Deaktivieren von Einschränkungen"
  - "Deaktivieren von Einschränkungen"
  - "UPDATE-Anweisung [SQL Server], Fremdschlüsseleinschränkungen"
  - "INSERT-Anweisung [SQL Server], Fremdschlüsseleinschränkungen"
ms.assetid: 029168d7-085e-4b13-9b86-5644b67c6e24
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Deaktivieren von Fremdschl&#252;sseleinschr&#228;nkungen mit INSERT- und UPDATE-Anweisungen
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können eine Fremdschlüsseleinschränkung während der Durchführung von INSERT- und UPDATE-Transaktionen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]deaktivieren. Verwenden Sie diese Option, wenn Sie wissen, dass neue Daten gegen die vorhandene Einschränkung verstoßen, oder wenn die Einschränkung nur für die bereits in der Datenbank vorhandenen Daten gilt.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So deaktivieren Sie eine Fremdschlüsseleinschränkung für INSERT- und UPDATE-Anweisungen mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Sobald diese Einschränkungen deaktiviert worden sind, wird die Spalte bei Einfügungen oder Updates nicht mehr bezüglich der Einschränkungsbedingungen überprüft.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So deaktivieren Sie eine Fremdschlüsseleinschränkung für die Anweisungen INSERT und UPDATE  
  
1.  Erweitern Sie im **Objekt-Explorer**die Tabelle mit der Einschränkung, und erweitern Sie dann den Ordner **Schlüssel** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Einschränkung, und wählen Sie anschließend **Ändern** aus.  
  
3.  Klicken Sie im Raster unter dem **Tabellen-Designer** auf **Fremdschlüsseleinschränkung erzwingen**, und wählen Sie im Dropdownmenü **Nein** aus.  
  
4.  Klicken Sie auf **Schließen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So deaktivieren Sie eine Fremdschlüsseleinschränkung für die Anweisungen INSERT und UPDATE  
  
1.  Stellen Sie im Objekt-Explorer ****eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie die folgenden Beispiele, fügen Sie sie in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT FK_PurchaseOrderHeader_Employee_EmployeeID;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  