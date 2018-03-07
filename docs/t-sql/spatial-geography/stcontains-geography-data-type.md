---
title: STContains (Geography-Datentyp) | Microsoft Docs
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
dev_langs:
- TSQL
helpviewer_keywords:
- STContains method (geography)
ms.assetid: b10e8f0a-2926-449a-82ea-be42543420ca
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a787a75bbf4e9ab54ebc6aab90b64cd74fb50d03
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="stcontains--geography-data-type"></a>STContains (Geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt an, ob die aufrufende **Geography** -Instanz räumlich enthält die **Geography** Instanz, die an die Methode übergeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STContains ( other_geography )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geography*  
 Eine andere **Geography** Instanz mit der Instanz, für die zu vergleichende `STContains()` aufgerufen wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Gibt 1 zurück, wenn die aufrufende **Geography** -Instanz räumlich enthält die **Geography** Instanz an die Methode übergeben, und gibt 0 zurück, wenn dies nicht der Fall. Gibt **null** Wenn der SRID der beiden **Geography** Instanzen stimmen nicht überein.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STContains()` um zwei `geography` -Instanzen daraufhin zu überprüfen, ob die erste Instanz die zweite Instanz enthält.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SET @h = geography::Parse('POINT(-121.703796 46.893985)');  
```  
  
 `SELECT @g.STContains(@h);`  
  
  
