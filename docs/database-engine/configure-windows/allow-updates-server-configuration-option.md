---
title: Updates zulassen (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: af6c995607abbc672b5f27e425dbd661204153fb
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="allow-updates-server-configuration-option"></a>Updates zulassen (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Diese Option ist in der gespeicherten Prozedur **sp_configure** weiterhin vorhanden, obwohl ihre Funktionalität nicht in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zur Verfügung steht. (Die Einstellung hat keine Auswirkungen.) Für Systemtabellen werden keine direkten Updates unterstützt.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Wird die Option **Updates zulassen** geändert, führt dies zu einem Fehler bei der RECONFIGURE-Anweisung. Änderungen an der Option **Updates zulassen** sollten aus allen Skripts entfernt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  

