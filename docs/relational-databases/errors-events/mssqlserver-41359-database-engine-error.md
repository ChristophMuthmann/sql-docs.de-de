---
title: MSSQLSERVER_41359 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: d968578a85366ab4fb6c72057434473dc5a0e909
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver41359"></a>MSSQLSERVER_41359
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|41359|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQL_READ_COMMITTED_SNAPSHOT_NOT_SUPPORTED|  
|Meldungstext|Eine Abfrage, die auf speicheroptimierte Tabellen mit der READ COMMITTED-Isolationsstufe zugreift, kann auf datenträgerbasierte Tabellen nicht zugreifen, wenn die Datenbankoption READ_COMMITTED_SNAPSHOT auf ON gesetzt ist. Geben Sie eine unterstützte Isolationsstufe für die speicheroptimierte Tabelle mithilfe eines Tabellentipps wie WITH (SNAPSHOT) an.|  
  
## <a name="explanation"></a>Erklärung  
Die Datenbank mit READ_COMMITTED_SNAPSHOT=ON unterstützt nicht die Transaktionen, die sowohl auf speicheroptimierte Tabellen als auch auf datenträgerbasierte Tabellen zugreifen.  
  
## <a name="user-action"></a>Benutzeraktion  
Setzen Sie READ_COMMITTED_SNAPSHOT auf OFF oder stellen Sie eine unterstützte Isolationsstufe für die speicheroptimierte Tabelle mithilfe eines Tipps auf Tabellenebene wie WITH (SNAPSHOT) bereit. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Siehe auch  
[In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
