---
title: Aktualisieren des Auftragsaktivitätsmonitors | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.jobactivitymon.refresh.f1
ms.assetid: 413a368e-fd2b-4e1f-b370-002cdbc85bab
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 68de718d9dd0fbdbe245b76dbb404ca206632bdd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="job-activity-monitor-refresh"></a>Aktualisieren des Auftragsaktivitätsmonitors
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe des Dialogfelds **Aktualisierungseinstellungen** können Sie konfigurieren, wie oft durch den Auftragsaktivitätsmonitor neue Informationen zur Serveraktivität abgerufen werden. Der Auftragsaktivitätsmonitor muss Abfragen an die überwachten Server ausführen, um Informationen für das Raster des Auftragsaktivitätsmonitors zu erhalten. Wenn für das Intervall für die automatische Aktualisierung weniger als 30 Sekunden festgelegt ist, kann die für die Ausführung der Abfragen benötigte Zeit die Serverleistung beeinträchtigen.  
  
 Zum Öffnen dieses Dialogfelds klicken Sie im Abschnitt **Status**des Auftragsaktivitätsmonitors auf **Aktualisierungseinstellungen anzeigen** .  
  
## <a name="options"></a>Tastatur  
 **Automatische Aktualisierung alle**  
 Wählen Sie diese Option, um die automatische Aktualisierung der Aktivitätsmonitorinformationen zu aktivieren. Standardmäßig ist die automatische Aktualisierung ausgeschaltet.  
  
 **Sekunden**  
 Anzahl der Sekunden zwischen den automatischen Aktualisierungsversuchen. Der Standardwert ist 60 Sekunden. Wenn der Wert auf 5 oder weniger festgelegt ist, erfolgt die Aktualisierung alle 5 Sekunden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen der Auftragsaktivität](http://msdn.microsoft.com/library/71cb432b-631d-4b8b-9965-e731b3d8266d)  
  
  
