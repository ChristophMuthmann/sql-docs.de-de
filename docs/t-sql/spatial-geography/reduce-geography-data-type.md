---
title: Reduce (geography-Datentyp) | Microsoft-Dokumentation
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
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f1301c5625554d2e023c9abd75bb57fec43827b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="reduce-geography-data-type-"></a>Reduce (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt einen Näherungswert der gegebenen **geography** -Instanz zurück. Dieser Näherungswert wird unter Verwendung des Douglas-Peucker-Algorithmus mit der angegebenen Toleranz ermittelt.  
  
 Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumente  
  
|||  
|-|-|  
|Begriff|Definition|  
|*tolerance*|Ein Wert vom Typ **float**. *tolerance* ist die Toleranz, die für den Douglas-Peucker-Algorithmus angegeben wird. *tolerance* muss eine positive Zahl sein.|  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Bei Auflistungstypen arbeitet dieser Algorithmus unabhängig für jeden **geography** -Wert, der in der Instanz enthalten ist. Dieser Algorithmus ändert keine **Point** -Instanzen.  
  
 Diese Methode versucht, die Endpunkte von **LineString** -Instanzen beizubehalten. Dies kann aber fehlschlagen, um ein gültiges Ergebnis zu erhalten.  
  
 Wenn `Reduce()` mit einem negativen Wert aufgerufen wird, erzeugt diese Methode eine **ArgumentException**. In `Reduce()` verwendete Toleranzen müssen positive Zahlen sein.  
  
 Der Douglas-Peucker-Algorithmus kann für jede Kurve oder jeden Ring in der **geography** -Instanz verwendet werden, indem alle Punkte mit Ausnahme des Start- und Endpunkts entfernt werden. Anschließend wird jeder entfernte Punkt erneut hinzugefügt, beginnend mit dem äußersten Punkt, bis kein Punkt mehr als *tolerance* vom Ergebnis entfernt ist. Das Ergebnis wird dann gegebenenfalls gültig gemacht, da ein gültiges Ergebnis garantiert wird.  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] wurde diese Methode auf **FullGlobe**-Instanzen erweitert.  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und `Reduce()` verwendet, um die Instanz zu vereinfachen.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
