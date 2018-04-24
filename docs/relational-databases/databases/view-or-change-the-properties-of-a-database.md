---
title: Anzeigen oder Ändern der Eigenschaften einer Datenbank | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying databases
- database viewing [SQL Server]
- databases [SQL Server], viewing
- viewing databases
ms.assetid: 9e8ac097-84b7-46c7-85e3-c1e79f94d747
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f692617f989b42111030128257e708c57857bc04
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-or-change-the-properties-of-a-database"></a>Anzeigen oder Ändern der Eigenschaften einer Datenbank
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird die Vorgehensweise zum Anzeigen oder Ändern der Eigenschaften einer Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]beschrieben. Nachdem Sie eine Datenbankeigenschaft geändert haben, tritt die Änderung sofort in Kraft.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **So zeigen Sie die Eigenschaften einer Datenbank an oder ändern diese mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Ist AUTO_CLOSE auf ON festgelegt, geben einige Spalten in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht sowie die DATABASEPROPERTYEX-Funktion den Wert NULL zurück, da die Datenbank nicht für den Abruf der Daten verfügbar ist. Um dies zu beheben, öffnen Sie die Datenbank.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Zum Ändern der Eigenschaften einer Datenbank ist die ALTER-Berechtigung für die Datenbank erforderlich. Zum Anzeigen der Eigenschaften einer Datenbank ist mindestens eine Mitgliedschaft in der Public-Datenbankrolle erforderlich.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>So zeigen Sie die Eigenschaften einer Datenbank an oder ändern diese  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf die anzuzeigende Datenbank, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie im Dialogfeld **Datenbankeigenschaften** eine anzuzeigende Seite aus, um die entsprechenden Informationen anzuzeigen. Wählen Sie z. B. die Seite **Dateien** aus, um Daten- und Protokolldateiinformationen anzuzeigen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Transact-SQL bietet eine Reihe von verschiedenen Methoden zum Anzeigen der Eigenschaften einer Datenbank und zum Ändern der Eigenschaften einer Datenbank. Zum Anzeigen der Eigenschaften einer Datenbank können Sie die Funktion [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) und die Katalogsicht [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) verwenden. Zum Ändern der Eigenschaften einer Datenbank können Sie die Version der ALTER DATABASE-Anweisung für Ihre Umgebung verwenden:[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) oder [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md). Zum Anzeigen der datenbankweiten Eigenschaften verwenden Sie die Katalogsicht [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) , und zum Ändern der datenbankweiten Eigenschaften verwenden Sie die Anweisung [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) .  
  
#### <a name="to-view-a-property-of-a-database-by-using-the-databasepropertyex-function"></a>So zeigen Sie eine Eigenschaft einer Datenbank mit der Funktion DATABASEPROPERTYEX an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] und dann mit der Datenbank her, deren Eigenschaften Sie anzeigen möchten.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die Systemfunktion [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) verwendet, um den Status der AUTO_SHRINK-Datenbankoption in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank zurückzugeben. Der Rückgabewert 1 bedeutet, dass die Option auf ON festgelegt ist, und der Rückgabewert 0 bedeutet, dass die Option auf OFF festgelegt ist.  
  
    ```sql  
    SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>So zeigen Sie die Eigenschaften einer Datenbank durch das Abfragen von sys.databases an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] und dann mit der Datenbank her, deren Eigenschaften Sie anzeigen möchten.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht abgefragt, um mehrere Eigenschaften der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank anzuzeigen. In diesem Beispiel wird die Datenbank-ID-Nummer (`database_id`), der Schreibschutz- oder Lese-/Schreibstatus der Datenbank (`is_read_only`), die Sortierung für die Datenbank (`collation_name`) und der Datenbank-Kompatibilitätsgrad (`compatibility_level`) zurückgegeben.  
  
    ```sql  
    SELECT database_id, is_read_only, collation_name, compatibility_level  
    FROM sys.databases WHERE name = 'AdventureWorks2012';  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-scoped-configuration-by-querying-sysdatabasesscopedconfiguration"></a>So zeigen Sie die Eigenschaften einer datenbankweit gültigen Konfiguration durch Abfragen von sys.databases_scoped_configuration an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] und dann mit der Datenbank her, deren Eigenschaften Sie anzeigen möchten.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) abgefragt, um mehrere Eigenschaften der aktuellen Datenbank anzuzeigen.  
  
    ```sql  
    SELECT configuration_id, name, value, value_for_secondary  
    FROM sys.database_scoped_configurations;  
    ```  
  
     Weitere Beispiele finden Sie unter [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  
  
#### <a name="to-change-the-properties-of-a-sql-server-2016-database-using-alter-database"></a>So ändern Sie die Eigenschaften einer SQL Server 2016-Datenbank mithilfe von ALTER DATABASE  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, und fügen Sie es in das Abfragefenster ein. Im Beispiel wird der Momentaufnahmen-Isolationsstatus für die Datenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] bestimmt und der Zustand der Eigenschaft geändert. Anschließend wird die Änderung überprüft.  
  
     Um den Momentaufnahmen-Isolationsstatus zu bestimmen, wählen Sie die erste `SELECT` -Anweisung aus und klicken auf **Ausführen**.  
  
     Um den Momentaufnahmen-Isolationsstatus zu ändern, wählen Sie die `ALTER DATABASE` -Anweisung aus und klicken auf **Ausführen**.  
  
     Um die Änderung zu überprüfen, wählen Sie die zweite `SELECT` -Anweisung aus und klicken auf **Ausführen**.  
  
     [!code-sql[DatabaseDDL#AlterDatabase9](../../relational-databases/databases/codesnippet/tsql/view-or-change-the-prope_1.sql)]  
  
#### <a name="to-change-the-database-scoped-properties-using-alter-database-scoped-configuration"></a>So ändern Sie die datenbankweit gültigen Eigenschaften mit ALTER_DATABASE SCOPED CONFIGURATION  
  
1.  Stellen Sie eine Verbindung mit einer Datenbank in Ihrer SQL Server-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, und fügen Sie es in das Abfragefenster ein. Im folgenden Beispiel wird MAXDOP für eine sekundäre Datenbank auf den Wert für die primäre Datenbank festgelegt.  
  
    ```sql  
    ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY   
    ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER DATABASE (Azure SQL-Datenbank)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  

  
  
