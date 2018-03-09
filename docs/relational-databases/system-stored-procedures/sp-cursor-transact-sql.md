---
title: Sp_cursor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e85732afe35198cea86a605dfde8396b013842dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spcursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fordert positionierte Updates an. Mithilfe dieser Prozedur werden Vorgänge für mindestens eine Zeile im Fetchpuffer eines Cursors ausgeführt. Sp_cursor wird aufgerufen, indem ID = 1 in einem tabular Data Stream (TDS)-Paket.  
  
||  
|-|  
|**Gilt für**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>Argumente  
 *Cursor*  
 Das Cursorhandle. *Cursor* ist ein erforderlicher Parameter, der erfordert eine **Int** Eingabewert. *Cursor* ist die *behandeln* Wert von SQL Server generiert und von der Prozedur Sp_cursoropen zurückgegeben.  
  
 *optype*  
 Ein erforderlicher Parameter, der festlegt, welcher Vorgang vom Cursor ausgeführt wird. *Optype* muss eine der folgenden **Int** Eingabewerte.  
  
|Wert|Name|Description|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|Wird zum Update mindestens einer Zeile im Fetchpuffer verwendet.  Die Zeilen im angegebenen *Rownum* erneut abgerufen und aktualisiert werden.|  
|0x0002|DELETE|Wird zum Löschen mindestens einer Zeile im Fetchpuffer verwendet. Die Zeilen im angegebenen *Rownum* erneut abgerufen und gelöscht werden.|  
|0X0004|INSERT|Fügt Daten ohne erstellen ein SQL **einfügen** Anweisung.|  
|0X0008|REFRESH|Wird verwendet, um den Puffer mithilfe zugrunde liegender Tabellen aufzufüllen, und kann zum Update der Zeile verwendet werden, wenn ein Update- oder Löschvorgang aufgrund der Steuerung durch vollständige Parallelität fehlerhaft ist, oder nachdem ein UPDATE-Vorgang ausgeführt wurde.|  
|0X10|LOCK|Bewirkt, dass eine SQL Server U-Sperre auf der Seite mit der angegebenen Zeile abgerufen werden. Diese Sperre ist mit S-Sperren kompatibel, jedoch nicht mit X-Sperren oder anderen U-Sperren. Kann verwendet werden, um eine kurzfristige Sperre zu implementieren.|  
|0X20|SETPOSITION|Wird verwendet, nur wenn das Programm eine nachfolgende SQL-Server ausgeben möchten DELETE- oder UPDATE-Anweisung positioniert.|  
|0X40|ABSOLUTE|Kann nur in Verbindung mit UPDATE oder DELETE verwendet werden.  ABSOLUTE wird nur mit KEYSET-Cursorn verwendet (wird für DYNAMIC-Cursor ignoriert, und STATIC-Cursor können nicht aktualisiert werden).<br /><br /> Hinweis: Wenn ABSOLUTE für eine Zeile im Keyset angegeben wird, die nicht abgerufen wurde, die der Vorgang kann fehlschlagen, die Überprüfung auf Parallelität, und das Rückgabeergebnis nicht garantiert werden kann.|  
  
 *rowNum*  
 Gibt an, welche Zeilen der Cursor im Fetchpuffer verwendet, aktualisiert oder löscht.  
  
> [!NOTE]  
>  Weder dieser Wert noch die über sp_cursor ausgeführten Update- oder Löschvorgänge wirken sich auf den Ausgangspunkt eines Abrufvorgangs RELATIVE, NEXT oder PREVIOUS aus.  
  
 *RowNum* ist ein erforderlicher Parameter, der erfordert eine **Int** Eingabewert.  
  
 1  
 Gibt die erste Zeile im Fetchpuffer an.  
  
 2  
 Gibt die zweite Zeile im Fetchpuffer an.  
  
 3, 4, 5  
 Gibt die dritte Zeile an usw.  
  
 n  
 Gibt die n-te Zeile im Fetchpuffer an.  
  
 0  
 Gibt alle Zeilen im Fetchpuffer an.  
  
