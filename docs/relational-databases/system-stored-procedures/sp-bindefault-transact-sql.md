---
title: Sp_bindefault (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
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
- sp_bindefault
- sp_bindefault_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7a01ab44ac03ae5782f5983e781d21c9d32f8f0b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spbindefault-transact-sql"></a>sp_bindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bindet einen Standard an eine Spalte oder einen Aliasdatentyp.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Es wird empfohlen, Default-Definitionen erstellen, mit dem DEFAULT-Schlüsselwort von der [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) oder [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) Anweisungen stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@defname=** ] **'***default***'**  
 Der Name des Standards, der von CREATE DEFAULT erstellt wird. *standardmäßige* ist **nvarchar(776)**, hat keinen Standardwert.  
  
 [  **@objname=** ] **"***Object_name***"**  
 Der Name der Tabelle und der Spalte, oder der Aliasdatentyp, an den der Standardwert gebunden werden soll. *Object_name* ist **nvarchar(776)** hat keinen Standardwert. *Object_name* kann nicht definiert werden, mit der **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml**, oder CLR Benutzerdefinierte Typen.  
  
 Wenn *Object_name* ist ein einteiliger Name, wird er als Aliasdatentyp aufgelöst. Ist er ein - oder dreiteiliger Name, wird es zuerst als eine Tabelle und Spalte aufgelöst; und wenn die Auflösung fehlschlägt, wird Sie als einen Aliasdatentyp aufgelöst. Vorhandene Spalten des aliasdatentyps erben standardmäßig *Standard*, es sei denn, Sie direkt auf die Spalte ein Standardwert gebunden wurde. Ein Standard kann nicht gebunden werden, um eine **Text**, **Ntext**, **Image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml**, **Zeitstempel**, oder CLR UDT-Spalte, eine Spalte mit der IDENTITY-Eigenschaft, eine berechnete Spalte oder eine Spalte, die hat bereits eine DEFAULT-Einschränkung.  
  
> [!NOTE]  
>  *Object_name* können Klammern enthalten **[]** als begrenzungsbezeichnern angegeben wird. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 [ **@futureonly=** ] **'***futureonly_flag***'**  
 Wird nur beim Binden eines Standardwerts an einen Aliasdatentyp verwendet. *Futureonly_flag* ist **varchar(15)** hat den Standardwert NULL. Wenn dieser Parameter festgelegt ist, um **Futureonly**, vorhandene Spalten dieses Datentyps den neuen Standard können nicht geerbt werden. Dieser Parameter wird nie beim Binden eines Standards an eine Spalte verwendet. Wenn *Futureonly_flag* NULL ist, wird der neue Standard an alle Spalten des aliasdatentyps, die aktuell keinen Standard aufweisen oder die den vorhandenen Standard des aliasdatentyps, gebunden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie können **Sp_bindefault** an einen neuen Standardwert an eine Spalte binden, obwohl empfohlen wird, verwenden die DEFAULT-Einschränkung oder einen Aliasdatentyp, ohne die Bindung eines vorhandenen Standards. Der alte Standard wird überschrieben. Sie können einen Standard nicht an einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp oder an einen CLR-benutzerdefinierten Typ binden. Ist der Standard nicht kompatibel mit der Spalte, an die er gebunden wurde, gibt [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] eine Fehlermeldung zurück, wenn der Standardwert eingefügt werden soll (nicht beim Binden).  
  
 Vorhandene Spalten des aliasdatentyps erben den neuen Standard, es sei denn, die entweder eine standardmäßige direkt an sie gebunden oder *Futureonly_flag* angegeben ist, als **Futureonly**. Neue Spalten des Aliasdatentyps erben immer den Standard.  
  
 Wenn Sie einen Standard an eine Spalte binden, zugehörige Informationen hinzugefügt die **sys.columns** -Katalogsicht angezeigt. Wenn Sie einen Standard an einen Aliasdatentyp binden, zugehörige Informationen hinzugefügt die **sys.types** -Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer muss Besitzer der Tabelle oder ein Mitglied der **Sysadmin** festen Serverrolle oder die **Db_owner** und **Db_ddladmin** festen Datenbankrollen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-binding-a-default-to-a-column"></a>A. Bindet eines Standardwerts an eine Spalte  
 In der aktuellen Datenbank wurde mit CREATE DEFAULT ein Standard mit dem Namen `today` definiert. Im folgenden Beispiel wird der Standard an die `HireDate`-Spalte der `Employee`-Tabelle gebunden. Wird zur `Employee`-Tabelle eine Zeile hinzugefügt und werden für die `HireDate`-Spalte keine Daten angegeben, erhält die Spalte den Wert des Standards `today`.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. Binden eines Standards an einen Aliasdatentyp  
 Ein Standard namens `def_ssn` und ein Aliasdatentyp namens `ssn` sind bereits vorhanden. Im folgenden Beispiel wird der Standard `def_ssn` an den Typ `ssn` gebunden. Wenn eine Tabelle erstellt wird, wird der Standard von allen Spalten geerbt, denen der Aliasdatentyp `ssn` zugewiesen ist. Vorhandene Spalten des Typs **"ssn"** erben ebenfalls den Standard **Def_ssn**, es sei denn, **Futureonly** für angegeben *Futureonly_flag* Wert oder, wenn die Spalte einen direkt gebundenen Standard besitzt. An Spalten gebundene Standards haben stets Vorrang vor den an Datentypen gebundenen Standards.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Verwenden von futureonly_flag  
 Im folgenden Beispiel bindet der Standard `def_ssn` an den Aliasdatentyp `ssn`. Da **Futureonly** angegeben wird, keine vorhandenen Spalten des Typs `ssn` betroffen sind.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Verwendung von begrenzungsbezeichnern  
 Das folgende Beispiel zeigt die Verwendung von begrenzungsbezeichnern, `[t.1]`im *Object_name*.  
  
```  
USE master;  
GO  
CREATE TABLE [t.1] (c1 int);   
-- Notice the period as part of the table name.  
EXEC sp_bindefault 'default1', '[t.1].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name,   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
