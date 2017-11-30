---
title: InStr (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5638c358-47da-40ad-b988-1a5214c05492
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4772f212c075cec7b0acd239833604bd2213d3c0
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="instr-mdx"></a>Instr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Position des ersten Vorkommens einer Zeichenfolge innerhalb einer anderen Zeichenfolge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>Argumente  
 *Starten*  
 (Optional) Ein numerischer Ausdruck, der die Startposition für jede Suche festlegt. Wenn Sie diesen Wert weglassen, beginnt die Suche an der ersten Zeichenposition. Wenn Start NULL ist, wird von der Funktion ein nicht definierter Wert zurückgegeben.  
  
 *searched_string*  
 Der Zeichenfolgenausdruck, der durchsucht werden soll.  
  
 *search_string*  
 Der Zeichenfolgenausdruck, nach dem gesucht werden soll.  
  
 *Vergleichen*  
 (optional) Ein ganzzahliger Wert. Dieses Argument wird immer ignoriert. Es wird definiert, um die Kompatibilität mit anderen **Instr** Funktionen in anderen Sprachen.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Ganzzahlwert, mit die Anfangsposition der *Zeichenfolge2* in *String1*.  
  
 Darüber hinaus **InStr** Funktion gibt in Abhängigkeit von der Bedingung in der folgenden Tabelle aufgeführten Werte zurück:  
  
|Bedingung|Rückgabewert|  
|---------------|------------------|  
|String1 hat die Länge 0 (null)|Null (0)|  
|String1 ist NULL|nicht definiert|  
|String2 hat die Länge 0 (null)|start|  
|String2 ist NULL|nicht definiert|  
|String2 wurde nicht gefunden|Null (0)|  
|start ist größer als Len(String2)|Null (0)|  
  
## <a name="remarks"></a>Hinweise  
  
> [!WARNING]  
>  **InStr** führt immer groß-und Kleinschreibung unterschieden.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel zeigt die Verwendung der **Instr** -Funktion gezeigt sowie verschiedene ergebnisszenarien.  
  
```  
with   
    member [Date].[Date].[Results] as "Results"  
    member measures.[lowercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[uppercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "O")  
    member measures.[searched string is empty]            as InStr( "", "o")  
    member measures.[searched string is null]             as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[search string is empty]              as InStr( "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is empty start 10]     as InStr(10, "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is null]               as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[found from start 10]                 as InStr( 10, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NOT found from start 17]             as InStr( 17, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NULL start]                          as iif(IsError(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Error", iif(IsNull(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Null","Is undefined"))  
    member measures.[start greater than searched length]  as InStr( 170, "abcdefghijklmnñopqrstuvwxyz", "o")  
  
select  [Results] on columns,  
       { measures.[lowercase found in lowercase string]  
       , measures.[uppercase found in lowercase string]  
       , measures.[searched string is empty]  
       , measures.[searched string is null]  
       , measures.[search string is empty]  
       , measures.[search string is empty start 10]  
       , measures.[search string is null]  
       , measures.[found from start 10]  
       , measures.[NOT found from start 17]  
       , measures.[NULL start]   
       , measures.[start greater than searched length]  
       } on rows  
  
from [Adventure Works]  
```  
  
 In der folgenden Tabelle werden die erhaltenen Ergebnisse angezeigt:  
  
|||  
|-|-|  
||Ergebnisse|  
|Kleinbuchstaben in Zeichenfolge mit Kleinbuchstaben gefunden|16|  
|Großbuchstaben in Zeichenfolge mit Kleinbuchstaben gefunden|16|  
|Gesuchte Zeichenfolge ist leer|0|  
|Gesuchte Zeichenfolge ist NULL|Ist nicht definiert|  
|Suchzeichenfolge ist leer|1|  
|Suchzeichenfolge ist leer, Start 10|10|  
|Suchzeichenfolge ist NULL|Ist nicht definiert|  
|Gefunden von Start 10|16|  
|Nicht gefunden von Start 17|0|  
|NULL-Start|Ist nicht definiert|  
|Start ist größer als die gesuchte Länge|0|  
  
  
