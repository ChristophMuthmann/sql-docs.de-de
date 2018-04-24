---
title: Verteilereinstellungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.monitor.DistributorSettings.f1
helpviewer_keywords:
- Distributor Settings dialog box
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c957a97ed2473b0313ab718d3dc4442e3e25f03
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="distributor-settings"></a>Verteilereinstellungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Im Dialogfeld **Verteilereinstellungen** können Sie die Einstellungen für Verteiler ändern, die dem linken Bereich des Replikationsmonitors hinzugefügt wurden.  
  
## <a name="options"></a>Tastatur  
 **Beim Starten des Replikationsmonitors automatisch Verbindung herstellen**  
 Wählen Sie diese Option aus, damit der Replikationsmonitor eine Verbindung mit dem Verteiler herstellen und Statusinformationen abrufen kann.  
  
 **Verbindung**  
 Klicken Sie hier, um das Dialogfeld **Verbindung mit Server herstellen** anzuzeigen. In diesem Dialogfeld können Sie die Verbindungseigenschaften und die Anmeldeinformationen anzeigen, die vom Replikationsmonitor zum Herstellen einer Verbindung mit dem Verteiler verwendet werden.  
  
 **Status dieses Verteilers und seiner Veröffentlichungen automatisch aktualisieren**  
 Wählen Sie diese Option aus, damit der Replikationsmonitor automatisch den Status für den Verteiler aktualisieren kann. Wenn diese Option ausgewählt ist, ruft der Replikationsmonitor die Statusinformationen für den Verteiler anhand des Abrufintervalls ab, das mit der Option **Aktualisierungsrate** festgelegt wurde. Weitere Informationen zum Aktualisieren im Replikationsmonitor finden Sie unter [Caching, Refresh, and Replication Monitor Performance](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Aktualisierungsrate**  
 Geben Sie einen Wert (in Sekunden) ein, um anzugeben, wie oft der Replikationsmonitor Statusinformationen über den Verteiler abrufen soll. Niedrigere Werte bedeuten häufigere Abrufe. Dies kann die Leistung des Verteilers beeinträchtigen, wenn Sie viele Verleger überwachen. Es wird empfohlen, das eigene System zu testen, um einen angemessenen Wert zu bestimmen. Die Einstellung **Aktualisierungsrate** wird ebenfalls verwendet, wenn Sie in einem der Detailfenster des Replikationsmonitors die Option **Automatisch aktualisieren** ausgewählt haben.  
  
 **Alle Verleger dieses Verteilers in folgender Gruppe anzeigen**  
 Wählen Sie eine Verlegergruppe aus der Liste aus. Der Verleger wird unter dieser Gruppe im linken Bereich angezeigt. Gruppen stellen eine Möglichkeit zum Organisieren von Verlegern dar und haben keinen Einfluss auf die Funktion der Replikation.  
  
 **Neue Gruppe**  
 Klicken Sie auf diese Option, um eine neue Verlegergruppe zu erstellen. Eine Verlegergruppe stellt eine einfache Möglichkeit dar, um die Verleger innerhalb des Replikationsmonitors zu organisieren. Gruppen haben keinen Einfluss auf die Replikation der Daten oder die Beziehungen zwischen den Servern in der Replikationstopologie.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
