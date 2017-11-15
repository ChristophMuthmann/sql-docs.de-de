---
title: MSSQLSERVER_17084 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 0e01e53b34548e6825f215f63616f146ecccc7c9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17084"></a>MSSQLSERVER_17084
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|17084|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|P3_ATOMIC_WITH_MISSING_OPTION|  
|Meldungstext|Die WITH-Klausel der Anweisung BEGIN ATOMIC muss einen Wert für die Option "%ls" angeben.|  
  
## <a name="explanation"></a>Erklärung  
Die WITH-Klausel der Anweisung BEGIN ATOMIC gab keinen Wert für eine Option an.  
  
## <a name="user-action"></a>Benutzeraktion  
**ATOMIC**-Blöcke erfordern Werte für die **WITH**-Optionen **TRANSACTION ISOLATION LEVEL** und **LANGUAGE**. Beispiel:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N’us_english’)  
```  
  
Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Siehe auch  
[In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
