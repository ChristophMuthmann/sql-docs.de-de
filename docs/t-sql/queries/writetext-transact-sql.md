---
title: WRITETEXT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- WRITETEXT_TSQL
- WRITETEXT
dev_langs:
- TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f2a5eb2808bf0f438adbe606f2d59e39b4ec3c55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ermöglicht das minimal protokollierte, interaktive Aktualisieren einer vorhandenen Spalte vom Typ **text**, **ntext** oder **image**. WRITETEXT überschreibt alle vorhandenen Daten in der betreffenden Spalte. WRITETEXT kann nicht für Spalten vom Datentyp **text**, **ntext** und **image** und in Sichten verwendet werden.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen die Datentypen für große Werte und die **.** WRITE-Klausel der [UPDATE](../../t-sql/queries/update-transact-sql.md)-Anweisung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WRITETEXT [BULK]  
  { table.column text_ptr }  
  [ WITH LOG ] { data }  
```  
  
## <a name="arguments"></a>Argumente  
 BULK  
 Aktiviert Uploadtools, um einen Binärdaten-Datenstrom hochzuladen. Der Datenstrom muss vom Tool auf TDS-Protokollebene bereitgestellt werden. Wenn der Datenstrom nicht vorhanden ist, ignoriert der Abfrageprozessor die BULK-Option.  
  
> [!IMPORTANT]  
>  Es wird empfohlen, die BULK-Option nicht in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-basierten Anwendungen zu verwenden. Diese Option kann in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geändert oder entfernt werden.  
  
 *table* **.column**  
 Der Name der zu aktualisierenden Tabelle oder der zu aktualisierenden Spalte vom Datentyp **text**, **ntext** oder **image**. Tabellen- und Spaltennamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Das Angeben des Datenbank- und des Besitzernamens ist optional.  
  
 *text_ptr*  
 Ein Wert, in dem der Zeiger auf die Daten vom Typ **text**, **ntext** oder **image** gespeichert wird. *text_ptr* muss vom Datentyp **binary(16)** sein. Führen Sie zum Erstellen eines Textzeigers eine [INSERT](../../t-sql/statements/insert-transact-sql.md)- oder eine [UPDATE](../../t-sql/queries/update-transact-sql.md)-Anweisung für die Spalte **text**, **ntext** oder **image** mit Daten aus, die nicht NULL ist.  
  
 WITH LOG  
 Wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignoriert. Die Protokollierung wird durch das für die Datenbank wirksame Wiederherstellungsmodell bestimmt.  
  
 *data*  
 Die tatsächlichen Daten vom Typ **text**, **ntext** oder **image**, die gespeichert werden sollen. *data* kann ein Literal oder ein Parameter sein. Die maximale Textlänge, die interaktiv mit WRITETEXT eingefügt werden kann, entspricht für Daten vom Typ **text**, **ntext** und **image** ungefähr 120 KB.  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie WRITETEXT zum Ändern von Daten vom Typ **text**, **ntext** und **image** und UPDATETEXT zum Ändern von Daten vom Typ **text**, **ntext** und **image**. UPDATETEXT ist flexibler, weil damit nicht die gesamte Spalte, sondern nur ein Teil einer **text**-, **ntext**- oder **image**-Spalte geändert wird.  
  
 Für eine optimale Leistung empfiehlt es sich, Daten vom Typ **text**, **ntext** und **image** in Segmenten mit der Größe eines Vielfachen von 8040 Bytes einzufügen oder zu aktualisieren.  
  
 Wenn Sie das einfache oder massenprotokollierte Wiederherstellungsmodell verwenden, sind Vorgänge vom Typ **text**, **ntext** und **image**, die WRITETEXT verwenden, minimal protokollierte Vorgänge, wenn neue Daten eingefügt oder angefügt werden.  
  
> [!NOTE]  
>  Die minimale Protokollierung wird nicht verwendet, wenn vorhandene Werte aktualisiert werden.  
  
 Die Spalte muss bereits einen gültigen Textzeiger enthalten, damit WRITETEXT ordnungsgemäß ausgeführt wird.  
  
 Wenn die Tabelle keinen Text in Zeilen enthält, spart [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Speicherplatz, indem Spalten vom Datentyp **text** nicht initialisiert werden, wenn in Spalten vom Datentyp **text** explizite oder implizite NULL-Werte mit INSERT hinzugefügt werden. Für diese NULL-Werte kann kein Textzeiger erhalten werden. Verwenden Sie die UPDATE-Anweisung, um Spalten vom Datentyp **text** für NULL-Werte zu initialisieren. Wenn die Tabelle über Text in Zeilen verfügt, muss die text-Spalte nicht für NULL-Werte initialisiert werden, und Sie können immer einen Textzeiger erhalten.  
  
 Die ODBC-Funktion SQLPutData ist schneller und verwendet weniger dynamischen Arbeitsspeicher als WRITETEXT. Diese Funktion kann bis zu 2 GB an Daten vom Typ **text**, **ntext** oder **image** einfügen.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Textzeiger auf **text**-, **ntext**- oder **image**-Daten in Zeilen zwar vorhanden sein, sie sind aber möglicherweise ungültig. Informationen zur Option „text in row“ finden Sie unter [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Informationen dazu, wie Textzeiger ungültig gemacht werden können, finden Sie unter [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die UPDATE-Berechtigung für die angegebene Tabelle. Die Berechtigung ist übertragbar, wenn die UPDATE-Berechtigung übertragen wird.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Textzeiger in die lokale Variable `@ptrval` eingefügt. Anschließend wird die neue Textzeichenfolge von `WRITETEXT` in die Zeile eingefügt, auf die `@ptrval` zeigt.  
  
> [!NOTE]  
>  Um dieses Beispiel auszuführen, müssen Sie die pubs-Beispieldatenbank installieren.  
  
```  
USE pubs;  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
DECLARE @ptrval binary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books'  
WRITETEXT pub_info.pr_info @ptrval 'New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!';  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DEKLARIEREN SIE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
