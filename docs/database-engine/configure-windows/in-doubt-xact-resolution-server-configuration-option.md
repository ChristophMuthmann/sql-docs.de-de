---
title: "Lösung für unklare Transaktion (Serverkonfigurationsoption) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- distributed transactions [SQL Server], unresolved transactions
- unresolved transactions
- in-doubt xact resolution option
ms.assetid: 3426fd32-cad2-4f2f-8ca9-e0296cc12703
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9fd01be5efcc847708bb7f12f2e9eb5e83a1806f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="in-doubt-xact-resolution-server-configuration-option"></a>Lösung für unklare Transaktion (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mit der Option **in-doubt xact resolution** steuern Sie das Standardergebnis von Transaktionen, die der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) nicht auflösen kann. Die mangelnde Fähigkeit zur Auflösung von Transaktionen kann mit der Ausfalldauer des MS DTC zusammenhängen oder auch mit einem unbekannten Transaktionsergebnis zum Zeitpunkt der Wiederherstellung.  
  
 Die nachstehende Tabelle enthält die möglichen Ergebniswerte für das Auflösen einer unsicheren Transaktion.  
  
|Ergebniswert|Beschreibung|  
|-------------------|-----------------|  
|0|Keine Annahme. Die Wiederherstellung erzeugt einen Fehler, falls der MS DTC keine unsicheren Transaktionen auflösen kann.|  
|1|Commit annehmen. Alle unsicheren MS DTC-Transaktionen werden als übermittelt angesehen.|  
|2|Abbruch annehmen. Alle unsicheren MS DTC-Transaktionen werden als abgebrochen angesehen.|  
  
 Um die Gefahr längerer Ausfallzeiten zu minimieren, kann ein Administrator diese Option so konfigurieren, dass entweder die Übermittlung oder der Abbruch angenommen wird, wie im nachstehenden Beispiel dargestellt.  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 2 -– presume abort  
GO  
RECONFIGURE  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 Alternativ hat der Administrator die Möglichkeit, die Standardeinstellung beizubehalten (also keine Annahmen) und das Fehlschlagen der Wiederherstellung zuzulassen, damit ein eventueller DTC-Ausfall sofort bemerkt werden kann, wie im nachstehenden Beispiel erläutert.  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 1 -– presume commit  
GO  
reconfigure  
GO  
ALTER DATABASE pubs SET ONLINE –- run recovery again  
GO  
sp_configure 'in-doubt xact resolution', 0 –- back to no assumptions  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 Bei **in-doubt xact resolution** handelt es sich um eine erweiterte Option. Wenn Sie die Einstellung mithilfe der gespeicherten Systemprozedur **sp_configure** ändern, können Sie **in-doubt xact resolution** nur ändern, wenn **Erweiterte Optionen anzeigen** auf 1 festgelegt ist. Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
> [!NOTE]  
>  Die konsistente Konfiguration dieser Option auf allen [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen, die an verteilten Transaktionen beteiligt sind, trägt dazu bei, Inkonsistenzen in den Daten zu vermeiden.  
  
## <a name="see-also"></a>Siehe auch  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
