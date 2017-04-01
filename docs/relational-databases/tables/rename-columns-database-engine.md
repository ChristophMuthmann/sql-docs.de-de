---
title: "Umbenennen von Spalten (Datenbankmodul) | Microsoft Docs"
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
  - "Spalten [SQL Server], Namen"
  - "Umbenennen von Spalten"
  - "Spaltennamen [SQL Server]"
ms.assetid: 7c71ec9f-0180-4398-b32a-4bfb7592e75d
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Umbenennen von Spalten (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Tabellenspalte in [!INCLUDE[tsql](../../includes/tsql-md.md)]umbenennen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So benennen Sie Spalten um mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Durch die Umbenennung einer Spalte werden nicht automatisch auch die Verweise auf diese Spalte umbenannt. Sie müssen Objekte, die auf die umbenannte Spalte verweisen, manuell ändern. Wenn Sie z. B. eine Tabellenspalte umbenennen und in einem Trigger auf diese Spalte verwiesen wird, müssen Sie den Trigger ändern, sodass er den neuen Spaltennamen wiedergibt. Verwenden Sie [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md), um Abhängigkeiten vom Objekt aufzulisten, bevor Sie es umbenennen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für das Objekt.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So benennen Sie eine Spalte mit Objekt-Explorer um  
  
1.  Stellen Sie im Objekt-Explorer ** **eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf die Tabelle, in der Sie Spalten umbenennen möchten, und klicken Sie dann auf **Umbenennen**.  
  
3.  Geben Sie einen neuen Spaltennamen ein.  
  
#### So benennen Sie eine Spalte mit dem Tabellen-Designer um  
  
1.  Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf die Tabelle, in der Sie Spalten umbenennen möchten, und klicken Sie dann auf **Entwerfen**.  
  
2.  Wählen Sie unter **Spaltenname**den zu ändernden Namen aus, und geben Sie einen neuen Namen ein.  
  
3.  Klicken Sie im Menü **Datei** auf **Speichern***table name*.  
  
> [!NOTE]  
>  Sie können den Spaltennamen auch auf der Registerkarte **Spalteneigenschaften** ändern. Wählen Sie die Spalte aus, deren Name geändert werden soll, und geben Sie für **Name**einen neuen Wert ein.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So benennen Sie eine Spalte um**  
  
#### So benennen Sie eine Spalte um  
  
1.  Stellen Sie im Objekt-Explorer ** **eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Im folgenden Beispiel wird die Spalte `TerritoryID` in der Tabelle `Sales.SalesTerritory` in `TerrID`umbenannt. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md).  
  
  