> [!NOTE]  
>  Gilt nur für die Verwendung mit AKTUALISIERUNGS-, Lösch-, REFRESH oder LOCK *Optype* Werte.  
  
 *table*  
 Tabellenname, der die Tabelle identifiziert, *Optype* wendet auf, wenn die Cursordefinition einen Join einschließt oder mehrdeutige Spaltennamen, durch zurückgegeben werden die *Wert* Parameter. Wenn keine bestimmte Tabelle festgelegt wird, wird die erste Tabelle in der FROM-Klausel als Standard verwendet. *Tabelle* ist ein optionaler Parameter, die Zeichenfolgen-Eingabewerte erfordert. Die Zeichenfolge kann als beliebiges Zeichen oder UNICODE-Datentyp angegeben werden. *Tabelle* kann ein mehrteiliger Tabellenname sein.  
  
 *value*  
 Wird zum Einfügen oder Aktualisieren von Werten verwendet. Die *Wert* Zeichenfolgenparameter dient lediglich mit Update- und INSERT *Optype* Werte. Die Zeichenfolge kann als beliebiges Zeichen oder UNICODE-Datentyp angegeben werden.  
  
> [!NOTE]  
>  Die Parameternamen für *Wert* kann vom Benutzer zugewiesen werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Bei Verwendung von RPC zurück ein positionierter DELETE- oder UPDATE-Vorgang mit der puffernummer 0 eine DONE-Meldung mit einer *Rowcount* 0 (Fehler) oder 1 (Erfolg) für jede Zeile im Fetchpuffer.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="optype-parameter"></a>optype-Parameter  
 Mit Ausnahme der Kombinationen von SETPOSITION mit UPDATE, DELETE, Aktualisierung oder SPERRE; bzw. ABSOLUTE mit UPDATE oder DELETE, die *Optype* Werte schließen sich gegenseitig.  
  
 Die SET-Klausel des UPDATE-Werts wird erstellt, aus der *Wert* Parameter.  
  
 Ein Vorteil der Verwendung von INSERT *Optype* Wert ist, Sie vermeiden können, Konvertieren von nicht-Zeichendaten in das Zeichenformat für einfügungen. Die Werte werden auf die gleiche Weise wie bei UPDATE angegeben. Wenn eine der erforderlichen Spalten nicht eingeschlossen wird, tritt ein INSERT-Fehler auf.  
  
-   Weder der SETPOSITION-Wert noch die über die sp_cursor-Schnittstelle ausgeführten Update- oder Löschvorgänge wirken sich auf den Ausgangspunkt eines Abrufvorgangs RELATIVE, NEXT oder PREVIOUS aus. Jede Zahl, die keine Zeile im Fetchpuffer angibt, führt dazu, dass die Position auf 1 festgelegt und kein Fehler zurückgegeben wird. Nachdem SETPOSITION ausgeführt wurde, der die Position bleibt wirksam, bis der nächste Sp_cursorfetch-Vorgang, T-SQL- **FETCH** Vorgang oder Sp_cursor SETPOSITION-Vorgang über den gleichen Cursor. Durch einen nachfolgenden sp_cursorfetch-Vorgang wird die Cursorposition auf die erste Zeile im neuen Fetchpuffer festgelegt, während sich andere Cursoraufrufe nicht auf den Wert der Position auswirken. SETPOSITION kann von einer OR-Klausel mit REFRESH, UPDATE, DELETE oder LOCK verknüpft werden, um den Wert der Position auf die letzte geänderte Zeile festzulegen.  
  
 Wenn eine Zeile im Fetchpuffer nicht über angegeben ist die *Rownum* Parameter, der die Position wird auf 1 festgelegt werden, und kein Fehler zurückgegeben. Nachdem die Position festgelegt wurde, bleibt sie so lange wirksam, bis der nächste sp_cursorfetch-Vorgang, T-SQL FETCH-Vorgang oder sp_cursor SETPOSITION-Vorgang für den gleichen Cursor ausgeführt wird.  
  
 SETPOSITION kann von einer OR-Klausel mit REFRESH, UPDATE, DELETE oder LOCK verknüpft werden, um die Cursorposition auf die letzte geänderte Zeile festzulegen.  
  
