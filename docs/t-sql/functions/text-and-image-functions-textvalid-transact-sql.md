---
title: TEXTVALID (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d64916b441c65dc00e0e387e08c2967124721514
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>Text- und Bildfunktionen: TEXTVALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Eine **text**-, **ntext**- oder **image**-Funktion, die prüft, ob der angegebene Textzeiger gültig ist.  
  
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
  
 *column*  
 Der Name der zu verwendenden Spalte  
  
 *text_ptr*  
 Der zu prüfende Textzeiger  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Remarks  
 Gibt 1 zurück, wenn der Zeiger gültig ist, oder 0, wenn er ungültig ist. Beachten Sie, dass der Bezeichner für die **text**-Spalte auch den Tabellennamen enthalten muss. Sie können UPDATETEXT, WRITETEXT oder READTEXT nicht ohne einen gültigen Textzeiger verwenden.  
  
 Die folgenden Funktionen und Anweisungen sind auch bei Daten vom Typ **text**, **ntext** oder **image** hilfreich.  
  
|Funktion oder Anweisung|Description|  
|---------------------------|-----------------|  
|PATINDEX**(**'*%pattern%**'***,** *expression***)**|Gibt die Zeichenposition einer angegebenen Zeichenfolge in Spalten vom Typ **text** oder **ntext** zurück.|  
|DATALENGTH**(***expression***)**|Gibt die Länge der Daten in den **text**-, **ntext**- und **image**-Spalten zurück.|  
|SET TEXTSIZE|Gibt das Limit der **text**-, **ntext**- oder **image**-Daten, die von einer SELECT-Anweisung zurückgegeben werden sollen, in Byte zurück.|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird gemeldet, ob für jeden Wert in der `logo`-Spalte der `pub_info`-Tabelle ein gültiger Textzeiger vorhanden ist.  
  
> [!NOTE]  
>  Um dieses Beispiel auszuführen, müssen Sie die **pubs**-Datenbank installieren.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Text- und Bildfunktionen &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  
