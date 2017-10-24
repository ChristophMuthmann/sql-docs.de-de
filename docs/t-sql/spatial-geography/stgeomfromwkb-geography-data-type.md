---
title: STGeomFromWKB (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeomFromWKB_TSQL
- STGeomFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromWKB method
ms.assetid: 79d39d88-5440-49a7-9247-190eafce3f4f
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22841fbeff43f2d81d3760057d501004e44de534
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stgeomfromwkb-geography-data-type"></a>STGeomFromWKB (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **geography** -Instanz von einer Open Geospatial-Konsortium (OGC) Well-Known binary (WKB)-Darstellung zurück.
  
Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STGeomFromWKB ( 'WKB_geography' , SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *WKB_geography*  
 Die WKB-Darstellung der Instanz von **geography** , die zurückgegeben werden soll. *WKB_geography* ist ein **varbinary(max)** -Ausdruck.  
  
 *SRID*  
 Ein **int** -Ausdruck, der die SRID (Spatial Reference ID) der Instanz von **geography** darstellt, die zurückgegeben wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Der OGC-Typ der **geography** -Instanz, die von `STGeomFromText()` zurückgegeben wird, wird auf die entsprechende WKB-Eingabe festgelegt.  
  
 Diese Methode löst eine **FormatException** aus, wenn die Eingabe nicht korrekt formatiert ist.  
  
 Diese Methode löst **ArgumentException** aus, wenn die Eingabe eine gegenüberliegende Kante enthält.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STGeomFromWKB()` verwendet, um eine `geography` -Instanz zu erstellen.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statische Geography-Methoden des OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

