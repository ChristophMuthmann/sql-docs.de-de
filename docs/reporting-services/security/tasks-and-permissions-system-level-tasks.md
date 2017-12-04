---
title: Aufgaben auf Systemebene | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: system-level tasks [Reporting Services]
ms.assetid: 7023b388-40b2-4590-b227-115cf380a1e7
caps.latest.revision: "36"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3c8a3edfbeafe5ab2f417e514e011899c528c283
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="tasks-and-permissions---system-level-tasks"></a>Aufgaben und Berechtigungen: Aufgaben auf Systemebene
  Eine Aufgabe auf Systemebene ist eine Auflistung von Berechtigungen im Hinblick auf Vorgänge, die die Berichtsserversite insgesamt betreffen. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthält auch Aufgaben auf Elementebene, die sich auf bestimmte Elemente beziehen. Weitere Informationen finden Sie unter [Aufgaben auf Elementebene](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md). Weitere Informationen zu Aufgaben und Berechtigungen im Allgemeinen finden Sie unter [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md).  
  
> [!NOTE]  
>  Wenn Sie mit diesen Aufgaben programmgesteuert arbeiten, müssen Sie Methoden verwenden, die Aufgaben auf Systemebene unterstützen. Weitere Informationen finden Sie unter <xref:ReportService2010.ReportingService2010.ListTasks%2A> und <xref:ReportService2010.ReportingService2010.ListRoles%2A>.  
  
## <a name="permissions-in-system-level-tasks"></a>Berechtigungen für Aufgaben auf Systemebene  
 In der folgenden Tabelle sind die Berechtigungsarten für jede Systemaufgabe aufgeführt. Die Berechtigungsarten sind nur zu Informationszwecken aufgeführt, um eine genauere Beschreibung der über die verschiedenen Aufgaben verfügbaren Funktionalität bereitzustellen.  
  
|Task|Berechtigungen|  
|----------|-----------------|  
|Berichtsdefinitionen ausführen|Berichtsdefinitionen ausführen (Berechtigungs- und Aufgabenname sind identisch)|  
|Ereignisse generieren|Ereignisse generieren|  
|Aufträge verwalten|Lesen von Systemeigenschaften<br /><br /> Aktualisieren von Systemeigenschaften|  
|Berichtsservereigenschaften verwalten|Lesen von Systemeigenschaften<br /><br /> Aktualisieren von Systemeigenschaften|  
|Rollen verwalten|Erstellen von Rollen<br /><br /> Löschen von Rollen<br /><br /> Lesen von Rolleneigenschaften<br /><br /> Aktualisieren von Rolleneigenschaften|  
|Freigegebene Zeitpläne verwalten|Erstellen von Zeitplänen|  
|Berichtsserversicherheit verwalten|Lesen von Systemsicherheitsrichtlinien<br /><br /> Aktualisieren von Systemsicherheitsrichtlinien|  
|Berichtsservereigenschaften anzeigen|Lesen von Systemeigenschaften|  
|Freigegebene Zeitpläne anzeigen|Lesen von Zeitplänen|  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
