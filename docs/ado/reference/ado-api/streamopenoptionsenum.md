---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 268d495d2163d03244a6bec57762b93a26ab32ea
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Gibt Optionen zum Öffnen einer [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt. Die Werte können mit einer OR-Operation kombiniert werden.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Öffnet die **Stream** Objekt im asynchronen Modus ausgeführt.|  
|**adOpenStreamFromRecord**|4|Identifiziert den Inhalt der *Quelle* Parameter bereits geöffnet sein [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt. Das Standardverhalten besteht, behandeln *Quelle* als eine URL, die direkt mit einem Knoten in einer Struktur verweist. Der diesem Knoten zugeordnete Standarddatenstrom wird geöffnet.|  
|**adOpenStreamUnspecified**|-1|Standard. Gibt an, öffnen die **Stream** Objekt mit den Standardoptionen.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [Open-Methode (ADO-Datenstrom)](../../../ado/reference/ado-api/open-method-ado-stream.md)

