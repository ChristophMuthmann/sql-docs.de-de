---
title: MinDbCompatibilityLevel (Geography-Datentyp) | Microsoft Docs
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
- MinDbCompatibilityLevel
- MinDbCompatibilityLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geography)
ms.assetid: a9e44748-4a9e-4179-abc4-7631597be5a7
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6c95aafc0278834c6108b99dd67908958fb47b17
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mindbcompatibilitylevel-geography-data-type"></a>MinDbCompatibilityLevel (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt den minimalen Datenbankkompatibilitätsgrad zurück, von dem der **geography** -Datentyp erkannt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
. MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Int**  
  
 CLR-Rückgabetyp: **int**  
  
## <a name="remarks"></a>Hinweise  
 Testen Sie die Kompatibilität eines räumlichen Objekts mithilfe von `MinDbCompatibilityLevel()` , bevor Sie den Kompatibilitätsgrad einer Datenbank ändern. Ein ungültiger **geography** -Typ gibt 110 zurück.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. Testen der Kompatibilität des CircularString-Typs mit Kompatibilitätsgrad 110  
 Das folgende Beispiel testet eine `CircularString` Instanz für die Kompatibilität mit einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 110  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. Testen der Kompatibilität des LineString-Typs mit Kompatibilitätsgrad 100  
 Im folgenden Beispiel wird die Kompatibilität einer `LineString`-Instanz mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] getestet:  
  
```  
DECLARE @g geometry = 'LINESTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 100  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="c-testing-the-value-of-a-geography-instance-for-compatibility"></a>C. Testen der Kompatibilität für den Wert einer geography-Instanz  
 Im folgenden Beispiel werden die Kompatibilitätsgrade für zwei `geography` -Instanzen veranschaulicht. Ein Beispiel ist kleiner als eine Hemisphäre, und das andere ist größer als eine Hemisphäre:  
  
```  
DECLARE @g geography = geography::Parse('POLYGON((0 -10, 120 -10, 240 -10, 0 -10))');  
DECLARE @h geography = geography::Parse('POLYGON((0 10, 120 10, 240 10, 0 10))');  
IF (@g.EnvelopeAngle() >= 90)  
BEGIN  
SELECT @g.MinDbCompatibilityLevel();  
END     
IF (@h.EnvelopeAngle() < 90)  
BEGIN  
SELECT @h.MinDbCompatibilityLevel();  
END  
  
```  
  
 Die erste SELECT-Anweisung gibt 110 zurück, und die zweite SELECT-Anweisung gibt 100 zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [SQL Server-Datenbank-Engine-Abwärtskompatibilität](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
  

