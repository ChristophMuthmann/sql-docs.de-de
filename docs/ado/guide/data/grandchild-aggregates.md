---
title: Untergeordnete Aggregate | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8889be6c78765d7eadf211016de92d041c9419f3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="grandchild-aggregates"></a>Untergeordnete Aggregate
In einer-Klausel einer Shape-Befehl erstellte Kapitelspalte zugewiesen werden kann ein *Kapitel-Aliasnamen* (in der Regel mit dem AS-Schlüsselwort). Bestimmen Sie eine Spalte in jeder der geformten Kapitel **Recordset** mit einem vollqualifizierten Namen, der das untergeordnete Element mit der Spalte identifiziert. Beispielsweise enthält das übergeordnete Kapitel Kap1, untergeordnete Kapitel Kap2, besitzt eine Mengenspalte "Amt" und dann der qualifizierte Namen wäre chap1.chap2.amt. Der qualifizierte Name kann dann als Argument für einen der Aggregatfunktionen (SUM, AVG, MAX, MIN, COUNT, STDEV oder alle) verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Data Shaping Example (Beispiele der Datenstrukturierung)](../../../ado/guide/data/data-shaping-example.md)
