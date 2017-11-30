---
title: Sp_cursoropen (Transact-SQL) | Microsoft Docs
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
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec112810e691aceac5085f3ded941564331f74b9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spcursoropen-transact-sql"></a>sp_cursoropen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Öffnet einen Cursor. Sp_cursoropen definiert die SQL-Anweisung, die dem Cursor und den Cursoroptionen zugeordnet, und klicken Sie dann den Cursor füllt. Sp_cursoropenis entspricht der Kombination der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen DECLARE_CURSOR und OPEN. Diese Prozedur wird aufgerufen, indem ID = 2 in einem Tabular Data Stream-Paket (TDS) angegeben wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>Argumente  
 *Cursor*  
 Ein von SQL Server generierter Cursorbezeichner. *Cursor* ist ein *behandeln* Wert, der für alle nachfolgenden Prozeduren, die den Cursor einschließen, z. B. Sp_cursorfetch angegeben werden muss. *Cursor* ist ein erforderlicher Parameter mit einem **Int** Rückgabewert.  
  
 *Cursor* können mehrere Cursor auf eine einzelne datenbankverbindung aktiv sein.  
  
 *stmt*  
 Ein erforderlicher Parameter, der das Cursorresultset definiert. Kann eine beliebige gültige Abfragezeichenfolge (Syntax und Bindung) eines beliebigen Zeichenfolgentyps (unabhängig von Unicode, Größe usw.) als gültige dienen *Stmt* Werttyp.  
  
 *scrollopt*  
 Option für den Bildlauf. *Scrollopt* ist ein optionaler Parameter, der einen der folgenden erfordert **Int** Eingabewerte.  
  
|Wert|Description|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 Aufgrund der Möglichkeit, der der angeforderte Wert nicht für den durch definierten Cursor geeignet ist *Stmt*, dieser Parameter dient als Eingabe und Ausgabe. In solchen Fällen weist SQL Server einen passenden Wert zu.  
  
 *ccopt*  
 Option für die Parallelitätssteuerung. *Ccopt* ist ein optionaler Parameter, der einen der folgenden erfordert **Int** Eingabewerte.  
  
