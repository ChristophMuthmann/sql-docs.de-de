---
title: STGeomCollFromWKB (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
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
- STGeomCollFromWKB (geography Data Type)
- STGeomCollFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STMGeomCollFromWKB method
ms.assetid: bbed028c-9cd6-4236-b5e5-8e914a21f2e4
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4551839c69157e7ba1d5d24232661c9901f54aa6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stgeomcollfromwkb-geography-data-type"></a>STGeomCollFromWKB (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **GeometryCollection**-Instanz von einer Open Geospatial Consortium (OGC) Well-Known Binary (WKB)-Darstellung zurück.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STGeomCollFromWKB ( 'WKB_geometrycollection' , SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *WKB_geometrycollection*  
 Die WKB-Darstellung der Instanz von **GeometryCollection** , die zurückgegeben werden soll. *WKB_geometrycollection* ist ein **varbinary(max)** -Ausdruck.  
  
 *SRID*  
 Ein **int** -Ausdruck, der den SRID (Spatial Reference ID) der **GeometryCollection** -Instanz darstellt, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Die OGC-Typ, der die **Geography** vom STGeomCollFromWKB() zurückgegebene Instanz wird festgelegt, um **GeometryCollection**, **MultiPolygon**, **MultiLineString**, oder **MultiPoint**, abhängig von der entsprechenden WKB-Eingabe.  
  
 Diese Methode löst eine **FormatException** -Ausnahme aus, wenn die Eingabe nicht korrekt formatiert ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STGeomCollFromWKB()` verwendet, um eine `geography` -Instanz zu erstellen.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomCollFromWKB(0x01070000000200000001010000007593180456965EC017D9CEF753D34740010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statische geography-Methoden des OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
