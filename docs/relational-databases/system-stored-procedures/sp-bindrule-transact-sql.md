---
title: Sp_bindrule (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs: TSQL
helpviewer_keywords: sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbc90db869ea98ebfdf99bf9cbdf56d9019b28a8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spbindrule-transact-sql"></a>sp_bindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bindet eine Regel an eine Spalte oder an einen Aliasdatentyp.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Verwendung[Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md) stattdessen. Überprüfen Sie die Einschränkungen werden mit dem CHECK-Schlüsselwort von erstellt die [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) oder [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) Anweisungen.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@rulename=**] **"***Regel***"**  
 Der Name einer von der CREATE RULE-Anweisung erstellten Regel. *Regel* ist **nvarchar(776)**, hat keinen Standardwert.  
  
 [  **@objname=**] **"***Object_name***"**  
 Die Tabelle und Spalte oder der Aliasdatentyp, an die bzw. den die Regel gebunden werden soll. Eine Regel kann nicht gebunden werden, um eine **Text**, **Ntext**, **Image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml**, CLR-benutzerdefinierten Typ oder **Zeitstempel**Spalte. An eine berechnete Spalte kann keine Regel gebunden werden.  
  
 *Object_name* ist **nvarchar(776)** hat keinen Standardwert. Wenn *Object_name* ist ein einteiliger Name, wird er als Aliasdatentyp aufgelöst. Ein zwei- oder dreiteiliger Name wird zunächst als Tabelle und Spalte aufgelöst. Wenn die Auflösung fehlschlägt, wird er als Aliasdatentyp aufgelöst. Vorhandene Spalten des aliasdatentyps erben standardmäßig *Regel* , wenn eine Regel direkt auf die Spalte gebunden wurde.  
  
> [!NOTE]  
>  *Object_name* darf die Klammer **[** und **]** Zeichen als Begrenzungsbezeichner. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Regeln, die für Ausdrücke erstellt werden, die Aliasdatentypen verwenden, können an Spalten oder Aliasdatentypen gebunden werden. Wenn darauf verwiesen wird, schlägt jedoch die Kompilierung fehl. Vermeiden Sie die Verwendung von Regeln, die für Aliasdatentypen erstellt wurden.  
  
 [  **@futureonly=** ] **"***Futureonly_flag***"**  
 Wird nur beim Binden einer Regel an einen Aliasdatentyp verwendet. *Future_only_flag* ist **varchar(15)** hat den Standardwert NULL. Dieser Parameter, die bei Festlegung auf **Futureonly** verhindert, dass vorhandene Spalten des aliasdatentyps erben die neue Regel. Wenn *Futureonly_flag* NULL ist, die neue Regel an Spalten des aliasdatentyps, die aktuell keine Regel haben oder die vorhandene Regel des aliasdatentyps, gebunden ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie können eine neue Regel an eine Spalte binden (obwohl empfohlen) eine CHECK-Einschränkung zu verwenden wird, oder an einen Aliasdatentyp mit **Sp_bindrule** ohne die Bindung einer vorhandenen Regel. Die alte Regel wird überschrieben. Wenn eine Regel an eine Spalte gebunden wird, für die eine CHECK-Einschränkung vorhanden ist, werden alle Einschränkungen ausgewertet. Das Binden einer Regel an einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp ist nicht möglich.  
  
 Die Regel tritt in Kraft, wenn eine INSERT-Anweisung ausgeführt wird, nicht aber beim Binden. Sie können eine Zeichenregel an eine Spalte binden **numerischen** -Datentyp, obwohl dieser INSERT-Vorgang ungültig ist.  
  
 Vorhandene Spalten des aliasdatentyps erben die neue Regel, es sei denn, *Futureonly_flag* angegeben ist, als **Futureonly**. Neue Spalten, die mit dem Aliasdatentyp definiert sind, erben immer die Regel. Wenn jedoch die ALTER COLUMN-Klausel einer ALTER TABLE-Anweisung den Datentyp einer Spalte in einen Aliasdatentyp ändert, der an eine Regel gebunden ist, wird diese Regel nicht an die Spalte vererbt. Die Regel muss speziell an die Spalte gebunden werden, mithilfe von **Sp_bindrule**.  
  
 Wenn Sie eine Regel an eine Spalte binden, zugehörige Informationen hinzugefügt die **sys.columns** Tabelle. Wenn Sie eine Regel an einen Aliasdatentyp binden, zugehörige Informationen hinzugefügt die **sys.types** Tabelle.  
  
## <a name="permissions"></a>Berechtigungen  
 Um eine Regel an eine Tabellenspalte zu binden, benötigen Sie die ALTER-Berechtigung für die Tabelle. Um eine Regel an einen Aliasdatentyp zu binden, benötigen Sie die CONTROL-Berechtigung für den Aliasdatentyp oder die ALTER-Berechtigung für das Schema, dem der Typ angehört.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-binding-a-rule-to-a-column"></a>A. Binden einer Regel an eine Spalte  
 Unter der Annahme, dass in der aktuellen Datenbank eine Regel mit dem Namen `today` mit der CREATE RULE-Anweisung erstellt wurde, wird in diesem Beispiel diese Regel an die Spalte `HireDate` der Tabelle `Employee` gebunden. Wird der Tabelle `Employee` eine Zeile hinzugefügt, werden die Daten für die Spalte `HireDate` in Hinblick auf die Regel `today` überprüft.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>B. Binden einer Regel an einen Aliasdatentyp  
 Unter der Annahme, eine Regel namens `rule_ssn` und ein Aliasdatentyp namens `ssn` sind vorhanden, wird in diesem Beispiel `rule_ssn` an `ssn` gebunden. Alle Spalten vom Datentyp `ssn` erben in einer CREATE TABLE-Anweisung die Regel `rule_ssn`. Vorhandene Spalten des Typs `ssn` erben ebenfalls die `rule_ssn` auszuschließen, es sei denn, **Futureonly** für angegeben *Futureonly_flag*, oder `ssn` enthält eine Regel, die direkt an sie gebunden. An Spalten gebundene Regeln haben immer Vorrang vor den an Datentypen gebundenen Regeln.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Verwenden von futureonly_flag  
 Im folgenden Beispiel wird die Regel `rule_ssn` an den Aliasdatentyp `ssn` gebunden. Da `futureonly` angegeben wurde, sind keine vorhandenen Spalten des Typs `ssn` betroffen.  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Verwendung von begrenzungsbezeichnern  
 Das folgende Beispiel zeigt die Verwendung von begrenzungsbezeichnern im *Object_name* Parameter.  
  
```  
USE master;  
GO  
CREATE TABLE [t.2] (c1 int) ;  
-- Notice the period as part of the table name.  
EXEC sp_bindrule rule1, '[t.2].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [Sp_unbindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
