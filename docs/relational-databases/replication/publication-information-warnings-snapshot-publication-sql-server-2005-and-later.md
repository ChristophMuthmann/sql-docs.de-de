---
title: "Veröffentlichungsinformationen, Warnungen (Momentaufnahmeveröffentlichung, SQL Server 2005 und höher) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.publicationinfo.warningsandagents.snapshot.f1
ms.assetid: 7aa2eb52-b6b7-4dd3-8483-8ef00d9f0435
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f54f16bf0153e28d3ff1f37f878727e00711f57a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="publication-information-warnings-snapshot-publication-sql-server-2005-and-later"></a>Veröffentlichungsinformationen, Warnungen (Momentaufnahmeveröffentlichung, SQL Server 2005 und höher)
  Die Registerkarte **Warnungen** ist für Verteiler verfügbar, auf denen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höhere Versionen ausgeführt werden. Auf der Registerkarte **Warnungen** können Sie folgende Tasks für die ausgewählte Veröffentlichung ausführen:  
  
-   Aktivieren von Warnungen.  
  
-   Angeben von Schwellenwerten, die den Warnungen zugeordnet werden.  
  
-   Festlegen von Hinweisen, die den Warnungen zugeordnet werden.  
  
## <a name="warnings-thresholds-and-alerts"></a>Warnungen, Schwellenwerte und Warnhinweise  
 Standardmäßig werden vom Replikationsmonitor Warnungen zu nicht initialisierten Abonnements angezeigt: auf den Seiten mit den Abonnementinformationen wird in der Spalte **Status** - der Status **Nicht initialisiertes Abonnement** als Warnung angezeigt. Für Momentaufnahmeveröffentlichungen können Sie auch angeben, dass ein bevorstehender Abonnementablauf zu einer Warnung führt. Legen Sie hierzu die Option **Warnung, wenn ein Abonnement innerhalb des Schwellenwerts abläuft**fest. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird als Abonnementstatus **Läuft demnächst ab/Abgelaufen** angezeigt (wenn kein Problem mit einer höheren Priorität angezeigt werden muss).  
  
 Neben der Warnung im Replikationsmonitor kann bei Erreichen eines Schwellenwerts auch ein Warnhinweis ausgelöst werden. Zum Definieren eines Warnhinweises klicken Sie auf **Warnungen konfigurieren** , und stellen Sie im Dialogfeld **Replikationswarnungen konfigurieren** die entsprechenden Informationen bereit.  
  
## <a name="options"></a>Optionen  
 **Aktiviert**  
 Wählen Sie diese Option aus, um eine Warnung zu aktivieren und einen Schwellenwert anzugeben.  
  
 **Warnung**  
 Eine Beschreibung der Warnung, die einem Schwellenwert zugeordnet ist.  
  
 **Schwellenwert**  
 Geben Sie einen Wert für den Schwellenwert an.  
  
 **Warnungen konfigurieren**  
 Wählen Sie im Raster **Warnungen** die gewünschte Zeile aus, und klicken Sie auf **Warnungen konfigurieren** , um das Dialogfeld **Replikationswarnungen konfigurieren** zu öffnen. In dem Dialogfeld können Sie einen Warnhinweis definieren, der dem ausgewählten Schwellenwert und der Warnung zugeordnet wird.  
  
 **Änderungen verwerfen**  
 Klicken Sie hier, um die Änderungen an Warnungen und Schwellenwerten zu verwerfen.  
  
> [!NOTE]  
>  Die Schaltfläche **Änderungen verwerfen** hat keine Auswirkungen auf die im Dialogfeld **Replikationswarnungen konfigurieren** definierten Warnungen.  
  
 **Änderungen speichern**  
 Klicken Sie hier, um die Änderungen an Warnungen und Schwellenwerten zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
