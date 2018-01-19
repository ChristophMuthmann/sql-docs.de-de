---
title: STGeomFromText (Geography-Datentyp) | Microsoft Docs
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
- STGeomFromText (geography Data Type)
- STGeomFromText_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full globe
- STGeomFromText method
ms.assetid: 3717987b-77d8-4ccf-a1db-5a8016ac1083
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 488a55f82cabd9700f4bf9f7ee70d519e87b8661
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="stgeomfromtext-geography-data-type"></a>STGeomFromText (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **Geography** Instanz aus einer Open Geospatial Consortium (OGC) Well-Known Text (WKT)-Darstellung getragenen Z-(Höhe) und M (Measure)-Werte von der Instanz getragen.
  
Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STGeomFromText ( 'geography_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *geography_tagged_text*  
 Die WKT-Darstellung der Instanz von **geography** , die zurückgegeben werden soll. *Geography_tagged_text* ist ein **nvarchar(max)** Ausdruck.  
  
 *SRID*  
 Ein **int** -Ausdruck, der die SRID (Spatial Reference ID) der Instanz von **geography** darstellt, die zurückgegeben wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Die OGC-Typ, der die **Geography** vom STGeomFromText() zurückgegebene Instanz auf die entsprechende WKT-Eingabe festgelegt ist.  
  
 Diese Methode löst eine **ArgumentException** , wenn die Eingabe eine gegenüberliegende Kante enthält.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STGeomFromText()` zum Erstellen einer `geography` Instanz.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statische geography-Methoden des OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
