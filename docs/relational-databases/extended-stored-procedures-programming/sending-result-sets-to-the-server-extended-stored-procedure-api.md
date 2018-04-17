---
title: Senden von Resultsets an den Server (API für erweiterte gespeicherte Prozeduren) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 517b016376ac89c37c237257d26c9c5f9d12c6e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Senden von Resultsets an den Server (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Beim Senden eines Resultsets zum [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die erweiterte gespeicherte Prozedur sollte die entsprechende API wie folgt aufrufen:  
  
-   Die **Srv_sendmsg** Funktion kann in beliebiger Reihenfolge aufgerufen werden, bevor oder nachdem alle Zeilen (sofern vorhanden) mit gesendet wurden **Srv_sendrow**. Alle Nachrichten müssen an den Client gesendet werden, bevor der Abschlussstatus mit gesendet wird **Srv_senddone**.  
  
-   Die **srv_sendrow** -Funktion wird einmal für jede an den Client gesendete Zeile aufgerufen. Alle Zeilen müssen gesendet werden, an den Client, bevor Nachrichten, Statuswerte oder Abschlussstatus mit gesendet werden **Srv_sendmsg**, **Srv_status** Argument **Srv_pfield**, oder **Srv_senddone**.  
  
-   Beim Senden einer Zeile, die nicht alle Spalten, die mit hatte **Srv_describe** bewirkt, dass die Anwendung eine informationsfehlermeldung an und gibt FAIL zurück an den Client. In diesem Fall wird die Zeile nicht gesendet.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen erweiterter gespeicherter Prozeduren](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
