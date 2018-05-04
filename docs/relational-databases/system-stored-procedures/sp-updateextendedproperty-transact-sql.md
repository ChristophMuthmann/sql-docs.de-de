---
title: Sp_updateextendedproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_updateextendedproperty_TSQL
- sp_updateextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updateextendedproperty
ms.assetid: 7f02360f-cb9e-48b4-b75f-29b4bc9ea304
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 61ce9da4c904811708e70a8670ecf64271e98574
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spupdateextendedproperty-transact-sql"></a>sp_updateextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Aktualisiert den Wert einer vorhandenen erweiterten Eigenschaft.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_updateextendedproperty  
    [ @name = ]{ 'property_name' }   
    [ , [ @value = ]{ 'value' }  
        [, [ @level0type = ]{ 'level0_object_type' }  
         , [ @level0name = ]{ 'level0_object_name' }  
              [, [ @level1type = ]{ 'level1_object_type' }  
               , [ @level1name = ]{ 'level1_object_name' }  
                     [, [ @level2type = ]{ 'level2_object_type' }  
                      , [ @level2name = ]{ 'level2_object_name' }  
                     ]  
              ]  
        ]  
    ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @name=] {"*Property_name*'}  
 Der Name der zu aktualisierenden Eigenschaft. *Property_name* ist **Sysname**, und darf nicht NULL sein.  
  
 [ @value=] {"*Wert*'}  
 Der Wert, der der Eigenschaft zugeordnet ist. *Wert* ist **Sql_variant**, hat den Standardwert NULL. Die Größe des *Wert* darf nicht größer als 7.500 Bytes sein.  
  
 [ @level0type=] {"*level0_object_type*'}  
 Der Benutzer oder benutzerdefinierte Typ. *level0_object_type* ist **varchar(128)**, hat den Standardwert NULL. Gültige Eingaben sind ASSEMBLY, Vertrag, EVENT NOTIFICATION, DATEIGRUPPE, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, PLAN GUIDE, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, Benutzer, TRIGGER, Typ und NULL.  
  
> [!IMPORTANT]  
>  USER und TYPE als Typen der Ebene 0 werden in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr unterstützt. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktionen zurzeit verwenden. Verwenden Sie SCHEMA anstelle von USER als Typ der Ebene 0. Verwenden Sie für TYPE als Typ der Ebene 0 SCHEMA und TYPE als Typ der Ebene 1.  
  
 [ @level0name=] {"*level0_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 1. *level0_object_name* ist **Sysname** hat den Standardwert NULL.  
  
 [ @level1type=] {"*level1_object_type*'}  
 Der Typ des Objekts der Ebene 1. *level1_object_type* ist **varchar(128)** hat den Standardwert NULL. Gültige Eingabewerte sind AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION und NULL.  
  
 [ @level1name=] {"*level1_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 1. *level1_object_name* ist **Sysname** hat den Standardwert NULL.  
  
 [ @level2type=] {"*level2_object_type*'}  
 Der Typ des Objekts der Ebene 2. *level2_object_type* ist **varchar(128)** hat den Standardwert NULL. Gültige Eingabewerte sind COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER und NULL.  
  
 [ @level2name=] {"*level2_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 2. *level2_object_name* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Für das Angeben erweiterter Eigenschaften werden die Objekte in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank in drei Ebenen (0, 1 und 2) unterteilt. Die Ebene 0 ist die höchste Ebene und ist definiert als Objekte, die im Datenbankbereich enthalten sind. Objekte der Ebene 1 sind in einem Schema- oder Benutzerbereich enthalten, und Objekte der Ebene 2 sind in Objekten der Ebene 1 enthalten. Erweiterte Eigenschaften können für Objekte auf einer dieser Ebenen definiert werden. Verweise auf ein Objekt einer Ebene müssen mit den Namen der Objekte der höheren Ebene gekennzeichnet werden, die diese besitzen oder enthalten.  
  
 Wenn bei einem gültigen *Property_name* und *Wert*, wenn alle Objekttypen und-Namen null sind, gehört die aktualisierte Eigenschaft zur aktuellen Datenbank.  
  
## <a name="permissions"></a>Berechtigungen  
 Mitglieder der festen Datenbankrollen db_owner und db_ddladmin können die erweiterten Eigenschaften jedes Objekts mit einer Ausnahme aktualisieren: db_ddladmin kann der Datenbank selbst oder Benutzern bzw. Rollen keine Eigenschaften hinzufügen.  
  
 Die Benutzer können erweiterte Eigenschaften für Objekte aktualisieren, die sie besitzen oder für die sie die ALTER- oder CONTROL-Berechtigung haben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-updating-an-extended-property-on-a-column"></a>A. Aktualisieren einer erweiterten Eigenschaft für eine Spalte  
 Im folgenden Beispiel wird der Wert der `Caption`-Eigenschaft für die `ID`-Spalte in der `T1`-Tabelle aktualisiert.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
    @name = N'Caption'  
    ,@value = N'Employee ID'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
--Update the extended property.  
EXEC sp_updateextendedproperty   
    @name = N'Caption'  
    ,@value = 'Employee ID must be unique.'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
```  
  
### <a name="b-updating-an-extended-property-on-a-database"></a>B. Aktualisieren einer erweiterten Eigenschaft für eine Datenbank  
 Im folgenden Beispiel wird zunächst eine erweiterte Eigenschaft für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank erstellt und dann der Wert dieser Eigenschaft aktualisiert.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample OLTP Database';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_updateextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample Database';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Sys.fn_listextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
