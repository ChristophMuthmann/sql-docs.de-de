---
title: Aufgaben und Berechtigungen | Microsoft Docs
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
helpviewer_keywords:
- permissions [Reporting Services], tasks
- role-based security [Reporting Services], permissions
- security [Reporting Services], tasks
- security [Reporting Services], permissions
- role-based security [Reporting Services], tasks
- predefined tasks [Reporting Services]
- tasks [Reporting Services]
ms.assetid: d7ff90b5-b976-4270-b9ad-9d7b801d8263
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1e2822182d644b90aa419986f75a6fdc6fd3296
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="tasks-and-permissions"></a>Aufgaben und Berechtigungen
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]stellen *Aufgaben* Aktionen dar, die ein Benutzer oder Administrator ausführen kann. Aufgaben sind vordefiniert. Es ist nicht möglich, benutzerdefinierte Aufgaben zu erstellen oder die vom Programm oder über ein Tool bereitgestellten Aufgaben zu ändern. Es gibt insgesamt fünfundzwanzig Aufgaben. Diese Aufgaben enthalten alle Vorgänge, die für die rollenbasierte Sicherheit zur Verfügung stehen. Beispiele für Aufgaben sind "Berichte anzeigen", "Berichte verwalten" oder "Berichtsservereigenschaften verwalten".  
  
 Jede Aufgabe besteht aus Berechtigungen, die ebenfalls vordefiniert sind. Beispielsweise enthält die Aufgabe "Ordner verwalten" Berechtigungen zum Erstellen und Löschen von Ordnern sowie zum Anzeigen und Aktualisieren der Ordnereigenschaften. Die Berechtigungen für die einzelnen Aufgaben sind dokumentiert, um eine genauere Beschreibung der einzelnen Aufgaben bereitzustellen. Die direkte Interaktion mit Berechtigungen und das Angeben von Berechtigungen in Rollenzuweisungen sind nicht möglich. Vielmehr werden Benutzern Berechtigungen indirekt über die Aufgaben erteilt, die zu Rollendefinitionen gehören.  
  
 Aufgaben können nur ausgeführt werden, wenn sie Teil einer Rolle sind und diese Rolle in einer Rollenzuweisung enthalten ist. Wenn z. B. die Aufgabe Modelle anzeigen nicht in einer Rolle enthalten ist oder diese Rolle nicht Teil einer Rollenzuweisung ist, können Benutzer keine Berichtsmodelle anzeigen. Das folgende Diagramm veranschaulicht, wie Berechtigungen in Aufgaben kombiniert und wie Aufgaben in Rollen kombiniert werden, die für spezielle Rollenzuweisungen verwendet werden können.  
  
 ![Diagramm für Berechtigungen und Aufgabe](../../reporting-services/security/media/report-securityobjects.gif "Diagramm für Berechtigungen und Aufgabe")  
Diagramm für Berechtigungen und Aufgaben  
  
## <a name="system-and-item-level-tasks"></a>Aufgaben auf System- und Elementebene  
 Aufgaben können zwei Kategorien zugeordnet werden: Aufgaben auf Systemebene und auf Elementebene. In einer Rolle können nur Aufgaben aus einer einzigen Kategorie vorhanden sein. In der folgenden Tabelle sind die verschiedenen Aufgabenkategorien beschrieben.  
  
|Kategorie|Description|  
|--------------|-----------------|  
|[Aufgaben auf Elementebene](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md)|Aktionen, die für Elemente ausgeführt werden, die von einem Berichtsserver verwaltet werden, wie z. B. Ordner, Berichte, Berichtsmodelle und Ressourcen.<br /><br /> Als Bereich für Aufgaben auf Elementebene gilt der Ordnernamespace des Berichtsservers. Alle Elemente, auf die über die Ordner auf einem Berichtsserver oder über eine URL zugegriffen wird, sind durch Rollenzuweisungen gesichert, die Aufgaben auf Elementebene enthalten.|  
|[Aufgaben auf Systemebene](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)|Aktionen, die auf Systemebene ausgeführt werden, wie z. B. die Verwaltung von Aufträgen oder freigegebenen Zeitplänen, die für viele Elemente verwendet werden können. Der Bereich für Aufgaben auf Systemebene liegt außerhalb des Ordnernamespaces des Berichtsservers.|  
  
## <a name="see-also"></a>Siehe auch  
 [Rollendefinitionen](../../reporting-services/security/role-definitions.md)   
 [Vordefinierte Rollen](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
