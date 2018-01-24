---
title: MultiLineString | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: spatial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c153fcef8dbec7f8cc516b12af806c4d00488732
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="multilinestring"></a>MultiLineString
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Ein **MultiLineString**-Objekt ist eine Sammlung von null (0) oder mehr **geometry**- oder **geographyLineString**-Instanzen.  
  
## <a name="multilinestring-instances"></a>MultiLineString-Instanzen  
 Die nachfolgende Abbildung enthält Beispiele für **MultiLineString** -Instanzen.  
  
 ![Beispiele für MultiLineString-Geometrieinstanzen](../../relational-databases/spatial/media/multilinestring.gif "Examples of geometry MultiLineString instances")  
  
 Folgendes wird dargestellt:  
  
-   Abbildung 1 zeigt eine einfache **MultiLineString** -Instanz, deren Begrenzung aus den vier Endpunkten ihrer beiden **LineString** -Elemente besteht.  
  
-   Abbildung 2 zeigt eine einfache **MultiLineString** -Instanz, da sich nur die Endpunkte der **LineString** -Elemente überschneiden. Die Begrenzung besteht aus den zwei nicht überlappenden Endpunkten.  
  
-   Abbildung 3 zeigt eine nicht einfache **MultiLineString** -Instanz, da der Innenbereich eines ihrer **LineString** -Elemente geschnitten wird. Die Begrenzung dieser **MultiLineString** -Instanz besteht aus den vier Endpunkten.  
  
-   Abbildung 4 zeigt eine nicht einfache, nicht geschlossene **MultiLineString** -Instanz.  
  
-   Abbildung 5 zeigt eine einfache, nicht geschlossene **MultiLineString**-Instanz. Sie ist nicht geschlossen, da ihre **LineStrings** -Elemente nicht geschlossen sind. Sie ist einfach, da keiner der Innenbereiche der **LineStrings** -Instanzen sich mit anderen überschneidet.  
  
-   Abbildung 6 zeigt eine einfache, geschlossene **MultiLineString** -Instanz. Sie ist geschlossen, weil alle ihre Elemente geschlossen sind. Sie ist einfach, weil keines ihrer Elemente sich im Innenbereich mit anderen überschneidet.  
  
### <a name="accepted-instances"></a>Akzeptierte Instanzen  
 Damit eine **MultiLineString** -Instanz akzeptiert wird, muss sie entweder leer sein, oder sie darf nur aus **LineString** bestehen, die akzeptiert werden. Weitere Informationen über akzeptierte **LineString** -Instanzen finden Sie unter [LineString](../../relational-databases/spatial/linestring.md). In den folgenden Beispielen werden akzeptierte **MultiLineString** -Instanzen veranschaulicht.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 Im folgenden Beispiel wird eine `System.FormatException` ausgelöst, da die zweite **LineString** -Instanz nicht gültig ist.  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>Gültige Instanzen  
 Damit eine **MultiLineString** -Instanz gültig ist, muss sie die folgenden Kriterien erfüllen:  
  
1.  Alle Instanzen, die die **MultiLineString** -Instanz beinhalten, müssen gültige **LineString** -Instanzen sein.  
  
2.  Zwei **LineString** -Instanzen, die die **MultiLineString** -Instanz beinhalten, dürfen sich nicht  im Verlauf eines Intervalls überlappen. Die **LineString** -Instanzen können sich nur mit einer endlichen Anzahl von Punkten überschneiden oder sich selbst oder andere **LineString** -Instanzen berühren.  
  
 Im folgenden Beispiel werden drei gültige **MultiLineString** -Instanzen und eine nicht gültige **MultiLineString** -Instanz gezeigt.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` ist nicht gültig, da die zweite **LineString** -Instanz die erste **LineString** -Instanz in einem Intervall überlappt. Sie berühren sich mit einer unendlichen Anzahl von Punkten.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine einfache `geometry``MultiLineString` -Instanz erstellt, die zwei `LineString` -Elemente mit der SRID 0 enthält.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
 Um diese Instanz mit einem anderen SRID zu instanziieren, verwenden Sie `STGeomFromText()` oder `STMLineStringFromText()`. Sie können auch `Parse()` verwenden und den SRID dann ändern, wie im folgenden Beispiel gezeigt.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [STLength &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STIsClosed &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)   
 [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
