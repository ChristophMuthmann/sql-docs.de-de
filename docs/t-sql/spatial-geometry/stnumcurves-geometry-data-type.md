---
title: STNumCurves (geometry-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 947baac6cd2a562bc24469bcf9554aca7a735ae7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Mit dieser Methode wird die Anzahl der Kurven in einer Instanz von **geometry** zurückgegeben, wenn es sich dabei um einen eindimensionalen räumlichen Datentyp handelt. Eindimensionale räumliche Datentypen schließen **LineString**, **CircularString**und **CompoundCurve**ein. `STNumCurves`() funktioniert nur mit einfachen Typen; **geometry**-Collections wie **MultiLineString** gehören nicht dazu.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geometry**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Eine leere eindimensionale Instanz von **geometry** gibt 0 zurück. **NULL** wird zurückgegeben, wenn die **geometry** -Instanz keine eindimensionale oder eine nicht initialisierte Instanz ist.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. Verwenden von STNumCurves() in einer CircularString-Instanz  
 Im folgenden Beispiel wird gezeigt, wie die Anzahl der Kurven einer Instanz von `CircularString` abgerufen wird:  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. Verwenden von STNumCurves() in einer CompoundCurve-Instanz  
 Im folgenden Beispiel wird mit `STNumCurves()` die Anzahl der Kurven in einer Instanz von `CompoundCurve` zurückgegeben.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

