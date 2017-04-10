---
title: "Sichern und Wiederherstellen von replizierten Datenbanken | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sicherungen [SQL Server-Replikation]"
  - "Verwalten der Replikation, wiederherstellen"
  - "Sichern von replizierten Datenbanken"
  - "Sicherungen [SQL Server-Replikation], Informationen zu Sicherungen"
  - "Wiederherstellen von replizierten Datenbanken [SQL Server-Replikation]"
  - "Wiederherstellung [SQL Server-Replikation], Informationen zur Wiederherstellung"
  - "Wiederherstellen von Datenbanken [SQL Server], replizierte Datenbanken"
  - "Sichern von Datenbanken [SQL Server], replizierte Datenbanken"
  - "Wiederherstellen [SQL Server-Replikation], Informationen zur Wiederherstellung"
  - "Wiederherstellung [SQL Server-Replikation]"
  - "Replikation [SQL Server], verwalten"
  - "Verteilungsdatenbanken [SQL Server-Replikation], sichern"
  - "Wiederherstellen [SQL Server-Replikation]"
  - "Verwalten der Replikations, sichern"
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Sichern und Wiederherstellen von replizierten Datenbanken
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Bei replizierten Datenbanken gibt es besondere Aspekte im Hinblick auf das Sichern und Wiederherstellen von Daten. In diesem Thema finden Sie einleitende Informationen sowie Verweise auf weitere Informationen in Bezug auf Sicherungs- und Wiederherstellungsstrategien für die einzelnen Replikationstypen.  
  
 Die Replikation ermöglicht das Wiederherstellen replizierter Datenbanken auf dem Server und in die Datenbank, die zum Erstellen der Sicherung herangezogen wurden. Wenn Sie eine Sicherungskopie einer replizierten Datenbank auf einem anderen Server bzw. in einer anderen Datenbank wiederherstellen, können Replikationseinstellungen nicht beibehalten werden. In diesem Fall müssen nach der Wiederherstellung der Sicherungskopien sämtliche Veröffentlichungen und Abonnements neu erstellt werden.  
  
> [!NOTE]  
>  Wenn der Protokollversand verwendet wird, kann eine replizierte Datenbank auf einem Standbyserver wiederhergestellt werden. Weitere Informationen finden Sie unter [Protokollversand und Replikation & #40; SQL Server & #41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 Replizierte Datenbanken und ihre zugeordneten Systemdatenbanken sollten in regelmäßigen Abständen gesichert werden. Erstellen Sie Sicherungskopien folgender Datenbanken:  
  
-   Veröffentlichungsdatenbank auf dem Verleger  
  
-   Verteilungsdatenbank auf dem Verteiler  
  
-   Abonnementdatenbank auf den einzelnen Abonnenten  
  
-   Die Systemdatenbanken **master** und **msdb** auf dem Verleger, Verteiler und allen Abonnenten. Diese Datenbanken sollten zur selben Zeit wie alle anderen Datenbanken und die entsprechende Replikationsdatenbank gesichert werden. Sichern Sie also z. B. die **master** - und **msdb** -Datenbanken auf dem Verleger immer dann, wenn Sie auch die Veröffentlichungsdatenbank sichern. Beim Wiederherstellen der Veröffentlichungsdatenbank müssen Sie sicherstellen, dass die **master** - und **msdb** -Datenbanken hinsichtlich der Replikationskonfiguration und der Replikationseinstellungen mit der Veröffentlichungsdatenbank übereinstimmen.  
  
 Wenn Sie regelmäßige Protokollsicherungen ausführen, sollten in den Protokollsicherungen auch alle replikationsrelevanten Änderungen erfasst werden. Wenn Sie keine Protokollsicherungen ausführen, sollte immer dann eine Sicherungskopie erstellt werden, wenn eine für die Replikation relevante Einstellung geändert wird. Weitere Informationen finden Sie unter [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## Sicherungs- und Wiederherstellungsstrategien  
 Die Strategien hinsichtlich der Sicherung und Wiederherstellung der einzelnen Knoten in einer Replikationstopologie variieren je nach verwendetem Replikationstyp. Informationen zu den Sicherungs- und Wiederherstellungsstrategien für die einzelnen Replikationstypen erhalten Sie unter folgenden Themen:  
  
-   [Strategien zum Sichern und Wiederherstellen einer Momentaufnahme- und Transaktionsreplikation](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [Strategien zum Sichern und Wiederherstellen einer Mergereplikation](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 Fester Bestandteil jeder Wiederherstellungsstrategie sollte sein, immer ein aktuelles Skript der Replikationseinstellungen an einem sicheren Ort aufzubewahren. Wenn ein Server ausfällt oder eine Testumgebung eingerichtet werden muss, können Sie das Skript durch Ändern der Verweise auf Servernamen modifizieren. Im Anschluss kann es zur Wiederherstellung der Replikationseinstellungen verwendet werden. Zusätzlich zum Erstellen eines Skripts für die aktuellen Replikationseinstellungen sollten Sie für das Aktivieren oder Deaktivieren der Replikation ein Skript erstellen. Informationen zur Skripterstellung für Replikationsobjekte finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
## Siehe auch  
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Bewährte Methoden für die Replikationsverwaltung](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  