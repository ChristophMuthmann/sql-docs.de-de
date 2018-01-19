---
title: Parse (Geography-Datentyp) | Microsoft Docs
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
dev_langs: TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32d8925fdf53a1d0bcac33719348138b354376c2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="parse-geography-data-type"></a>Parse (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **geography** -Instanz aus einer Open Geospatial-Konsortium (OGC) Well-Known Text (WKT)-Darstellung zurück. Parse() entspricht [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md), außer dass es spatial Reference ID (SRID) mit dem Wert 4326 als Parameter voraus. Die Eingabe kann optional Z- (Höhe) und M-Werte (Measure) tragen.
  
Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.
  
## <a name="syntax"></a>Syntax  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumente  
 *geography_tagged_text*  
 Die WKT-Darstellung der Instanz von **geography** , die zurückgegeben werden soll. *geography_tagged_text* ist ein **nvarchar** -Ausdruck.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Der OGC-Typ der **geography** -Instanz, die von `Parse()` zurückgegeben wird, wird auf die entsprechende WKT-Eingabe festgelegt.  
  
 Die Zeichenfolge 'Null' wird als eine NULL- **geography** -Instanz interpretiert.  
  
 Diese Methode löst **ArgumentException** aus, wenn die Eingabe eine gegenüberliegende Kante enthält.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `Parse()` verwendet, um eine `geography` -Instanz zu erstellen.  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte statische Geography-Methoden](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
