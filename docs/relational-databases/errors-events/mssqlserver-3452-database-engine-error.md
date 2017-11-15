---
title: MSSQLSERVER_3452 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 52865b3a6a4a036acafffa97cff5d0fbc6abbbf9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3452"></a>MSSQLSERVER_3452
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3452|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|REC_CHECKIDENTITY|  
|Meldungstext|Bei der Wiederherstellung der '%.*ls'-Datenbank (%d) wurden mögliche inkonsistente Identitätswerte in der Tabelle mit der ID %d erkannt. Führen Sie DBCC CHECKIDENT ('%.\*ls') aus.|  
  
## <a name="explanation"></a>Erklärung  
Beim Upgrade auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] wurde vom Prozess zum Wiederherstellen der Identitätswerte in der Datenbank eine Inkonsistenz in den Metadaten festgestellt.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie DBCC CHECKIDENT aus.  
  
