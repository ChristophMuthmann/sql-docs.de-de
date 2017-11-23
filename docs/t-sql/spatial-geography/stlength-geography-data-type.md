---
title: STLength (Geography-Datentyp) | Microsoft Docs
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
- STLength (geography Data Type)
- STLength_TSQL
dev_langs: TSQL
helpviewer_keywords: STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa8b74ee4f1eec0b9bfb6f85dad0d8c335e15909
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stlength-geography-data-type"></a>STLength (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt die Gesamtlänge der Elemente in einer **geography** -Instanz oder der **geography** in einer **GeometryCollection**zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **"float"**  
  
 CLR-Rückgabetyp: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine **geography** -Instanz geschlossen ist, wird ihre Länge als Gesamtlänge um die Instanz herum berechnet. Die Länge eines Polygons entspricht seinem Umfang und die Länge eines Punkts ist 0. Die Länge einer **GeometryCollection** wird ermittelt, indem die Summe der Längen aller in der Auflistung enthaltenen **geography** -Instanzen berechnet wird.  
  
 STLength() funktioniert sowohl für gültige als auch für ungültige LineStrings. In der Regel ist ein LineString aufgrund überlappender Segmente ungültig, die möglicherweise durch Anomalien wie ungenaue GPS-Ablaufverfolgungen verursacht werden. STLength() entfernt keine überlappenden oder ungültigen Segmente. Sie schließt überlappende und ungültige Segmente in den zurückgegebenen Längenwert ein. Die MakeValid()-Methode kann überlappende Segmente aus einem LineString entfernen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und `STLength()` verwendet, um die Länge der Instanz zu bestimmen.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
