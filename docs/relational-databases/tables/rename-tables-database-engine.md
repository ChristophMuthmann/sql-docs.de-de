---
title: Umbenennen von Tabellen (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
ms.assetid: 2f5c922d-4d71-4694-9fca-28dd99375799
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1a341ca5d2c39c5d7c5071d135f58fd37d6b9d73
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="rename-tables-database-engine"></a>Umbenennen von Tabellen (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] eine Tabelle mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]umbenennen.  
  
> [!CAUTION]  
>  Das Umbenennen einer Tabelle muss sorgfältig überlegt sein. Alle Abfragen, Sichten, benutzerdefinierten Funktionen, gespeicherten Prozeduren und Programme, die auf diese Tabelle verweisen, werden durch die Namensänderung ungültig.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So benennen Sie eine Tabelle um mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Durch Umbenennen einer Tabelle werden die Verweise auf diese Tabelle nicht automatisch umbenannt. Sie müssen Objekte, die auf die umbenannte Tabelle verweisen, manuell ändern. Wenn Sie z. B. eine Tabelle umbenennen und in einem Trigger auf diese Tabelle verwiesen wird, müssen Sie den Trigger ändern, sodass er den neuen Tabellennamen wiedergibt. Verwenden Sie [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) für eine Auflistung der Abhängigkeiten von der Tabelle, bevor Sie sie umbenennen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-rename-a-table"></a>So benennen Sie eine Tabelle um  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Tabelle, die umbenannt werden soll, und wählen Sie im Kontextmenü **Entwerfen** aus.  
  
2.  Wählen Sie im Menü **Ansicht** die Option **Eigenschaften**aus.  
  
3.  Geben Sie im Fenster **Eigenschaften** im Feld **Name** einen neuen Namen für die Tabelle ein.  
  
4.  Wenn Sie diesen Vorgang abbrechen möchten, drücken Sie die ESC-TASTE, bevor Sie das Feld verlassen.  
  
5.  Klicken Sie im Menü **Datei** auf **Speichern***table name*.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-rename-a-table"></a>So benennen Sie eine Tabelle um  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Im folgenden Beispiel wird die `SalesTerritory` -Tabelle im Schema `SalesTerr` in `Sales` umbenannt. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
    ```  
  
 Weitere Beispiele finden Sie unter [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md).  
  
  
