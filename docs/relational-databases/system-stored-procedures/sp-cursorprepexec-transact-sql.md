---
title: Sp_cursorprepexec (Transact-SQL) | Microsoft Docs
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
- sp_cursorprepexec_TSQL
- sp_cursorprepexec
dev_langs: TSQL
helpviewer_keywords: sp_cursorprepexec
ms.assetid: 8094fa90-35b5-4cf4-8012-0570cb2ba1e6
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5264e1c645cf1716d01e352f2b248b3b80a038d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spcursorprepexec-transact-sql"></a>sp_cursorprepexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Kompiliert einen Plan für die gesendete Cursoranweisung oder den gesendeten Batch, erstellt dann den Cursor und füllt ihn auf. Sp_cursorprepexec vereint die Funktionen von Sp_cursorprepare und Sp_cursorexecute. Diese Prozeduren werden aufgerufen, indem ID =5 in einem Tabular Data Stream-Paket (TDS) angegeben wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
```  
  
## <a name="arguments"></a>Argumente  
 *vorbereitete handle*  
 Ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert vorbereitet *behandeln* Bezeichner. *vorbereitete Handle* ist erforderlich und gibt **Int**.  
  
 *Cursor*  
 Der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generierte Cursorbezeichner. *Cursor* ist ein erforderlicher Parameter, die für alle nachfolgenden Prozeduren angegeben werden muss, die sich auf diesen Cursor auswirken, z. B. Sp_cursorfetch.  
  
 *params*  
 Identifiziert parametrisierte Anweisungen. Die *params* -Definition der Variablen wird in der Anweisung an die Stelle der Parametermarkierungen gesetzt. *params* ist ein erforderlicher Parameter, der einen Eingabewert vom Typ **ntext**, **nchar**,oder **nvarchar** erfordert.  
  
> [!NOTE]  
>  Verwenden einer **Ntext** -Zeichenfolge als Eingabewert Wert *Stmt* parametrisiert und der *Scrollopt* PARAMETERIZED_STMT-Wert ist auf.  
  
 *statement*  
 Definiert das Resultset des Cursors. Die *Anweisung* -Parameter ist erforderlich und erfordert eine **Ntext**, **Nchar** oder **Nvarchar** Eingabewert.  
  
> [!NOTE]  
>  Die Regeln zum Angeben des Stmt-Werts entsprechen denen für Sp_cursoropen, mit der Ausnahme, die die *Stmt* String-Datentyp muss **Ntext**.  
  
 *Optionen*  
 Ein optionaler Parameter, der eine Beschreibung der Spalten im Cursorresultset zurückgibt. *Optionen* erfordert die folgenden **Int** Eingabewert.  
  
|Wert|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Scroll (Option). *Scrollopt* ist ein optionaler Parameter, der einen der folgenden erfordert **Int** Eingabewerte.  
  
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
  
 Aufgrund der Möglichkeit, die die angeforderte Option nicht für den durch definierten Cursor geeignet ist  *\<Stmt >*, dieser Parameter dient als Eingabe und Ausgabe. In solchen Fällen weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen entsprechenden Typ zu und ändert diesen Wert.  
  
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
  
 Wie bei *Scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können einen anderen Wert als die angeforderte zuweisen.  
  
 *Zeilenanzahl*  
 Ein optionaler Parameter, der die Anzahl der mit AUTO_FETCH zu verwendenden Fetchpufferzeilen angibt. Der Standardwert ist 20 Zeilen. *Überprüfung der Zeilenanzahl* verhält sich anders, wenn als Eingabewert oder Rückgabewert zugewiesen.  
  
|Als Eingabewert|Als Rückgabewert|  
|--------------------|---------------------|  
|Wenn AUTO_FETCH mit FAST_FORWARD-Cursorn angegeben *Rowcount* stellt die Anzahl der Zeilen im Fetchpuffer platziert.|Stellt die Anzahl der Zeilen im Resultset dar. Wenn die *Scrollopt* -Wert AUTO_FETCH angegeben wird, *Rowcount* gibt die Anzahl der Zeilen im Fetchpuffer abgerufen wurden.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Wenn *Params* gibt einen Nullwert zurück, und klicken Sie dann die Anweisung nicht parametrisiert ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_cursoropen &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Sp_cursorexecute &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [Sp_cursorprepare &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [Sp_cursorfetch &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
