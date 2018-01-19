---
title: STBuffer (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs: TSQL
helpviewer_keywords: STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b6d744ac8a275d48c1acb65ab7ea7c870692a1a1
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="stbuffer-geography-data-type"></a>STBuffer (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt eine Geography-Objekt, das die Vereinigung aller darstellt verweist, deren Abstand zu einer **Geography** Instanz ist kleiner oder gleich einem angegebenen Wert.  
  
 Diese geography-Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>Argumente  
 *distance*  
 Ist ein Wert vom Typ **"float"** (**doppelte** in .NET Framework) angeben des Abstands zwischen den **Geography** Instanz, die der Puffer berechnet werden soll.  
  
 Der maximale Abstand des Puffers darf 0.999 nicht überschreiten \* *π* * MinorAxis \* MinorAxis / MajorAxis (~0.999 \* 1/2 kugelumfang) oder die vollständige Kugel.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 STBuffer() berechnet einen Puffer auf die gleiche Weise wie [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md), wobei *Toleranz* = abs(distance) \* .001 und *relative*  =  **"false"**.  
  
 Ein negativer Puffer entfernt alle Punkte innerhalb des angegebenen Abstands von der Begrenzung der **Geography** Instanz.  
  
 `STBuffer()`Gibt zurück, eine **FullGlobe** Instanz in bestimmten Fällen; z. B. `STBuffer()` gibt eine **FullGlobe** -Instanz auf, wenn der Pufferabstand größer als der Abstand vom Äquator bis zu den Polen ist. Ein Puffer kann nicht über die vollständige Kugel hinausgehen.  
  
 Diese Methode löst eine **ArgumentException** in **FullGlobe** Instanzen, in denen der Abstand des Puffers die folgende Einschränkung überschreitet:  
  
 0,999 \* *π* * MinorAxis \* MinorAxis / MajorAxis (~0.999 \* 1/2 kugelumfang)  
  
 Die Begrenzung des maximal möglichen Abstands ermöglicht das Erstellen von äußerst flexiblen Puffern.  
  
 Die Abweichung zwischen dem theoretischen und dem berechnetem Puffer ist max (Toleranz, Blöcke * 1.E-7), in denen Toleranz = Distance \* .001. Weitere Informationen zu Blöcken, finden Sie unter [Geography-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt eine `LineString``geography` Instanz. Anschließend wird `STBuffer()` verwendet, um den Bereich innerhalb von 1 Meter Umkreis um die Instanz zurückzugeben.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BufferWithTolerance &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
