---
title: Erstellen von DML-Triggern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption [SQL Server], DML triggers
- deferred name resolution, DML triggers
- WITH ENCRYPTION clause
- IF UPDATE
- SET statement, DML triggers
- DML triggers, programming
- testing column changes
- results [SQL Server], DML triggers
ms.assetid: b2b52258-642b-462e-8e0f-18c09d2eccf4
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 21011d77337e517154b4732071253a934984363d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="create-dml-triggers"></a>Erstellen von DML-Triggern
  In diesem Thema wird beschrieben, wie ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -DML-Trigger mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] unter Verwendung der [!INCLUDE[tsql](../../includes/tsql-md.md)] - CREATE TRIGGER-Anweisung erstellt wird.  
  
##  <a name="Top"></a> Vorbereitungen  
  
### <a name="limitations-and-restrictions"></a>Einschränkungen  
 Eine Liste der Einschränkungen in Zusammenhang mit der Erstellung von DML-Triggern finden Sie unter [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
###  <a name="Permissions"></a> Berechtigungen  
 Es ist die ALTER-Berechtigung für die Tabelle oder Sicht erforderlich, für die der Trigger erstellt wird.  
  
##  <a name="Procedures"></a> So erstellen Sie einen DML-Trigger  
 Sie können eine der folgenden Anwendungen verwenden:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank und **Tabellen** , und erweitern Sie dann die Tabelle **Purchasing.PurchaseOrderHeader**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Trigger**, und wählen Sie **Neuer Trigger**aus.  
  
4.  Klicken Sie im Menü **Abfrage** auf **Werte für Vorlagenparameter angeben**. Alternativ können Sie die Tastenkombination STRG+UMSCHALT+M drücken, um das Dialogfeld **Werte für Vorlagenparameter angeben** zu öffnen.  
  
5.  Geben Sie im Dialogfeld **Werte für Vorlagenparameter angeben** die folgenden Werte für die angezeigten Parameter ein.  
  
    |Parameter|Wert|  
    |---------------|-----------|  
    |Autor|*Ihr Name*|  
    |Erstellt am|*Das heutige Datum*|  
    |Beschreibung|Überprüft die Anbieterbonität, bevor eine neue Bestellung mit dem einzufügenden Anbieter zugelassen wird.|  
    |Schema_Name|Purchasing|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|UPDATE und DELETE aus der Liste entfernen.|  
  
6.  Klicken Sie auf **OK**.  
  
7.  Ersetzen Sie im **Abfrage-Editor**den Kommentar `-- Insert statements for trigger here` durch die folgende Anweisung:  
  
    ```tsql  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
8.  Zum Überprüfen der Syntax klicken Sie im Menü **Abfrage** auf **Analysieren**. Wenn eine Fehlermeldung zurückgegeben wird, vergleichen Sie die Anweisung mit den Informationen oben, korrigieren diese gegebenenfalls und wiederholen diesen Schritt.  
  
9. Zum Erstellen des DML-Triggers klicken Sie im Menü **Abfrage** auf **Ausführen**. Der DML-Trigger wird als Objekt in der Datenbank erstellt.  
  
10. Zum Anzeigen des DML-Triggers im Objekt-Explorer klicken Sie mit der rechten Maustaste auf **Trigger** und wählen **Aktualisieren**aus.  
  
 [Vorbereitungen](#Top)  
  
###  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie im Menü **Datei** auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird derselbe gespeicherte DML-Trigger wie oben erstellt.  
  
    ```  
    -- Trigger valid for multirow and single row inserts  
    -- and optimal for single row inserts.  
    USE AdventureWorks2012;  
    GO  
    CREATE TRIGGER NewPODetail3  
    ON Purchasing.PurchaseOrderDetail  
    FOR INSERT AS  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
##  <a name="PowerShellProcedure"></a> [Vorbereitungen](#Top)  
  
  
