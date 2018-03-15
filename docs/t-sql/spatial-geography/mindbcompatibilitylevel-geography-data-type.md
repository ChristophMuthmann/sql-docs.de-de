---
title: MinDbCompatibilityLevel (geography-Datentyp) | Microsoft-Dokumentation
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
- MinDbCompatibilityLevel
- MinDbCompatibilityLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geography)
ms.assetid: a9e44748-4a9e-4179-abc4-7631597be5a7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 76ee741885646f8df0a84f93bb41f0de0f027e79
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="mindbcompatibilitylevel-geography-data-type"></a>MinDbCompatibilityLevel (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt den minimalen Datenbankkompatibilitätsgrad zurück, von dem der **geography** -Datentyp erkannt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
. MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **int**  
  
 CLR-Rückgabetyp: **int**  
  
## <a name="remarks"></a>Remarks  
 Testen Sie die Kompatibilität eines räumlichen Objekts mithilfe von `MinDbCompatibilityLevel()` , bevor Sie den Kompatibilitätsgrad einer Datenbank ändern. Ein ungültiger **geography** -Typ gibt 110 zurück.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. Testen der Kompatibilität des CircularString-Typs mit Kompatibilitätsgrad 110  
 Im folgenden Beispiel wird die Kompatibilität einer `CircularString`-Instanz mit einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] getestet:  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Abwärtskompatibilität der SQL Server-Datenbank-Engine](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
  
