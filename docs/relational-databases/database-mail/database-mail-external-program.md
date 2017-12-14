---
title: Externes Datenbank-E-Mail-Programm | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mail
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- external programs [Database Mail]
- DatabaseMail90.exe
- Database Mail [SQL Server], external programs
ms.assetid: bc124164-eb6e-4b7f-bf66-98a3113d02f7
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 25f98ba2cfdbd7c0731091b4bf1db5b0b728eb94
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="database-mail-external-program"></a>Externes Datenbank-E-Mail-Programm
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die ausführbare Datei für das externe Datenbank-E-Mail-Programm, **DatabaseMail.exe**, ist im Verzeichnis **MSSQL\Binn** der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation gespeichert. Datenbank-E-Mail verwendet die Service Broker-Aktivierung, um das externe Programm zu starten, wenn E-Mail-Nachrichten zur Verarbeitung vorhanden sind. Datenbank-E-Mail startet eine Instanz des externen Programms. Das externe Programm wird im Sicherheitskontext des Dienstkontos für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt.  
  
 **In diesem Thema:**  
  
-   [Konzepte des externen Datenbank-E-Mail-Programms](#ComponentsAndConcepts)  
  
-   [Tasks, die sich auf die Konfiguration des externe Datenbank-E-Mail-Programms beziehen](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Konzepte des externen Datenbank-E-Mail-Programms  
 Wenn das externe Programm gestartet wird, stellt das Programm mithilfe der Windows-Authentifizierung eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her und beginnt mit der Verarbeitung von E-Mail-Nachrichten. Wenn keine zu sendenden Nachrichten für den angegebenen Timeoutzeitraum vorhanden sind, wird das Programm beendet. Mithilfe des Assistenten zum Konfigurieren von Datenbank-E-Mail oder der gespeicherten Prozeduren von Datenbank-E-Mail können Sie konfigurieren, nach welcher Wartezeit das Programm beendet wird. Weitere Informationen finden Sie unter [sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)ausgeführt.  
  
 Das externe Programm speichert Informationen in Systemtabellen in der **msdb** -Datenbank. Falls das externe Programm nicht mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kommunizieren kann, protokolliert das Programm Fehler im Microsoft Windows-Anwendungsereignisprotokoll. Eine zusätzliche Meldungsprotokollierung ist verfügbar, wenn der Protokolliergrad im Dialogfeld **Systemparameter konfigurieren** des **Assistenten zum Konfigurieren von Datenbank-E-Mail** auf **Ausführlich**festgelegt wird.  
  
 Beachten Sie, dass das externe Programm aus Gründen der Effizienz Konto- und Profilinformationen zwischenspeichert. Deshalb kann es sein, dass Konfigurationsänderungen an Konten und Profilen erst nach ein paar Minuten im externen Programm angezeigt werden.  
  
##  <a name="RelatedTasks"></a> Tasks, die sich auf die Konfiguration des externe Datenbank-E-Mail-Programms beziehen  
  
|Konfigurationstask|Themenlink|  
|------------------------|----------------|  
|Geben Sie die Zeit für das externe Programm vor dem Beenden an.|[sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Datenbank-E-Mail-Protokoll und -Überwachung](../../relational-databases/database-mail/database-mail-log-and-audits.md)   
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
