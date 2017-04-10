---
title: "Senden einer Nachricht &#252;ber das Herunterfahren (Befehlszeile) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server, beenden"
  - "benannte Instanzen [SQL Server], Senden von Nachrichten über das Herunterfahren"
  - "Herunterfahren-Nachricht senden"
  - "Senden einer Nachricht über das Herunterfahren"
  - "Eingabeaufforderung [SQL Server], Senden von Nachrichten über das Herunterfahren"
  - "Standardinstanzen [SQL Server], Senden von Nachrichten über das Herunterfahren"
  - "Beenden von SQL Server"
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Senden einer Nachricht &#252;ber das Herunterfahren (Befehlszeile)
  In diesem Thema wird beschrieben, wie Sie mit dem Befehl **net send** eine Nachricht zum Herunterfahren in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] übertragen. Schließen Sie den Zeitpunkt, zu dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beendet wird, in die Nachricht ein, damit alle Benutzer ihre Aufgaben beenden können.  
  
##  <a name="SSMSProcedure"></a>  
  
#### So senden Sie eine Nachricht über das Herunterfahren  
  
1.  Geben Sie in einer Befehlszeile Folgendes ein:  
  
     **net send /users "Nachricht"**  
  
     Durch die Option **/users** wird angegeben, dass die Nachricht an alle Benutzer gesendet wird, die mit dem Server verbunden sind.  
  
> [!NOTE]  
>  Der Befehl **net send** erfordert, dass der Nachrichtendienst sowohl auf dem sendenden als auch auf den empfangenden Computern ausgeführt wird. Der Nachrichtendienst ist in Windows Server 2003 standardmäßig deaktiviert. Weitere Informationen zu **net send**finden Sie in der Windows-Dokumentation.  
  
 Es könnte im Netzwerk geeigneter sein, die Benutzer per E-Mail oder telefonisch zu verständigen. Verwenden Sie zum Bestimmen, welche Benutzer gerade mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden sind, den Aktivitätsmonitor. Informationen zum Aktivitätsmonitor finden Sie unter [Aktivitätsmonitor](../../relational-databases/performance-monitor/activity-monitor.md) und [Öffnen des Aktivitätsmonitors &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md).  
  
## Siehe auch  
 [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)  
  
  