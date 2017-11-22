---
title: MSSQLSERVER_5554 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f5b8dd08230e8fbb22961dafc4b469acedcac05
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver5554"></a>MSSQLSERVER_5554
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|MSSQLSERVER|  
|Ereignis-ID|5554|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|FS_MINIVER_OVERFLOW|  
|Meldungstext|Das maximale Limit des Dateisystems an Versionen insgesamt für eine einzige Datei wurde erreicht.|  
  
## <a name="explanation"></a>Erklärung  
In MARS (Multiple Active Result Sets) oder Triggerszenarios verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Miniversion des Betriebssystems.  
  
## <a name="user-action"></a>Benutzeraktion  
Versuchen Sie, wiederholte Datenupdates in derselben Transaktion zu vermeiden.  
  
