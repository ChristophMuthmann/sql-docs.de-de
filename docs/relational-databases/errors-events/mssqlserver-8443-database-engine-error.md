---
title: MSSQLSERVER_8443 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 91c13057d0aa37e88e074babcb5261dda7736e4d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|8443|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SB_DIALOG_WO_CONV_GROUP|  
|Meldungstext|Die Konversation mit der ID '%.*ls' und dem Initiator %d verweist auf die fehlende Konversationsgruppe '%.\*ls'. Führen Sie DBCC CHECKDB aus, um die Datenbank zu analysieren und zu reparieren.|  
  
## <a name="explanation"></a>Erklärung  
Von der Metadatenebene wurde NULL für die Konversationsgruppe zurückgegeben. Die Datenbank wurde in irgendeiner Weise beschädigt. Eine mögliche Ursache für eine Beschädigung kann ein Datenträgerfehler sein.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie DBCC CHECKDB im Reparaturmodus aus, um die Datenbank wieder in einen konsistenten Zustand zu bringen. Möglicherweise werden dabei Meldungen gelöscht, um die Konsistenz wiederherzustellen. Untersuchen Sie die Systemfehlerprotokolle, um festzustellen, ob dieser Fehler durch einen anderen Fehler im System verursacht wurde.  
  

