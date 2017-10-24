---
title: "(Umgekehrter Schrägstrich) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
helpviewer_keywords:
- backwhack
- backslash
- excape character
- hack character
- '\ (backslash)'
- backslant
- bash
- reverse slant
- slosh
- reversed virgule
- line continuation character
- reverse solidus
ms.assetid: c97fbb20-3d12-4d0b-9b52-62a229bc83c0
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 011025d20b6341b9fa43b25f6c14c91a135a6ffa
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-utilities-statements---backslash"></a>Anweisungen für SQL Server-Hilfsprogramme - umgekehrter Schrägstrich
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthält Befehle, die nicht [!INCLUDE[tsql](../../includes/tsql-md.md)] sind aber -Anweisungen erkannt, durch die **Sqlcmd** und **Osql** Hilfsprogramme und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Code-Editor. Die Befehle können zur Vereinfachung der Lesbarkeit und Ausführung von Batches und Skripts verwendet werden.  
  
\ eine lange Zeichenfolge in zwei oder mehr Zeilen zur besseren Lesbarkeit Konstante unterbrochen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>Argumente  
 \<erster Abschnitt der Zeichenfolge >  
 Ist der Anfang einer Zeichenfolge.  
  
 \<Fortsetzung der Abschnitt der Zeichenfolge >  
 Ist die Fortsetzung einer Zeichenfolge.  
  
## <a name="remarks"></a>Hinweise  
 Dieser Befehl gibt den ersten und den fortgesetzten Abschnitt der Zeichenfolge ohne den umgekehrten Schrägstrich als eine einzige Zeichenfolge zurück.  
  
 Der umgekehrte Schrägstrich ist keine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung. Es ist ein Befehl, der vom erkannt wird die **Sqlcmd** und **Osql** Hilfsprogramme und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Code-Editor.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden ein umgekehrter Schrägstrich und ein Wagenrücklauf verwendet, um die Zeichenfolge in zwei Zeilen zu teilen.  
  
```  
SELECT 'abc\  
def' AS ColumnResult;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40; aufgrund einer Division &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40; Teilen gleich &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  

