---
title: RingN (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- RingN
- RingN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RingN method
ms.assetid: 30f47275-2727-4d22-bbec-c0c54bcb3ac2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e08cc4d2a3359362b0e5bff28c2e18459863b120
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="ringn-geography-data-type"></a>RingN (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den angegebenen Ring der **geography** -Instanz zurück: `1 ≤ n ≤ NumRings()`.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.RingN (expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein **int** -Ausdruck zwischen 1 und der Anzahl der Ringe in einer **polygon** -Instanz.  
  
## <a name="return-value"></a>Rückgabewert  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Wert des ringindex  **n**  ist kleiner als 1 ist, löst diese Methode eine **ArgumentOutOfRangeException.** aus. Der Wert des Ringindex muss größer oder gleich 1 sein und sollte kleiner oder gleich dem Wert sein, der von `NumRings()`.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird eine `Polygon` -Instanz mit zwei Ringen erstellt. Dann wird der zweite Ring zurückgegeben.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.RingN(2).ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [NumRings &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
  
