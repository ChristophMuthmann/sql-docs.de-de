---
title: Anzeigen der Eigenschaften der Planhinweisliste | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-plan-guides
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.planguideprop.general.f1
helpviewer_keywords:
- plan guides [SQL Server], view plan guide properties
- viewing plan guide properties
ms.assetid: 8c0d2f39-59c1-4168-a649-65473f6a771b
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0b417f711c899d6ea5fe03a20d68637f016c6d7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-plan-guide-properties"></a>Anzeigen der Eigenschaften der Planhinweisliste
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Sie können die Eigenschaften von Planhinweislisten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So zeigen Sie die Eigenschaften von Planhinweislisten an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Sichtbarkeit der Metadaten in Katalogsichten ist auf sicherungsfähige Elemente beschränkt, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>So zeigen Sie die Eigenschaften einer Planhinweisliste an  
  
1.  Klicken Sie auf das Pluszeichen, um die Datenbank zu erweitern, in der Sie die Eigenschaften einer Planhinweisliste anzeigen möchten, und klicken Sie dann auf das Pluszeichen, um den Ordner **Programmierbarkeit** zu erweitern.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Planhinweislisten** zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Planhinweisliste, deren Eigenschaften Sie anzeigen möchten, und wählen Sie **Eigenschaften**.  
  
     Die folgenden Eigenschaften werden im Dialogfeld **Die Eigenschaften der Planhinweisliste** angezeigt.  
  
     **Hinweise**  
     Zeigt die Abfragehinweise oder den Abfrageplan zur Anwendung auf die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung an. Wenn ein Abfrageplan als Hinweis gekennzeichnet ist, wird die XML-Showplanausgabe für den Plan angezeigt.  
  
     **Ist deaktiviert**  
     Zeigt den Status der Planhinweisliste an. Mögliche Werte sind **True** und **False**.  
  
     **Name**  
     Zeigt den Namen der Planhinweisliste an.  
  
     **Parameter**  
     Wenn es sich beim Bereichstyp um SQL oder TEMPLATE handelt, wird hiermit der Name und Datentyp aller Parameter angezeigt, die in die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung eingebettet sind.  
  
     **Bereichsbatch**  
     Zeigt den Batchtext an, in dem die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung enthalten ist.  
  
     **Name von Bereichsobjekt**  
     Wenn es sich beim Bereichstyp um OBJECT handelt, wird hiermit der Name der gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozedur, benutzerdefinierten Skalarfunktion, aus mehreren Anweisungen bestehenden Funktion mit Tabellenrückgabe oder des DML-Triggers angezeigt, die bzw. der die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung enthält.  
  
     **Name von Bereichsschema**  
     Wenn es sich beim Bereichstyp um OBJECT handelt, wird hiermit der Name des Schemas angezeigt, in dem sich das Objekt befindet.  
  
     **Bereichstyp**  
     Zeigt den Typ der Entität an, in dem die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung enthalten ist. Dies gibt den Kontext zum Abgleich der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung mit der Planhinweisliste an. Mögliche Werte sind **OBJECT**, **SQL**und **TEMPLATE**.  
  
     **Statement**  
     Zeigt die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung an, auf die die Planhinweisliste angewendet wird.  
  
4.  Klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>So zeigen Sie die Eigenschaften einer Planhinweisliste an  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- If a plan guide named “Guide1” already exists in the AdventureWorks2012 database, delete it.  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID(N'Guide1') IS NOT NULL  
       EXEC sp_control_plan_guide N'DROP', N'Guide1';  
    GO  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
    GO  
    -- Gets the name, created date, and all other relevant property information on the plan guide created above.   
    SELECT name AS plan_guide_name,  
       create_date,  
       query_text,  
       scope_type_desc,  
       OBJECT_NAME(scope_object_id) AS scope_object_name,  
       scope_batch,  
       parameters,  
       hints,  
       is_disabled  
    FROM sys.plan_guides  
    WHERE name = N’Guide1’;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md).  
  
  
