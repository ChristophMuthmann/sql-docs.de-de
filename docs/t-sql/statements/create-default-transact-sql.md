---
title: CREATE DEFAULT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_DEFAULT_TSQL
- CREATE DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], default
- default objects
- CREATE DEFAULT statement
- objects [SQL Server], creating
- DEFAULT definition
ms.assetid: 08475db4-7d90-486a-814c-01a99d783d41
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a51a1045532b9194586d197c6b1b537d795d1996
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt ein Objekt, das als Standardwert bezeichnet wird. Wenn ein Standardwert an eine Spalte oder einen Aliasdatentyp gebunden ist, gibt er den Wert an, der in diese Spalte (oder im Fall eines Aliasdatentyps in alle Spalten) eingefügt werden soll, wenn beim Einfügen nicht explizit ein Wert angegeben ist.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen Standarddefinitionen, die mithilfe des DEFAULT-Schlüsselworts von ALTER TABLE oder CREATE TABLE erstellt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE DEFAULT [ schema_name . ] default_name   
AS constant_expression [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem der Standardwert gehört.  
  
 *default_name*  
 Der Name des Standardwerts. Namen für Standardwerte müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Das Angeben des Standardbesitzernamens ist optional.  
  
 *constant_expression*  
 Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md), der nur konstante Werte enthält (nicht zulässig sind Namen von Spalten oder anderen Datenbankobjekten). Es kann jede Konstante, jede integrierte Funktion oder jeder mathematische Ausdruck verwendet werden, außer solchen, die Aliasdatentypen enthalten. Benutzerdefinierte Funktionen können nicht verwendet werden. Setzen Sie Zeichen- und Datumskonstanten in einfache Anführungszeichen (**'**). Bei Integer-, Währungs- und Gleitkommakonstanten sind keine Anführungszeichen erforderlich. Binären Daten muss 0x vorangestellt werden, und Währungsdaten muss das Dollarzeichen ($) vorangestellt werden. Der Standardwert muss mit dem Datentyp der Spalte kompatibel sein.  
  
## <a name="remarks"></a>Remarks  
 Der Name eines Standardwerts kann nur in der aktuellen Datenbank erstellt werden. Innerhalb einer Datenbank müssen die Namen für Standardwerte für jedes Schema eindeutig sein. Verwenden Sie nach dem Erstellen eines Standardwerts **sp_bindefault**, um diesen an eine Spalte oder einen Aliasdatentyp zu binden.  
  
 Falls der Standardwert inkompatibel mit dem Datentyp der Spalte ist, an die er gebunden ist, erzeugt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Versuch, den Standardwert einzufügen, eine Fehlermeldung. N/V kann z.B. nicht als Standardwert für **numeric**-Spalten verwendet werden.  
  
 Falls der Standardwert zu lang für die Spalte ist, an die er gebunden ist, wird er gekürzt.  
  
 CREATE DEFAULT-Anweisungen können nicht mit anderen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem einzelnen Batch kombiniert werden.  
  
 Der Standardwert muss gelöscht werden, bevor ein neuer Standardwert mit dem gleichen Namen erstellt werden kann. Außerdem muss seine Bindung durch Ausführen von **sp_unbindefault** aufgehoben werden, bevor dieser gelöscht werden kann.  
  
 Falls einer Spalte sowohl ein Standardwert als auch eine Regel zugeordnet ist, darf der Standardwert nicht diese Regel verletzen. Ein Standardwert, der gegen eine Regel verstößt, wird nicht eingefügt. Bei jedem Versuch, einen solchen Standardwert einzufügen, erzeugt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Fehlermeldung.  
  
 Ist ein Standardwert an eine Spalte gebunden, wird er unter folgenden Umständen eingefügt:  
  
-   Es wird kein Wert explizit eingefügt.  
  
-   Das DEFAULT VALUES- oder DEFAULT-Schlüsselwort wird mit INSERT verwendet, um Standardwerte einzufügen.  
  
 Falls beim Erstellen einer Spalte NOT NULL angegeben und für die Spalte kein Standardwert erstellt ist, wird jedes Mal eine Fehlermeldung erzeugt, wenn ein Benutzer keinen Eintrag in dieser Spalte bereitstellt. In der folgenden Tabelle wird die Beziehung zwischen dem Vorhandensein eines Standardwerts und der Definition einer Spalte als NULL oder NOT NULL verdeutlicht. Das jeweilige Ergebnis geht aus den Einträgen in der Tabelle hervor.  
  
|Spaltendefinition|Kein Eintrag, kein Standardwert|Kein Eintrag, Standardwert|Eingabe von NULL, kein Standardwert|Eingabe von NULL, Standardwert|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULL|default|NULL|NULL|  
|**NOT NULL**|Fehler|default|Fehler|Fehler|  
  
 Um einen Standardwert umzubenennen, verwenden Sie **sp_rename**. Um einen Bericht über einen Standardwert zu erhalten, verwenden Sie **sp_help**.  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Ausführung von CREATE DEFAULT benötigt ein Benutzer zumindest die CREATE DEFAULT-Berechtigung für die aktuelle Datenbank sowie die ALTER-Berechtigung für das Schema, in dem der Standardwert erstellt wird.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-simple-character-default"></a>A. Erstellen eines einfachen Zeichenstandards  
 Im folgenden Beispiel wird ein Zeichenstandardwert namens `unknown` erstellt.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. Binden eines Standards  
 Im folgenden Beispiel wird der in Beispiel A erstellte Standardwert an eine Spalte gebunden. Der Standardwert tritt nur dann in Kraft, wenn kein Eintrag in der `Phone`-Spalte der `Contact`-Tabelle angegeben ist. Beachten Sie, dass sich das Auslassen eines Eintrags vom expliziten Angeben von NULL in einer INSERT-Anweisung unterscheidet.  
  
 Da kein Standardwert namens `phonedflt` vorhanden ist, schlägt die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung fehl. Dieses Beispiel dient nur zur Veranschaulichung.  
  
```sql  
USE AdventureWorks2012;  
GO  
sp_bindefault 'phonedflt', 'Person.PersonPhone.PhoneNumber';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
