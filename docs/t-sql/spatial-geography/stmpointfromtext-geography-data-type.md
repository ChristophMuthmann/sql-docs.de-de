---
title: STMPointFromText (Geography-Datentyp) | Microsoft Docs
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
- STMPointFromText (geography Data Type)
- STMPointFromText_TSQL
dev_langs: TSQL
helpviewer_keywords: STMPointFromText method
ms.assetid: fe91a9f5-8de6-464e-88db-00650eae79b0
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4ca1effa784e492a80f6b40bfebe4379ec490d4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stmpointfromtext-geography-data-type"></a>STMPointFromText (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **geography** -Instanz von einer Open Geospatial Consortium (OGC) Well-Known Text (WKT)-Darstellung zurück, die um alle von der Instanz getragenen Z (Höhe)- und M (Measure)-Werte erweitert ist.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STMPointFromText ( 'multipoint_tagged_text', SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *multipoint_tagged_text*  
 Ist die WKT-Darstellung der **GeographyMultiPoint** Instanz, die Sie zurückgeben möchten. *Multipoint_tagged_text* ist ein **nvarchar(max)** Ausdruck.  
  
 *SRID*  
 Ist ein **Int** Ausdruck darstellt, die räumliche verweisen ID (SRID), der die **GeographyMultiPoint** Instanz, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
 OGC-Typ: **MultiPoint**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode löst eine **FormatException** aus, wenn die Eingabe nicht korrekt formatiert ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STMPointFromText()` zum Erstellen einer `geography` Instanz.  
  
```  
DECLARE @g geography;   
SET @g = geography::STMPointFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statische geography-Methoden des OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
