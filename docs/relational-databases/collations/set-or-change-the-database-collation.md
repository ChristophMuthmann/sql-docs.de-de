---
title: "Festlegen oder Ändern der Datenbanksortierung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: collations
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 627e3b1c423404cd0bfc89273d27aa2ef3c11505
ms.sourcegitcommit: d28d9e3413b6fab26599966112117d45ec2c7045
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/11/2018
---
# <a name="set-or-change-the-database-collation"></a>Festlegen oder Ändern der Datenbanksortierung
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie die Datenbanksortierung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] festgelegt und geändert werden kann. Wenn keine Sortierung angegeben wird, wird die Sortierung des Servers verwendet.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **Festlegen oder Ändern der Datenbanksortierung mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Nur-Unicode-Sortierungen unter Windows, können nur mit der COLLATE-Klausel verwendet werden, um auf Spalten- und Ausdrucksebene Sortierungen auf die Datentypen **nchar**, **nvarchar**und **ntext** anzuwenden. Sie können nicht mit der COLLATE-Klausel verwendet werden, um die Sortierung einer Datenbank oder Serverinstanz zu ändern.  
  
-   Wenn die angegebene Sortierung oder die Sortierung des Objekts, auf das verwiesen wird, eine Codepage verwendet, die nicht von Windows unterstützt wird, zeigt [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler an.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Die Namen der unterstützten Sortierungen finden Sie unter [Name der Windows-Sortierung &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) und [SQL Server-Sortierungsname &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md). Alternativ können Sie die Systemfunktion [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) verwenden.  
  
-   Das Ändern der Datenbanksortierung ändert Folgendes:  
  
    -   Alle **char**-, **varchar**-, **text**-, **nchar**-, **nvarchar**- und **ntext** -Spalten in Systemtabellen erhalten die neue Sortierung.  
  
    -   Sämtliche vorhandene **char**-, **varchar**-, **text**-, **nchar**-, **nvarchar**- und **ntext** -Parameter und skalare Rückgabewerte für gespeicherte Prozeduren und benutzerdefinierte Funktionen erhalten die neue Sortierung.  
  
    -   Die Systemdatentypen **char**, **varchar**, **text**, **nchar**oder **nvarchar**oder **ntext** sowie alle benutzerdefinierten Datentypen, die auf Systemdatentypen basieren, erhalten die neue Standardsortierung.  
  
-   Sie können die Sortierung von neuen Objekten, die in einer Benutzerdatenbank erstellt werden, mithilfe der COLLATE-Klausel der [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) -Anweisung ändern. Diese Anweisung ändert jedoch nicht die Sortierung der Spalten in vorhandenen benutzerdefinierten Tabellen. Letztere können mithilfe der COLLATE-Klausel der [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)-Anweisung geändert werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 CREATE DATABASE  
 Erfordert die Berechtigung CREATE DATABASE in der **master** -Datenbank oder die Berechtigungen CREATE ANY DATABASE oder ALTER ANY DATABASE.  
  
 ALTER DATABASE  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>So legen Sie die Datenbanksortierung oder ändern sie  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, erweitern Sie diese Instanz und dann **Datenbanken**.  
  
2.  Wenn Sie eine neue Datenbank erstellen, klicken mit der rechten Maustaste auf **Datenbanken** , und klicken Sie anschließend auf **Neue Datenbank**. Wenn Sie die Standardsortierung nicht möchten, klicken auf die Seite **Optionen** , und wählen aus der Dropdownliste **Sortierung** eine Sortierung aus.  
  
     Wenn eine Datenbank bereits vorhanden ist, können Sie alternativ mit der rechten Maustaste auf die Datenbank klicken, die geändert werden soll, und auf **Eigenschaften**klicken. Klicken Sie auf die Seite **Optionen** , und wählen Sie aus der Dropdownliste **Sortierung** eine Sortierung aus.  
  
3.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>So legen Sie die Datenbanksortierung fest  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie die [COLLATE-Klausel](~/t-sql/statements/collations.md) verwendet wird, um einen Sortierungsnamen anzugeben. Im folgenden Beispiel wird die Datenbank mit dem Namen `MyOptionsTest` erstellt, die die Sortierung `Latin1_General_100_CS_AS_SC` verwendet. Nachdem Sie die Datenbank erstellt haben, führen Sie die `SELECT` -Anweisung aus, um die Einstellung zu überprüfen.  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
#### <a name="to-change-the-database-collation"></a>So ändern Sie die Datenbanksortierung  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie die [COLLATE-Klausel](~/t-sql/statements/collations.md) in einer [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) -Anweisung verwendet wird, um den Sortierungsnamen zu ändern. Führen Sie die `SELECT` -Anweisung aus, um die Änderung zu überprüfen.  
  
```sql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [SQL Server-Sortierungsname &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)   
 [Name der Windows-Sortierung &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)   
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [Rangfolge von Sortierungen &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
