---
title: Aktivieren oder Deaktivieren einer Planhinweisliste | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- plan guides [SQL Server], disabling
- enabling plan guides
- plan guides [SQL Server], enabling
- disabling plan guides
ms.assetid: b00ab550-5308-4cb8-8330-483cd1d25654
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bc2185e7ece0af55344e248abe8f3c6b6b591b5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="enable-or-disable-a-plan-guide"></a>Aktivieren oder Deaktivieren einer Planhinweisliste
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Sie können Planhinweislisten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] deaktivieren und aktivieren. Es können entweder eine einzelne Planhinweisliste oder alle Planhinweislisten in einer Datenbank aktiviert oder deaktiviert werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So deaktivieren und aktivieren Sie Planhinweislisten mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Das Löschen oder Ändern einer Funktion, einer gespeicherten Prozedur oder eines DML-Triggers, auf die bzw. den in einer Planhinweisliste verwiesen wird, verursacht einen Fehler. Überprüfen Sie die oben aufgeführten Objekte vor dem Löschen oder Ändern immer auf Abhängigkeiten.  
  
-   Das Deaktivieren einer deaktivierten bzw. das Aktivieren einer aktivierten Planhinweisliste hat keine Auswirkung und kann ausgeführt werden, ohne einen Fehler zu verursachen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Das Deaktivieren oder Aktivieren einer OBJECT-Planhinweisliste erfordert die ALTER-Berechtigung für das Objekt (z. B. Funktion, gespeicherte Prozedur), auf das von der Planhinweisliste verwiesen wird. Für alle anderen Planhinweislisten ist die ALTER DATABASE-Berechtigung erforderlich.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>So deaktivieren oder aktivieren Sie eine Planhinweisliste  
  
1.  Klicken Sie auf das Pluszeichen, um die Datenbank zu erweitern, in der Sie eine Planhinweisliste deaktivieren oder aktivieren möchten, und klicken Sie dann auf das Pluszeichen, um den Ordner **Programmierbarkeit** zu erweitern.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Planhinweislisten** zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Planhinweisliste, die deaktiviert oder aktiviert werden soll, und wählen Sie entweder **Deaktivieren** oder **Aktivieren**aus.  
  
4.  Überprüfen Sie im Dialogfeld **Planhinweisliste deaktivieren** oder **Planhinweisliste aktivieren** , ob die ausgewählte Aktion erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>So deaktivieren oder aktivieren Sie alle Planhinweislisten in einer Datenbank  
  
1.  Klicken Sie auf das Pluszeichen, um die Datenbank zu erweitern, in der Sie eine Planhinweisliste deaktivieren oder aktivieren möchten, und klicken Sie dann auf das Pluszeichen, um den Ordner **Programmierbarkeit** zu erweitern.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Planhinweislisten** , und wählen Sie dann **Alle aktivieren** oder **Alle deaktivieren**aus.  
  
3.  Überprüfen Sie im Dialogfeld **Alle Planhinweislisten deaktivieren** oder **Alle Planhinweislisten aktivieren** , ob die ausgewählte Aktion erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>So deaktivieren oder aktivieren Sie eine Planhinweisliste  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    --Create a procedure on which to define the plan guide.  
    IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetSalesOrderByCountry;  
    GO  
    CREATE PROCEDURE Sales.GetSalesOrderByCountry   
        (@Country nvarchar(60))  
    AS  
    BEGIN  
        SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country;  
    END  
    GO  
    --Create the plan guide.  
    EXEC sp_create_plan_guide N'Guide3',  
        N'SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country',  
        N'OBJECT',  
        N'Sales.GetSalesOrderByCountry',  
        NULL,  
        N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
    --Disable the plan guide.  
    EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
    GO  
    --Enable the plan guide.  
    EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
    GO  
  
    ```  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>So deaktivieren oder aktivieren Sie alle Planhinweislisten in einer Datenbank  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    --Disable all plan guides in the database.  
    EXEC sp_control_plan_guide N'DISABLE ALL';  
    GO  
    --Enable all plan guides in the database.  
    EXEC sp_control_plan_guide N'ENABLE ALL';  
    GO  
  
    ```  
  
 Weitere Informationen finden Sie unter [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md).  
  
  
