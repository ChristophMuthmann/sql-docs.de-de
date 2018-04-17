---
title: Sp_dropextendedproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproperty_TSQL
- sp_dropextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproperty
ms.assetid: 4851865a-86ca-4823-991a-182dd1934075
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b8937b491afa9489779513a20ace182a49ef56e6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spdropextendedproperty-transact-sql"></a>sp_dropextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht eine vorhandene erweiterte Eigenschaft.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropextendedproperty   
    [ @name = ] { 'property_name' }  
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
```  
  
## <a name="arguments"></a>Argumente  
 [ @name=] {"*Property_name*'}  
 Der Name der zu löschenden Eigenschaft. *Property_name* ist **Sysname** und darf nicht NULL sein.  
  
 [ @level0type=] {"*level0_object_type*'}  
 Der Name des angegebenen Objekttyps der Ebene 0. *level0_object_type* ist **varchar(128)**, hat den Standardwert NULL.  
  
 Gültige Eingabewerte sind ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, USER, TRIGGER, TYPE und NULL.  
  
> [!IMPORTANT]  
>  USER und TYPE als Typen der Ebene 0 werden in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr unterstützt. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktionen zurzeit verwenden. Verwenden Sie SCHEMA anstelle von USER als Typ der Ebene 0. Verwenden Sie für TYPE als Typ der Ebene 0 SCHEMA und TYPE als Typ der Ebene 1.  
  
 [ @level0name=] {"*level0_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 0. *level0_object_name* ist **Sysname** hat den Standardwert NULL.  
  
 [ @level1type=] {"*level1_object_type*'}  
 Der Typ des Objekts der Ebene 1. *level1_object_type* ist **varchar(128)** hat den Standardwert NULL. Gültige Eingabewerte sind AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION und NULL.  
  
 [ @level1name=] {"*level1_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 1. *level1_object_name* ist **Sysname** hat den Standardwert NULL.  
  
 [ @level2type=] {"*level2_object_type*'}  
 Der Typ des Objekts der Ebene 2. *level2_object_type* ist **varchar(128)** hat den Standardwert NULL. Gültige Eingabewerte sind COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER und NULL.  
  
 [ @level2name=] {"*level2_object_name*'}  
 Der Name des angegebenen Objekttyps der Ebene 2. *level2_object_name* ist **Sysname** hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Für das Angeben erweiterter Eigenschaften werden die Objekte in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank in drei Ebenen unterteilt: 0, 1 und 2. Die Ebene 0 ist die höchste Ebene und ist definiert als Objekte, die im Datenbankbereich enthalten sind. Objekte der Ebene 1 sind in einem Schema- oder Benutzerbereich enthalten, und Objekte der Ebene 2 sind in Objekten der Ebene 1 enthalten. Erweiterte Eigenschaften können für Objekte auf einer dieser Ebenen definiert werden. Verweise auf ein Objekt einer Ebene müssen mit den Typen und Namen aller Objekte der höheren Ebenen gekennzeichnet werden.  
  
 Wenn bei einem gültigen *Property_name*, wenn alle Objekttypen und-Namen null sind und eine Eigenschaft, die in der aktuellen Datenbank vorhanden ist, diese Eigenschaft gelöscht wird. Weitere Informationen finden Sie im Beispiel B, weiter unten in diesem Thema.  
  
## <a name="permissions"></a>Berechtigungen  
 Mitglieder der festen Datenbankrollen db_owner und db_ddladmin können erweiterte Eigenschaften beliebiger Objekte mit folgender Ausnahme löschen: db_ddladmin kann weder der Datenbank noch Benutzern oder Rollen Eigenschaften hinzufügen.  
  
 Benutzer können erweiterte Eigenschaften von Objekten löschen, die sie besitzen, oder für die sie über die ALTER- oder CONTROL-Berechtigung verfügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-an-extended-property-on-a-column"></a>A. Löschen der erweiterten Eigenschaft einer Spalte  
 Im folgenden Beispiel wird die `caption`-Eigenschaft aus der `id`-Spalte in der `T1`-Tabelle entfernt, die im `dbo`-Schema enthalten ist.  
  
```  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
     @name = 'caption'   
    ,@value = 'Employee ID'   
    ,@level0type = 'schema'   
    ,@level0name = dbo  
    ,@level1type = 'table'  
    ,@level1name = 'T1'  
    ,@level2type = 'column'  
    ,@level2name = id;  
GO  
EXEC sp_dropextendedproperty   
     @name = 'caption'   
    ,@level0type = 'schema'   
    ,@level0name = dbo  
    ,@level1type = 'table'  
    ,@level1name = 'T1'  
    ,@level2type = 'column'  
    ,@level2name = id;  
GO  
DROP TABLE T1;  
GO  
```  
  
### <a name="b-dropping-an-extended-property-on-a-database"></a>B. Löschen der erweiterten Eigenschaft einer Datenbank  
 Im folgenden Beispiel wird die Eigenschaft mit dem Namen `MS_Description` aus der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank. Da die Eigenschaft zur Datenbank selbst gehört, werden keine Objekttypen und -namen angegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_dropextendedproperty   
@name = N'MS_Description';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Sys.fn_listextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [Sp_updateextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
