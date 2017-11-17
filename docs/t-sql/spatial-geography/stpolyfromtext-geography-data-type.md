---
title: STPolyFromText (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
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
- STPolyFromText_TSQL
- STPolyFromText (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPolyFromText method
ms.assetid: d7e6a2bb-d301-49fb-9202-c70a9d169b4d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33eef062e4a72cb84c077979de7717a10fdc3a3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stpolyfromtext-geography-data-type"></a>STPolyFromText (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **Geography** Instanz aus einer Open Geospatial Consortium (OGC) Well-Known Text (WKT)-Darstellung getragenen Z-(Höhe) und M (Measure)-Werte von der Instanz getragen.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STPolyFromText ( 'polygon_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *polygon_tagged_text*  
 Ist die WKT-Darstellung der **GeographyPolygon** Instanz, die Sie zurückgeben möchten. *Polygon_tagged_text* ist ein **nvarchar(max)** Ausdruck.  
  
 *SRID*  
 Ist ein **Int** Ausdruck darstellt, die räumliche verweisen ID (SRID), der die **GeographyPolygon** Instanz, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
 OGC-Typ: **Polygon**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode löst eine **FormatException** aus, wenn die Eingabe nicht korrekt formatiert ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STPolyFromText()` zum Erstellen einer `geography` Instanz.  
  
```  
DECLARE @g geography;  
SET @g = geography::STPolyFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statische Geography-Methoden des OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

