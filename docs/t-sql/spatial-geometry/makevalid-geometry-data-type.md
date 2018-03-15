---
title: MakeValid (geometry-Datentyp) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/03/2017
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
- MakeValid
- MakeValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid (geometry Data Type)
ms.assetid: 38673010-ab77-4ebb-9c4d-b26b79e3b7ea
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0694b49b23d87d30e7134c822de295ec5b840544
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="makevalid-geometry-data-type"></a>MakeValid (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Konvertiert eine ungültige **geometry** -Instanz in eine **geometry** -Instanz mit einem gültigen Open Geospatial-Consortium (OGC)-Typ.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geometry**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Diese Methode verursacht möglicherweise eine Änderung des Typs der **geometry** -Instanz sowie eine leichte Verschiebung der Punkte einer **geometry** -Instanz.  
  
## <a name="examples"></a>Beispiele  
 Im ersten Beispiel wird eine ungültige `LineString` -Instanz erstellt, die sich selbst überlappt. Mithilfe von `STIsValid()` wird die Ungültigkeit dieser Instanz bestätigt. `STIsValid()` gibt für eine ungültige Instanz den Wert 0 (null) zurück.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 0);  
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
  
 Im folgenden Beispiel wird eine CircularString-Instanz in eine Point-Instanz konvertiert.  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 1 1, 1 1)';  
SELECT @g.MakeValid().ToString();  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [STIsValid &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Erweiterte Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

