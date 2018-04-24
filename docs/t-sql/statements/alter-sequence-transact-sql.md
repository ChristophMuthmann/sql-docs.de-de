---
title: ALTER SEQUENCE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ba1b939e4ca20e4fb191296ad0d5f49be5c4380e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-sequence-transact-sql"></a>ALTER SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Ändert die Argumente eines vorhandenen Sequenzobjekts. Wenn die Sequenz mit der **CACHE**-Option erstellt wurde, wird der Cache durch Ändern der Sequenz neu erstellt.  
  
 Sequenzobjekte werden mit der [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md)-Anweisung erstellt. Sequenzen sind ganzzahlige Werte und können jeden Datentyp aufweisen, der eine ganze Zahl zurückgibt. Der Datentyp kann nicht mit der ALTER SEQUENCE-Anweisung geändert werden. Löschen und erstellen Sie das Sequenzobjekt, um den Datentyp zu ändern.  
  
 Eine Sequenz ist ein benutzerdefiniertes schemagebundenes Objekt, das anhand einer Spezifikation eine Reihe von numerischen Werten generiert. Neue Werte werden aus einer Sequenz generiert, indem die NEXT VALUE FOR-Funktion aufgerufen wird. Mit **sp_sequence_get_range** können Sie mehrere Sequenznummern gleichzeitig abrufen. Informationen und Szenarios, in denen die CREATE SEQUENCE-Funktion, **sp_sequence_get_range** und die NEXT VALUE FOR-Funktion verwendet werden, finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
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
 Gibt den eindeutigen Namen der Sequenz in der Datenbank an. Der Typ ist **sysname**.  
  
 RESTART [ WITH \<constant> ]  
 Der nächste Wert, der vom Sequenzobjekt zurückgegeben wird. Falls der RESTART WITH-Wert angegeben wird, muss er eine ganze Zahl kleiner oder gleich dem maximalen und größer oder gleich dem minimalen Wert des Sequenzobjekts darstellen. Wenn der WITH-Wert weggelassen wird, wird die Sequenznummerierung anhand der ursprünglichen CREATE SEQUENCE-Option neu gestartet.  
  
 INCREMENT BY \<constant>  
 Der Wert, um den der Basiswert des Sequenzobjekts bei jedem Aufruf der NEXT VALUE FOR-Funktion inkrementiert (oder bei negativem Wert dekrementiert) wird. Wenn als Inkrement ein negativer Wert verwendet wird, ist der Wert des Sequenzobjekts absteigend, andernfalls ist er aufsteigend. Das Inkrement kann nicht 0 sein.  
  
 [ MINVALUE \<constant> | NO MINVALUE ]  
 Gibt die Grenzen für das Sequenzobjekt an. Wenn NO MINVALUE angegeben wird, wird der minimal mögliche Wert des Sequenzdatentyps verwendet.  
  
 [ MAXVALUE \<constant> | NO MAXVALUE  
 Gibt die Grenzen für das Sequenzobjekt an. Wenn NO MAXVALUE angegeben wird, wird der maximal mögliche Wert des Sequenzdatentyps verwendet.  
  
 [ CYCLE | NO CYCLE ]  
 Diese Eigenschaft gibt an, ob das Sequenzobjekt vom minimalen Wert (oder bei absteigenden Sequenzobjekten vom maximalen Wert) neu gestartet oder ob eine Ausnahme ausgelöst werden soll, wenn der minimale oder maximale Wert überschritten wird.  
  
> [!NOTE]  
>  Der nächste Wert nach dem Durchlauf ist der minimale oder maximale Wert, nicht der START VALUE der Sequenz.  
  
 [ CACHE [\<constant> ] | NO CACHE ]  
 Vergrößert die Leistung für Anwendungen mit Sequenzobjekten durch Minimieren der Anzahl erforderlicher E/As zum Beibehalten von generierten Werten in den Systemtabellen.  
  
 Weitere Informationen zum Verhalten des Caches finden Sie unter [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Informationen zum Erstellen von Sequenzen sowie zum Verwalten des Sequenzcaches finden Sie unter [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 Der MINVALUE für aufsteigende Sequenzen und der MAXVALUE für absteigende Sequenzen können nicht auf einen Wert festgelegt werden, der den START WITH-Wert der Sequenz nicht zulässt. Um den MINVALUE einer aufsteigenden Sequenz auf einen höheren Wert als START WITH festzulegen, oder um den MAXVALUE einer absteigenden Sequenz auf einen niedrigeren Wert als START WITH festzulegen, schließen Sie das RESTART WITH-Argument ein, damit die Sequenz an einem gewünschten Punkt neu gestartet wird, der innerhalb des minimalen und maximalen Bereichswerts liegt.  
  
## <a name="metadata"></a>Metadaten  
 Weitere Informationen zu Sequenzen erhalten Sie durch Abfragen von [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die **ALTER**-Berechtigung für die Sequenz oder die **ALTER**-Berechtigung für das Schema. Die **ALTER**-Berechtigung für die Sequenz kann mit **ALTER ON OBJECT** im folgenden Format erteilt werden:  
  
```  
GRANT ALTER ON OBJECT::Test.TinySeq TO [AdventureWorks\Larry]  
```  
  
 Der Besitz eines Sequenzobjekts kann mit der **ALTER AUTHORIZATION**-Anweisung übertragen werden.  
  
### <a name="audit"></a>Überwachen von  
 Überwachen Sie **SCHEMA_OBJECT_CHANGE_GROUP**, um **ALTER SEQUENCE** zu überwachen.  
  
## <a name="examples"></a>Beispiele  
 Beispiele zum Erstellen von Sequenzen und Verwenden der **NEXT VALUE FOR**-Funktion für das Generieren von Sequenznummern finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
### <a name="a-altering-a-sequence"></a>A. Ändern einer Sequenz  
 Im folgenden Beispiel werden das Schema „Test“ und die Sequenz „TestSeq“ mit dem **int**-Datentyp und einem Bereich von 0 bis 255 erstellt. Die Sequenz beginnt mit 125 und wird immer um 25 inkrementiert, wenn eine Zahl generiert wurde. Da die Sequenz zum Durchlaufen konfiguriert wurde, wird sie beim Überschreiten des maximalen Werts von 200 beim minimalen Wert von 100 neu gestartet.  
  
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
  
 Im folgenden Beispiel wird die Sequenz „TestSeq“ so geändert, dass sie über einen Bereich von 0 bis 255 verfügt. Die Nummerierung wird von der Sequenz bei 100 neu gestartet und wird immer um 50 inkrementiert, wenn eine Zahl generiert wurde.  
  
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
  
 Da die Sequenz keine Durchläufe ausführt, führt die **NEXT VALUE FOR**-Funktion zu einem Fehler, wenn die Sequenz 200 überschreitet.  
  
### <a name="b-restarting-a-sequence"></a>B. Neustarten einer Sequenz  
 Im folgenden Beispiel wird die Sequenz „CountBy1“ erstellt. Die Sequenz verwendet die Standardwerte.  
  
```  
CREATE SEQUENCE Test.CountBy1 ;  
```  
  
 Um einen Sequenzwert zu generieren, wird vom Besitzer folgende Anweisung ausgeführt:  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1  
```  
  
 Der zurückgegebene Wert –9.223.372.036.854.775.808 ist der niedrigst mögliche Wert des **bigint**-Datentyps. Der Besitzer erkennt, dass die Sequenz bei 1 beginnen sollte, die **START WITH**-Klausel beim Erstellen der Sequenz allerdings nicht angegeben wurde. Um diesen Fehler zu korrigieren, wird die folgende Anweisung vom Besitzer ausgeführt.  
  
```  
ALTER SEQUENCE Test.CountBy1 RESTART WITH 1 ;  
```  
  
 Anschließend wird die folgende Anweisung vom Besitzer ausgeführt, um erneut eine Sequenznummer zu generieren.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1;  
```  
  
 Die Zahl ist jetzt 1, wie erwartet.  
  
 Die Sequenz „CountBy1“ wurde mit dem Standardwert von NO CYCLE erstellt. Nachdem die Zahl 9.223.372.036.854.775.807 generiert wurde, wird die Ausführung daher beendet. Nachfolgende Aufrufe des Sequenzobjekts geben den Fehler 11728 zurück. Die folgende Anweisung ändert das Sequenzobjekt auf Durchläufe und legt einen Cache von 20 fest.  
  
```  
ALTER SEQUENCE Test.CountBy1  
    CYCLE  
    CACHE 20 ;  
  
```  
  
 Wenn vom Sequenzobjekt jetzt der Wert 9.223.372.036.854.775.807 erreicht wird, erfolgt ein Durchlauf, und die nächste Zahl nach dem Durchlauf ist der minimale Wert des Datentyps -9.223.372.036.854.775.808.  
  
 Der Besitzer hat festgestellt, dass der **bigint**-Datentyp jeweils 8 Byte verwendet. Der **int**-Datentyp, der 4 Byte verwendet, ist ausreichend. Der Datentyp eines Sequenzobjekts kann jedoch nicht geändert werden. Eine Änderung in den **int**-Datentyp erfordert das Löschen des Sequenzobjekts durch den Besitzer und das Neuerstellen des Objekts mit dem korrekten Datentyp.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
