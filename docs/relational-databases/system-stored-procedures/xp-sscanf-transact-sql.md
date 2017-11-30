---
title: Xp_sscanf (Transact-SQL) | Microsoft Docs
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
- xp_sscanf_TSQL
- xp_sscanf
dev_langs: TSQL
helpviewer_keywords: xp_sscanf
ms.assetid: 619a9df1-7008-407e-a75a-bc6f851454a8
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70835bdde4e84dbe889c8ae4f2ec5da24b314d5f
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="xpsscanf-transact-sql"></a>xp_sscanf (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Liest Daten aus einer Zeichenfolge in die durch die Formatargumente angegebenen Speicherbereiche ein.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
xp_sscanf { string OUTPUT , format } [ ,argument [ ,...n ] ]   
```  
  
## <a name="arguments"></a>Argumente  
 **Zeichenfolge**  
 Die Zeichenfolge, aus der die Argumentwerte gelesen werden.  
  
 OUTPUT  
 Wenn dieser Parameter angegeben wird, wird der Wert von *argument* im Ausgabeparameter platziert.  
  
 *Format*  
 Eine Zeichenfolge, deren Formatierung den Formatparametern der **sscanf** -Funktion der Programmiersprache C gleicht. Derzeit wird nur das %s-Formatierungsargument unterstützt.  
  
 *Argument*  
 Eine **varchar** -Variable, die auf den Wert des entsprechenden *format* -Arguments festgelegt ist.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass bis zu 50 Argumente angegeben werden können.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 **xp_sscanf** gibt die folgende Meldung aus:  
  
 `Command(s) completed successfully.`  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel extrahiert mit `xp_sscanf` zwei Werte aus einer Quellzeichenfolge anhand ihrer Positionen im Format der Quellzeichenfolge.  
  
```  
DECLARE @filename varchar (20), @message varchar (20);  
EXEC xp_sscanf 'sync -b -fproducts10.tmp -rrandom', 'sync -b -f%s -r%s',   
  @filename OUTPUT, @message OUTPUT;  
SELECT @filename, @message;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------- --------------------   
products10.tmp        random  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Allgemeine erweiterte gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Xp_sprintf &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-sprintf-transact-sql.md)  
  
  
