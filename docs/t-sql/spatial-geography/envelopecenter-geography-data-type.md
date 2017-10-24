---
title: EnvelopeCenter (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0638e8793c75ad78aafa12bec1d1f8a3061022c2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt einen Punkt zurück, der als Mittelpunkt eines umschließenden Kreises für die **geography** -Instanz verwendet werden kann.  
  
 Um den umschließenden Kreis festzulegen, wird jeder Punkt in der Instanz als ein Vektor vom Mittelpunkt der Erde zu dem Punkt auf der Erdoberfläche beschrieben. Der Mittelpunkt des umschließenden Kreises wird berechnet, indem der Durchschnitt aller Vektoren ermittelt wird. Für geschlossene Schleifen in einer **polygon** -Instanz oder einer **linestring** -Instanz werden der erste und letzte Punkt nur einmal verwendet.  
  
 Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt einen **point**zurück. Bei Verwendung mit `EnvelopeAngle()`gibt `EnvelopeCenter()` einen umschließenden Kreis einer **geography** -Instanz verwendet werden kann.  
  
> [!NOTE]  
>  `EnvelopeCenter()`Gibt einen umschließenden Kreis für eine **Geography** Instanz, aber die Ergebnisse sind nicht unbedingt den minimalen umschließenden Kreis erstellen. Im Gegensatz dazu ist für die Methode **geometry** vom `STEnvelope()` -Datentyp garantiert, dass sie den minimalen Begrenzungsrahmen zurückgibt, wenn sie auf eine **geometry** -Instanz verwendet werden kann.  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höher gibt die Mitte des Kreises, der den Umschlag dieser Instanz entsprechend den darstellt eine **zeigen**. Für alle großen Objekte, wie von `EnvelopeAngle()` = 180 definiert, wird (90,0) von `EnvelopeCenter()` zurückgegeben.  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  

