---
title: MakeValid (Geography-Datentyp) | Microsoft Docs
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
dev_langs: TSQL
helpviewer_keywords: MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: becd452525b999e0a23810aefd2455ee74ab0c67
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="makevalid-geography-data-type"></a>MakeValid (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Konvertiert eine **Geography** -Instanz, die nicht in eine gültige ist **Geography** Instanz mit einem gültigen Open Geospatial Consortium (OGC)-Typ.  
  
 Wenn ein Eingabeobjekt für STIsValid(), "false" zurückgibt `MakeValid()` konvertiert die Instanz, die auf eine gültige Instanz ungültig ist.  
  
 Diese geography-Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode ändert möglicherweise den Typ, der die **Geography** Instanz. Darüber hinaus die Punkte einer **Geography** Instanz möglicherweise geringfügige Verschiebung. Die Ergebnisse einiger Methoden wie z. B. NumPoint() können geändert werden.  
  
 In Fällen, bei denen die ungültige räumliche Instanz den Äquator und eine EnvelopeAngle() = 180, eine **FullGlobe** Instanz zurückgegeben werden. Die `MakeValid()` **Geography** -Datentypmethode wird versucht, gültige Instanzen zurückzugeben, aber die Ergebnisse sind nicht unbedingt genau oder präzise sein.  
  
> [!NOTE]  
>  Objekte, die nicht gültig sind, können in der Datenbank gespeichert werden. Die Methoden, die für ungültige Instanzen ausgeführt werden kann (diese Instanzen für die STIsValid() "false" zurück) werden, die Gültigkeit überprüfen oder Exporte ermöglichen: STIsValid(), MakeValid() STAsText(), STAsBinary(), ToString(), AsTextZM() und AsGml().  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
 Im ersten Beispiel wird eine ungültige `LineString` -Instanz erstellt, die sich selbst überlappt. Mithilfe von `STIsValid()` wird die Ungültigkeit dieser Instanz bestätigt. `STIsValid()`Gibt den Wert 0 für eine ungültige Instanz.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 4326);  
SELECT @g.STIsValid();  
```  
  
 Im zweiten Beispiel wird die Instanz mit `MakeValid()` gültig gemacht, und die tatsächliche Gültigkeit wird überprüft. `STIsValid()`Gibt den Wert 1 für eine gültige Instanz zurück.  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 Das dritte Beispiel überprüft, ob die Instanz zu einer gültigen Instanz geändert wurde.  
  
```  
SELECT @g.ToString();  
```  
  
 Wenn in diesem Beispiel die `LineString` -Instanz ausgewählt wird, werden die Werte als gültige `MultiLineString` -Instanz zurückgegeben.  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
## <a name="see-also"></a>Siehe auch  
 [STIsValid &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
