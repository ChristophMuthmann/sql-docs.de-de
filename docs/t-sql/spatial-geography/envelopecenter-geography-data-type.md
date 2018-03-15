---
title: EnvelopeCenter (geography-Datentyp) | Microsoft-Dokumentation
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
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb0e6dbe7e93aa0ee4b6f124621b97d255d185cc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt einen Punkt zurück, der als Mittelpunkt eines umschließenden Kreises für die **geography** -Instanz verwendet werden kann.  
  
 Um den umschließenden Kreis festzulegen, wird jeder Punkt in der Instanz als ein Vektor vom Mittelpunkt der Erde zu dem Punkt auf der Erdoberfläche beschrieben. Der Mittelpunkt des umschließenden Kreises wird berechnet, indem der Durchschnitt aller Vektoren ermittelt wird. Für geschlossene Schleifen in einer **polygon** -Instanz oder einer **linestring** -Instanz werden der erste und letzte Punkt nur einmal verwendet.  
  
 Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Diese Methode gibt einen **point**zurück. Bei Verwendung mit `EnvelopeAngle()`gibt `EnvelopeCenter()` einen umschließenden Kreis einer **geography** -Instanz verwendet werden kann.  
  
> [!NOTE]  
>  `EnvelopeCenter()`gibt einen umschließenden Kreis für eine **geography**-Instanz zurück. Es wird jedoch nicht garantiert, dass die Ergebnisse den minimalen umschließenden Kreis erstellen. Im Gegensatz dazu ist für die Methode **geometry** vom `STEnvelope()` -Datentyp garantiert, dass sie den minimalen Begrenzungsrahmen zurückgibt, wenn sie auf eine **geometry** -Instanz verwendet werden kann.  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höher wird der Mittelpunkt des Kreises zurückgegeben, der den Umschlag dieser Instanz als **point** darstellt. Für alle großen Objekte, wie von `EnvelopeAngle()` = 180 definiert, wird (90,0) von `EnvelopeCenter()` zurückgegeben.  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
