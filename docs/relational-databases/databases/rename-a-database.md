---
title: Umbenennen einer Datenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8f6377b37fc350caa110d46236b1329eeab9c3df
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
# <a name="rename-a-database"></a>Umbenennen einer Datenbank
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
In diesem Thema wird beschrieben, wie eine benutzerdefinierte Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]umbenannt wird. Der Name der Datenbank kann alle Zeichen enthalten, die den Regeln für Bezeichner entsprechen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Security](#Security)  
  
-   **So benennen Sie eine Datenbank um mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [After renaming a database](#FollowUp)  

> [!NOTE]
> Um eine Datenbank in Azure SQL-Datenbank umzubenennen, verwenden Sie die Anweisung [ALTER DATABASE (Azure SQL-Datenbank)](../../t-sql/statements/alter-database-azure-sql-database.md). Um eine Datenbank in Azure SQL Data Warehouse oder Parallel Data Warehouse umzubenennen, verwenden Sie die Anweisung [RENAME (Transact-SQL)](/t-sql/statements/rename-transact-sql).
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Systemdatenbanken können nicht umbenannt werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-rename-a-database"></a>So benennen Sie eine Datenbank um  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Stellen Sie sicher, dass die Datenbank zurzeit nicht verwendet wird, und fahren Sie dann mit der [Festlegung des Einzelbenutzermodus für die Datenbank](../../relational-databases/databases/set-a-database-to-single-user-mode.md)fort.  
  
3.  Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf die Datenbank, die umbenannt werden soll, und klicken Sie anschließend auf **Umbenennen**.  
  
4.  Geben Sie den neuen Datenbanknamen ein, und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-rename-a-database"></a>So benennen Sie eine Datenbank um  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird der Name der Datenbank `AdventureWorks2012` in `Northwind`geändert.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
###  <a name="TsqlExample"></a>   
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Umbenennen einer Datenbank  
 Sichern Sie die **master** -Datenbank nach jedem Umbenennen einer Datenbank.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md)  
  
  
