---
title: Filter (geography-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 320ecb9b538300bd4d25dbb365bfbe1058833a7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="filter-geography-data-type"></a>Filter (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Eine Methode, die eine schnelle, nur indexbezogene Schnittmethode bietet, um zu ermitteln, ob eine **geography** -Instanz eine andere **geography** -Instanz überschneidet, vorausgesetzt, dass ein Index verfügbar ist.  
  
 Gibt 1 zurück, wenn eine **geography** -Instanz möglicherweise eine andere **geography** -Instanz überschneidet. Diese Methode erzeugt eventuell eine falsche positive Rückgabe, und das genaue Ergebnis ist unter Umständen planabhängig. Gibt einen genauen Wert 0 (wahr negative Rückgabe) zurück, wenn keine Überschneidung von **geography** -Instanzen gefunden wird.  
  
 Wenn kein Index verfügbar ist oder verwendet wird, gibt die Methode dieselben Werte zurück wie **STIntersects()** , wenn diese Methode mit denselben Parametern aufgerufen wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.Filter ( other_geography )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geography*  
 Eine andere **geography**-Instanz zum Vergleich mit der Instanz, in der Filter() aufgerufen wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Diese Methode ist weder deterministisch noch präzise.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `Filter()` verwendet, um festzustellen, wo sich zwei `geography` -Instanzen schneiden.  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
