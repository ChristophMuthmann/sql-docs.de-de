---
title: Updates zulassen (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f874caf6697a12e7988a9ae3a2ead4be13a97aa1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="allow-updates-server-configuration-option"></a>Updates zulassen (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Diese Option ist in der gespeicherten Prozedur **sp_configure** weiterhin vorhanden, obwohl ihre Funktionalität nicht in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zur Verfügung steht. (Die Einstellung hat keine Auswirkungen.) Für Systemtabellen werden keine direkten Updates unterstützt.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Wird die Option **Updates zulassen** geändert, führt dies zu einem Fehler bei der RECONFIGURE-Anweisung. Änderungen an der Option **Updates zulassen** sollten aus allen Skripts entfernt werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
