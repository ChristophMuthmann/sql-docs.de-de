---
title: Erstellen von Sichten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: views
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- views [SQL Server], creating
ms.assetid: 0b7bd2a1-544c-42ba-8e7b-4822f34d7b64
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2b575e509a34c03aca052250c220fcf1726ba2e0
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="create-views"></a>Erstellen von Sichten
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]
  Sie können in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]Sichten erstellen. Eine Sicht kann für folgende Zwecke verwendet werden:  
  
-   Um die Darstellung einer Datenbank für jeden einzelnen Benutzer einzuschränken, zu vereinfachen und anzupassen.  
  
-   Als Sicherheitsmechanismus, indem Benutzern der Zugriff auf Daten über die Sicht ermöglicht wird, ohne diesen Benutzern jedoch die Berechtigungen für den direkten Zugriff auf die zugrunde liegenden Basistabellen zu gewähren.  
  
-   Um eine abwärtskompatible Schnittstelle zum Emulieren einer Tabelle bereitzustellen, deren Schema geändert wurde.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Security](#Security)  
  
-   **So erstellen Sie eine Sicht mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Eine Sicht kann nur in der aktuellen Datenbank erstellt werden.  
  
 Für eine Sicht sind maximal 1.024 Spalten zulässig.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die CREATE VIEW-Berechtigung in der Datenbank und die ALTER-Berechtigung für das Schema, in dem die Sicht erstellt wird.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-a-view-by-using-the-query-and-view-designer"></a>So erstellen Sie eine Sicht mit dem Abfrage- und Sicht-Designer  
  
1.  Erweitern Sie im **Objekt-Explorer**die Datenbank, in der Sie die neue Sicht erstellen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Sichten** , und klicken Sie anschließend auf **Neue Sicht…**.  
  
3.  Wählen Sie im Dialogfeld **Tabelle hinzufügen** das Element oder die Elemente, die Sie in die neue Sicht einschließen möchten, auf einer der folgenden Registerkarten aus: Tabellen, Sichten, Funktionen und Synonyme.  
  
4.  Klicken Sie auf **Hinzufügen**und dann auf **Schließen**.  
  
5.  Wählen Sie im **Diagrammbereich**die Spalten bzw. die anderen Elemente aus, die in der neuen Sicht enthalten sein sollen.  
  
6.  Wählen Sie im **Kriterienbereich**zusätzliche Sortier- oder Filterkriterien für die Spalten aus.  
  
7.  Klicken Sie im Menü **Datei** auf **Speichern***Ansichtsname*.  
  
8.  Geben Sie im Dialogfeld **Namen auswählen** einen Namen für die neue Sicht ein, und klicken Sie auf **OK**.  
  
     Weitere Informationen über den Abfrage- und Sicht-Designer finden Sie unter [Tools im Abfrage- und Sicht-Designer &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/12e4b5a5-b793-4b6c-a0e5-c450c49bf26f).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-view"></a>So erstellen Sie eine Sicht  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
    GO  
    -- Query the view  
    SELECT FirstName, LastName, HireDate  
    FROM HumanResources.EmployeeHireDate  
    ORDER BY LastName;  
  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
  
