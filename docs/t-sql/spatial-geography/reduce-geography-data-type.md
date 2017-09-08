---
title: Reduce (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c5b174f3f4b8daf99c402b110ba10d95345783d7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="reduce-geography-data-type-"></a>Reduce (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt einen Näherungswert der gegebenen **geography** -Instanz zurück. Dieser Näherungswert wird unter Verwendung des Douglas-Peucker-Algorithmus mit der angegebenen Toleranz ermittelt.  
  
 Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumente  
  
|||  
|-|-|  
|Begriff|Definition|  
|*Fehlertoleranz*|Ein Wert vom Typ **float**. *tolerance* ist die Toleranz, die für den Douglas-Peucker-Algorithmus angegeben wird. *tolerance* muss eine positive Zahl sein.|  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Bei Auflistungstypen arbeitet dieser Algorithmus unabhängig für jeden **geography** -Wert, der in der Instanz enthalten ist. Dieser Algorithmus ändert keine **Point** -Instanzen.  
  
 Diese Methode versucht, die Endpunkte von **LineString** -Instanzen beizubehalten. Dies kann aber fehlschlagen, um ein gültiges Ergebnis zu erhalten.  
  
 Wenn `Reduce()` mit einem negativen Wert aufgerufen wird, erzeugt diese Methode eine **ArgumentException**. In `Reduce()` verwendete Toleranzen müssen positive Zahlen sein.  
  
 Der Douglas-Peucker-Algorithmus kann für jede Kurve oder jeden Ring in der **geography** -Instanz verwendet werden, indem alle Punkte mit Ausnahme des Start- und Endpunkts entfernt werden. Anschließend wird jeder entfernte Punkt erneut hinzugefügt, beginnend mit dem äußersten Punkt, bis kein Punkt mehr als *tolerance* vom Ergebnis entfernt ist. Das Ergebnis wird dann gegebenenfalls gültig gemacht, da ein gültiges Ergebnis garantiert wird.  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], diese Methode wurde erweitert und **FullGlobe** Instanzen.  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und `Reduce()` verwendet, um die Instanz zu vereinfachen.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
