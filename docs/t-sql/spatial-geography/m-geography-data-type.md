---
title: M (Geography-Datentyp) | Microsoft Docs
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
- M (geography Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M method
ms.assetid: cdba04f0-4e17-48f6-bafb-b1f918c5a501
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9edb3d7c84fe1f92bb5888e97a782985d05ddd4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="m-geography-data-type"></a>M (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Der **M** (Measure)-Wert der **geography** -Instanz. Die Semantik des Measurewerts ist benutzerdefiniert, beschreibt jedoch im Allgemeinen die Entfernung entlang eines LineString. Zum Beispiel könnte der Measurewert dazu verwendet werden, Kilometersteine an einer Straße mitzuzählen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.M  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Typ: **"float"**  
  
 CLR-Typ: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieser Eigenschaft ist NULL, wenn die **geography** -Instanz kein **Point**ist. Sie ist außerdem NULL für jede **Point** -Instanz, für die sie nicht festgelegt ist.  
  
 Diese Eigenschaft ist schreibgeschützt.  
  
 M-Werte werden in Berechnungen der Bibliothek nicht verwendet und werden nicht durch Berechnungen durchgeführt werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `Point` -Instanz mit Z (Höhe)- und M (Measure)-Werten erstellt und `M` verwendet, um den `M` -Wert der Instanz abzurufen.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  

