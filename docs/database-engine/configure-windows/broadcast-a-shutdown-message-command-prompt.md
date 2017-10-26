---
title: "Senden einer Nachricht über das Herunterfahren (Befehlszeile) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server, stopping
- named instances [SQL Server], broadcasting shutdown messages
- shutdown message broadcast
- broadcasting shutdown message
- command prompt [SQL Server], broadcasting shutdown messages
- default instances [SQL Server], broadcasting shutdown messages
- stopping SQL Server
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 796fc61fe4080f5202fded550999951a27e43639
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="broadcast-a-shutdown-message-command-prompt"></a>Senden einer Nachricht über das Herunterfahren (Befehlszeile)
  In diesem Thema wird beschrieben, wie Sie mit dem Befehl [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] net send **eine Nachricht zum Herunterfahren in** übertragen. Schließen Sie den Zeitpunkt, zu dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beendet wird, in die Nachricht ein, damit alle Benutzer ihre Aufgaben beenden können.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-broadcast-a-shutdown-message"></a>So senden Sie eine Nachricht über das Herunterfahren  
  
1.  Geben Sie in einer Befehlszeile Folgendes ein:  
  
     **net send /users "Nachricht"**  
  
     Durch die Option **/users** wird angegeben, dass die Nachricht an alle Benutzer gesendet wird, die mit dem Server verbunden sind.  
  
> [!NOTE]  
>  Der Befehl **net send** erfordert, dass der Nachrichtendienst sowohl auf dem sendenden als auch auf den empfangenden Computern ausgeführt wird. Der Nachrichtendienst ist in Windows Server 2003 standardmäßig deaktiviert. Weitere Informationen zu **net send**finden Sie in der Windows-Dokumentation.  
  
 Es könnte im Netzwerk geeigneter sein, die Benutzer per E-Mail oder telefonisch zu verständigen. Verwenden Sie zum Bestimmen, welche Benutzer gerade mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden sind, den Aktivitätsmonitor. Informationen zum Aktivitätsmonitor finden Sie unter [Aktivitätsmonitor](../../relational-databases/performance-monitor/activity-monitor.md) und [Öffnen des Aktivitätsmonitors &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  

