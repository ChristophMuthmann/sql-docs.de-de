---
title: STNumCurves (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 718289c6785bec8f9bba15ccec76507ac2501f47
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Mit dieser Methode wird die Anzahl der Kurven in einer Instanz von **geometry** zurückgegeben, wenn es sich dabei um einen eindimensionalen räumlichen Datentyp handelt. Eindimensionale räumliche Datentypen schließen **LineString**, **CircularString**und **CompoundCurve**ein. `STNumCurves`() funktioniert nur für einfache Typen. Es funktioniert nicht mit **Geometrie** -Auflistungen wie **MultiLineString**.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 Eine leere eindimensionale Instanz von **geometry** gibt 0 zurück. **NULL** wird zurückgegeben, wenn die **geometry** -Instanz keine eindimensionale oder eine nicht initialisierte Instanz ist.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. Verwenden von STNumCurves() in einer CircularString-Instanz  
 Im folgenden Beispiel wird gezeigt, wie die Anzahl der Kurven einer Instanz von `CircularString` abgerufen wird:  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');`  
  
 `SELECT @g.STNumCurves();`  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. Verwenden von STNumCurves() in einer CompoundCurve-Instanz  
 Im folgenden Beispiel wird mit `STNumCurves()` die Anzahl der Kurven in einer Instanz von `CompoundCurve` zurückgegeben.  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');`  
  
 `SELECT @g.STNumCurves();`  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [OGC-Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


