---
title: BufferWithTolerance (Geography-Datentyp) | Microsoft Docs
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
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: feaa401cfd6e2077035d164412941392412011ae
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt ein geometrisches Objekt, das die Vereinigung aller Punktwerte darstellt, Werte, deren Abstand zu einer **Geography** Instanz ist kleiner oder gleich einem angegebenen Wert einer angegebenen Toleranz.  
  
 Diese geography-Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumente  
 *Abstand*  
 Ist eine **"float"** Ausdruck, der den Abstand zwischen angibt der **Geography** Instanz, die der Puffer berechnet werden soll.  
  
 Der maximale Abstand des Puffers darf 0.999 nicht überschreiten \* *π* * MinorAxis \* MinorAxis / MajorAxis (~0.999 \* 1/2 kugelumfang) oder die vollständige Kugel.  
  
 *Fehlertoleranz*  
 Ein **float** -Ausdruck, der die Toleranz des Pufferabstands angibt.  
  
 Die *Toleranz* -Wert bezieht sich auf die maximale Variation im idealen Pufferabstand für die zurückgegebene lineare Näherung.  
  
 Beispielsweise kann der ideale Pufferabstand eines Punkts ein Kreis sein, dieser muss jedoch durch ein Polygon näherungsweise angegeben werden. Je geringer die Toleranz, desto mehr Punkte hat das Polygon, wodurch die Komplexität des Ergebnisses erhöht, der Fehler jedoch verringert wird.  
  
 Die minimale Grenze ist 0,1 Prozent des Abstands, und geringere Toleranzen werden auf die minimale Grenze aufgerundet.  
  
 *relative*  
 Ein **bit** , das angibt, ob der *tolerance* -Wert relativ oder absolut ist. Wenn 'TRUE' oder 1, die Toleranz relativ und wird als Produkt des berechnet die *Toleranz* -Parameter und Winkelweite \* äquatorradius des ellipsoids. Wenn 'FALSE' oder 0, ist die Toleranz absolut und der *tolerance* -Wert ist die absolute maximale Variation im idealen Pufferabstand für die zurückgegebene lineare Näherung.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode löst eine **ArgumentException** Wenn die *Abstand* ist keine Zahl (NAN) ist, oder wenn *Abstand* positiv oder negativ unendlich ist.  Diese Methode löst auch ein **ArgumentException** Wenn *Toleranz* ist NULL (0), keine Zahl (NaN), negativ oder positiv oder minus unendlich.  
  
 `STBuffer()`Gibt zurück, eine **FullGlobe** Instanz in bestimmten Fällen; z. B. `STBuffer()` gibt eine **FullGlobe** Instanz für zwei Pole zurück, wenn der Pufferabstand größer als der Abstand vom Äquator bis zu ist den Polen reichen.  
  
 Diese Methode löst eine **ArgumentException** in **FullGlobe** Instanzen, in denen der Abstand des Puffers die folgende Einschränkung überschreitet:  
  
 0,999 \* *π* * MinorAxis \* MinorAxis / MajorAxis (~0.999 \* 1/2 kugelumfang)  
  
 Die Abweichung zwischen dem theoretischen und dem berechnetem Puffer ist max (Toleranz, Blöcke \* 1.E-7) Toleranz ist, in dem der Wert der *Toleranz* Parameter. Weitere Informationen zu Blöcken, finden Sie unter [Geography-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `Point` -Instanz erstellt und `BufferWithTolerance()` verwendet, um einen groben Puffer um die Instanz zu erhalten.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [STBuffer &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
