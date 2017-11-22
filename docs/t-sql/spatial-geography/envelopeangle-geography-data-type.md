---
title: EnvelopeAngle (Geography-Datentyp) | Microsoft Docs
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
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs: TSQL
helpviewer_keywords: EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 41e560a4fa5ad869d126a1e594b57b96dc0f1558
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den maximalen Winkel zwischen dem durch `EnvelopeCenter()` zurückgegebenen Punkt und einem Punkt in der **geography** -Instanz in Grad zurück.  
  
 Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **"float"**  
  
 CLR-Rückgabetyp: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt einen Punkt in der **geography** -Instanz in Grad zurück. Bei Verwendung mit EnvelopeCenter(), `EnvelopeAngle()` gibt einen umschließenden Kreis einer **Geography** Instanz.  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], diese Methode wurde erweitert und **FullGlobe** Instanzen.  
  
 Die hemisphäreneinschränkung auf `EnvelopeAngle()` in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wurde entfernt. Bei Instanzen, deren Winkel 90 Grad übersteigt, wird jedoch 180 Grad zurückgegeben. `EnvelopeAngle()`ist nicht exakt für **Geography** Instanzen, die mehr als eine Hemisphäre umfassen.  
  
## <a name="examples"></a>Beispiele  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
