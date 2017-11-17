---
title: ALTER PROCEDURE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_PROCEDURE_TSQL
- ALTER_PROC_TSQL
- ALTER PROC
- ALTER PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROCEDURE statement
- stored procedure modifications [SQL Server]
- modifying stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: ed9b2f76-11ec-498d-a95e-75b490a75733
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3dc195d3f6ca908253ff5726c3f336435e7f2bd1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-procedure-transact-sql"></a>ALTER PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ändert eine zuvor durch Ausführen der CREATE PROCEDURE-Anweisung erstellte Prozedur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ VARYING ] [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH <procedure_option> [ ,...n ] ]  
[ FOR REPLICATION ]   
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }  
[;]  
  
<procedure_option> ::=   
    [ ENCRYPTION ]  
    [ RECOMPILE ]  
    [ EXECUTE AS Clause ]  
```  
  
```  
-- Syntax for SQL Server CLR Stored Procedure  
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH EXECUTE AS Clause ]  
AS { EXTERNAL NAME assembly_name.class_name.method_name }  
[;]  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name  
    [ { @parameterdata_type } [= ] ] [ ,...n ]  
AS { [ BEGIN ] sql_statement [ ; ] [ ,...n ] [ END ] }  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem die Prozedur gehört.  
  
 *procedure_name*  
 Der Name der Prozedur zu ändern. Prozedurnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md)entsprechen.  
  
 **;**  *Anzahl*  
 Eine vorhandene optionale ganze Zahl ist, die zum Gruppieren von Prozeduren mit dem gleichen Namen verwendet, sodass sie zusammen mit einer DROP PROCEDURE-Anweisung gelöscht werden können.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 **@***Parameter*  
 Ein Parameter in der Prozedur. Es können bis zu 2.100 Parameter angegeben werden.  
  
 [ *Type_schema_name***.** ] *Data_type*  
 Der Datentyp des Parameters und des Schemas, zu dem dieser gehört.  
  
 Informationen zu datentypeinschränkungen finden Sie unter [CREATE PROCEDURE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 VARYING  
 Gibt das als Ausgabeparameter unterstützte Resultset an. Dieser Parameter wird durch die gespeicherte Prozedur dynamisch erstellt, und sein Inhalt kann variieren. Gilt nur für cursor-Parameter. Diese Option ist für CLR-Prozeduren nicht gültig.  
  
 *Standardwert*  
 Ein Standardwert für den Parameter.  
  
 OUT | OUTPUT  
 Zeigt an, dass es sich bei dem Parameter um einen Rückgabeparameter handelt.  
  
 READONLY  
 Gibt an, dass der Parameter darf nicht aktualisiert oder innerhalb der Textkörper der Prozedur geändert. Wenn der Parametertyp ein Tabellenwerttyp ist, muss READONLY angegeben werden.  
  
 RECOMPILE  
 Zeigt an, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Plan für diese Prozedur nicht zwischenspeichert und die Prozedur zur Laufzeit neu kompiliert wird.  
  
 ENCRYPTION  
 **Gilt für**: SQLServer ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) und [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Originaltext der ALTER PROCEDURE-Anweisung in ein verborgenes Format umwandelt. Die Ausgabe der Verbergung ist nicht direkt in den Katalogsichten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sichtbar. Benutzer, die keinen Zugriff auf Systemtabellen oder Datenbankdateien haben, können den verborgenen Text nicht abrufen. Jedoch der Text stehen berechtigten Benutzern, die entweder Systemtabellen, über zugreifen können die [DAC-Port](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) oder direkt auf die Datenbankdateien zugreifen. Des Weiteren können Benutzer, die einen Debugger an den Serverprozess anfügen können, die Originalprozedur zur Laufzeit vom Arbeitsspeicher abrufen. Weitere Informationen zum Zugreifen auf Systemmetadaten finden Sie unter [die Konfiguration der Metadatensichtbarkeit](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 Prozeduren, die mit dieser Option erstellt wurden, können nicht als Teil der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Replikation veröffentlicht werden.  
  
 Die Option kann nicht für CLR-gespeicherte Prozeduren (Common Language Runtime) angegeben werden.  
  
> [!NOTE]  
>  Während eines Upgrades der [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwendet die verborgenen Kommentare, die in gespeicherten **sql_modules** Prozeduren neu zu erstellen.  
  
 EXECUTE AS  
 Gibt den Sicherheitskontext an, unter dem die gespeicherte Prozedur ausgeführt wird, nachdem auf sie zugegriffen wurde.  
  
 Weitere Informationen finden Sie unter [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 FOR REPLICATION  

  
 Gibt an, dass für die Replikation erstellte gespeicherte Prozeduren nicht auf dem Abonnenten ausgeführt werden können. Eine gespeicherte Prozedur, die mit der Option FOR REPLICATION erstellt wurde, wird als Filter für gespeicherte Prozeduren verwendet und nur während der Replikation ausgeführt. Parameter können nicht deklariert werden, wenn FOR REPLICATION angegeben ist. Diese Option ist für CLR-Prozeduren nicht gültig. Die Option RECOMPILE wird bei Prozeduren ignoriert, die mit FOR REPLICATION erstellt wurden.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 {[BEGIN] *Sql_statement* [;] [ ...  *n*  ] [END]}  
 Eine oder mehrere [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die den Textkörper der Prozedur umfassen. Sie können die optionalen BEGIN- und END-Schlüsselwörter zum Einschließen der Anweisungen verwenden. Weitere Informationen finden Sie in den Abschnitten bewährte Methoden, allgemeinen hinweisen und Einschränkungen in [CREATE PROCEDURE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 EXTERNAL NAME *Assembly_name***.** *Class_name***.** *keine Variablenargumentlisten verwenden*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Methode eine [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Assembly für eine CLR-gespeicherte Prozedur zu verweisen. *CLASS_NAME* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Bezeichner und als Klasse in der Assembly vorhanden sein. Wenn die Klasse hat ein Namespace qualifizierten Namen ein Punkt verwendet (**.**) um die einzelnen Bestandteile des Namespace voneinander zu trennen, muss der Klassenname durch eckige Klammern begrenzt werden (**[]**) oder Anführungszeichen (**""**). Bei der angegebenen Methode muss es sich um eine statische Methode der Klasse handeln.  
  
 Standardmäßig kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keinen CLR-Code ausführen. Sie können erstellen, ändern und Löschen von Datenbankobjekten, die common Language Runtime-Module verweisen; Allerdings kann nicht Ausführen dieser Verweise in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erst nach Aktivierung der [Option Clr-fähig](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Verwenden Sie zum Aktivieren der Option [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  CLR-Prozeduren werden in einer enthaltenen Datenbank nicht unterstützt.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] -gespeicherte Prozeduren können nicht in CLR-gespeicherte Prozeduren geändert werden und umgekehrt.  
  
 ALTER PROCEDURE ändert keine Berechtigungen und wirkt sich nicht auf abhängige gespeicherte Prozeduren oder Trigger aus. Die Einstellungen der aktuellen Sitzung für QUOTED_IDENTIFIER und ANSI_NULLS werden jedoch in der gespeicherten Prozedur berücksichtigt, wenn diese geändert wird. Unterscheiden sich die Einstellungen von denen, die bei der Erstellung der gespeicherten Prozedur gültig waren, ändert sich das Verhalten der gespeicherten Prozedur möglicherweise.  
  
 Wenn eine vorherige Prozedurdefinition mit WITH ENCRYPTION oder WITH RECOMPILE erstellt wurde, sind diese Optionen nur dann aktiviert, wenn sie in der ALTER PROCEDURE-Anweisung enthalten sind.  
  
 Weitere Informationen zu gespeicherten Prozeduren finden Sie unter [CREATE PROCEDURE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-procedure-transact-sql.md).  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert **ALTER** Berechtigung für die Prozedur oder die Mitgliedschaft in der **Db_ddladmin** festen Datenbankrolle "".  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die gespeicherte `uspVendorAllInfo`-Prozedur erstellt. Diese Prozedur gibt die Namen, die gelieferten Produkte, die Bonität und die Verfügbarkeit aller Hersteller, die [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] beliefern, zurück. Nachdem diese Prozedur erstellt wurde, wird sie so geändert, dass ein anderes Resultset zurückgegeben wird.  
  
```  
  
IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
    DROP PROCEDURE Purchasing.uspVendorAllInfo;  
GO  
CREATE PROCEDURE Purchasing.uspVendorAllInfo  
WITH EXECUTE AS CALLER  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS Vendor, p.Name AS 'Product name',   
      v.CreditRating AS 'Rating',   
      v.ActiveFlag AS Availability  
    FROM Purchasing.Vendor v   
    INNER JOIN Purchasing.ProductVendor pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product p  
      ON pv.ProductID = p.ProductID   
    ORDER BY v.Name ASC;  
GO  
  
```  
  
 Im folgenden Beispiel wird die gespeicherte `uspVendorAllInfo`-Prozedur geändert. Die EXECUTE AS CALLER-Klausel entfernt, und ändert den Textkörper der Prozedur nur Hersteller zurückgegeben, die das angegebene Produkt liefern. Mit den Funktionen `LEFT` und `CASE` wird die Darstellung des Resultsets angepasst.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER PROCEDURE Purchasing.uspVendorAllInfo  
    @Product varchar(25)   
AS  
    SET NOCOUNT ON;  
    SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
    'Rating' = CASE v.CreditRating   
        WHEN 1 THEN 'Superior'  
        WHEN 2 THEN 'Excellent'  
        WHEN 3 THEN 'Above average'  
        WHEN 4 THEN 'Average'  
        WHEN 5 THEN 'Below average'  
        ELSE 'No rating'  
        END  
    , Availability = CASE v.ActiveFlag  
        WHEN 1 THEN 'Yes'  
        ELSE 'No'  
        END  
    FROM Purchasing.Vendor AS v   
    INNER JOIN Purchasing.ProductVendor AS pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID   
    WHERE p.Name LIKE @Product  
    ORDER BY v.Name ASC;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Vendor               Product name  Rating    Availability  
-------------------- ------------- -------   ------------  
Proseware, Inc.      LL Crankarm   Average   No  
Vision Cycles, Inc.  LL Crankarm   Superior  Yes  
(2 row(s) affected)`  
```  

## <a name="see-also"></a>Siehe auch  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DROP PROCEDURE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Führen Sie AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Gespeicherte Prozeduren &#40;Datenbankmodul&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [Sys.Procedures &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)  
  
  

