---
title: NumRings (geography-Datentyp) | Microsoft-Dokumentation
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
- NumRings_TSQL
- NumRings
dev_langs:
- TSQL
helpviewer_keywords:
- NumRings method
ms.assetid: 0e4e4fa2-b608-4cc4-98ba-0845ddb4214c
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db4e01713017ab2c06d71b11fda343720c124f85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="numrings-geography-data-type"></a>NumRings (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Anzahl der Ringe in einer **Polygon** -Instanz zurück. Bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography**-Typ werden externe und interne Ringe nicht voneinander unterschieden, da jeder Ring als der externe Ring betrachtet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.NumRings ()  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **int**  
  
 CLR-Rückgabetyp: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 Diese Methode gibt NULL zurück, wenn es sich nicht um ein **Polygon** handelt, und 0, wenn die Instanz leer ist. Diese Methode ist exakt.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird eine `Polygon` -Instanz mit zwei Ringen erstellt. Dann wird geprüft, ob sie zwei Ringe hat.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.NumRings();  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
