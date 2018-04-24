---
title: STDistance (geography-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
f1_keywords:
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1520ed3cc4554c7311d35aa6499ebf19e3eb2137
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stdistance-geography-data-type"></a>STDistance (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt die kürzeste Entfernung zwischen einem Punkt in einer **geography** -Instanz und einem Punkt in einer anderen **geography** -Instanz zurück.  
  
> [!NOTE]  
>  `STDistance()` gibt den kürzesten **LineString** zwischen zwei geography-Typen zurück. Dies ist ein naher Schätzwert der geodätische Entfernung. Die Abweichung von `STDistance()` bei allgemeinen Erdemodellen von der genauen geodätischen Entfernung beträgt nicht mehr als 0,25%. Dies verhindert Verwechslungen über die feinen Unterschiede zwischen Länge und Entfernung in geodätischen Typen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STDistance ( other_geography )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geography*  
 Eine andere **geography**-Instanz, von der aus die Entfernung zu der Instanz gemessen werden soll, in der STDistance() aufgerufen wird. Wenn *other_geography* leer ist, gibt STDistance() NULL zurück.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **float**  
  
 CLR-Rückgabetyp: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 STDistance() gibt immer NULL zurück, wenn die SRIDs (Spatial Reference IDs) der **geography**-Instanzen nicht übereinstimmen.  
  
> [!NOTE]  
>  Methoden für den **geography** -Datentyp, mit denen eine Fläche oder eine Entfernung berechnet wird, geben abhängig vom SRID der in der jeweiligen Methode verwendeten Instanz unterschiedliche Ergebnisse zurück.   Weitere Informationen über SRIDs finden Sie unter [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Abstand zwischen zwei **geography** -Instanzen gesucht.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
