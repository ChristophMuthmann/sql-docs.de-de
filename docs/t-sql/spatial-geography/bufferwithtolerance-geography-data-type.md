---
title: BufferWithTolerance (geography-Datentyp) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb70f24c521fd5f0325ecbb718e7d76aa43f935d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt ein geometrisches Objekt zurück, das die Vereinigung aller Punktwerte darstellt, deren Abstand zu einer **geography**-Instanz kleiner oder gleich einem angegebenen Wert ist, wobei eine angegebene Toleranz gewährt wird.  
  
 Diese geography-Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumente  
 *distance*  
 Ein **float**-Ausdruck, der den Abstand zu der **geometry**-Instanz angibt, um die der Puffer berechnet werden soll.  
  
 Der maximale Abstand des Puffers darf 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 Kugelumfang) oder die vollständige Kugel nicht überschreiten.  
  
 *tolerance*  
 Ein **float** -Ausdruck, der die Toleranz des Pufferabstands angibt.  
  
 Der *Toleranz*wert verweist auf die maximale Variation im idealen Pufferabstand für die zurückgegebene lineare Näherung.  
  
 Beispielsweise kann der ideale Pufferabstand eines Punkts ein Kreis sein, dieser muss jedoch durch ein Polygon näherungsweise angegeben werden. Je geringer die Toleranz, desto mehr Punkte hat das Polygon, wodurch die Komplexität des Ergebnisses erhöht, der Fehler jedoch verringert wird.  
  
 Die minimale Grenze ist 0,1 Prozent des Abstands, und geringere Toleranzen werden auf die minimale Grenze aufgerundet.  
  
 *relative*  
 Ein **bit** , das angibt, ob der *tolerance* -Wert relativ oder absolut ist. Bei TRUE oder 1 ist die Toleranz relativ und wird aus dem *tolerance*-Parameter und der Winkelweite \* (Äquatorradius) des Ellipsoids berechnet. Wenn 'FALSE' oder 0, ist die Toleranz absolut und der *tolerance* -Wert ist die absolute maximale Variation im idealen Pufferabstand für die zurückgegebene lineare Näherung.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Diese Methode löst eine **ArgumentException** aus, wenn *distance* keine Zahl (NAN) oder wenn *distance* positiv oder minus unendlich ist.  Diese Methode löst eine **ArgumentException** aus, wenn *tolerance* Null (0), keine Zahl (NAN), negativ oder positiv oder minus unendlich ist.  
  
 `STBuffer()` gibt in bestimmten Fällen eine Instanz von **FullGlobe** zurück. Beispielsweise gibt `STBuffer()` eine **FullGlobe**-Instanz für zwei Pole zurück, wenn der Pufferabstand größer als der Abstand vom Äquator zu den Polen ist.  
  
 Diese Methode löst eine **ArgumentException** in **FullGlobe**-Instanzen aus, bei denen der Abstand des Puffers die folgende Einschränkung überschreitet:  
  
 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 Kugelumfang)  
  
 Die Abweichung zwischen dem theoretischen und dem berechnetem Puffer beträgt max(tolerance, extents \* 1,0E-7), wobei die Toleranz der Wert des Parameters *tolerance* ist. Weitere Informationen zu Erweiterungen finden Sie unter [geography-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `Point` -Instanz erstellt und `BufferWithTolerance()` verwendet, um einen groben Puffer um die Instanz zu erhalten.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [STBuffer &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
