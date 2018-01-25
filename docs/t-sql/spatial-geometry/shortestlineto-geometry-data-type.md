---
title: ShortestLineTo (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08e83f7bb1993d3b55a48e5e3714c75d4bd33429
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt eine **LineString** -Instanz mit zwei Punkten zurück, die den kürzesten Abstand zwischen den zwei **geometry** -Instanzen darstellen. Die Länge der **LineString** -Instanz, die zurückgegeben wurde, entspricht dem Abstand zwischen den beiden **geometry** -Instanzen.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>Argumente  
 *geometry_other*  
 Die zweite **geometry** -Instanz, für die von der aufrufenden **geometry** -Instanz versucht wird, den kürzesten Abstand zu bestimmen.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 Die Methode gibt eine **LineString** -Instanz mit Endpunkten zurück, die auf den Rändern der beiden Instanzen von **geometry** liegen, die verglichen werden und sich nicht überschneiden. Die Länge der **LineString** -Instanz, die zurückgegeben wurde, entspricht dem geringsten Abstand zwischen den beiden **geometry** -Instanzen. Wenn sich die beiden Instanzen von **LineString** überschneiden, wird eine leere Instanz von **geometry** zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. Aufrufen von ShortestLineTo() für sich nicht überschneidende Instanzen  
 In diesem Beispiel wird der geringste Abstand zwischen einer Instanz von `CircularString` und einer Instanz von `LineString` ermittelt, und die Instanz von `LineString` wird zurückgegeben, die die beiden Punkte verbindet:  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(-4 7, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. Aufrufen von ShortestLineTo() für sich überschneidende Instanzen  
 In diesem Beispiel wird eine leere Instanz von `LineString` zurückgegeben, da die sich die Instanz von `LineString` und die Instanz von `CircularString` überschneiden:  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(0 5, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [ShortestLineTo &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  

