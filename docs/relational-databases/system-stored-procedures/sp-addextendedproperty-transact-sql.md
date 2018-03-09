---
title: Sp_addextendedproperty (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addextendedproperty
- sp_addextendedproperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproperty
ms.assetid: 565483ea-875b-4133-b327-d0006d2d7b4c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5788b9d376acd46d7e7b357d70a4dd93aaa58064
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spaddextendedproperty-transact-sql"></a>sp_addextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Fügt eine neue erweiterte Eigenschaft zu einem Datenbankobjekt hinzu.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addextendedproperty  
    [ @name = ] { 'property_name' }  
    [ , [ @value = ] { 'value' }   
        [ , [ @level0type = ] { 'level0_object_type' }   
          , [ @level0name = ] { 'level0_object_name' }   
                [ , [ @level1type = ] { 'level1_object_type' }   
                  , [ @level1name = ] { 'level1_object_name' }   
                        [ , [ @level2type = ] { 'level2_object_type' }   
                          , [ @level2name = ] { 'level2_object_name' }   
                        ]   
                ]  
        ]   
    ]   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @name ] = {'*Property_name*'}  
 Ist der Name der Eigenschaft hinzugefügt werden. *Property_name* ist **Sysname** und darf nicht NULL sein. Namen können auch leere oder nicht alphanumerische Zeichenfolgen sowie binäre Werte sein.  
  
 [ @value=] {"*Wert*'}  
 Der Wert, der der Eigenschaft zugeordnet werden soll. *Wert* ist **Sql_variant**, hat den Standardwert NULL. *value* kann nicht größer als 7.500 Bytes sein.  
  
 [ @level0type=] {"*level0_object_type*'}  
 Der Typ des Objekts der Ebene 0. *level0_object_type* ist **varchar(128)**, hat den Standardwert NULL.  
  
 Gültige Eingabewerte sind ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, USER, TRIGGER, TYPE, PLAN GUIDE und NULL.  
  
> [!IMPORTANT]  
>  In zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird es nicht mehr möglich sein, USER als Typ der Ebene 0 in einer erweiterten Eigenschaft eines Typobjekts der Ebene 1 anzugeben. Verwenden Sie stattdessen SCHEMA als Typ der Ebene 0. Beispiel: Wenn Sie eine erweiterte Eigenschaft für eine Tabelle definieren, geben Sie das Schema der Tabelle statt eines Benutzernamens an. In zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann TYPE nicht mehr als Typ der Ebene 0 angegeben werden. Verwenden Sie für TYPE als Typ der Ebene 0 SCHEMA und TYPE als Typ der Ebene 1.  
  
 [ @level0name=] {"*level0_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 0. *level0_object_name* ist **Sysname** hat den Standardwert NULL.  
  
 [ @level1type=] {"*level1_object_type*'}  
 Der Typ des Objekts der Ebene 1. *level1_object_type* ist **varchar(128)**, hat den Standardwert NULL. Gültige Eingabewerte sind AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION und NULL.  
  
 [ @level1name=] {"*level1_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 1. *level1_object_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ @level2type=] {"*level2_object_type*'}  
 Der Typ des Objekts der Ebene 2. *level2_object_type* ist **varchar(128)**, hat den Standardwert NULL. Gültige Eingabewerte sind COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER und NULL.  
  
 [ @level2name=] {"*level2_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 2. *level2_object_name* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Beim Festlegen erweiterter Eigenschaften werden die Objekte in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank in drei Ebenen unterteilt: 0, 1 und 2. Ebene 0 ist die höchste Ebene und als im Datenbankbereich enthaltene Objekte definiert. Objekte der Ebene 1 sind in einem Schema- oder Benutzerbereich enthalten, und Objekte der Ebene 2 sind in Objekten der Ebene 1 enthalten. Erweiterte Eigenschaften können für Objekte auf einer dieser Ebenen definiert werden.  
  
 Verweise auf ein Objekt einer Ebene müssen mit den Namen der Objekte der höheren Ebene gekennzeichnet werden, die diese besitzen oder enthalten. Wenn Sie beispielsweise einer Tabellenspalte (Ebene 2) eine erweiterte Eigenschaft hinzufügen, müssen Sie auch den Tabellennamen (Ebene 1) angeben, der die Spalte und das Schema (Ebene 0) enthält, das die Tabelle enthält.  
  
 Wenn alle Objekttypen und -namen NULL sind, gehört die Eigenschaft zur aktuellen Datenbank.  
  
 Erweiterte Eigenschaften sind für Systemobjekte, Objekte außerhalb des Bereichs einer benutzerdefinierten Datenbank oder Objekte, die nicht als gültige Eingaben unter den Argumenten aufgelistet sind, nicht zulässig.  
  
 Erweiterte Eigenschaften werden für Speicheroptimierte Tabellen nicht zulässig.  
  
## <a name="replicating-extended-properties"></a>Replizieren erweiterter Eigenschaften  
 Erweiterte Eigenschaften werden nur in der ersten Synchronisierung zwischen dem Verleger und dem Abonnenten repliziert. Wenn Sie eine erweiterte Eigenschaft nach der ersten Synchronisierung hinzufügen oder ändern, wird die Änderung nicht repliziert. Weitere Informationen über das Replizieren von Datenbanken finden Sie unter [Veröffentlichen von Daten und Datenbankobjekte](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
## <a name="schema-vs-user"></a>Schema oder Benutzer  
 Es wird nicht empfohlen, USER als einen Typ der Ebene 0 anzugeben, wenn eine erweiterte Eigenschaft auf ein Datenbankobjekt angewendet wird, da dies zu Mehrdeutigkeiten bei der Namensauflösung führen kann. Angenommen, Benutzer Mary besitzt beispielsweise zwei Schemas (Mary und MySchema), und diese Schemas enthalten beide eine Tabelle namens MyTable. Wenn Mary MyTable-Tabelle eine erweiterte Eigenschaft hinzufügt und gibt  **@level0type @level0type = "**,  **@level0name = Mary**, es ist nicht klar, auf welche Tabelle die erweiterte Eigenschaft angewendet wird. Aus Gründen der Abwärtskompatibilität wendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Eigenschaft auf die Tabelle im Schema namens Mary an.  
  
## <a name="permissions"></a>Berechtigungen  
 Mitglieder der festen Datenbankrollen db_owner und db_ddladmin können beliebigen Objekten erweiterte Eigenschaften hinzufügen, wobei die folgende Ausnahme gilt: db_ddladmin kann weder der Datenbank noch Benutzern oder Rollen Eigenschaften hinzufügen.  
  
 Benutzer können erweiterte Eigenschaften zu Objekten hinzufügen, die sie besitzen, oder für die sie die ALTER- oder CONTROL-Berechtigung haben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-adding-an-extended-property-to-a-database"></a>A. Hinzufügen einer erweiterten Eigenschaft zu einer Datenbank  
 Im folgenden Beispiel wird der `'Caption'` -Beispieldatenbank der Eigenschaftsname `'AdventureWorks2012 Sample OLTP Database'` mit dem Wert `AdventureWorks2012` hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
--Add a caption to the AdventureWorks2012 Database object itself.  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'AdventureWorks2012 Sample OLTP Database';  
```  
  
### <a name="b-adding-an-extended-property-to-a-column-in-a-table"></a>B. Hinzufügen einer erweiterten Eigenschaft zu einer Spalte in einer Tabelle  
 Im folgenden Beispiel wird der `PostalCode` -Spalte in der `Address`-Tabelle eine Caption-Eigenschaft hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'Postal code is a required column.',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table',  @level1name = 'Address',  
@level2type = N'Column', @level2name = 'PostalCode';  
GO  
```  
  
### <a name="c-adding-an-input-mask-property-to-a-column"></a>C. Hinzufügen einer InputMask-Eigenschaft zu einer Spalte  
 Im folgenden Beispiel wird der`99999 or 99999-9999 or #### ###`-Spalte in der `PostalCode` -Tabelle eine InputMask-Eigenschaft mit dem Wert ' `Address`hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Input Mask ', @value = '99999 or 99999-9999 or #### ###',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table', @level1name = 'Address',   
@level2type = N'Column',@level2name = 'PostalCode';  
GO  
```  
  
### <a name="d-adding-an-extended-property-to-a-filegroup"></a>D. Hinzufügen einer erweiterten Eigenschaft zu einer Dateigruppe  
 Im folgenden Beispiel wird der `PRIMARY` -Dateigruppe eine erweiterte Eigenschaft hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Primary filegroup for the AdventureWorks2012 sample database.',   
@level0type = N'FILEGROUP', @level0name = 'PRIMARY';  
GO  
```  
  
### <a name="e-adding-an-extended-property-to-a-schema"></a>E. Hinzufügen einer erweiterten Eigenschaft zu einem Schema  
 Im folgenden Beispiel wird dem `HumanResources` -Schema eine erweiterte Eigenschaft hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',  
@value = N'Contains objects related to employees and departments.',  
@level0type = N'SCHEMA',   
@level0name = 'HumanResources';  
```  
  
### <a name="f-adding-an-extended-property-to-a-table"></a>F. Hinzufügen einer erweiterten Eigenschaft zu einer Tabelle  
 Im folgenden Beispiel wird der `Address` -Tabelle im `Person` -Schema eine erweiterte Eigenschaft hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Street address information for customers, employees, and vendors.',   
@level0type = N'SCHEMA', @level0name = 'Person',  
@level1type = N'TABLE',  @level1name = 'Address';  
GO  
```  
  
### <a name="g-adding-an-extended-property-to-a-role"></a>G. Hinzufügen einer erweiterten Eigenschaft zu einer Rolle  
 Im folgenden Beispiel wird eine Anwendungsrolle erstellt, und der Rolle wird eine erweiterte Eigenschaft hinzugefügt.  
  
```  
USE AdventureWorks2012;   
GO  
CREATE APPLICATION ROLE Buyers  
WITH Password = '987G^bv876sPY)Y5m23';   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Application Role for the Purchasing Department.',  
@level0type = N'USER',  
@level0name = 'Buyers';  
```  
  
### <a name="h-adding-an-extended-property-to-a-type"></a>H. Hinzufügen einer erweiterten Eigenschaft zu einem Typ  
 Im folgenden Beispiel wird einem Typ eine erweiterte Eigenschaft hinzugefügt.  
  
```  
USE AdventureWorks2012;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Data type (alias) to use for any column that represents an order number. For example a sales order number or purchase order number.',   
@level0type = N'SCHEMA',   
@level0name = N'dbo',   
@level1type = N'TYPE',   
@level1name = N'OrderNumber';  
```  
  
### <a name="i-adding-an-extended-property-to-a-user"></a>I. Hinzufügen einer erweiterten Eigenschaft zu einem Benutzer  
 Im folgenden Beispiel wird ein Benutzer erstellt und diesem eine erweiterte Eigenschaft hinzugefügt.  
  
```  
USE AdventureWorks2012;   
GO  
CREATE USER CustomApp WITHOUT LOGIN ;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'User for an application.',   
@level0type = N'USER',   
@level0name = N'CustomApp';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Sys.fn_listextendedproperty &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [Sp_dropextendedproperty &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [Sp_updateextendedproperty &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)  
  
  
