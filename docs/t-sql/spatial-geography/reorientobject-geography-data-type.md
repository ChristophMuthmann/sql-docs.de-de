---
title: ReorientObject (Geography-Datentyp) | Microsoft Docs
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
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f132cc69c1e4acdf20fbcf88280c212fc1a13ca
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt eine **geography** -Instanz mit ausgetauschtem inneren und äußeren Bereich zurück.  
  
 Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.ReorientObject (geography)  
```  
  
## <a name="arguments"></a>Argumente  
 *geography*  
 Eine andere Instanz von **geography** , für die `ReorientObject()` aufgerufen wird.  
  
## <a name="return-value"></a>Rückgabewert  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Mit dieser Methode wird die Ringausrichtung aller **Polygons** in eine **GeometryCollection** geändert, ohne **Points** oder **Linestrings** in der angegebenen Auflistung zu ändern.  
  
 Wenn eine **GeometryCollection** an die Methode übergeben wird, werden alle Instanzen in der Auflistung neu ausgerichtet, die Auflistung als Ganzes wird jedoch nicht neu ausgerichtet.  
  
## <a name="examples"></a>Beispiele  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
