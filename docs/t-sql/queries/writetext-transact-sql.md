---
title: WRITETEXT-Anweisung (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WRITETEXT_TSQL
- WRITETEXT
dev_langs: TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
caps.latest.revision: "52"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fda340750c555d7e6e858ddac1a87401e215891e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ermöglicht die minimal protokollierte, interaktive Aktualisierung einer vorhandenen **Text**, **Ntext**, oder **Image** Spalte. WRITETEXT überschreibt alle vorhandenen Daten in der betreffenden Spalte. WRITETEXT kann nicht verwendet werden, auf **Text**, **Ntext**, und **Image** Spalten in den Ansichten.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwenden Sie die Datentypen mit umfangreichen Werten und die **.** WRITE-Klausel aus, der die [UPDATE](../../t-sql/queries/update-transact-sql.md) Anweisung stattdessen.  
  
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
 Der Name der Tabelle und **Text**, **Ntext**, oder **Image** zu aktualisierenden Spalte. Tabellen- und Spaltennamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Das Angeben des Datenbank- und des Besitzernamens ist optional.  
  
 *text_ptr*  
 Ist ein Wert, der den Zeiger zu speichert die **Text**, **Ntext**, oder **Image** Daten. *Text_ptr* muss **binary(16)**. Führen Sie zum Erstellen eines Textzeigers eine [einfügen](../../t-sql/statements/insert-transact-sql.md) oder [UPDATE](../../t-sql/queries/update-transact-sql.md) -Anweisung mit Daten ungleich null für den **Text**, **Ntext**, oder **Image** Spalte.  
  
 WITH LOG  
 Wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignoriert. Die Protokollierung wird durch das für die Datenbank wirksame Wiederherstellungsmodell bestimmt.  
  
 *data*  
 Der tatsächliche **Text**, **Ntext** oder **Image** zum Speichern von Daten. *Daten* kann ein Literal oder ein Parameter sein. Die maximale Länge des Texts, die interaktiv mit WRITETEXT eingefügt werden kann, ist etwa 120 KB **Text**, **Ntext**, und **Image** Daten.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie WRITETEXT, um ersetzen **Text**, **Ntext**, und **Image** Daten und so ändern Sie UPDATETEXT **Text**, **Ntext**, und **Image** Daten. UPDATETEXT ist flexibler, da sie nur einen Teil des ändert ein **Text**, **Ntext**, oder **Image** Spalte nicht die gesamte Spalte.  
  
 Für eine optimale Leistung empfehlen wir **Text**, **Ntext**, und **Image** Daten eingefügt oder aktualisiert in Blockgrößen, die ein Vielfaches von 8.040 Byte sind.  
  
 Wenn das Wiederherstellungsmodell einfach oder Massenprotokolliert ist **Text**, **Ntext**, und **Image** Vorgänge, die WRITETEXT-Anweisung zu verwenden sind minimal protokollierte Vorgänge aus, wenn neue Daten eingefügt oder angefügt.  
  
> [!NOTE]  
>  Die minimale Protokollierung wird nicht verwendet, wenn vorhandene Werte aktualisiert werden.  
  
 Die Spalte muss bereits einen gültigen Textzeiger enthalten, damit WRITETEXT ordnungsgemäß ausgeführt wird.  
  
 Verfügt die Tabelle nicht Text in Zeilen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird Speicherplatz gespart, indem Sie nicht initialisieren **Text** Spalten, wenn explizite oder implizite null-Werte in hinzugefügt werden **Text** Spalten mit einfügen und keine Textzeiger werden können für diese NULL-Werte abgerufen. Initialisieren **Text** -Spalten mit NULL, verwenden Sie die UPDATE-Anweisung. Wenn die Tabelle über Text in Zeilen verfügt, muss die text-Spalte nicht für NULL-Werte initialisiert werden, und Sie können immer einen Textzeiger erhalten.  
  
 Der ODBC-Funktion SQLPutData ist schneller und verwendet weniger dynamischen Arbeitsspeicher als WRITETEXT. Diese Funktion kann bis zu 2 GB an einfügen **Text**, **Ntext**, oder **Image** Daten.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in Zeile Textzeiger auf **Text**, **Ntext**, oder **Image** Daten vorhanden, die jedoch möglicherweise nicht mehr gültig. Informationen zu dem Text in Row-Option finden Sie unter [Sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Weitere Informationen zu den Textzeiger, finden Sie unter [Sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40; Transact-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
