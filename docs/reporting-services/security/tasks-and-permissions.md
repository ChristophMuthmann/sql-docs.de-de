---
title: Aufgaben und Berechtigungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], tasks
- role-based security [Reporting Services], permissions
- security [Reporting Services], tasks
- security [Reporting Services], permissions
- role-based security [Reporting Services], tasks
- predefined tasks [Reporting Services]
- tasks [Reporting Services]
ms.assetid: d7ff90b5-b976-4270-b9ad-9d7b801d8263
caps.latest.revision: "40"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 242fbc404f49f41c1051a900144a7a61e46d3714
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="tasks-and-permissions"></a>Aufgaben und Berechtigungen
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]stellen *Aufgaben* Aktionen dar, die ein Benutzer oder Administrator ausführen kann. Aufgaben sind vordefiniert. Es ist nicht möglich, benutzerdefinierte Aufgaben zu erstellen oder die vom Programm oder über ein Tool bereitgestellten Aufgaben zu ändern. Es gibt insgesamt fünfundzwanzig Aufgaben. Diese Aufgaben enthalten alle Vorgänge, die für die rollenbasierte Sicherheit zur Verfügung stehen. Beispiele für Aufgaben sind "Berichte anzeigen", "Berichte verwalten" oder "Berichtsservereigenschaften verwalten".  
  
 Jede Aufgabe besteht aus Berechtigungen, die ebenfalls vordefiniert sind. Beispielsweise enthält die Aufgabe "Ordner verwalten" Berechtigungen zum Erstellen und Löschen von Ordnern sowie zum Anzeigen und Aktualisieren der Ordnereigenschaften. Die Berechtigungen für die einzelnen Aufgaben sind dokumentiert, um eine genauere Beschreibung der einzelnen Aufgaben bereitzustellen. Die direkte Interaktion mit Berechtigungen und das Angeben von Berechtigungen in Rollenzuweisungen sind nicht möglich. Vielmehr werden Benutzern Berechtigungen indirekt über die Aufgaben erteilt, die zu Rollendefinitionen gehören.  
  
 Aufgaben können nur ausgeführt werden, wenn sie Teil einer Rolle sind und diese Rolle in einer Rollenzuweisung enthalten ist. Wenn z. B. die Aufgabe Modelle anzeigen nicht in einer Rolle enthalten ist oder diese Rolle nicht Teil einer Rollenzuweisung ist, können Benutzer keine Berichtsmodelle anzeigen. Das folgende Diagramm veranschaulicht, wie Berechtigungen in Aufgaben kombiniert und wie Aufgaben in Rollen kombiniert werden, die für spezielle Rollenzuweisungen verwendet werden können.  
  
 ![Diagramm für Berechtigungen und Aufgaben](../../reporting-services/security/media/report-securityobjects.gif "Permissions and task diagram")  
Diagramm für Berechtigungen und Aufgaben  
  
## <a name="system-and-item-level-tasks"></a>Aufgaben auf System- und Elementebene  
 Aufgaben können zwei Kategorien zugeordnet werden: Aufgaben auf Systemebene und auf Elementebene. In einer Rolle können nur Aufgaben aus einer einzigen Kategorie vorhanden sein. In der folgenden Tabelle sind die verschiedenen Aufgabenkategorien beschrieben.  
  
|Kategorie|Description|  
|--------------|-----------------|  
|[Aufgaben auf Elementebene](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md)|Aktionen, die für Elemente ausgeführt werden, die von einem Berichtsserver verwaltet werden, wie z. B. Ordner, Berichte, Berichtsmodelle und Ressourcen.<br /><br /> Als Bereich für Aufgaben auf Elementebene gilt der Ordnernamespace des Berichtsservers. Alle Elemente, auf die über die Ordner auf einem Berichtsserver oder über eine URL zugegriffen wird, sind durch Rollenzuweisungen gesichert, die Aufgaben auf Elementebene enthalten.|  
|[Aufgaben auf Systemebene](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)|Aktionen, die auf Systemebene ausgeführt werden, wie z. B. die Verwaltung von Aufträgen oder freigegebenen Zeitplänen, die für viele Elemente verwendet werden können. Der Bereich für Aufgaben auf Systemebene liegt außerhalb des Ordnernamespaces des Berichtsservers.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Rollendefinitionen](../../reporting-services/security/role-definitions.md)   
 [Vordefinierte Rollen](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [Granting Permissions on a Native Mode Report Server (Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus)](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
