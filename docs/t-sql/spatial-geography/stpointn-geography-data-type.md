---
title: STPointN (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90c80d8b9d6ec81c078d9de0db5f26a900c8b5d6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stpointn-geography-data-type"></a>STPointN (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den angegebenen Punkt in einer **geography** -Instanz zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein **int** -Ausdruck zwischen 1 und der Anzahl der Punkte in der **geography** -Instanz.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
 Open Geospatial Consortium (OGC)-Typ: **Point**  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine **Geography** Instanz Benutzer erstellt, STPointN() wird die vom angegebenen Punkt *Ausdruck* indem die Punkte in der Reihenfolge, in der sie ursprünglich eingegeben wurden.  
  
 Wenn eine **Geography** -Instanz vom System erstellt wurde, STPointN() gibt die vom angegebenen Punkt *Ausdruck* indem alle Punkte in der gleichen Reihenfolge Ausgabe werden: erst nach  **Geography** Instanz, dann nach dem Ring innerhalb der Instanz (falls zutreffend) und schließlich nach Punkt innerhalb des Rings. Diese Reihenfolge ist deterministisch.  
  
 Wenn diese Methode mit einem geringeren Wert als 1 aufgerufen wird, löst sie eine **ArgumentOutOfRangeException**aus.  
  
 Wenn diese Methode mit einem Wert aufgerufen wird, der die Anzahl der Punkte in der Instanz übersteigt, gibt sie NULL zurück.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und `STPointN()` verwendet, um den zweiten Punkt in der Beschreibung der Instanz abzurufen.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
