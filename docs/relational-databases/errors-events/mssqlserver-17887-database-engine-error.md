---
title: MSSQLSERVER_17887 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 3fce6828cbb09c0677d3beaf76f4441a2fbf1334
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17887"></a>MSSQLSERVER_17887
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|17887|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SRV_IO_COMP_LISTENER_NONYIELDING|  
|Meldungstext|E/A-Abschlussüberwachung (0x%lx) Arbeitsthread 0x%p stellt im Knoten %ld kein Ergebnis bereit. Ungefähre CPU-Belegung: Kernel %I64d Millisek., Benutzer %I64d Millisek., Intervall: %I64d.|  
  
## <a name="explanation"></a>Erklärung  
Kennzeichnet ein mögliches Problem mit der E/A-Abschlussportüberwachung an dem spezifischen Knoten, wenn die E/A-Abschlussroutine für ein Netzwerk-Lese-/Schreibereignis ausgeführt wird. Dieser Fehler wird behoben, wenn die E/A-Abschlussportüberwachung nach der Ausführung der E/A-Abschlussroutine zurückgegeben wird.  
  
## <a name="user-action"></a>Benutzeraktion  
Wenden Sie sich an den Microsoft-Kundendienst (Customer Support Services, CSS).  
  
