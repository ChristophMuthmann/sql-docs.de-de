---
title: CREATE DEFAULT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71c0f964d245be92fb8d2be19e074fbd34dd616e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
 Der Name des Standardwerts. Namen für Standardwerte müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Das Angeben des Standardbesitzernamens ist optional.  
  
 *constant_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) , enthält nur konstante Werte, die (es kann nicht die Namen von Spalten oder andere Datenbankobjekte enthalten). Es kann jede Konstante, jede integrierte Funktion oder jeder mathematische Ausdruck verwendet werden, außer solchen, die Aliasdatentypen enthalten. Benutzerdefinierte Funktionen können verwendet werden... Schließen Sie Zeichen- und Datumskonstanten in einfache Anführungszeichen (**"**); monetären, Integer und Gleitkommakonstanten erfordern keine Anführungszeichen. Binären Daten muss 0x vorangestellt werden, und Währungsdaten muss das Dollarzeichen ($) vorangestellt werden. Der Standardwert muss mit dem Datentyp der Spalte kompatibel sein.  
  
## <a name="remarks"></a>Hinweise  
 Der Name eines Standardwerts kann nur in der aktuellen Datenbank erstellt werden. Innerhalb einer Datenbank müssen die Namen für Standardwerte für jedes Schema eindeutig sein. Verwenden Sie der Standardwert erstellt wurde, **Sp_bindefault** sie an eine Spalte oder an einen Aliasdatentyp binden.  
  
 Falls der Standardwert inkompatibel mit dem Datentyp der Spalte ist, an die er gebunden ist, erzeugt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Versuch, den Standardwert einzufügen, eine Fehlermeldung. Beispielsweise kann nicht n/v verwendet werden, als Standardwert für eine **numerischen** Spalte.  
  
 Falls der Standardwert zu lang für die Spalte ist, an die er gebunden ist, wird er gekürzt.  
  
 CREATE DEFAULT-Anweisungen können nicht mit anderen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem einzelnen Batch kombiniert werden.  
  
 Ein Standardwert muss gelöscht werden, bevor Sie eine neue mit demselben Namen erstellen, und der Standardwert muss aufgehoben werden, durch das Ausführen **Sp_unbindefault** bevor er gelöscht wird.  
  
 Falls einer Spalte sowohl ein Standardwert als auch eine Regel zugeordnet ist, darf der Standardwert nicht diese Regel verletzen. Ein Standardwert, der gegen eine Regel verstößt, wird nicht eingefügt. Bei jedem Versuch, einen solchen Standardwert einzufügen, erzeugt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Fehlermeldung.  
  
 Ist ein Standardwert an eine Spalte gebunden, wird er unter folgenden Umständen eingefügt:  
  
-   Es wird kein Wert explizit eingefügt.  
  
-   Das DEFAULT VALUES- oder DEFAULT-Schlüsselwort wird mit INSERT verwendet, um Standardwerte einzufügen.  
  
 Falls beim Erstellen einer Spalte NOT NULL angegeben und für die Spalte kein Standardwert erstellt ist, wird jedes Mal eine Fehlermeldung erzeugt, wenn ein Benutzer keinen Eintrag in dieser Spalte bereitstellt. In der folgenden Tabelle wird die Beziehung zwischen dem Vorhandensein eines Standardwerts und der Definition einer Spalte als NULL oder NOT NULL verdeutlicht. Das jeweilige Ergebnis geht aus den Einträgen in der Tabelle hervor.  
  
|Spaltendefinition|Kein Eintrag, kein Standardwert|Kein Eintrag, Standardwert|Eingabe von NULL, kein Standardwert|Eingabe von NULL, Standardwert|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULL|default|NULL|NULL|  
|**NOT NULL**|Fehler|default|Fehler|Fehler|  
  
 Um einen Standardwert umzubenennen, verwenden Sie **"Sp_rename"**. Verwenden Sie für einen Bericht über einen Standardwert, **Sp_help**.  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Ausführung von CREATE DEFAULT benötigt ein Benutzer zumindest die CREATE DEFAULT-Berechtigung für die aktuelle Datenbank sowie die ALTER-Berechtigung für das Schema, in dem der Standardwert erstellt wird.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-simple-character-default"></a>A. Erstellen eines einfachen Zeichenstandards  
 Im folgenden Beispiel wird ein Zeichenstandardwert namens `unknown` erstellt.  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. Binden eines Standards  
 Im folgenden Beispiel wird der in Beispiel A erstellte Standardwert an eine Spalte gebunden. Der Standardwert tritt nur dann in Kraft, wenn kein Eintrag in der `Phone`-Spalte der `Contact`-Tabelle angegeben ist. Beachten Sie, dass sich das Auslassen eines Eintrags vom expliziten Angeben von NULL in einer INSERT-Anweisung unterscheidet.  
  
 Da kein Standardwert namens `phonedflt` vorhanden ist, schlägt die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung fehl. Dieses Beispiel dient nur zur Veranschaulichung.  
  
```tsql  
USE AdventureWorks2012;  
GO  
sp_bindefault 'phonedflt', 'Person.PersonPhone.PhoneNumber';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Löschen Sie die STANDARDMÄßIGE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Sp_bindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [Sp_unbindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  