|Wert|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (vormals bekannt als LOCKCC)|  
|0x0004|**OPTIMISTISCHE** (vormals bekannt als OPTCC)|  
|0x0008|OPTIMISTIC (vormals bekannt als OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Wie bei *Scrollopt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können überschreiben, die angeforderte *Ccopt* Werte.  
  
 *Zeilenanzahl*  
 Die Anzahl der mit AUTO_FETCH zu verwendenden Fetchpufferzeilen. Der Standardwert ist 20 Zeilen. *Überprüfung der Zeilenanzahl* verhält sich anders, wenn als Eingabewert oder Rückgabewert zugewiesen.  
  
|Als Eingabewert|Als Rückgabewert|  
|--------------------|---------------------|  
|Wenn die AUTO_FETCH *Scrollopt* -Wert angegeben *Rowcount* stellt die Anzahl der Zeilen im Fetchpuffer platziert.<br /><br /> Hinweis: > 0 ist ein gültiger Wert aus, wenn AUTO_FETCH angegeben ist, wird jedoch andernfalls ignoriert.|Stellt die Anzahl der Zeilen im Resultset festgelegt, außer wenn die *Scrollopt* -Wert AUTO_FETCH angegeben.|  
  
-  
  
 *boundparam*  
 Gibt die Verwendung zusätzlicher Parameter an. *Boundparam* ist ein optionaler Parameter, der Wenn angegeben werden, sollte die *Scrollopt* -Wert PARAMETERIZED_STMT auf ON festgelegt ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Wenn kein Fehler ausgelöst wird, gibt sp_cursoropen einen der folgenden Werte zurück.  
  
 0  
 Die Prozedur erfolgreich ausgeführt wurde.  
  
 0x0001  
 Fehler während der Ausführung (geringfügiger Fehler, nicht schwerwiegend genug, um einen Fehler im Betriebsablauf auszulösen).  
  
 0x0002  
 Ein asynchroner Vorgang wird ausgeführt.  
  
 0x0002  
 Ein FETCH-Vorgang wird ausgeführt.  
  
 Ein  
 Die Zuordnung dieses Cursors wurde von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgehoben, und er ist nicht verfügbar.  
  
 Wenn ein Fehler ausgelöst wird, sind die Rückgabewerte möglicherweise inkonsistent, und die Genauigkeit kann nicht gewährleistet werden.  
  
 Wenn die *Rowcount* als Rückgabewert, Parameter angegeben wird, tritt das folgende Resultset.  
  
 -1  
 Wird zurückgegeben, wenn die Anzahl der Zeilen unbekannt oder nicht anwendbar ist.  
  
 -n  
 Wird zurückgegeben, wenn eine asynchrone Auffüllung aktiviert ist. Gibt die Anzahl von Zeilen, die FETCH im Fetchpuffer platziert wurden beim Puffern der *Scrollopt* -Wert AUTO_FETCH angegeben.  
  
 Wenn RPC verwendet wird, lauten die Rückgabewerte wie folgt.  
  
 0  
 Die Prozedur ist erfolgreich.  
  
 1  
 Fehler bei der Prozedur.  
  
 2  
 Ein KEYSET-Cursor wird asynchron generiert.  
  
 16  
 Ein FAST_FORWARD-Cursor wurde automatisch geschlossen.  
  
> [!NOTE]  
>  Wenn die Prozedur sp_cursoropen erfolgreich ausgeführt wird, werden die RPC-Rückgabeparameter und ein Resultset mit TDS-Spaltenformatinformationen (Meldungen 0xa0 und 0xa1) gesendet. Andernfalls wird mindestens eine TDS-Fehlermeldung gesendet. In beiden Fällen keine Zeilendaten zurückgegeben werden, und die *Fertig* Nachrichtenanzahl wird 0 (null) sein. Wenn Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version vor 7.0 verwenden, werden 0xa0 und 0xa1 (Standard für SELECT-Anweisungen) zusammen mit den Tokendatenströmen 0xa5 und 0xa4 zurückgegeben. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 verwenden, wird 0x81 (Standard für SELECT-Anweisungen) zusammen mit den Tokendatenströmen 0xa5 und 0xa4 zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="stmt-parameter"></a>stmt-Parameter  
 Wenn *Stmt* gibt an, die Ausführung einer gespeicherten Prozedur können die Eingabeparameter entweder als Konstanten als Teil des definiert werden die *Stmt* Zeichenfolge oder als angegeben *Boundparam* Argumente. Deklarierte Variablen können auf diese Weise als gebundene Parameter übergeben werden.  
  
 Die zulässigen Inhalt der *Stmt* Parameter hängen davon ab, ob die *Ccopt* ALLOW_DIRECT-Rückgabewert durch OR mit den restlichen Wert verknüpft wurde die *Ccopt* Werte, d. h.:  
  
-   Wenn ALLOW_DIRECT nicht, entweder angegeben wird eine [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT oder EXECUTE Anweisung Aufrufen eine gespeicherte Prozedur mit einer einzelnen SELECT-Anweisung verwendet werden muss. Darüber hinaus muss die SELECT-Anweisung als Cursor qualifizieren; Es darf keine, also die Schlüsselwörter SELECT INTO oder FOR BROWSE enthalten.  
  
-   Wenn ALLOW_DIRECT angegeben wird, kann dies zu mindestens einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung führen, einschließlich der Anweisungen, die ihrerseits andere gespeicherte Prozeduren mit mehreren Anweisungen ausführen. Nicht-SELECT-Anweisungen oder beliebige SELECT-Anweisungen, die die Schlüsselwörter SELECT INTO oder FOR BROWSE enthalten, werden einfach ausgeführt und führen nicht zur Erstellung eines Cursors. Dies trifft auch auf jede SELECT-Anweisung zu, die in einem aus mehreren Anweisungen bestehenden Batch enthalten ist. Wenn eine SELECT-Anweisung Klauseln enthält, die nur Cursor betreffen, werden diese Klauseln ignoriert. Für die Instanz, wenn der Wert der *Ccopt* ist 0 x 2002, dies ist eine Anforderung:  
  
    -   Ein Cursor mit Bildlaufsperren, wenn es nur eine einzelne SELECT-Anweisung gibt, die sich als Cursor qualifiziert, oder  
  
    -   Eine direkte Anweisungsausführung, wenn mehrere Anweisungen, eine einzelne Nicht-SELECT-Anweisung oder eine SELECT-Anweisung, die sich nicht als Cursor qualifiziert, vorhanden sind.  
  
## <a name="scrollopt-parameter"></a>scrollopt-Parameter  
 Die ersten fünf *Scrollopt* Werte (Keyset, DYNAMIC, FORWARD_ONLY, STATIC und FAST_FORWARD) schließen sich gegenseitig.  
  
 PARAMETERIZED_STMT und CHECK_ACCEPTED_TYPES können durch OR mit einem der ersten fünf Werte verknüpft werden.  
  
 AUTO_FETCH und AUTO_CLOSE können durch OR mit FAST_FORWARD verknüpft werden.  
  
 Wenn CHECK_ACCEPTED_TYPES ON, mindestens die letzten fünf *Scrollopt* Werte (KEYSET_ACCEPTABLE`,` DYNAMIC_ACCEPTABLE, FORWARD_ONLY_ACCEPTABLE, STATIC_ACCEPTABLE oder FAST_FORWARD_ACCEPTABLE) auch ON sein.  
  
 STATIC-Cursor werden immer als READ_ONLY geöffnet. Dies bedeutet, dass die zugrunde liegende Tabelle über diesen Cursor nicht aktualisiert werden kann.  
  
## <a name="ccopt-parameter"></a>ccopt-Parameter  
 Die ersten vier *Ccopt* Werte (READ_ONLY, SCROLL_LOCKS und beide OPTIMISTIC-Werte) schließen sich gegenseitig.  
  
> [!NOTE]  
>  Auswahl einer der ersten vier *Ccopt* -Werte wird bestimmt, ob der Cursor schreibgeschützt ist oder wenn lock- oder optimistische-Methoden verwendet werden, um verlorene Updates zu verhindern. Wenn eine *Ccopt* kein Wert angegeben wird, der Standardwert OPTIMISTIC.  
  
 ALLOW_DIRECT und CHECK_ACCEPTED_TYPES können durch OR mit einem der ersten vier Werte verknüpft werden.  
  
 UPDT_IN_PLACE kann durch OR mit READ_ONLY, SCROLL_LOCKS oder einem der OPTIMISTIC-Werte verknüpft werden.  
  
 Wenn CHECK_ACCEPTED_TYPES ON, mindestens die letzten vier *Ccopt* Werte (READ_ONLY_ACCEPTABLE, SCROLL_LOCKS_ACCEPTABLE und einer der OPTIMISTIC_ACCEPTABLE-Werte) auch ON sein.  
  
 Positionierte Update- und DELETE-Funktionen können ausgeführt werden, nur innerhalb des fetchpuffers und nur, wenn die *Ccopt* Wert SCROLL_LOCKS oder OPTIMISTIC entspricht. Wenn SCROLL_LOCKS als Wert angegeben wird, verläuft der Vorgang mit Sicherheit erfolgreich. Wenn OPTIMISTIC als Wert angegeben wird, ist der Vorgang fehlerhaft, wenn die Zeile seit dem letzten Abruf geändert wurde.  
  
 Die Fehlerursache liegt darin, dass bei Angabe des Werts OPTIMISTIC eine Funktion für die Steuerung durch vollständige Parallelität ausgeführt wird, indem entsprechend der Vorgabe in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Zeitstempel oder Prüfsummenwerte verglichen werden. Wenn beliebige dieser Zeilen nicht übereinstimmen, ist der Vorgang fehlerhaft.  
  
 Wenn UPDT_IN_PLACE als Rückgabewert angegeben wird, sind die Ergebnisse wie folgt:  
  
-   Wenn der Parameter beim Ausführen eines positionierten Updates für eine Tabelle mit einem eindeutigen Index nicht festgelegt ist, löscht der Cursor die Zeile aus seiner Arbeitstabelle und fügt sie am Ende einer beliebigen vom Cursor verwendeten Schlüsselspalte ein. Dabei werden die Spalten geändert.  
  
-   Wenn der Parameter auf ON festgelegt ist, aktualisiert der Cursor einfach die Schlüsselspalten in der ursprünglichen Zeile der Arbeitstabelle.  
  
## <a name="boundparam-parameter"></a>bound_param-Parameter  
 Der Name des Parameters muss *Paramdef* Wenn PARAMETERIZED_STMT angegeben ist, entsprechend der Fehlermeldung im Code. Wenn PARAMETERIZED_STMT nicht angegeben ist, wird kein Name in der Fehlermeldung angegeben.  
  
## <a name="rpc-considerations"></a>Überlegungen zu RPC  
 Das RPC-RETURN_METADATA-Eingabeflag kann auf 0x0001 festgelegt werden. Dadurch wird angefordert, dass Metadaten zur SELECT-Liste des Cursors im TDS-Datenstrom zurückgegeben werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="boundparam-parameter"></a>bound_param-Parameter  
 Alle nach dem fünften Parameter übergebenen Parameter werden als Eingabeparameter an den Anweisungsplan übergeben. Der erste derartige Parameter muss eine Zeichenfolge im folgenden Format sein:  
  
 *{Fehler bei Datentyp-Name der lokalen Variablen} [,... n] '.*  
  
 Nachfolgende Parameter werden verwendet, um die Übergabe der Werte, die für ersetzen sollen die *lokalen Variablennamen* in der Anweisung.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_cursorfetch &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
