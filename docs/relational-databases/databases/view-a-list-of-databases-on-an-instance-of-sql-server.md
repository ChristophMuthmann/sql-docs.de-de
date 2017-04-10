---
title: "Anzeigen einer Liste der Datenbanken in einer Instanz von SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Aktuelle Datenbanken"
  - "Momentan auf dem Server vorhandene Datenbanken [SQL Server]"
  - "Datenbankliste [SQL Server]"
  - "Anzeigen der Datenbankliste"
  - "Einblenden der Datenbankliste"
  - "Datenbanken [SQL Server], anzeigen"
  - "Server [SQL Server], aufgelistete Datenbanken"
  - "Auflisten von Datenbanken"
ms.assetid: 7ee7a789-db36-4be9-8a0e-0362a1e152dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Anzeigen einer Liste der Datenbanken in einer Instanz von SQL Server
  In diesem Thema wird beschrieben, wie eine Liste mit Datenbanken für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]angezeigt werden kann.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So zeigen Sie eine Liste der Datenbanken in einer Instanz von SQL Server an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Wenn der Aufrufer von **sys.databases** nicht der Besitzer der Datenbank und die Datenbank keine **master**- oder **tempdb**-Datenbank ist, ist zum Anzeigen der entsprechenden Zeile mindestens die Berechtigung ALTER ANY DATABASE oder VIEW ANY DATABASE auf Serverebene bzw. die Berechtigung CREATE DATABASE für die **master**-Datenbank erforderlich. Die Datenbank, mit der der Aufrufer eine Verbindung hergestellt hat, kann immer in **sys.databases**angezeigt werden.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So zeigen Sie eine Liste der Datenbanken in einer Instanz von SQL Server an  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, um eine Liste aller Datenbanken in der Instanz anzuzeigen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So zeigen Sie eine Liste der Datenbanken in einer Instanz von SQL Server an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Das Beispiel gibt für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eine Liste mit den Datenbanken zurück. Die Liste enthält die Namen der Datenbanken, die dazugehörigen Datenbank-IDs und die Datumsangaben zur Datenbankerstellung.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT name, database_id, create_date  
FROM sys.databases ;  
GO  
  
```  
  
## Siehe auch  
 [Datenbanken und Dateikatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  