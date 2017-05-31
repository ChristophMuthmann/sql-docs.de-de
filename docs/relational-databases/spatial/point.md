---
title: Punkt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Point geometry subtype [SQL Server]
- geometry data type [SQL Server], spatial data
ms.assetid: 2a596ec4-8b2f-4962-bcb4-e5c8f77edad5
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3ab4b354292130b01c73f771c221a13b595bdbdc
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="point"></a>Punkt
  In räumlichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten ist ein **Punkt** ein nulldimensionales Objekt, das eine einzelne Position darstellt und einen Z-Wert (Höhe) und einen M-Wert (Maßeinheit) enthalten kann.  
  
## <a name="geography-data-type"></a>geography-Datentyp  
 Der Point-Typ für den geography-Datentyp stellt einen einzelnen Ort dar, wobei *Lat* für den Breitengrad und *Long* für den Längengrad steht. Die Werte für die Breite und Länge werden in Grad gemessen. Die Werte für den Breitengrad liegen immer im Bereich [-90, 90], und eingegebene Werte, die außerhalb dieses Bereichs liegen, lösen eine Ausnahme aus. Werte für den Längengrad liegen immer im Bereich [-180, 180], und eingegebene Werte, die außerhalb dieses Bereichs liegen, werden entsprechend angepasst. Wird etwa für den Längengrad der Wert 190 eingegeben, wird dieser Wert automatisch in den Wert -170 konvertiert. *SRID* stellt die SRID (Spatial Reference ID) der **geography** -Instanz dar, die Sie zurückgeben möchten.  
  
## <a name="geometry-data-type"></a>geometry-Datentyp  
 Der Point-Typ für den geometry-Datentyp stellt einen einzelnen Ort dar, wobei *X* die X-Koordinate und *Y* die Y-Koordinate des generierten Punkts darstellt. *SRID* stellt die SRID (Spatial Reference ID) der **geometry** -Instanz dar, die Sie zurückgeben möchten.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine einfache `geometry Point`-Instanz erstellt, die den Punkt (3, 4) mit dem SRID 0 darstellt.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT (3 4)', 0);  
```  
  
 Im nächsten Beispiel wird eine `geometry``Point` -Instanz erstellt, die den Punkt (3, 4) mit dem Z-Wert (Höhe) 7, dem M-Wert (Maßeinheit) 2,5 und dem Standard-SRID 0 darstellt.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 7 2.5)');  
```  
  
 Im abschließenden Beispiel werden die Werte X, Y, Z, und M für die `geometry``Point` -Instanz zurückgegeben.  
  
```  
SELECT @g.STX;  
SELECT @g.STY;  
SELECT @g.Z;  
SELECT @g.M;  
```  
  
 Z-Wert und M-Wert können explizit als NULL angegeben werden, wie im folgenden Beispiel gezeigt.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 NULL NULL)');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MultiPoint](../../relational-databases/spatial/multipoint.md)   
 [STX &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
