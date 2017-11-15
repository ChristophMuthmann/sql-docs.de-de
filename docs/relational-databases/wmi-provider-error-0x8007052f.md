---
title: WMI-Fehler 0x8007052f | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 050f4c13d5c7c5f232cca65dd38dbcfcdb27c5bb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="wmi-provider-error-0x8007052f"></a>WMI-Anbieterfehler 0x8007052f
    
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|0x8007052f|  
|Ereignisquelle|WMI-Anbieterfehler|  
|Komponente|SQL Server-Konfigurations-Manager|  
|Symbolischer Name|NA|  
|Meldungstext|Anmeldefehler: Eingeschränktes Benutzerkonto. Mögliche Ursachen hierfür sind, dass leere Kennwörter nicht zulässig sind, Einschränkungen der Anmeldezeiten vorliegen oder eine Richtlinieneinschränkung erzwungen wurde.|  
  
## <a name="explanation"></a>Erklärung  
 Dieser Fehler kann auftreten, wenn der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konfigurations-Manager verwendet wird, um zu den integrierten Konten zu wechseln (Netzwerkdienst, Lokaler Dienst oder Lokales System), während [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Windows Server 2003-Cluster oder einem Windows Server-Domänencontroller ausgeführt wird. Führen Sie Dienste auf einem Windows Server-Cluster oder einem Windows Server-Domänencontroller nicht unter integrierten Konten aus. Empfehlungen zu Dienstkonten finden Sie unter "Einrichten von Windows-Dienstkonten" in der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="user-action"></a>Benutzeraktion  
 Konfigurieren Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für die Verwendung eines Domänenkontos.  
  
  
