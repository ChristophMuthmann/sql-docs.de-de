---
title: STDistance (Geography-Datentyp) | Microsoft Docs
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
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cf72157a0168fb2bbf8aeb7ef6ec6381a0cab748
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="stdistance-geography-data-type"></a>STDistance (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt die kürzeste Entfernung zwischen einem Punkt in einer **geography** -Instanz und einem Punkt in einer anderen **geography** -Instanz zurück.  
  
> [!NOTE]  
>  `STDistance()`Gibt die kürzeste **LineString** zwischen zwei Geography-Typen. Dies ist ein naher Schätzwert der geodätische Entfernung. Die Abweichung von `STDistance()` bei allgemeinen Erdemodellen von der genauen geodätischen Entfernung beträgt nicht mehr als 0,25%. Dies verhindert Verwechslungen über die feinen Unterschiede zwischen Länge und Entfernung in geodätischen Typen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STDistance ( other_geography )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geography*  
 Eine andere **Geography** Instanz, aus der die Entfernung zur Instanz gemessen, auf dem STDistance() aufgerufen wird. Wenn *Other_geography* ein leeres festgelegt ist, gibt STDistance() null zurück.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **"float"**  
  
 CLR-Rückgabetyp: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 STDistance() gibt immer Null zurück, wenn das spatial Reference IDs (SRIDs) auf, der die **Geography** -Instanzen nicht übereinstimmen.  
  
> [!NOTE]  
>  Methoden für den **geography** -Datentyp, mit denen eine Fläche oder eine Entfernung berechnet wird, geben abhängig vom SRID der in der jeweiligen Methode verwendeten Instanz unterschiedliche Ergebnisse zurück.   Weitere Informationen über SRIDs finden Sie unter [Spatial Reference Identifiers &#40; SRIDs &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Abstand zwischen zwei **geography** -Instanzen gesucht.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
