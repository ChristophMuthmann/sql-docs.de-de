---
title: Filter (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
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
- Filter
- Filter_TSQL
- Filter (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 3d629a39-157e-4159-a3ca-a3c2e0ed4160
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: de93cc3be1f1a571b82c2d9ff2943af222f4f337
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="filter-geometry-data-type"></a>Filter (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Eine Methode, die eine schnelle, nur indexbezogene Schnittmethode bietet, um zu ermitteln, ob eine **geometry** -Instanz eine andere **geometry** -Instanz überschneidet, vorausgesetzt, dass ein Index verfügbar ist.
  
Gibt 1 zurück, wenn eine **geometry** -Instanz möglicherweise eine andere **geometry** -Instanz überschneidet. Diese Methode erzeugt eventuell eine falsche positive Rückgabe, und das genaue Ergebnis ist unter Umständen planabhängig. Gibt einen genauen Wert 0 (wahr negative Rückgabe) zurück, wenn keine Überschneidung von **geometry** -Instanzen gefunden wird.
  
Wenn kein Index verfügbar ist oder verwendet wird, gibt die Methode dieselben Werte zurück wie **STIntersects()** , wenn diese Methode mit denselben Parametern aufgerufen wird.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geometry*  
 Eine andere **Geometrie** Instanz, für die Instanz verglichen werden soll, auf dem Filter() aufgerufen wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode ist weder deterministisch noch präzise.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `Filter()` verwendet, um festzustellen, wo sich zwei `geometry` -Instanzen schneiden.  
  
```  
CREATE TABLE sample (id int primary key, g geometry);  
GO  
INSERT INTO sample VALUES  
   (0, geometry::Point(0, 0, 0)),  
   (1, geometry::Point(0, 1, 0)),  
   (2, geometry::Point(0, 2, 0)),  
   (3, geometry::Point(0, 3, 0)),  
   (4, geometry::Point(0, 4, 0));  
  
CREATE SPATIAL INDEX sample_idx ON sample(g)  
WITH (bounding_box = (-8000, -8000, 8000, 8000));  
GO  
SELECT id  
FROM sample   
WHERE g.Filter(geometry::Parse('POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))')) = 1;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  


