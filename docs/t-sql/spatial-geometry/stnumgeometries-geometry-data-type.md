---
title: STNumGeometries (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
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
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs: TSQL
helpviewer_keywords: STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4094aa647ddfa3bf5ffaf191896c9e65677f027
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die Anzahl von Geometrien zurück eine **Geometrie** Instanz.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Int**  
  
 CLR-Rückgabetyp: **SqlInt32**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt 1 zurück, wenn die **Geometrie** -Instanz ist eine **MultiPoint**, **MultiLineString**, **MultiPolygon**, oder  **GeometryCollection** -Instanz, und 0, wenn die **Geometrie** -Instanz leer ist.  
  
> [!NOTE]  
>  Wenn eine **GeometryCollection** geschachtelte leere Elemente `STNumGeometries()` nicht 0 zurück. Obwohl die Elemente in der **GeometryCollection** Instanz leer sind, ist die Instanz selbst ist ein leeres Resultset.  
  
  

