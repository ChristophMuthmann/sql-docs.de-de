---
title: BufferWithTolerance (geometry-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/03/2017
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
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 941eb7f9cdf39475631b8ab45789cd2082ad3084
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt ein geometrisches Objekt zurück, dass die Vereinigung aller Punktwerte darstellt, deren Abstand zu einer **geometry** -Instanz kleiner oder gleich einem angegebenen Wert ist, wobei eine angegebene Toleranz gewährt wird.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumente  
 *distance*  
 Ein **float** -Ausdruck, der den Abstand zu der **geometry** -Instanz angibt, um die der Puffer berechnet werden soll.  
  
 *tolerance*  
 Ein **float** -Ausdruck, der die Toleranz des Pufferabstands angibt.  
  
 *Toleranz* verweist auf die maximale Variation im idealen Pufferabstand für die zurückgegebene lineare Näherung.  
  
 Beispielsweise kann der ideale Pufferabstand eines Punkts ein Kreis sein, dieser muss jedoch durch ein Polygon näherungsweise angegeben werden. Je geringer die Toleranz, desto mehr Punkte hat das Polygon, wodurch die Komplexität des Ergebnisses erhöht, der Fehler jedoch verringert wird.  
  
 *relative*  
 Ein **bit** , das angibt, ob der *tolerance* -Wert relativ oder absolut ist. Wenn 'TRUE' oder 1, ist die Toleranz relativ und wird als Produkt des *tolerance* -Parameters und des Durchmessers des umgebenden Felds der Instanz berechnet. Wenn 'FALSE' oder 0, ist die Toleranz absolut und der *tolerance* -Wert ist die absolute maximale Variation im idealen Pufferabstand für die zurückgegebene lineare Näherung.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geometry**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="exceptions"></a>Ausnahmen  
 Der *tolerance* -Parameter muss größer als 0 sein. Wenn *tolerance* <= 0, wird `System.ArgumentOutOfRangeException` ausgelöst.  
  
> [!NOTE]  
>  Da *tolerance* is a **float** ist, kann aufgrund der Rundungsprobleme mit Gleitkommatypen eine `System.Runtime.InteropServices.COMException` ausgelöst werden, wenn der angegebene Toleranzwert sehr klein ist.  
  
## <a name="remarks"></a>Remarks  
 Wenn *distance* > 0, wird eine **Polygon**- oder **MultiPolygon**-Instanz zurückgegeben.  
  
> [!NOTE]  
>  Da der Abstand vom Typ **float**ist, kann ein sehr kleiner Wert in den Berechnungen mit 0 gleichgesetzt werden. In diesem Fall wird eine Kopie der aufrufenden Instanz von **geometry** zurückgegeben. Informationen hierzu finden Sie unter [float und real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Wenn *distance* = 0 ist, wird eine Kopie der aufrufenden Instanz von **geometry** zurückgegeben.  
  
 Wenn *distance* < 0, gilt Folgendes:  
  
-   Es wird eine leere Instanz von **GeometryCollection** zurückgegeben, wenn die Dimensionen der Instanz 0 oder 1 betragen.  
  
-   Ein negativer Puffer wird zurückgegeben, wenn die Dimensionen der Instanz 2 oder mehr betragen.  
  
    > [!NOTE]  
    >  Ein negativer Puffer erstellt auch möglicherweise eine leere Instanz von **GeometryCollection** .  
  
 Ein negativer Puffer entfernt alle Punkte innerhalb des angegebenen Abstands von der Begrenzung der **geometry** -Instanz.  
  
 Die Abweichung zwischen dem theoretischen und dem berechnetem Puffer beträgt max(tolerance, extents \* 1,0E-7), wobei die Toleranz der Wert des Parameters *tolerance* ist. Weitere Informationen zu Erweiterungen finden Sie unter [geometry-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `Point` -Instanz erstellt und `BufferWithTolerance()` verwendet, um einen groben Puffer um die Instanz zu erhalten.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [STBuffer &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [Erweiterte Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

