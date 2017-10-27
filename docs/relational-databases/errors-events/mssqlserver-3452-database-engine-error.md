---
title: MSSQLSERVER_3452 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 61fbabc84b9ef22a7275faa4ab2c04b208466193
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

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
  

