---
title: Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], examples
- metadata [SQL Server], frequently asked questions
- metadata [SQL Server], example queries
- system catalogs [SQL Server], example queries
- catalog views [SQL Server], frequently asked questions
ms.assetid: ca202580-c37e-4ccd-9275-77ce79481f64
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 28cf58ccd693f0c958901487a8387dd9d1c1073b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="querying-the-sql-server-system-catalog-faq"></a>FAQ: Abfragen des SQL Server-Systemkatalogs
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dieses Thema enthält eine Liste häufig gestellter Fragen. Die Antworten auf diese Fragen sind Abfragen, die auf Katalogsichten basieren.  
  
##  <a name="_TOP"></a> Häufig gestellte Fragen  
 In den nachfolgenden Abschnitten werden häufig gestellte Fragen nach Kategorien aufgelistet.  
  
### <a name="data-types"></a>Datentypen  
  
-   [Wie finde ich die Datentypen der Spalten einer angegebenen Tabelle?](#_FAQ7)  
  
-   [Wie finde ich die LOB-Datentypen einer angegebenen Tabelle?](#_FAQ14)  
  
-   [Wie finde ich die Spalten, die einen angegebenen Datentyp abhängig sind?](#_FAQ22)  
  
-   [Wie finde ich die berechneten Spalten, die von einem angegebenen CLR-benutzerdefinierten Typ oder Aliasdatentyp abhängen?](#_FAQ23)  
  
-   [Wie finde ich die Parameter, die von einem angegebenen CLR-benutzerdefinierten Typ oder Aliasdatentyp abhängen?](#_FAQ24)  
  
-   [Wie finde ich die CHECK-Einschränkungen, die einem angegebenen CLR-benutzerdefinierten Typ abhängig sind?](#_FAQ25)  
  
-   [Wie finde ich die Sichten, Transact-SQL-Funktionen und gespeicherten Transact-SQL-Prozeduren, die von einem angegebenen CLR-benutzerdefinierten Typ oder Aliasdatentyp abhängen?](#_FAQ26)  
  
### <a name="tables-indexes-views-and-constraints"></a>Tabellen, Indizes, Sichten und Einschränkungen  
  
-   [Wie finde ich alle benutzerdefinierten Tabellen in einer angegebenen Datenbank?](#_FAQ31)  
  
-   [Wie finde ich alle Tabellen, auf denen kein gruppierten Indexes in einer angegebenen Datenbank?](#_FAQ1)  
  
-   [Wie finde ich alle Tabellen, die nicht über einen Index besitzen?](#_FAQ4)  
  
-   [Wie finde ich alle Tabellen, die nicht über einen Primärschlüssel verfügen?](#_FAQ3)  
  
-   [Wie finde ich alle Tabellen, die eine Identitätsspalte verfügen?](#_FAQ5)  
  
-   [Wie finde ich alle Tabellen und Indizes, die partitioniert sind?](#_FAQ32)  
  
-   [Wie finde ich alle Sichten in einer Datenbank?](#_FAQ13)  
  
-   [Wie finde ich die Definition einer Sicht?](#_FAQ35)  
  
-   [Wie finde ich alle Entitäten, die in den letzten N Tagen geändert wurden?](#_FAQ6)  
  
-   [Wie finde ich die Spalten eines Primärschlüssels für eine angegebene Tabelle?](#_FAQ16)  
  
-   [Wie finde ich die Spalten eines Fremdschlüssels für eine angegebene Tabelle?](#_FAQ17)  
  
-   [Wie erkenne ich, wenn eine Spalte in einem berechneten Spaltenausdruck verwendet wird?](#_FAQ20)  
  
-   [Wie finde ich alle Spalten, die verwendet werden, in einem berechneten Spaltenausdruck?](#_FAQ21)  
  
-   [Wie finde ich alle Einschränkungen für eine angegebene Tabelle?](#_FAQ27)  
  
-   [Wie finde ich alle Indizes für eine angegebene Tabelle?](#_FAQ28)  
  
-   [Wie finde ich alle Tabellen, die einen angegebenen Spaltennamen aufweisen?](#_FAQ30)  
  
-   [Wie finde ich alle Statistiken für ein angegebenes Objekt?](#_FAQ33)  
  
-   [Wie finde ich alle Statistiken und Statistikspalten für ein angegebenes Objekt?](#_FAQ34)  
  
### <a name="modules-stored-procedures-user-defined-functions-and-triggers"></a>Module (Gespeicherte Prozeduren, benutzerdefinierte Funktionen und Trigger).  
  
-   [Wie finde ich alle gespeicherten Prozeduren in einer Datenbank?](#_FAQ9)  
  
-   [Wie finde ich alle benutzerdefinierten Funktionen in einer Datenbank?](#_FAQ12)  
  
-   [Wie finde ich die Parameter für eine angegebene gespeicherte Prozedur oder Funktion?](#_FAQ10)  
  
-   [Wie finde ich die Abhängigkeiten von einer angegebenen Funktion?](#_FAQ8)  
  
-   [Wie zeige ich die Definition eines Moduls an?](#_FAQ15)  
  
-   [Wie zeige ich die Definition eines Triggers auf Serverebene an?](#_FAQ19)  
  
### <a name="schemas-users-roles-and-permissions"></a>Schemas, Benutzer, Rollen und Berechtigungen  
  
-   [Wie finde ich alle Besitzer von Entitäten in einem angegebenen Schema enthalten sind?](#_FAQ2)  
  
-   [Wie finde ich die Berechtigungen, die einem angegebenen Prinzipal erteilt oder verweigert?](#_FAQ18)  
  
## <a name="answers"></a>Antworten  
  
###  <a name="_FAQ1"></a> Wie finde ich alle Tabellen, auf denen kein gruppierten Indexes in einer angegebenen Datenbank?  
 Vor dem Ausführen der folgenden Abfragen ersetzen Sie `<database_name>` durch einen gültigen Datenbanknamen.  
  
```  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name, t.name AS table_name  
FROM sys.tables AS t  
WHERE NOT EXISTS   
   (  
     SELECT * FROM sys.indexes AS i  
     WHERE i.object_id = t.object_id  
     AND i.type = 1  -- or type_desc = 'CLUSTERED'  
   )  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 Sie können auch die `OBJECTPROPERTY`-Funktion wie im folgenden Beispiel gezeigt verwenden.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name, name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasClustIndex') = 0  
ORDER BY schema_id, name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ2"></a> Wie finde ich alle Besitzer von Entitäten in einem angegebenen Schema enthalten sind?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT 'OBJECT' AS entity_type  
    ,USER_NAME(OBJECTPROPERTY(object_id, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.objects WHERE SCHEMA_NAME(schema_id) = '<schema_name>'  
UNION   
SELECT 'TYPE' AS entity_type  
    ,USER_NAME(TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.types WHERE SCHEMA_NAME(schema_id) = '<schema_name>'   
UNION  
SELECT 'XML SCHEMA COLLECTION' AS entity_type   
    ,COALESCE(USER_NAME(xsc.principal_id),USER_NAME(s.principal_id)) AS owner_name  
    ,xsc.name   
FROM sys.xml_schema_collections AS xsc JOIN sys.schemas AS s  
    ON s.schema_id = xsc.schema_id  
WHERE s.name = '<schema_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ3"></a> Wie finde ich alle Tabellen, die nicht über einen Primärschlüssel verfügen?  
 Vor dem Ausführen der folgenden Abfragen ersetzen Sie `<database_name>` durch einen gültigen Datenbanknamen.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name  
    ,t.name AS table_name  
FROM sys.tables t   
WHERE object_id NOT IN   
   (  
    SELECT parent_object_id   
    FROM sys.key_constraints   
    WHERE type_desc = 'PRIMARY_KEY_CONSTRAINT' -- or type = 'PK'  
    );  
GO  
  
```  
  
 Alternativ können Sie die folgende Abfrage ausführen:  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ4"></a> Wie finde ich alle Tabellen, die nicht über einen Index besitzen?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Datenbanknamen.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'IsIndexed') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ5"></a> Wie finde ich alle Tabellen, die eine Identitätsspalte verfügen?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Datenbanknamen.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    , t.name AS table_name  
    , c.name AS column_name  
FROM sys.tables AS t  
JOIN sys.identity_columns c ON t.object_id = c.object_id  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 Alternativ können Sie die folgende Abfrage ausführen:  
  
> [!NOTE]  
>  Diese Abfrage gibt nicht den Namen der Spalten zurück.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasIdentity') = 1  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ7"></a> Wie finde ich die Datentypen der Spalten einer angegebenen Tabelle?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.table_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT c.name AS column_name  
    ,c.column_id  
    ,SCHEMA_NAME(t.schema_id) AS type_schema  
    ,t.name AS type_name  
    ,t.is_user_defined  
    ,t.is_assembly_type  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
FROM sys.columns AS c   
JOIN sys.types AS t ON c.user_type_id=t.user_type_id  
WHERE c.object_id = OBJECT_ID('<schema_name.table_name>')  
ORDER BY c.column_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ8"></a> Wie finde ich die Abhängigkeiten von einer angegebenen Funktion?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.function_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS referencing_object_name  
    ,COALESCE(COL_NAME(object_id, column_id), '(n/a)') AS referencing_column_name  
    ,*  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.function_name>')  
ORDER BY OBJECT_NAME(object_id), COL_NAME(object_id, column_id);  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ9"></a> Wie finde ich alle gespeicherten Prozeduren in einer Datenbank?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen.  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS procedure_name   
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
FROM sys.procedures;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ10"></a> Wie finde ich die Parameter für eine angegebene gespeicherte Prozedur oder Funktion?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.object_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,o.name AS object_name  
    ,o.type_desc  
    ,p.parameter_id  
    ,p.name AS parameter_name  
    ,TYPE_NAME(p.user_type_id) AS parameter_type  
    ,p.max_length  
    ,p.precision  
    ,p.scale  
    ,p.is_output  
FROM sys.objects AS o  
INNER JOIN sys.parameters AS p ON o.object_id = p.object_id  
WHERE o.object_id = OBJECT_ID('<schema_name.object_name>')  
ORDER BY schema_name, object_name, p.parameter_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ12"></a> Wie finde ich alle benutzerdefinierten Funktionen in einer Datenbank?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Datenbanknamen.  
  
```  
USE <database_name>;  
GO  
SELECT name AS function_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE type_desc LIKE '%FUNCTION%';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ13"></a> Wie finde ich alle Sichten in einer Datenbank?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Datenbanknamen.  
  
```  
USE <database_name>;  
GO  
SELECT name AS view_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,OBJECTPROPERTYEX(object_id,'IsIndexed') AS IsIndexed  
  ,OBJECTPROPERTYEX(object_id,'IsIndexable') AS IsIndexable  
  ,create_date  
  ,modify_date  
FROM sys.views;  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ6"></a> Wie finde ich alle Entitäten, die in den letzten N Tagen geändert wurden?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` und `<n_days>` durch gültige Werte.  
  
```  
USE <database_name>;  
GO  
SELECT name AS object_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE modify_date > GETDATE() - <n_days>  
ORDER BY modify_date;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ14"></a> Wie finde ich die LOB-Datentypen einer angegebenen Tabelle?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.table_name>` durch gültige Namen.  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS column_name   
    ,column_id   
    ,TYPE_NAME(user_type_id) AS type_name  
    ,max_length  
    ,CASE   
       WHEN max_length = -1 AND TYPE_NAME(user_type_id) <> 'xml'  
            THEN 1  
            ELSE 0  
     END AS [(max)]  
FROM sys.columns  
WHERE object_id=OBJECT_ID('<schema_name.table_name>')   
    AND ( TYPE_NAME(user_type_id) IN ('xml','text', 'ntext','image')  
         OR (TYPE_NAME(user_type_id) IN ('varchar','nvarchar','varbinary')  
         AND max_length = -1)  
        );  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ15"></a> Wie zeige ich die Definition eines Moduls an?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.object_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 Sie können auch die `OBJECT_DEFINITION`-Funktion wie im folgenden Beispiel gezeigt verwenden.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ19"></a> Wie zeige ich die Definition eines Triggers auf Serverebene an?  
  
```  
SELECT definition  
FROM sys.server_sql_modules;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ16"></a> Wie finde ich die Spalten eines Primärschlüssels für eine angegebene Tabelle?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.table_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,ic.index_column_id  
    ,key_ordinal  
    ,c.name AS column_name  
    ,TYPE_NAME(c.user_type_id)AS column_type   
    ,is_identity  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
INNER JOIN sys.columns AS c   
    ON ic.object_id = c.object_id AND c.column_id = ic.column_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 Sie können auch die `COL_NAME`-Funktion wie im folgenden Beispiel gezeigt verwenden.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,key_ordinal  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ17"></a> Wie finde ich die Spalten eines Fremdschlüssels für eine angegebene Tabelle?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.table_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT   
    f.name AS foreign_key_name  
   ,OBJECT_NAME(f.parent_object_id) AS table_name  
   ,COL_NAME(fc.parent_object_id, fc.parent_column_id) AS constraint_column_name  
   ,OBJECT_NAME (f.referenced_object_id) AS referenced_object  
   ,COL_NAME(fc.referenced_object_id, fc.referenced_column_id) AS referenced_column_name  
   ,is_disabled  
   ,delete_referential_action_desc  
   ,update_referential_action_desc  
FROM sys.foreign_keys AS f  
INNER JOIN sys.foreign_key_columns AS fc   
   ON f.object_id = fc.constraint_object_id   
WHERE f.parent_object_id = OBJECT_ID('<schema_name.table_name>');  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ18"></a> Wie finde ich die Berechtigungen, die einem angegebenen Prinzipal erteilt oder verweigert?  
 Im folgenden Beispiel wird eine Funktion erstellt, die den Namen der Entität zurückgibt, deren Berechtigungen überprüft werden. Die Funktion wird in den nachfolgenden Abfragen aufgerufen. Die Funktion muss in jeder Datenbank erstellt werden, in der Sie die Berechtigungen überprüfen möchten.  
  
```  
-- Create a function to return the name of the entity on which the permissions are checked.  
IF OBJECT_ID (N'dbo.entity_instance_name', N'FN') IS NOT NULL  
    DROP FUNCTION dbo.entity_instance_name;  
GO  
CREATE FUNCTION dbo.entity_instance_name(@class_desc nvarchar(60), @major_id int)   
RETURNS sysname AS  
BEGIN  
    DECLARE @the_entity_name sysname  
    SELECT @the_entity_name = CASE  
        WHEN @class_desc = 'DATABASE' THEN DB_NAME()  
        WHEN @class_desc = 'SCHEMA' THEN SCHEMA_NAME(@major_id)  
        WHEN @class_desc = 'OBJECT_OR_COLUMN' THEN OBJECT_NAME(@major_id)  
        WHEN @class_desc = 'DATABASE_PRINCIPAL' THEN USER_NAME(@major_id)  
        WHEN @class_desc = 'ASSEMBLY' THEN   
            (SELECT name FROM sys.assemblies WHERE assembly_id=@major_id)  
        WHEN @class_desc = 'TYPE' THEN TYPE_NAME(@major_id)  
        WHEN @class_desc = 'XML_SCHEMA_COLLECTION' THEN   
            (SELECT name FROM sys.xml_schema_collections  
              WHERE xml_collection_id=@major_id)  
        WHEN @class_desc = 'MESSAGE_TYPE' THEN   
            (SELECT name FROM sys.service_message_types WHERE message_type_id=@major_id)  
        WHEN @class_desc = 'SERVICE_CONTRACT' THEN   
           (SELECT name FROM sys.service_contracts  
              WHERE service_contract_id=@major_id)  
        WHEN @class_desc = 'SERVICE' THEN  
          (SELECT name FROM sys.services WHERE service_id=@major_id)  
        WHEN @class_desc = 'REMOTE_SERVICE_BINDING' THEN  
          (SELECT name FROM sys.remote_service_bindings  
             WHERE remote_service_binding_id=@major_id)  
        WHEN @class_desc = 'ROUTE' THEN  
          (SELECT name FROM sys.routes WHERE route_id=@major_id)  
        WHEN @class_desc = 'FULLTEXT_CATALOG' THEN  
          (SELECT name FROM sys.fulltext_catalogs WHERE fulltext_catalog_id=@major_id)  
        WHEN @class_desc = 'SYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.symmetric_keys WHERE symmetric_key_id=@major_id)  
        WHEN @class_desc = 'CERTIFICATE' THEN  
          (SELECT name FROM sys.certificates WHERE certificate_id=@major_id)  
        WHEN @class_desc = 'ASYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.asymmetric_keys WHERE asymmetric_key_id=@major_id)  
        WHEN @class_desc = 'SERVER' THEN   
             (SELECT name FROM sys.servers WHERE server_id=@major_id)  
        WHEN @class_desc = 'SERVER_PRINCIPAL' THEN SUSER_NAME(@major_id)  
        WHEN @class_desc = 'ENDPOINT' THEN   
             (SELECT name FROM sys.endpoints WHERE endpoint_id=@major_id)        
        ELSE '?'  
    END  
    RETURN @the_entity_name  
END;  
GO  
-- Return server-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc, major_id) AS entity_name   
    ,minor_id  
    ,SUSER_NAME(grantee_principal_id) AS grantee  
    ,SUSER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc   
FROM sys.server_permissions   
WHERE grantee_principal_id = SUSER_ID('public');  
GO  
-- Return database-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc , major_id) AS entity_name   
    ,minor_id  
    ,USER_NAME(grantee_principal_id) AS grantee  
    ,USER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc     
FROM  sys.database_permissions   
WHERE grantee_principal_id = DATABASE_PRINCIPAL_ID('public');  
GO  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ20"></a> Wie erkenne ich, wenn eine Spalte in einem berechneten Spaltenausdruck verwendet wird?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>`, `<schema_name.table_name>` und `<column_name`> durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS computed_column   
    ,class_desc  
    ,is_selected  
    ,is_updated  
    ,is_select_all  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.table_name>')  
    AND referenced_minor_id = COLUMNPROPERTY(referenced_major_id, '<column_name>', 'ColumnId')  
    AND class = 1;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ21"></a> Wie finde ich alle Spalten, die verwendet werden, in einem berechneten Spaltenausdruck?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(d.referenced_major_id) AS object_name  
    ,COL_NAME(d.referenced_major_id, d.referenced_minor_id) AS column_name  
    ,OBJECT_NAME(referenced_major_id) AS dependent_object_name   
    ,COL_NAME(d.object_id, d.column_id) AS dependent_computed_column  
    ,cc.definition AS computed_column_definition  
FROM sys.sql_dependencies AS d  
JOIN sys.computed_columns AS cc   
    ON cc.object_id = d.object_id AND cc.column_id = d.column_id AND d.object_id=d.referenced_major_id       
WHERE d.class = 1  
ORDER BY object_name, column_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ22"></a> Wie finde ich die Spalten, die von einem angegebenen CLR-benutzerdefinierten Typ oder Aliasdatentyp abhängen?  
 Vor dem Ausführen der folgenden Abfrage ersetzen `<database_name>` durch einen gültigen Namen und `<schema_name.data_type_name>` mit einem gültigen, schemaqualifizierte CLR-benutzerdefinierten Typ oder schemaqualifizierte Alias-Typnamen. Die folgende Abfrage erfordert die Mitgliedschaft in der **Db_owner** Rolle oder die Berechtigungen zum Anzeigen aller abhängigen Spalten und berechneten Spalte Metadaten in der Datenbank.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,c.name AS column_name   
    ,SCHEMA_NAME(t.schema_id) AS schema_name  
    ,TYPE_NAME(c.user_type_id) AS user_type_name  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
    ,c.is_nullable  
    ,c.is_computed  
FROM sys.columns AS c  
INNER JOIN sys.types AS t ON c.user_type_id = t.user_type_id  
WHERE c.user_type_id = TYPE_ID('<schema_name.data_type_name>');   
GO  
  
```  
  
 Die folgende Abfrage gibt eine eingeschränkte und schmale Ansicht der Spalten von abhängt, die einen CLR-benutzerdefinierten Typ oder einen Alias zurück, aber das Resultset ist sichtbar, um die **öffentlichen** Rolle. Sie können diese Abfrage verwenden, wenn Sie anderen Benutzern REFERENCE-Berechtigungen für den benutzerdefinierten Typ gewährt haben, oder wenn Sie keine Berechtigung zum Anzeigen der Metadaten für Objekte haben, die von anderen Benutzern, die diesen Typ verwenden, erstellt wurden.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,COL_NAME(object_id, column_id) AS column_name  
    ,TYPE_NAME(user_type_id) AS user_type  
FROM sys.column_type_usages  
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ23"></a> Wie finde ich die berechneten Spalten, die von einem angegebenen CLR-benutzerdefinierten Typ oder Aliasdatentyp abhängen?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen und `<schema_name.data_type_name>` durch einen gültigen CLR-benutzerdefinierten Typ, der im Schema qualifiziert ist oder einen Alias-Typnamen.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS column_name  
FROM sys.sql_dependencies  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(object_id, 'IsTable') = 1;   -- exclude non-table dependencies  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ24"></a> Wie finde ich die Parameter, die von einem angegebenen CLR-benutzerdefinierten Typ oder Aliasdatentyp abhängen?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen und `<schema_name.data_type_name>` durch einen gültigen CLR-benutzerdefinierten Typ, der im Schema qualifiziert ist oder einen Alias-Typnamen. Die folgende Abfrage erfordert die Mitgliedschaft in der **Db_owner** Rolle oder die Berechtigungen zum Anzeigen aller abhängigen Spalten und berechneten Spalte Metadaten in der Datenbank.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,NULL AS procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
UNION   
SELECT OBJECT_NAME(object_id) AS object_name  
    ,procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.numbered_procedure_parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY object_name, procedure_number, param_num;  
GO  
  
```  
  
 Die folgende Abfrage gibt eine eingeschränkte und schmale Ansicht der Parameter, die von einem CLR-benutzerdefinierten Typ oder Alias abhängen, aber das Resultset ist sichtbar, um die **öffentlichen** Rolle. Sie können diese Abfrage verwenden, wenn Sie anderen Benutzern REFERENCE-Berechtigungen für den benutzerdefinierten Typ gewährt haben, oder wenn Sie keine Berechtigung zum Anzeigen der Metadaten für Objekte haben, die von anderen Benutzern, die diesen Typ verwenden, erstellt wurden.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,parameter_id  
    ,TYPE_NAME(user_type_id) AS type_name  
FROM sys.parameter_type_usages   
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ25"></a> Wie finde ich die CHECK-Einschränkungen, die einem angegebenen CLR-benutzerdefinierten Typ abhängig sind?  
 Vor dem Ausführen der folgenden Abfrage ersetzen `<database_name>` durch einen gültigen Namen und `<schema_name.data_type_name>` mit einem gültigen, der im Schema qualifiziert CLR-benutzerdefinierten Typ-Namen.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(o.parent_object_id) AS table_name  
    ,OBJECT_NAME(o.object_id) AS constraint_name  
FROM sys.sql_dependencies AS d  
JOIN sys.objects AS o ON o.object_id = d.object_id  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(o.object_id, 'IsCheckCnst') = 1; -- exclude non-CHECK dependencies  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ26"></a> Wie finde ich die Sichten, Transact-SQL-Funktionen und gespeicherten Transact-SQL-Prozeduren, die von einem angegebenen CLR-benutzerdefinierten Typ oder Aliasdatentyp abhängen?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen und `<schema_name.data_type_name>` durch einen gültigen CLR-benutzerdefinierten Typ, der im Schema qualifiziert ist oder einen Alias-Typnamen.  
  
 Die Parameter, die in einer Funktion oder Prozedur definiert werden, sind implizit schemagebunden. Aus diesem Grund können Parameter, die von einem CLR-benutzerdefinierten Typ oder Aliasdatentyp abhängen angezeigt werden, mithilfe der [sql_dependencies](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md) -Katalogsicht angezeigt. Prozeduren und Trigger sind nicht schemagebunden. Dies bedeutet, dass Abhängigkeiten zwischen Ausdrücken, die im Text einer Prozedur oder eines Triggers definiert werden, und einem CLR-benutzerdefinierten Typ oder Aliasdatentyp nicht beibehalten werden. Schemagebundene Sichten und schemagebundene benutzerdefinierte Funktionen, die Ausdrücke verfügen, die von einem CLR-benutzerdefinierten Typ abhängig sind oder Aliastyp in verwaltet die **sql_dependencies** -Katalogsicht angezeigt. Abhängigkeiten zwischen Typen, CLR-Funktionen und CLR-Prozeduren werden nicht beibehalten.  
  
 Mit der folgenden Abfrage werden alle schemagebundenen Abhängigkeiten in Sichten, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen und gespeicherten Prozeduren von [!INCLUDE[tsql](../../includes/tsql-md.md)] für einen angegebenen CLR-benutzerdefinierten Typ oder Aliastyp zurückgegeben.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS dependent_object_schema  
  ,OBJECT_NAME(o.object_id) AS dependent_object_name  
  ,o.type_desc AS dependent_object_type  
  ,d.class_desc AS kind_of_dependency  
  ,TYPE_NAME (d.referenced_major_id) AS type_name  
FROM sys.sql_dependencies AS d   
JOIN sys.objects AS o  
  ON d.object_id = o.object_id  
  AND o.type IN ('FN','IF','TF', 'V', 'P')  
WHERE d.class = 2 -- dependencies on types  
  AND d.referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY dependent_object_schema, dependent_object_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ27"></a> Wie finde ich alle Einschränkungen für eine angegebene Tabelle?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.table_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) as constraint_name  
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,OBJECT_NAME(parent_object_id) AS table_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
    ,is_ms_shipped  
    ,is_published  
    ,is_schema_published  
FROM sys.objects  
WHERE type_desc LIKE '%CONSTRAINT'   
    AND parent_object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ28"></a> Wie finde ich alle Indizes für eine angegebene Tabelle?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.table_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ30"></a> Wie finde ich alle Objekte, die einen angegebenen Spaltennamen aufweisen?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<column_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id)  
FROM sys.columns  
WHERE name = '<column_name>';  
GO  
  
```  
  
 oder  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name   
    ,o.name AS object_name  
    ,type_desc  
FROM sys.objects AS o  
INNER JOIN sys.columns AS c ON o.object_id = c.object_id  
WHERE c.name = '<column_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ31"></a> Wie finde ich alle benutzerdefinierten Tabellen in einer angegebenen Datenbank?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen.  
  
```  
USE <database_name>;  
GO  
SELECT *   
FROM sys.tables;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ32"></a> Wie finde ich alle Tabellen und Indizes, die partitioniert sind?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(p.object_id) AS table_name  
    ,i.name AS index_name  
    ,p.partition_number  
    ,rows   
FROM sys.partitions AS p  
INNER JOIN sys.indexes AS i ON p.object_id = i.object_id AND p.index_id = i.index_id  
INNER JOIN sys.partition_schemes ps ON i.data_space_id=ps.data_space_id  
INNER JOIN sys.objects AS o ON o.object_id = i.object_id  
ORDER BY index_name, partition_number;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ33"></a> Wie finde ich alle Statistiken für ein angegebenes Objekt?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen und `<schema_name.object_name>` durch eine gültige Tabelle oder eine indizierte Sicht oder einen gültigen Namen der Tabellenwertfunktion.  
  
```  
USE <database_name>;  
GO  
SELECT name AS statistics_name  
    ,stats_id  
    ,auto_created  
    ,user_created  
    ,no_recompute  
FROM sys.stats  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ34"></a> Wie finde ich alle Statistiken und Statistikspalten für ein angegebenes Objekt?  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Namen und `<schema_name.object_name>` durch eine gültige Tabelle oder eine indizierte Sicht oder einen gültigen Namen der Tabellenwertfunktion.  
  
```  
USE <database_name>;  
GO  
SELECT s.name AS statistics_name  
    ,c.name AS column_name  
    ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ35"></a> Wie finde ich die Definition einer Sicht?  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.object_name>` durch gültige Namen.  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 Sie können auch die `OBJECT_DEFINITION`-Funktion wie im folgenden Beispiel gezeigt verwenden.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
