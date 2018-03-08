---
title: Sp_addtype (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addtype
- sp_addtype_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_addtype
ms.assetid: ed72cd8e-5ff7-4084-8458-2d8ed279d817
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61a5e94d0e57bdaaac63181c9257defdfd87d8eb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spaddtype-transact-sql"></a>sp_addtype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Aliasdatentyp.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addtype [ @typename = ] type,   
    [ @phystype = ] system_data_type   
    [ , [ @nulltype = ] 'null_type' ] ;  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@typename=** ] *Typ*  
 Der Name des Aliasdatentyps. Alias Datentypnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) und muss in jeder Datenbank eindeutig sein. *Typ* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@phystype=**] *System_data_type*  
 Der physische oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellte Datentyp, auf denen der Aliasdatentyp basiert. *System_data_type* ist **Sysname**, hat keinen Standardwert und kann einen der folgenden Werte sein:  
  
||||  
|-|-|-|  
|**bigint**|**binary(n)**|**bit**|  
|**char(n)**|**datetime**|**decimal**|  
|**float**|**image**|**int**|  
|**money**|**NCHAR (n)**|**ntext**|  
|**numeric**|**nvarchar (n)**|**real**|  
|**smalldatetime**|**smallint**|**smallmoney**|  
|**sql_variant**|**text**|**tinyint**|  
|**uniqueidentifier**|**varbinary(n)**|**varchar(n)**|  
  
 Alle Parameter, die Leerzeichen oder Satzzeichen enthalten, müssen in einfachen Anführungszeichen stehen. Weitere Informationen zu verfügbaren Datentypen, finden Sie unter [Datentypen &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md).  
  
 *n*  
 Eine nicht negative ganze Zahl, die die Länge für den ausgewählten Datentyp angibt.  
  
 *P*  
 Eine nicht negative ganze Zahl, die die maximale Anzahl der Dezimalstellen angibt, die vor und nach dem Dezimalzeichen gespeichert werden können. Weitere Informationen finden Sie unter ["Decimal und Numeric" &#40; Transact-SQL &#41; ](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *s*  
 Eine nicht negative ganze Zahl, die die maximale Anzahl der Dezimalstellen angibt, die nach dem Dezimalzeichen gespeichert werden können. Diese Zahl muss kleiner oder gleich der Gesamtzahl der Stellen sein. Weitere Informationen finden Sie unter ["Decimal und Numeric" &#40; Transact-SQL &#41; ](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 [  **@nulltype =** ] **"***Null_type***"**  
 Gibt an, wie der Aliasdatentyp NULL-Werte behandelt. *Null_type* ist **Varchar (**8**)**, hat den Standardwert NULL und muss in einfache Anführungszeichen ('NULL', 'NOT NULL' oder 'NONULL') eingeschlossen werden. Wenn *Null_type* wird nicht explizit definiert **Sp_addtype**, wird er auf die aktuelle Standard-NULL-Zulässigkeit festgelegt. Verwenden Sie die GETANSINULL-Systemfunktion, um die aktuelle Standard-NULL-Zulässigkeit zu ermitteln. Diese kann mithilfe der SET-Anweisung oder ALTER DATABASE angepasst werden. Die NULL-Zulässigkeit sollte explizit definiert werden. Wenn  **@phystype**  ist **Bit**, und  **@nulltype**  nicht angegeben ist, wird der Standardwert ist NULL.  
  
> [!NOTE]  
>  Die *Null_type* -Parameter definiert nur die standardmäßige NULL-Zulässigkeit für diesen Datentyp. Wenn der Aliasdatentyp beim Erstellen der Tabelle verwendet und die NULL-Zulässigkeit explizit definiert wurde, hat diese Vorrang vor der definierten NULL-Zulässigkeit. Weitere Informationen finden Sie unter [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) und [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Der Name eines Aliasdatentyps muss in der Datenbank eindeutig sein, aber Aliasdatentypen mit unterschiedlichen Namen können dieselbe Definition aufweisen.  
  
 Ausführen von **Sp_addtype** erstellt einen Aliasdatentyp, die in der **sys.types** -Katalogsicht für eine bestimmte Datenbank. Wenn der Aliasdatentyp in allen neuen benutzerdefinierten Datenbanken verfügbar sein muss, fügen Sie ihn auf **Modell**. Nach der Erstellung eines Aliasdatentyps können Sie diesen mit CREATE TABLE oder ALTER TABLE verwenden sowie Standards und Regeln an den Aliasdatentyp binden. Alle skalaren Aliasdatentypen, die mithilfe von erstellt werden **Sp_addtype** enthalten sind, der **Dbo** Schema.  
  
 Aliasdatentypen erben die Standardsortierung der Datenbank. Die Sortierungen von Spalten und Variablen von Aliastypen sind in definiert die [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE, ALTER TABLE und DECLARE @*Local_variable* Anweisungen. Eine Änderung der Standardsortierung der Datenbank gilt nur für neue Spalten und Variablen des Typs; sie wirkt sich nicht auf die Sortierung bereits vorhandener Spalten und Variablen aus.  
  
> [!IMPORTANT]  
>  Aus Gründen der Abwärtskompatibilität der **öffentlichen** Datenbankrolle wird die REFERENCES-Berechtigung für Aliasdatentypen, die mithilfe von erstellt werden automatisch gewährt **Sp_addtype**. Beachten Sie, wenn Aliasdatentypen erstellt werden, mithilfe der CREATE TYPE-Anweisung anstelle von **Sp_addtype**, keine automatisch erteilt.  
  
 Aliasdatentypen können nicht definiert werden, indem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Zeitstempel**, **Tabelle**, **Xml**, **varchar(max)**, **nvarchar(max)** oder **varbinary(max)** Datentypen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Db_owner** oder **Db_ddladmin** festen Datenbankrolle "".  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-an-alias-data-type-that-does-not-allow-for-null-values"></a>A. Erstellen eines Aliasdatentyps, der keine NULL-Werte zulässt  
 Im folgenden Beispiel wird einen Aliasdatentyp namens `ssn` (Social Security Number) auf Grundlage der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-bereitgestellten **Varchar** -Datentyp. Der `ssn`-Datentyp wird für Spalten mit 11-stelligen Sozialversicherungsnummern verwendet (999-99-9999). Diese Spalte darf nicht den Wert NULL aufweisen.  
  
 Beachten Sie, dass `varchar(11)` in einfachen Anführungszeichen steht, da es Satzzeichen (Klammern) enthält.  
  
```  
USE master;  
GO  
EXEC sp_addtype ssn, 'varchar(11)', 'NOT NULL';  
GO  
```  
  
### <a name="b-creating-an-alias-data-type-that-allows-for-null-values"></a>B. Erstellen eines Aliasdatentyps, der NULL-Werte zulässt  
 Im folgenden Beispiel wird ein Aliasdatentyp (basierend auf `datetime`) namens `birthday` erstellt, der NULL-Werte zulässt.  
  
```  
USE master;  
GO  
EXEC sp_addtype birthday, datetime, 'NULL';  
```  
  
### <a name="c-creating-additional-alias-data-types"></a>C. Erstellen von zusätzlichen Aliasdatentypen  
 Im folgenden Beispiel werden zwei zusätzliche Aliasdatentypen, `telephone` und `fax`, für nationale und internationale Telefon- und Faxnummern erstellt.  
  
```  
USE master;  
GO  
EXEC sp_addtype telephone, 'varchar(24)', 'NOT NULL';  
GO  
EXEC sp_addtype fax, 'varchar(24)', 'NULL';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [Sp_bindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [Sp_bindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [Sp_droptype &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [Sp_unbindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [Sp_unbindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
