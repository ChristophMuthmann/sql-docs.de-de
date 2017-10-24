---
title: TEXTVALID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs:
- TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 279022316af7e3a396c7089f48933281264f900f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>Text- und Bildfunktionen - TEXTVALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ein **Text**, **Ntext**, oder **Image** -Funktion, die überprüft, ob der angegebene Textzeiger gültig ist.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Es steht keine alternative Funktionalität zur Verfügung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TEXTVALID ( 'table.column' ,text_ ptr )  
```  
  
## <a name="arguments"></a>Argumente  
 *table*  
 Der Name der zu verwendenden Tabelle  
  
 *Spalte*  
 Der Name der zu verwendenden Spalte  
  
 *text_ptr*  
 Der zu prüfende Textzeiger  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 Gibt 1 zurück, wenn der Zeiger gültig ist, oder 0, wenn er ungültig ist. Beachten Sie, dass der Bezeichner für die **Text** Spalte den Tabellennamen enthalten muss. Sie können UPDATETEXT, WRITETEXT oder READTEXT nicht ohne einen gültigen Textzeiger verwenden.  
  
 Die folgenden Funktionen und Anweisungen sind auch nützlich, bei der Arbeit mit **Text**, **Ntext**, und **Image** Daten.  
  
|Funktion oder Anweisung|Description|  
|---------------------------|-----------------|  
|PATINDEX**(**"*" % Muster "**"***,** *Ausdruck***)**|Gibt die Zeichenposition einer angegebenen Zeichenfolge in **Text** und **Ntext** Spalten.|  
|DATALENGTH**(***Ausdruck***)**|Gibt die Länge der Daten in **Text**, **Ntext**, und **Image** Spalten.|  
|SET TEXTSIZE|Gibt den Grenzwert, in Bytes, der die **Text**, **Ntext**, oder **Image** Daten, die mit einer SELECT-Anweisung zurückgegeben werden.|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird gemeldet, ob für jeden Wert in der `logo`-Spalte der `pub_info`-Tabelle ein gültiger Textzeiger vorhanden ist.  
  
> [!NOTE]  
>  Um dieses Beispiel auszuführen, müssen Sie installieren die **Pubs** Datenbank.  
  
```  
USE pubs;  
GO  
SELECT pub_id, 'Valid (if 1) Text data'   
   = TEXTVALID ('pub_info.logo', TEXTPTR(logo))   
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id Valid (if 1) Text data   
------ ----------------------   
0736   1                        
0877   1                        
1389   1                        
1622   1                        
1756   1                        
9901   1                        
9952   1                        
9999   1                        
  
(8 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DATALENGTH &#40; Transact-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [SET TEXTSIZE &#40; Transact-SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Text und Image-Funktionen &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40; Transact-SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  

