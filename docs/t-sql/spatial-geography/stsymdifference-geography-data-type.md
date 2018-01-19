---
title: STSymDifference (Geography-Datentyp) | Microsoft Docs
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
- STSymDifference (geography Data Type)
- STSymDifference_TSQL
dev_langs: TSQL
helpviewer_keywords: STSymDifference (geography Data Type)
ms.assetid: 82bbfa2c-a61b-4f41-9bf8-6f720f363bae
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 479d0badaced9808c5bd727b5f818dcab729605b
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="stsymdifference-geography-data-type"></a>STSymDifference (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt ein Objekt zurück, das alle Punkte darstellt, die sich entweder in einer **geography** -Instanz oder in einer anderen **geography** -Instanz befinden, nicht jedoch die Punkte, die sich innerhalb beider Instanzen befinden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STSymDifference ( other_geography )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geography*  
 Eine andere **Geography** Instanz zusätzlich zu der Instanz auf dem STSymDistance() aufgerufen wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt immer NULL zurück, wenn die SRIDs (Spatial Reference IDs) der **geography** -Instanzen nicht übereinstimmen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt räumliche Instanzen, die größer als eine Hemisphäre sind. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], der Satz von möglichen Ergebnissen, die auf dem Server wurde erweitert und **FullGlobe** Instanzen.  
  
 Im Ergebnis können nur dann Kreisbogensegmente enthalten sein, wenn die Eingabeinstanzen auch Kreisbogensegmente enthalten.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygons"></a>A. Berechnen des symmetrischen Unterschieds zweier Polygone  
 Im folgenden Beispiel wird `STSymDifference()` zum Berechnen der symmetrischen Differenz zweier `Polygon` -Instanzen verwendet.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-with-fullglobe"></a>B. Berechnen des symmetrischen Unterschieds mit FullGlobe  
 Im folgenden Beispiel wird der symmetrische Unterschied eines `Polygon` und eines `FullGlobe`verglichen.  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STSymDifference('FULLGLOBE').ToString();
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
