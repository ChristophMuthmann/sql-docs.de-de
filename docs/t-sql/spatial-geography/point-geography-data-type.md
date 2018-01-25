---
title: Point (Geography-Datentyp) | Microsoft Docs
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
- Point
- Point_TSQL
dev_langs: TSQL
helpviewer_keywords:
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f37072d64159d5d8bfb1d44a64dd017adf0fceed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="point-geography-data-type"></a>Point (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Erstellt eine **Geography** Instanz darstellt eine **Punkt** Instanz ihren Werten Breiten- und Längengrad sowie spatial Reference ID (SRID)).
  
## <a name="syntax"></a>Syntax  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *Lat*  
 Ist eine **"float"** Ausdruck, der die X-Koordinate des darstellt der **Punkt** generiert wird.  
  
 *Long*  
 Ist eine **"float"** Ausdruck, der die y-Koordinate des darstellt der **Punkt** generiert wird. Weitere Informationen zu gültigen Breiten- und längengradwerte finden Sie unter [Punkt](../../relational-databases/spatial/point.md).  
  
 *SRID*  
 Ist ein **Int** Ausdruck, der die SRID der darstellt, die **Geography** Instanz, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
> [!NOTE]  
>  Argumente für die Punktemethode (Geography-Datentyp) besitzen umgekehrte Koordinaten im Vergleich zu WKT.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `Point()` zum Erstellen einer `geography` Instanz.  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte statische geography-Methoden](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
