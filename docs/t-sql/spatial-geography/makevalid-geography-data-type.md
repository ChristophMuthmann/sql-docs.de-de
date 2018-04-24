---
title: MakeValid (geography-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c6990890ddfbd95a3cda0d31fe6376cbea4f82f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="makevalid-geography-data-type"></a>MakeValid (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Konvertiert eine ungültige **geography**-Instanz in eine gültige **geography**-Instanz mit einem gültigen Open Geospatial-Consortium-Typ (OGC).  
  
 Wenn von einem Eingabeobjekt FALSE für STIsValid() zurückgegeben wird, konvertiert `MakeValid()` die ungültige in eine gültige Instanz.  
  
 Diese geography-Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Diese Methode ändert möglicherweise den Typ der Instanz von **geography**. Darüber hinaus ist eine geringfügige Verschiebung der Punkte der Instanz von **geography** möglich. Die Ergebnisse einiger Methoden wie NumPoint() können sich ändern.  
  
 In Fällen, in denen die ungültige räumliche Instanz den Äquator schneidet und einen EnvelopeAngle() = 180 aufweist, wird eine Instanz von **FullGlobe** zurückgegeben. Die `MakeValid()`**geography**-Datentypmethode versucht, gültige Instanzen zurückzugeben. Die Richtigkeit oder Vollständigkeit der Ergebnisse kann jedoch nicht garantiert werden.  
  
> [!NOTE]  
>  Objekte, die nicht gültig sind, können in der Datenbank gespeichert werden. Für ungültige Instanzen (für die von STIsValid() FALSE zurückgegeben wird) können Methoden verwendet werden, die die Gültigkeit überprüfen oder Exporte ermöglichen: STIsValid(), MakeValid(), STAsText(), STAsBinary(), ToString(), AsTextZM() und AsGml().  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
 Im ersten Beispiel wird eine ungültige `LineString` -Instanz erstellt, die sich selbst überlappt. Mithilfe von `STIsValid()` wird die Ungültigkeit dieser Instanz bestätigt. `STIsValid()` gibt für eine ungültige Instanz den Wert 0 (null) zurück.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 4326);  
SELECT @g.STIsValid();  
```  
  
 Im zweiten Beispiel wird die Instanz mit `MakeValid()` gültig gemacht, und die tatsächliche Gültigkeit wird überprüft. `STIsValid()` gibt für eine gültige Instanz den Wert 1 zurück.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [STIsValid &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
