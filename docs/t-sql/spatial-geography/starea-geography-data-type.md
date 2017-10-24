---
title: STArea (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e96ee94983746e162990b8eadad4f6affb4f92fd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="starea-geography-data-type"></a>STArea (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die gesamte Oberfläche einer **Geography** Instanz. Ergebnisse für STArea() werden zurückgegeben, in das Quadrat der Maßeinheit, die von den spatial Reference Identifier verwendet die **Geography** Instanz; z. B. wenn die SRID der Instanz 4326 ist, STArea() gibt Ergebnisse zurück in Quadratmetern.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **"float"**  
  
 CLR-Rückgabetyp: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 STArea() gibt 0 zurück, wenn eine **Geography** -Instanz nur 0- und 1-dimensionale Abbildungen enthält oder wenn sie leer ist.  
  
> [!NOTE]  
>  Methoden für die **Geography** -Datentyp, einen metrischen Rückgabewert liefern, abhängig vom SRID der in der Methode verwendeten Instanz unterschiedliche Ergebnisse, erzeugen. Weitere Informationen zu SRIDs finden Sie unter [Spatial Reference Identifiers &#40; SRIDs &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STArea()` zum Erstellen einer `Polygon``geography` -Instanz und die Fläche des Polygons berechnet.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für Geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