## <a name="rownum-parameter"></a>rownum-Parameter  
 Wenn angegeben, die *Rownum* Parameter als Zeilennummer innerhalb des Keysets anstatt die Nummer der Zeile innerhalb des fetchpuffers interpretiert werden kann. Der Benutzer ist für die Einhaltung der Parallelitätssteuerung verantwortlich. Dies bedeutet, dass bei SCROLL_LOCKS-Cursorn eine Sperre für die angegebene Zeile unabhängig verwaltet werden muss (dies kann über eine Transaktion erfolgen). Bei OPTIMISTIC-Cursorn müssen Sie zuvor die Zeile abgerufen haben, um diesen Vorgang auszuführen.  
  
## <a name="table-parameter"></a>table-Parameter  
 Wenn die *Optype* -Wert UPDATE oder INSERT und ein vollständiges Update oder Insert-Anweisung wird als übermittelt die *Wert* Parameter, der angegebene Wert für *Tabelle* wird ignoriert.  
  
> [!NOTE]  
>  Bei Sichten kann nur eine zur Sicht gehörige Tabelle geändert werden. Die *Wert* Parameternamen für die Spalte müssen die Spaltennamen in der Sicht entsprechen, jedoch kann der Tabellenname, die von der zugrunde liegenden Basistabelle (in diesem Fall Sp_cursor des Ansichtsnamens ersetzt wird).  
  
## <a name="value-parameter"></a>value-Parameter  
 Es gibt zwei Alternativen zu den Regeln für die Verwendung von *Wert* wie zuvor im Abschnitt "Argumente" angegeben:  
  
1.  Können Sie einen Namen mit "@" vorangestellt, die auf den Namen der Spalte in der Select-Liste für jeden benannten *Wert* Parameter. Ein Vorteil dabei ist, dass möglicherweise keine Datenkonvertierung erforderlich ist.  
  
2.  Verwenden Sie einen Parameter, um eine vollständige Update- oder INSERT-Anweisung übermitteln, oder verwenden Sie mehrere Parameter, um Teile einer Update- oder INSERT-Anweisung zu übermitteln der SQL Server, klicken Sie dann in eine vollständige Anweisung erstellen. Beispiele dafür finden Sie im Abschnitt "Beispiele" weiter unten in diesem Thema.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="alternative-value-parameter-uses"></a>Alternative Verwendung des value-Parameters  
 Für UPDATE:  
  
 Wenn ein einzelner Parameter verwendet wird, kann eine UPDATE-Anweisung mit der folgenden Syntax übermittelt werden:  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,…n]`  
  
> [!NOTE]  
>  Wenn UPDATE \<Tabellenname > angegeben ist, wird ein Wert angegeben wird, für die *Tabelle* -Parameter wird ignoriert.  
  
 Wenn mehrere Parameter verwendet werden, muss der erste Parameter eine Zeichenfolge in der folgenden Form sein:  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 und die nachfolgenden Parameter müssen die folgende Form aufweisen:  
  
 `<column name> = expression  [,...n]`  
  
 In diesem Fall die \<Tabellenname > in der erstellten Update-Anweisung ist die einem angegebenen oder standardmäßig auf durch die *Tabelle* Parameter.  
  
 Für INSERT:  
  
 Wenn ein einzelner Parameter verwendet wird, kann eine INSERT-Anweisung mit der folgenden Syntax übermittelt werden:  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  Wenn INSERT  *\<Tabellenname >* angegeben ist, wird ein Wert angegeben wird, für die *Tabelle* -Parameter wird ignoriert.  
  
 Wenn mehrere Parameter verwendet werden, muss der erste Parameter eine Zeichenfolge in der folgenden Form sein:  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 und die nachfolgenden Parameter müssen die folgende Form aufweisen:  
  
 `expression [,...n]`  
  
 es sei denn, VALUES wurde angegeben; in diesem Fall muss der letzte Ausdruck mit einer abschließenden ")" enden. In diesem Fall die  *\<Tabellenname >* in der erstellten Update-Anweisung ist die einem angegebenen oder standardmäßig auf durch die *Tabelle* Parameter.  
  
> [!NOTE]  
>  Es ist möglich, einen Parameter als benannten Parameter zu übermitteln, d. h. "`@VALUES`". In diesem Fall können keine weiteren benannten Parameter verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_cursoropen &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Sp_cursorfetch &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
