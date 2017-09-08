---
title: CURSOR_STATUS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURSOR_STATUS
- CURSOR_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], cursors
- CURSOR_STATUS function
- cursors [SQL Server], status information
ms.assetid: 3a4a840e-04f8-43bd-aada-35d78c3cb6b0
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e88dd4f14d8bd6fc90c40df101bfd9b2895bf229
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="cursorstatus-transact-sql"></a>CURSOR_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Eine Skalarfunktion, mit welcher der Aufrufer einer gespeicherten Prozedur festlegen kann, ob die Prozedur einen Cursor und ein Resultset für einen angegebenen Parameter zurückgegeben hat.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CURSOR_STATUS   
     (  
          { 'local' , 'cursor_name' }   
          | { 'global' , 'cursor_name' }   
          | { 'variable' , 'cursor_variable' }   
     )  
```  
  
## <a name="arguments"></a>Argumente  
'local'  
Gibt eine Konstante an, die anzeigt, dass die Quelle des Cursors ein lokaler Cursorname ist.
  
"*Cursor_name*"  
Ist der Name des Cursors. Ein Cursorname muss den Regeln für Bezeichner entsprechen.
  
'global'  
Gibt eine Konstante an, die anzeigt, dass die Quelle des Cursors ein globaler Cursorname ist.
  
'variable'  
Gibt eine Konstante an, die anzeigt, dass die Quelle des Cursors eine lokale Variable ist.
  
"*Cursor_variable*"  
Der Name der Cursorvariablen. Eine Cursorvariable muss definiert werden, mithilfe der **Cursor** -Datentyp.
  
## <a name="return-types"></a>Rückgabetypen
**smallint**
  
|Rückgabewert|Cursorname|Cursorvariable|  
|---|---|---|
|1|Das Resultset des Cursors hat mindestens eine Zeile.<br /><br /> Für INSENSITIVE- und KEYSET-Cursor hat das Resultset mindestens eine Zeile.<br /><br /> Für dynamische Cursor kann das Resultset keine, eine oder mehrere Zeilen haben.|Der für diese Variable zugeordnete Cursor ist geöffnet.<br /><br /> Für INSENSITIVE- und KEYSET-Cursor hat das Resultset mindestens eine Zeile.<br /><br /> Für dynamische Cursor kann das Resultset keine, eine oder mehrere Zeilen haben.|  
|0|Das Resultset des Cursors ist leer.*|Der dieser Variable zugeordnete Cursor ist geöffnet, das Resultset ist jedoch definitiv leer.*|  
|-1|Der Cursor ist geschlossen.|Der dieser Variable zugeordnete Cursor ist geschlossen.|  
|-2|Nicht verfügbar.|Mögliche Werte sind:<br /><br /> Für diese OUTPUT-Variable wurde kein Cursor durch die zuvor aufgerufene Prozedur zugewiesen.<br /><br /> Die zuvor aufgerufene Prozedur hat dieser OUTPUT-Variablen einen Cursor zugewiesen; bei Abschluss der Prozedur befand sich der Cursor jedoch in geschlossenem Status. Deshalb wird die Zuordnung aufgehoben, und der Cursor wird nicht zur aufrufenden Prozedur zurückgegeben.<br /><br /> Einer deklarierten Cursorvariablen wird kein Cursor zugewiesen.|  
|-3|Ein Cursor mit dem angegebenen Namen ist nicht vorhanden.|Die Cursorvariable mit dem angegebenen Namen ist nicht vorhanden, oder für sie wurde noch kein Cursor zugeordnet.|  
  
* Dynamische Cursor geben dieses Ergebnis nie zurück.
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel verwendet die `CURSOR_STATUS`-Funktion, um den Status eines Cursors darzustellen, nachdem er geöffnet und geschlossen wurde.
  
```sql
CREATE TABLE #TMP  
(  
   ii int  
)  
GO  
  
INSERT INTO #TMP(ii) VALUES(1)  
INSERT INTO #TMP(ii) VALUES(2)  
INSERT INTO #TMP(ii) VALUES(3)  
  
GO  
  
--Create a cursor.  
DECLARE cur CURSOR  
FOR SELECT * FROM #TMP  
  
--Display the status of the cursor before and after opening  
--closing the cursor.  
  
SELECT CURSOR_STATUS('global','cur') AS 'After declare'  
OPEN cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Open'  
CLOSE cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Close'  
  
--Remove the cursor.  
DEALLOCATE cur  
  
--Drop the table.  
DROP TABLE #TMP  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`After declare`
  
`---------------`
  
 `-1`  
  
`After Open`
  
`----------`
  
 `1`  
  
`After Close`
  
`-----------`
  
 `-1`  
  
## <a name="see-also"></a>Siehe auch
[Cursorfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

