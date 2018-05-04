---
title: Sp_cursorfetch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 66343bef328a2194ed825152b64a7a9ba600d707
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spcursorfetch-transact-sql"></a>sp_cursorfetch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft einen Puffer mit mindestens einer Zeile aus der Datenbank ab. Die Gruppe der Zeilen in diesem Puffer wird aufgerufen, des Cursors *Fetchpuffer*. Sp_cursorfetch wird aufgerufen, indem ID = 7 in einem tabular Data Stream (TDS)-Paket.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>Argumente  
 *Cursor*  
 Ist eine *behandeln* generierter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und der von Sp_cursoropen zurückgegeben. *Cursor* ist ein erforderlicher Parameter, der erfordert eine **Int** Eingabewert. Weitere Informationen finden Sie im Abschnitt mit den Hinweisen weiter unten in diesem Thema.  
  
 *FetchType*  
 Gibt an, welcher Cursorpuffer abgerufen werden soll. *FetchType* ist ein optionaler Parameter, der einen der folgenden ganzzahligen Eingabewerte erfordert.  
  
|Wert|Name|Description|  
|-----------|----------|-----------------|  
|0x0001|FIRST|Ruft den ersten Puffer *Nrows* Zeilen. Wenn *Nrows* gleich 0 ist, wird der Cursor vor dem Resultset positioniert und keine Zeilen zurückgegeben werden.|  
|0x0002|NEXT|Ruft den nächsten Puffer *Nrows* Zeilen.|  
|0x0004|PREV|Ruft den vorherigen Puffer *Nrows* Zeilen.<br /><br /> Hinweis: Bei Verwendung von PREV für einen FORWARD_ONLY-Cursor wird eine Fehlermeldung angezeigt, weil FORWARD_ONLY nur den Bildlauf unterstützt in einer Richtung.|  
|0x0008|LAST|Ruft den letzten Puffer *Nrows* Zeilen. Wenn *Nrows* 0 entspricht, wird der Cursor positioniert ist, nachdem das Resultset und keine Zeilen zurückgegeben werden.<br /><br /> Hinweis: Bei Verwendung von LAST für einen FORWARD_ONLY-Cursor wird eine Fehlermeldung angezeigt, weil FORWARD_ONLY nur den Bildlauf unterstützt in einer Richtung.|  
|0x10|ABSOLUTE|Ruft einen Puffer von *Nrows* -Zeilen beginnend mit der *Rownum* Zeile.<br /><br /> Hinweis: Bei Verwendung von ABSOLUTE für einen dynamischen Cursor oder einen FORWARD_ONLY-Cursor wird eine Fehlermeldung angezeigt, weil FORWARD_ONLY nur den Bildlauf unterstützt in einer Richtung.|  
|0x20|RELATIVE|Ruft den Puffer *Nrows* -Zeilen beginnend mit der Zeile, die als angegeben, wird die *Rownum* Wert von Zeilen aus der ersten Zeile im aktuellen Block. In diesem Fall *Rownum* kann eine negative Zahl sein.<br /><br /> Hinweis: Bei Verwendung von RELATIVE für einen FORWARD_ONLY-Cursor wird eine Fehlermeldung angezeigt, weil FORWARD_ONLY nur den Bildlauf unterstützt in einer Richtung.|  
|0x80|REFRESH|Füllt den Puffer anhand zugrunde liegender Tabellen auf.|  
|0x100|INFO|Ruft Informationen zum Cursor ab. Diese Informationen werden zurückgegeben, mit der *Rownum* und *Nrows* Parameter. Wenn deshalb INFO angegeben wird, *Rownum* und *Nrows* werden Output-Parameter.|  
|0x200|PREV_NOADJUST|Wird analog zu PREV verwendet. Wenn der Anfang des Resultsets vorzeitig gefunden wird, können die Ergebnisse jedoch variieren.|  
|0x400|SKIP_UPDT_CNCY|Muss zusammen mit anderen *Fetchtype* -Werte außer INFO.|  
  
> [!NOTE]  
>  Der Wert 0x40 wird nicht unterstützt.  
  
 Weitere Informationen finden Sie im Abschnitt mit den Hinweisen weiter unten in diesem Thema.  
  
 *rowNum*  
 Ist ein optionaler Parameter, der verwendet wird, an die Zeilenposition für die ABSOLUTE und INFO *Fetchtype* Werte mit nur ganzzahlige Werte für die Eingabe oder Ausgabe oder beides. *RowNum* dient als Zeilenoffset für die *Fetchtype* -Bitwert RELATIVE. *RowNum* wird für alle anderen Werte ignoriert. Weitere Informationen finden Sie im Abschnitt mit den Hinweisen weiter unten in diesem Thema.  
  
 *nrows*  
 Ein optionaler Parameter, mit dem die Anzahl der abzurufenden Zeilen angegeben wird. Wenn *Nrows* nicht angegeben ist, wird der Standardwert ist 20 Zeilen. Geben Sie zum Festlegen der Position ohne Rückgabe von Daten den Wert 0 ein. Wenn *Nrows* wird angewendet, um die *Fetchtype* INFO-Abfrage wird die Gesamtanzahl der Zeilen in der Abfrage.  
  
