---
title: Parse (Geometry-Datentyp) | Microsoft Docs
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
helpviewer_keywords: Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 97fa8dad6e879cf976a3f790422b12cb09255a13
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="parse-geometry-data-type"></a>Parse (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **geometry** -Instanz aus einer Open Geospatial-Konsortium (OGC) Well-Known Text (WKT)-Darstellung zurück. `Parse()`entspricht dem [STGeomFromText()](../../t-sql/spatial-geometry/parse-geometry-data-type.md), mit der Ausnahme, dass es eine räumliche wird vorausgesetzt ID SRID (Spatial reference) 0 als Parameter. Die Eingabe kann optional Z- (Höhe) und M-Werte (Measure) tragen.
  
## <a name="syntax"></a>Syntax  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumente  
 *geometry_tagged_text*  
 Die WKT-Darstellung der Instanz von **geometry** , die zurückgegeben werden soll. *geometry_tagged_text* ist ein **nvarchar** -Ausdruck.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 Der OGC-Typ der **geometry** -Instanz, die von `Parse()` zurückgegeben wird, wird auf die entsprechende WKT-Eingabe festgelegt.  
  
 Die Zeichenfolge 'Null' wird als eine NULL- **geometry** -Instanz interpretiert.  
  
 Diese Methode löst eine **FormatException** aus, wenn die Eingabe nicht korrekt formatiert ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `Parse()` verwendet, um eine `geometry` -Instanz zu erstellen.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [Erweiterte statische geometry-Methoden](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

