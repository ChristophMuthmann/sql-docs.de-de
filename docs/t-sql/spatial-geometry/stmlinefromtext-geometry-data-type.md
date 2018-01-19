---
title: STMLineFromText (Geometry-Datentyp) | Microsoft Docs
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
f1_keywords:
- STMLineFromText (geometry Data Type)
- STMLineFromText_TSQL
dev_langs: TSQL
helpviewer_keywords: STMLineFromText (geometry Data Type)
ms.assetid: 39fe8559-c4c2-4d61-8508-86eb0a103807
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b02e61030c60e2df91d17b593eecb585896ade86
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="stmlinefromtext-geometry-data-type"></a>STMLineFromText (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **geometry** -Instanz aus einer Darstellung des Typs Open Geospatial Consortium (OGC) Well-Known Text (WKT) zurück, die um alle von der Instanz getragenen Z (Höhe)- und M (Measure)-Werte erweitert wurde.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STMLineFromText ( 'multilinestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *multilinestring_tagged_text*  
 Ist die WKT-Darstellung der **GeometryMultiLineString** Instanz, die Sie zurückgeben möchten. *Multilinestring_tagged_text* ist ein **nvarchar(max)** Ausdruck.  
  
 *SRID*  
 Ist ein **Int** Ausdruck darstellt, die räumliche verweisen ID (SRID), der die **GeometryMultiLineString** Instanz, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
 OGC-Typ: **MultiLineString**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode löst eine **FormatException** aus, wenn die Eingabe nicht korrekt formatiert ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STMLineFromText()` zum Erstellen einer `geometry` Instanz.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMLineFromText('MULTILINESTRING ((100 100, 200 200), (3 4, 7 8, 10 10))', 0);  
```  
  
 `SELECT @g.ToString();`  
  
## <a name="see-also"></a>Siehe auch  
 [Statische geometry-Methoden des OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