> [!NOTE]  
>  *Nrows* wird durch die Aktualisierung ignoriert *Fetchtype* -Bitwert.  
>   
>  Weitere Informationen finden Sie im Abschnitt mit den Hinweisen weiter unten in diesem Thema.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 In den folgenden Tabellen sind die Werte dargestellt, die bei Angabe des Bitwerts INFO zurückgegeben werden können.  
  
> [!NOTE]  
>  : Wenn keine Zeilen zurückgegeben werden, bleibt der Pufferinhalt wie waren.  
  
|*\<RowNum >*|Festlegen auf|  
|------------------|------------|  
|Falls nicht geöffnet|0|  
|Falls vor dem Resultset positioniert|0|  
|Falls nach dem Resultset positioniert|-1|  
|Für KEYSET- und STATIC-Cursor|Die absolute Zeilennummer der aktuellen Position im Resultset|  
|Für DYNAMIC-Cursor|1|  
|Für ABSOLUTE|-1 gibt die letzte Zeile in einem Satz zurück.<br /><br /> -2 gibt die vorletzte Zeile in einem Satz zurück usw.<br /><br /> Hinweis: Wenn mehr als eine Zeile in diesem Fall abgerufen werden angefordert wird, werden die letzten beiden Zeilen des Resultsets zurückgegeben.|  
  
|*\<Nrows >*|Festlegen auf|  
|-----------------|------------|  
|Falls nicht geöffnet|0|  
|Für KEYSET- und STATIC-Cursor|Normalerweise die aktuelle Keysetgröße.<br /><br /> **– m** , wenn der Cursor asynchron erstellt wird *m* Zeilen, die zum angegebenen Zeitpunkt gefunden.|  
|Für DYNAMIC-Cursor|-1|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="cursor-parameter"></a>cursor-Parameter  
 Bevor Abrufvorgänge stattgefunden haben, befindet sich die Standardposition eines Cursors vor der ersten Zeile des Resultsets.  
  
## <a name="fetchtype-parameter"></a>fetchtype-Parameter  
 Außer bei skip_upd_cncy schließen sich die *Fetchtype* Werte schließen sich gegenseitig.  
  
 Wenn SKIP_UPDT_CNCY angegeben wird, werden die timestamp-Spaltenwerte nicht in die Keysettabelle geschrieben, wenn eine Zeile abgerufen oder aktualisiert wird. Wenn die Keysetzeile aktualisiert wird, wird für die Werte der timestamp-Spalten der vorherige Wert beibehalten. Wenn die Keysetzeile eingefügt wird, wird die Definition der Werte für die timestamp-Spalten aufgehoben.  
  
 Bei KEYSET-Cursorn bedeutet dies, dass die Werte der Keysettabelle während des letzten durchgehenden FETCH-Vorgangs festgelegt wurden, falls einer ausgeführt wurde. Andernfalls werden die Werte während der Auffüllung festgelegt.  
  
 Bei DYNAMIC-Cursorn bedeutet dies, dass die gleichen Ergebnisse erzeugt werden wie bei KEYSET, wenn der SKIP-Vorgang mit einer Aktualisierung ausgeführt wird. Bei jedem anderen Fetchtyp wird die Keysettabelle abgeschnitten. Dies bedeutet, dass die Zeilen eingefügt werden und die Definition der Werte für die timestamp-Spalte(n) aufgehoben wird. Wenn Sie sp_cursorfetch für DYNAMIC-Cursor ausführen, sollten Sie SKIP_UPDT_CNCY bei jedem anderen Vorgang als REFRESH folglich vermeiden.  
  
 Wenn ein Abrufvorgang fehlerhaft ist, weil die angeforderte Cursorposition außerhalb des Resultsets liegt, wird die Cursorposition unmittelbar nach der letzten Zeile festgelegt. Wenn ein Abrufvorgang fehlerhaft ist, weil die angeforderte Cursorposition vor dem Resultset liegt, wird die Cursorposition vor der ersten Zeile festgelegt.  
  
## <a name="rownum-parameter"></a>rownum-Parameter  
 Bei Verwendung von *Rownum*, der Puffer voll ist, mit der angegebenen Zeile ab.  
  
 Die *Fetchtype* -Wert ABSOLUTE auf die Position des verweist *Rownum* innerhalb des gesamten Resultsets festgelegt. Eine negative Zahl mit ABSOLUTE gibt an, dass bei dem Vorgang Zeilen vom Ende des Resultsets gezählt werden.  
  
 Die *Fetchtype* -Wert RELATIVE, der die Position des verweist *Rownum* in Bezug auf die Position des Cursors am Anfang des aktuellen Puffers. Eine negative Zahl mit RELATIVE gibt an, dass sich der Cursor von der aktuellen Cursorposition rückwärts bewegt.  
  
