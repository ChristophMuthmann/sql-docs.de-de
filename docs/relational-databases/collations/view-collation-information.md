---
title: Anzeigen von Kollokations Informationen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eebc43acb7df6cf2d63dbc6d8e0d1c4f25fa9476
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="view-collation-information"></a>Anzeigen von Sortierungsinformationen
    
##  <a name="Top"></a> Sie können die Sortierung eines Servers, einer Datenbank oder Spalte in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mithilfe der Menüoptionen des Objekt-Explorers oder mit [!INCLUDE[tsql](../../includes/tsql-md.md)] anzeigen.  
  
##  <a name="Procedures"></a> So zeigen Sie eine Sortierungseinstellung an  
 Sie können eine der folgenden Anwendungen verwenden:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So zeigen Sie eine Sortierungseinstellung für einen Server (Instanz von SQL Server) im Objekt-Explorer an**  
  
1.  Stellen Sie mithilfe des Objekt-Explorers eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Instanz, und wählen Sie **Eigenschaften**aus.  
  
 **So zeigen Sie eine Sortierungseinstellung für eine Datenbank im Objekt-Explorer an**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf die Datenbank, und wählen Sie **Eigenschaften**aus.  
  
 **So zeigen Sie eine Sortierungseinstellung für eine Spalte im Objekt-Explorer an**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, die Datenbank und anschließend **Tabellen**.  
  
3.  Erweitern Sie die Tabelle, die die Spalte enthält, und erweitern Sie dann **Spalten**.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Spalte, und wählen Sie **Eigenschaften** aus. Wenn die Sortierungseigenschaft leer ist, ist die Spalte kein Zeichendatentyp.  
  
###  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So zeigen Sie die Sortierungseinstellung eines Servers an**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und klicken Sie auf der Symbolleiste auf **Neue Abfrage**.  
  
2.  Geben Sie im Abfragefenster die folgende Anweisung ein, die die SERVERPROPERTY-Systemfunktion verwendet:  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  Alternativ können Sie die gespeicherte Systemprozedur "sp_helpsort" verwenden.  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **So zeigen Sie alle von von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützten Sortierreihenfolgen an**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und klicken Sie auf der Symbolleiste auf **Neue Abfrage**.  
  
2.  Geben Sie im Abfragefenster die folgende Anweisung ein, die die SERVERPROPERTY-Systemfunktion verwendet:  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **So zeigen Sie die Sortierungseinstellung einer Datenbank an**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und klicken Sie auf der Symbolleiste auf **Neue Abfrage**.  
  
2.  Geben Sie im Abfragefenster die folgende Anweisung ein, die die sys.databases-Systemkatalogsicht verwendet.  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  Alternativ können Sie die DATABASEPROPERTYEX-Systemfunktion verwenden.  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **So zeigen Sie die Sortierungseinstellung einer Spalte an**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und klicken Sie auf der Symbolleiste auf **Neue Abfrage**.  
  
2.  Geben Sie im Abfragefenster die folgende Anweisung ein, die die sys.columns-Systemkatalogsicht verwendet.  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Rangfolge von Sortierungen &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [sp_helpsort &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsort-transact-sql.md)  
  
  
