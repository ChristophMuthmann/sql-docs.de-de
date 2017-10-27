---
title: UPDATETEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATETEXT
- UPDATETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text updates [SQL Server]
- updating data [SQL Server]
- data updates [SQL Server], UPDATETEXT statement
- UPDATETEXT statement
ms.assetid: d73c28ee-3972-4afd-af8d-ebbbd9e50793
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49bd324f97f6ba1d2e8a8120bb502199b4ca0f06
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="updatetext-transact-sql"></a>UPDATETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Aktualisiert ein vorhandenes **Text**, **Ntext**, oder **Image** Feld. Verwenden Sie UPDATETEXT so ändern Sie nur einen Teil einer **Text**, **Ntext**, oder **Image** Spalte vorhanden. Verwenden Sie WRITETEXT zum Aktualisieren und ersetzen die gesamte **Text**, **Ntext**, oder **Image** Feld.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwenden Sie die Datentypen mit umfangreichen Werten und die **.** WRITE-Klausel aus, der die [UPDATE](../../t-sql/queries/update-transact-sql.md) Anweisung stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
UPDATETEXT [BULK] { table_name.dest_column_name dest_text_ptr }  
  { NULL | insert_offset }  
     { NULL | delete_length }  
     [ WITH LOG ]  
     [ inserted_data  
    | { table_name.src_column_name src_text_ptr } ]  
```  
  
## <a name="arguments"></a>Argumente  
 BULK  
 Aktiviert Uploadtools, um einen Binärdaten-Datenstrom hochzuladen. Der Datenstrom muss vom Tool auf TDS-Protokollebene bereitgestellt werden. Wenn der Datenstrom nicht vorhanden ist, ignoriert der Abfrageprozessor die BULK-Option.  
  
> [!IMPORTANT]  
>  Es wird empfohlen, die BULK-Option nicht in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-basierten Anwendungen zu verwenden. Diese Option kann in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geändert oder entfernt werden.  
  
 *TABLE_NAME* **.** *dest_column_name*  
 Der Name der Tabelle und **Text**, **Ntext**, oder **Image** Spalte aktualisiert werden. Tabellen- und Spaltennamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Das Angeben des Datenbank- und des Besitzernamens ist optional.  
  
 *dest_text_ptr*  
 Ein Textzeiger Wert (zurückgegeben von der TEXTPTR-Funktion), die auf zeigt die **Text**, **Ntext**, oder **Image** Daten aktualisiert werden. *Dest_text_ptr* muss **binäre (**16**)**.  
  
 *insert_offset*  
 Die nullbasierte Startposition für das Update. Für **Text** oder **Image** Spalten *Insert_offset* ist die Anzahl der Bytes vom Beginn der vorhandenen Spalte zu überspringen, bevor neue Daten eingefügt werden. Für **Ntext** Spalten *Insert_offset*ist die Anzahl der Zeichen (jeder **Ntext** -Zeichen verwendet 2 Bytes). Die vorhandene **Text**, **Ntext**, oder **Image** Daten beginnend bei dieser nullbasierten Startposition verschoben wird, nach rechts, um Platz für die neuen Daten zu machen. Mit dem Wert 0 werden die neuen Daten am Beginn der vorhandenen Daten eingefügt. Mit dem Wert NULL werden die neuen Daten an den vorhandenen Datenwert angefügt.  
  
 *delete_length*  
 Die Länge der Daten aus der vorhandenen gelöscht **Text**, **Ntext**, oder **Image** Spalte ausgehend von der *Insert_offset* Position. Die *Delete_length*Wert wird angegeben, in Byte für **Text** und **Image** Spalten und in Zeichen für **Ntext** Spalten. Jede **Ntext** -Zeichen belegt 2 Byte. Mit dem Wert 0 werden keine Daten gelöscht. Ein Wert von NULL löscht alle Daten aus der *Insert_offset* Position bis zum Ende des vorhandenen **Text** oder **Image** Spalte.  
  
 WITH LOG  
 Die Protokollierung wird durch das für die Datenbank wirksame Wiederherstellungsmodell bestimmt.  
  
 *inserted_data*  
 Sind die Daten in den vorhandenen einzufügenden **Text**, **Ntext**, oder **Image** Spalte bei der *Insert_offset* Speicherort. Dies ist eine einzelne **Char**, **Nchar**, **Varchar**, **Nvarchar**, **binäre**,  **Varbinary**, **Text**, **Ntext**, oder **Image** Wert. *Inserted_data* kann ein Literal oder eine Variable sein.  
  
 *TABLE_NAME.src_column_name*  
 Der Name der Tabelle und **Text**, **Ntext**, oder **Image** Spalte, die als Quelle der eingefügten Daten verwendet. Tabellen- und Spaltennamen müssen den Regeln für Bezeichner entsprechen.  
  
 *src_text_ptr*  
 Ein Textzeiger Wert (zurückgegeben von der TEXTPTR-Funktion), die auf zeigt eine **Text**, **Ntext**, oder **Image** Spalte, die als Quelle der eingefügten Daten verwendet.  
  
> [!NOTE]  
>  *Scr_text_ptr* Wert darf nicht identisch sein *Dest_text_ptr*Wert.  
  
## <a name="remarks"></a>Hinweise  
 Neu eingefügte Daten können es sich um eine einzelne *Inserted_data* -Konstante, Tabellennamen, Spaltennamen oder Textzeiger.  
  
|Updateaktion|UPDATETEXT-Parameter|  
|-------------------|---------------------------|  
|Ersetzen vorhandener Daten|Geben Sie einen nicht-NULL *Insert_offset* -Wert, einen Wert ungleich NULL *Delete_length* Wert und die neuen Daten eingefügt werden.|  
|Löschen vorhandener Daten|Geben Sie einen nicht-NULL *Insert_offset* Wert und einen Wert ungleich NULL *Delete_length*. Geben Sie keine neuen einzufügenden Daten an.|  
|Einfügen neuer Dateien|Geben Sie die *Insert_offset* Wert, eine *Delete_length* 0 und die neuen Daten eingefügt werden.|  
  
 Für eine optimale Leistung empfehlen wir **Text**, **Ntext** und **Image** Daten eingefügt oder aktualisiert werden, in Blöcke Größen, die ein Vielfaches von 8.040 Byte sind.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um Textzeiger in Zeilen **Text**, **Ntext**, oder **Image** Daten vorhanden, die jedoch möglicherweise nicht mehr gültig. Informationen zu dem Text in Row-Option finden Sie unter [Sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Weitere Informationen zu den Textzeiger, finden Sie unter [Sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 Initialisieren **Text** -Spalten mit NULL, verwenden Sie WRITETEXT, Initialisiert UPDATETEXT **Text** Spalten auf eine leere Zeichenfolge.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die UPDATE-Berechtigung für die angegebene Tabelle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Textzeiger in die lokale Variable `@ptrval` eingefügt. Anschließend wird mit `UPDATETEXT` ein Rechtschreibfehler aktualisiert.  
  
> [!NOTE]  
>  Um dieses Beispiel auszuführen, müssen Sie die pubs-Datenbank installieren.  
  
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
UPDATETEXT pub_info.pr_info @ptrval 88 1 'b';  
GO  
ALTER DATABASE pubs SET RECOVERY FULL;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [READTEXT &#40; Transact-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40; Transact-SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)  
  
  