## <a name="nrows-parameter"></a>nrows-Parameter  
 Die *Fetchtype* -Werten REFRESH und INFO dieser Parameter ignoriert.  
  
 Geben Sie bei einer *Fetchtype* Wert des ersten, der verfügt über eine *Nrow* Wert 0 ist der Cursor positioniert ist, vor dem Resultset, die keine Zeilen im Fetchpuffer verfügt.  
  
 Geben Sie bei einer *Fetchtype* -Wert LAST, die verfügt ein *Nrow* Wert 0 ist der Cursor positioniert ist, nach dem Resultset, die keine Zeilen im aktuellen Fetchpuffer verfügt.  
  
 Für die *Fetchtype* Werte des nächsten, PREV, ABSOLUTE, RELATIVE und PREV_NOADJUST ist ein *Nrow* Wert 0 ist ungültig.  
  
## <a name="rpc-considerations"></a>Überlegungen zu RPC  
 Der RPC-Rückgabestatus gibt an, ob der KEYSET_SIZE-Parameter abgeschlossen ist, d. h., ob das Keyset oder die temporäre Tabelle asynchron aufgefüllt wird.  
  
 Der RPC-Statusparameter wird auf einen der Werte in der folgenden Tabelle festgelegt.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Die Prozedur wurde erfolgreich ausgeführt.|  
|0x0001|Fehler bei der Prozedur.|  
|0x0002|Ein Abruf in einer negativen Richtung hätte die Cursorposition auf den Anfang des Resultsets festgelegt, wenn der Abruf logisch vor den Ergebnissen erfolgt wäre.|  
|0x10|Ein FAST_FORWARD-Cursor wurde automatisch geschlossen.|  
  
 Die Zeilen werden als typisches Resultset zurückgegeben: Spaltenformat (0x2a), Zeilen (0xd1) gefolgt vom fertigen Resultset (0xfd). Metadatentoken werden im gleichen Format gesendet wie für sp_cursoropen angegeben: 0x81, 0xa5 und 0xa4 für SQL Server 7.0-Benutzer usw. Die Zeilenstatusindikatoren werden ähnlich dem BROWSE-Modus als ausgeblendete Spalten am Ende jeder Zeile mit dem Spaltennamen "rowstat" und dem Datentyp INT4 gesendet. Diese rowstat-Spalte verfügt über einen der Werte aus der folgenden Tabelle.  
  
|Wert|Description|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 Weil das TDS-Protokoll keine Möglichkeit bietet, die nachfolgende Statusspalte ohne die vorherigen Spalten zu senden, werden Pseudodaten für fehlende Zeilen gesendet (auf NULL festlegbare Felder sind auf NULL, Felder fester Datenlänge auf 0 (leer) oder ggf. den Standardwert für diese Spalte festgelegt).  
  
 Die DONE-Zeilenanzahl ist immer 0 (null). Die DONE-Meldung enthält die tatsächliche Zeilenanzahl des Resultsets, und Fehler- oder Informationsmeldungen können zwischen allen TDS-Meldungen angezeigt werden.  
  
 Damit die Metadaten zur SELECT-Liste des Cursors im TDS-Datenstrom zurückgegeben werden, legen Sie das RPC RETURN_METADATA-Eingabeflag auf 1 fest.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>A. Ändern einer Cursorposition mithilfe von PREV  
 Angenommen, der Cursor h2 würde ein Resultset erzeugen, das über den folgenden Inhalt mit der angegebenen aktuellen Position verfügt:  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 Als Nächstes ein Sp_cursorfetch PREV mit dem ein *Nrows* -Wert 5 würde logisch zwei CursorZeilen vor der ersten Zeile des Resultsets positionieren. In diesen Fällen wird der Cursor so eingerichtet, dass er an der ersten Zeile beginnt und die angeforderte Zeilenanzahl zurückgibt. Häufig bedeutet dies, dass er Zeilen aus dem PRIOR-Fetchpuffer zurückgibt.  
  
> [!NOTE]  
>  Genau in diesem Fall wird der RPC-Statusparameter auf 2 festgelegt.  
  
### <a name="b-using-prevnoadjust-to-return-fewer-rows-than-prev"></a>B. Zurückgeben von weniger Zeilen als PREV mithilfe von PREV_NOADJUST  
 PREV_NOADJUST schließt nie Zeilen ein, die sich an oder nach der aktuellen Cursorposition im Block zurückgegebener Zeilen befinden. In Fällen, in denen PREV Zeilen nach der aktuellen Position zurückgibt, gibt PREV_NOADJUST weniger Zeilen als angefordert in *Nrows*. Bei der aktuellen position in Beispiel A oben, wenn Prev angegeben ist, Sp_cursorfetch (h2, 4, 1, 5) die folgenden Zeilen:  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 Wenn jedoch PREV_NOADJUST angewendet wird, Sp_cursorfetch (h2, 512, 6, 5) nur die folgenden Zeilen:  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
