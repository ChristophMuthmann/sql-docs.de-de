---
title: ALTER SEQUENCE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/08/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SEQUENCE_TSQL
- ALTER SEQUENCE
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, altering
- ALTER SEQUENCE statement
ms.assetid: decc0760-029e-4baf-96c9-4a64073df1c2
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: de7fd182be8fd79574c098a499a40a34d38aaf21
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-sequence-transact-sql"></a>ALTER SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Ändert die Argumente eines vorhandenen Sequenzobjekts. Wenn die Sequenz erstellt wurde, mit der **CACHE** Option ändern die Sequenz den Cache neu erstellt.  
  
 Sequenzobjekte werden erstellt, mit der [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) Anweisung. Sequenzen sind ganzzahlige Werte und können jeden Datentyp aufweisen, der eine ganze Zahl zurückgibt. Der Datentyp kann nicht mit der ALTER SEQUENCE-Anweisung geändert werden. Löschen und erstellen Sie das Sequenzobjekt, um den Datentyp zu ändern.  
  
 Eine Sequenz ist ein benutzerdefiniertes schemagebundenes Objekt, das anhand einer Spezifikation eine Reihe von numerischen Werten generiert. Neue Werte werden aus einer Sequenz generiert, indem die NEXT VALUE FOR-Funktion aufgerufen wird. Mit **sp_sequence_get_range** können Sie mehrere Sequenznummern gleichzeitig abrufen. Informationen und Szenarien, die sowohl CREATE SEQUENCE verwenden **Sp_sequence_get_range**, und die NEXT VALUE FOR-Funktion, finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER SEQUENCE [schema_name. ] sequence_name  
    [ RESTART [ WITH <constant> ] ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE <constant> } | { NO MINVALUE } ]  
    [ { MAXVALUE <constant> } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *sequence_name*  
 Gibt den eindeutigen Namen der Sequenz in der Datenbank an. Der Typ ist **Sysname**.  
  
 Neu starten [WITH \<Konstante >]  
 Der nächste Wert, der vom Sequenzobjekt zurückgegeben wird. Falls der RESTART WITH-Wert angegeben wird, muss er eine ganze Zahl kleiner oder gleich dem maximalen und größer oder gleich dem minimalen Wert des Sequenzobjekts darstellen. Wenn der WITH-Wert weggelassen wird, wird die Sequenznummerierung anhand der ursprünglichen CREATE SEQUENCE-Option neu gestartet.  
  
 INCREMENT BY \<Konstante >  
 Der Wert, um den der Basiswert des Sequenzobjekts bei jedem Aufruf der NEXT VALUE FOR-Funktion inkrementiert (oder bei negativem Wert dekrementiert) wird. Wenn als Inkrement ein negativer Wert verwendet wird, ist der Wert des Sequenzobjekts absteigend, andernfalls ist er aufsteigend. Das Inkrement kann nicht 0 sein.  
  
 [MINVALUE \<Konstante > | KEIN MINVALUE]  
 Gibt die Grenzen für das Sequenzobjekt an. Wenn NO MINVALUE angegeben wird, wird der minimal mögliche Wert des Sequenzdatentyps verwendet.  
  
 [MAXVALUE \<Konstante > | KEINE "MAXVALUE"  
 Gibt die Grenzen für das Sequenzobjekt an. Wenn NO MAXVALUE angegeben wird, wird der maximal mögliche Wert des Sequenzdatentyps verwendet.  
  
 [ CYCLE | NO CYCLE ]  
 Diese Eigenschaft gibt an, ob das Sequenzobjekt vom minimalen Wert (oder bei absteigenden Sequenzobjekten vom maximalen Wert) neu gestartet oder ob eine Ausnahme ausgelöst werden soll, wenn der minimale oder maximale Wert überschritten wird.  
  
> [!NOTE]  
>  Der nächste Wert nach dem Durchlauf ist der minimale oder maximale Wert, nicht der START VALUE der Sequenz.  
  
 [CACHE [\<Konstante >] | KEIN CACHE]  
 Vergrößert die Leistung für Anwendungen mit Sequenzobjekten durch Minimieren der Anzahl erforderlicher E/As zum Beibehalten von generierten Werten in den Systemtabellen.  
  
 Weitere Informationen zum Verhalten des Caches finden Sie unter [CREATE SEQUENCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-sequence-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Informationen wie Sequenzen erstellt werden und wie der Verwalten des sequenzcaches finden Sie unter [CREATE SEQUENCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 Der MINVALUE für aufsteigende Sequenzen und der MAXVALUE für absteigende Sequenzen können nicht auf einen Wert festgelegt werden, der den START WITH-Wert der Sequenz nicht zulässt. Um den MINVALUE einer aufsteigenden Sequenz auf einen höheren Wert als START WITH festzulegen, oder um den MAXVALUE einer absteigenden Sequenz auf einen niedrigeren Wert als START WITH festzulegen, schließen Sie das RESTART WITH-Argument ein, damit die Sequenz an einem gewünschten Punkt neu gestartet wird, der innerhalb des minimalen und maximalen Bereichswerts liegt.  
  
## <a name="metadata"></a>Metadaten  
 Weitere Informationen zu Sequenzen erhalten Sie durch Abfragen von [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert **ALTER** -Berechtigung für die Sequenz oder **ALTER** Berechtigung für das Schema. Erteilen von **ALTER** -Berechtigung für die Sequenz kann mit **ALTER ON OBJECT** im folgenden Format:  
  
```  
GRANT ALTER ON OBJECT::Test.TinySeq TO [AdventureWorks\Larry]  
```  
  
 Der Besitz eines Sequenzobjekts kann übertragen werden, mithilfe der **ALTER AUTHORIZATION** Anweisung.  
  
### <a name="audit"></a>Überwachung  
 Überwachen der **ALTER SEQUENCE**, Überwachen der **SCHEMA_OBJECT_CHANGE_GROUP**.  
  
## <a name="examples"></a>Beispiele  
 Beispiele für Sequenzen Erstellung und Verwendung der **NEXT VALUE FOR** Funktion zum Generieren von Sequenznummern finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
### <a name="a-altering-a-sequence"></a>A. Ändern einer Sequenz  
 Das folgende Beispiel erstellt ein Schema mit dem Namen Test und die Sequenz TestSeq mithilfe der **Int** -Datentyp, und ein Bereich von 0 bis 255. Die Sequenz beginnt mit 125 und wird immer um 25 inkrementiert, wenn eine Zahl generiert wurde. Da die Sequenz zum Durchlaufen konfiguriert wurde, wird sie beim Überschreiten des maximalen Werts von 200 beim minimalen Wert von 100 neu gestartet.  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.TestSeq  
    AS int   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
GO  
```  
  
 Im folgenden Beispiel wird die Sequenz TestSeq, um einen Bereich von 0 bis 255 aufweisen. Die Nummerierung wird von der Sequenz bei 100 neu gestartet und wird immer um 50 inkrementiert, wenn eine Zahl generiert wurde.  
  
```  
ALTER SEQUENCE Test. TestSeq  
    RESTART WITH 100  
    INCREMENT BY 50  
    MINVALUE 50  
    MAXVALUE 200  
    NO CYCLE  
    NO CACHE  
;  
GO  
```  
  
 Da die Sequenz keine Durchläufe ausführt, führt der **NEXT VALUE FOR** Funktion führt zu einem Fehler, wenn die Sequenz 200 überschreitet.  
  
### <a name="b-restarting-a-sequence"></a>B. Neustarten einer Sequenz  
 Das folgende Beispiel erstellt eine Sequenz namens CountBy1. Die Sequenz verwendet die Standardwerte.  
  
```  
CREATE SEQUENCE Test.CountBy1 ;  
```  
  
 Um einen Sequenzwert zu generieren, wird vom Besitzer folgende Anweisung ausgeführt:  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1  
```  
  
 Ein Rückgabewert von -9.223.372.036.854.775.808 ist der niedrigst mögliche Wert für die **"bigint"** -Datentyp. Der Besitzer erkennt, dass er die Sequenz bei 1 beginnen möchten, aber nicht gab die **START WITH** -Klausel, wenn er die Sequenz erstellt. Um diesen Fehler zu korrigieren, wird die folgende Anweisung vom Besitzer ausgeführt.  
  
```  
ALTER SEQUENCE Test.CountBy1 RESTART WITH 1 ;  
```  
  
 Anschließend wird die folgende Anweisung vom Besitzer ausgeführt, um erneut eine Sequenznummer zu generieren.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1;  
```  
  
 Die Zahl ist jetzt 1, wie erwartet.  
  
 Die Sequenz CountBy1 erstellt wurde, den Standardwert von NO CYCLE verwenden, damit sie nach der Generierung Zahl 9.223.372.036.854.775.807 Betriebssystem beendet werden soll. Nachfolgende Aufrufe des Sequenzobjekts geben den Fehler 11728 zurück. Die folgende Anweisung ändert das Sequenzobjekt auf Durchläufe und legt einen Cache von 20 fest.  
  
```  
ALTER SEQUENCE Test.CountBy1  
    CYCLE  
    CACHE 20 ;  
  
```  
  
 Wenn vom Sequenzobjekt jetzt der Wert 9.223.372.036.854.775.807 erreicht wird, erfolgt ein Durchlauf, und die nächste Zahl nach dem Durchlauf ist der minimale Wert des Datentyps -9.223.372.036.854.775.808.  
  
 Der Besitzer hat festgestellt, dass die **"bigint"** -Datentyp verwendet 8 Bytes bei jedem dient. Die **Int** reicht-Datentyp, der 4 Bytes verwendet. Der Datentyp eines Sequenzobjekts kann jedoch nicht geändert werden. So ändern Sie in einer **Int** -Datentyp, der Besitzer muss das Sequenzobjekt, das Löschen und Neuerstellen des Objekts mit den richtigen Datentyp.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NÄCHSTEN Wert für &#40; Transact-SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [Sp_sequence_get_range &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  

