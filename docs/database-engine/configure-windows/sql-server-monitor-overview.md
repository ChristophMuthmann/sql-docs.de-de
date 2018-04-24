---
title: SQL Server-Monitor (Übersicht) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
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
f1_keywords:
- sql13.swb.sqlservermonitor.main.f1
helpviewer_keywords:
- SQL Server Monitor [SQL Server]
ms.assetid: 048ae16d-31c3-489a-9f1e-1400a3bacd39
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8025197baa6da578f999087a5d4cadc39d4a3bfd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-monitor-overview"></a>SQL Server-Monitor (Übersicht)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server-Monitor führt keine Überwachungsfunktionen aus, hostet jedoch Module, die diese Funktionen ausführen. Zu den SQL Server-Monitor-Modulen gehören der Replikationsmonitor und der Datenbankspiegelungs-Monitor.  
  
 Wählen Sie das betreffende Modul im Menü **Wechseln zu** aus, um eines dieser Module zu verwenden. Das aktuell ausgewählte Modul ist im Besitz des Inhalts der Navigations- und Detailbereiche, der Benutzerinteraktionen in den Detailbereichen und der Abfragen für Inhalt und Status.  
  
> [!NOTE]  
>  Weitere Informationen zu diesen Monitoren finden Sie unter [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md) und [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md).  
  
## <a name="permissions"></a>Berechtigungen  
  
-   Replikationsmonitor  
  
     Zum Überwachen der Replikation müssen Sie Mitglied der festen Serverrolle **sysadmin** auf dem Verteiler oder Mitglied der festen Datenbankrolle **replmonitor** in der Verteilungsdatenbank sein. Ein Systemadministrator kann jeden Benutzer zur **replmonitor** -Rolle hinzufügen. Anhand dieser Rolle kann ein Benutzer die Replikationsaktivität im Replikationsmonitor anzeigen. Er kann die Replikation jedoch nicht verwalten.  
  
-   Datenbankspiegelungs-Monitor  
  
     Zum Überwachen der Datenbankspiegelung müssen Sie entweder Mitglied der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **dbm_monitor** in der Serverinstanz sein. Wenn Sie Mitglied von **sysadmin** oder **dbm_monitor** auf nur einer der Partnerserverinstanzen sind, kann der Monitor nur mit diesem Partner eine Verbindung herstellen. Der Monitor kann keine Informationen von dem anderen Partner abrufen. Weitere Informationen finden Sie unter [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md).  
  
## <a name="menu-options"></a>Menüoptionen  
 Der SQL Server-Monitor hat ein Menü mit Befehlen, die sich auf den SQL Server-Monitor beziehen. Dieses Menü kann auch Befehle des ausgewählten Moduls enthalten.  
  
 Die folgenden Menüoptionen beziehen sich auf den SQL Server-Monitor.  
  
 **Zuletzt geöffnete Dateien**  
 Das Menü enthält den Befehl **Beenden** .  
  
 **Aktion**  
 Enthält das Kontextmenü des Knotens, der in der Navigationsstruktur ausgewählt ist.  
  
 **Wechseln zu**  
 Enthält eine Liste mit Überwachungskomponenten:  
  
-   Datenbankspiegelung  
  
-   Replikation  
  
 **So verwenden Sie SQL Server Management Studio zum Überwachen der Datenbankspiegelung**  
  
-   [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
