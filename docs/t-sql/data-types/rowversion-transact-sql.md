---
title: RowVersion (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- timestamp_TSQL
- timestamp
dev_langs:
- TSQL
helpviewer_keywords:
- rowversion data type
- size [SQL Server], rowversion
- row version-stamping [SQL Server]
- rowversion columns
- version-stamping table rows
- unique rowversion numbers
- unique timestamp numbers
- timestamp data type
- timestamp columns
- size [SQL Server], timestamp
ms.assetid: 65c9cf0e-3e8a-45f8-87b3-3460d96afb0b
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47bcf3007657c1cf8f77c364aa21839cdd27d1ba
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="rowversion-transact-sql"></a>rowversion (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Ein Datentyp, der automatisch generierte eindeutige, binäre Zahlen in einer Datenbank verfügbar macht. **RowVersion** wird normalerweise als Mechanismus für die versionskennung von Tabellenzeilen verwendet. Die Speichergröße beträgt 8 Byte. Die **Rowversion** -Datentyp ist nur eine inkrementelle Nummer und wird nicht beibehalten werden, ein Datum oder eine Uhrzeit. Verwenden Sie zum Aufzeichnen von Datum oder Uhrzeit einer **datetime2** -Datentyp.
  
## <a name="remarks"></a>Hinweise  
Jede Datenbank verfügt über einen Zähler, die für jeden Einfügevorgang erhöht oder Update-Vorgang für eine Tabelle ausgeführt wird, enthält eine **Rowversion** Spalte innerhalb der Datenbank. Dieser Zähler ist die Datenbankzeilenversion. Hiermit wird ein relativer Zeitpunkt innerhalb einer Datenbank nachverfolgt, keine tatsächliche Zeit, die einer Uhr zugeordnet werden kann. Eine Tabelle kann nur einen haben **Rowversion** Spalte. Jedes Mal, wenn, eine Zeile mit einem **Rowversion** Spalte geändert oder eingefügt wird, wird der inkrementierte Wert der datenbankzeilenversion eingefügt, der **Rowversion** Spalte. Diese Eigenschaft macht eine **Rowversion** -Spalten ungeeignete Kandidaten für Schlüssel, insbesondere für Primärschlüssel. Jedes Update der Zeile ändert den rowversion-Wert und somit auch den Wert des Schlüssels. Wenn die Spalte in einem Primärschlüssel verwendet wird, sind der alte Wert und somit auch alle Fremdschlüssel, die auf den alten Wert verweisen, nicht mehr gültig. Wenn in einem dynamischen Cursor auf die Tabelle verwiesen wird, ändern alle Updates die Position der Zeilen im Cursor. Falls die Spalte in einem Indexschlüssel verwendet wird, generieren alle Updates der Datenzeile auch Updates des Index.  Die **Rowversion** Wert wird bei jeder Update-Anweisung erhöht, selbst wenn keine Zeilenwerte geändert werden. (Z. B. wenn ein Spaltenwert 5 ist und eine Update-Anweisung der Wert auf 5 wird, diese Aktion gilt ein Update, obwohl keine Änderung aufgetreten ist und die **Rowversion** wird erhöht.)
  
**Zeitstempel** wird das Synonym für den **Rowversion** -Datentyp und unterliegt der Verhaltensweise von Datentypsynonymen. Verwenden Sie in DDL-Anweisungen **Rowversion** anstelle von **Zeitstempel** möglichst. Weitere Informationen finden Sie unter [Synonyme für Datentypen &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
Die [!INCLUDE[tsql](../../includes/tsql-md.md)] **Zeitstempel** Datentyp unterscheidet sich von der **Zeitstempel** Datentyp im ISO-Standard definiert.
  
> [!NOTE]  
>  Die **Zeitstempel** Syntax ist veraltet. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
In einer CREATE TABLE- oder ALTER TABLE-Anweisung, Sie müssen keinen Geben Sie einen Spaltennamen für die **Zeitstempel** -Datentyp, z. B.:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
Wenn Sie keinen Spaltennamen angeben der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] generiert die **Zeitstempel** Spaltenname, aber die **Rowversion** Synonym befolgt dieses Verhalten nicht. Bei Verwendung von **Rowversion**, müssen Sie einen Spaltennamen an, z. B. angeben:
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  Doppelte **Rowversion** Werte generiert werden, mithilfe der SELECT INTO-Anweisung in dem ein **Rowversion** Spalte in der SELECT-Liste ist. Es wird nicht empfohlen, mithilfe von **Rowversion** auf diese Weise.  
  
Ein NULL-Werte zulässt **Rowversion** Spalte ist semantisch gleichwertig mit einem **binary(8)** Spalte. Ein auf NULL festlegbares **Rowversion** Spalte ist semantisch gleichwertig mit einem **varbinary(8)** Spalte.
  
Sie können die **Rowversion** Spalte einer Zeile auf einfache Weise ermitteln, ob die Zeile mit eine Update-Anweisung wurde für sie ausgeführt wurde, seit dem letzten er gelesen wurde. Wenn eine Update-Anweisung für die Zeile ausgeführt wird, wird der Rowversion-Wert aktualisiert. Wenn keine Update-Anweisungen sind für die Zeile ausgeführt haben, ist der Rowversion-Wert identisch mit dem zuletzt gelesen wurde. Um den aktuellen Rowversion-Wert für eine Datenbank zurückzugeben, verwenden Sie [@@DBTS](../../t-sql/functions/dbts-transact-sql.md).
  
Sie können Hinzufügen einer **Rowversion** -Spalte einer Tabelle zur Erhaltung der Integrität der Datenbank, wenn mehrere Benutzer gleichzeitig Zeilen aktualisieren. Außerdem können Sie feststellen, wie viele und welche Zeilen aktualisiert wurden, ohne die Tabelle erneut abzufragen.
  
Nehmen Sie z. B. an, Sie erstellen eine Tabelle mit dem Namen `MyTest`. Sie laden einige Daten in der Tabelle durch Ausführen des folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen.
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
Anschließend können Sie die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Beispielanweisungen verwenden, um während des Updates eine Steuerung durch vollständige Parallelität in der `MyTest`-Tabelle zu implementieren.
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
`myValue`ist die **Rowversion** Spaltenwert für die Zeile, der Zeitpunkt der letzten angibt, dass die Zeile zu lesen. Dieser Wert ersetzt werden muss, durch den tatsächlichen **Rowversion** Wert. Ein Beispiel für den tatsächlichen **Rowversion** -Wert ist 0x00000000000007D3.
  
Sie können die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Beispielanweisungen auch in einer Transaktion ablegen. Indem Sie die `@t`-Variable im Gültigkeitsbereich der Transaktion abfragen, können Sie die aktualisierte `myKey`-Spalte der Tabelle abrufen, ohne die Tabelle t `MyTes`erneut abzufragen.
  
Im folgenden werden das gleiche Beispiel mit der **Zeitstempel** Syntax:
  
```sql
CREATE TABLE MyTest2 (myKey int PRIMARY KEY  
    ,myValue int, TS timestamp);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (2, 0);  
GO  
DECLARE @t TABLE (myKey int);  
UPDATE MyTest2  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND TS = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40; Transact-SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  

