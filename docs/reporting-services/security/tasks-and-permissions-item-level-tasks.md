---
title: Aufgaben auf Elementebene | Microsoft Docs
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
- item-level tasks [Reporting Services]
ms.assetid: fdeb7bc3-167a-4342-84e3-32e3faa1fa39
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 067a0b9d4f33e20625fb796fa98f7b4ec6184f3e
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="tasks-and-permissions---item-level-tasks"></a>Aufgaben und Berechtigungen - Aufgaben auf Elementebene
  Eine Aufgabe auf Elementebene ist eine Auflistung von Berechtigungen, die sich auf einen Bericht, einen Ordner, ein Berichtsmodell, eine Ressource oder eine freigegebene Datenquelle beziehen. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthält auch Aufgaben auf Systemebene, die sich auf die Berichtsserversite als Ganzes beziehen. Weitere Informationen finden Sie unter [Aufgaben auf Systemebene](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md). Weitere Informationen zu Aufgaben und Berechtigungen im Allgemeinen finden Sie unter [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md).  
  
> [!NOTE]  
>  Wenn Sie mit diesen Aufgaben programmgesteuert arbeiten, müssen Sie Methoden verwenden, die Aufgaben auf Elementebene unterstützen. Weitere Informationen finden Sie unter <xref:ReportService2010.ReportingService2010.ListTasks%2A> und <xref:ReportService2010.ReportingService2010.ListRoles%2A>.  
  
## <a name="permissions-in-item-level-tasks"></a>Berechtigungen in Aufgaben auf Elementebene  
 In der folgenden Tabelle sind die Aufgaben auf Elementebene, die in jeder Aufgabe enthaltenen Berechtigungen sowie die Elemente aufgelistet, für die diese Berechtigungen gelten. Die Berechtigungen sind nur zu Informationszwecken aufgeführt, um eine genauere Beschreibung der über die verschiedenen Aufgaben verfügbaren Funktionalität bereitzustellen.  
  
 Freigegebene Datasets verwenden den gleichen Satz von Berechtigungen wie Berichte. Berichtsteile verwenden den gleichen Satz von Berechtigungen wie Ressourcen.  
  
|Task|Gilt für Element|Berechtigungen|  
|----------|---------------------|-----------------|  
|Berichte lesen|Berichte|Lesen von Inhalt<br /><br /> Lesen von Berichtsdefinitionen<br /><br /> Lesen von Eigenschaften|  
|Berichte lesen|Freigegebene Datasets|Lesen von Inhalt<br /><br /> Lesen von Berichtsdefinitionen<br /><br /> Lesen von Eigenschaften|  
|Verknüpfte Berichte erstellen|Berichte|Erstellen von Links<br /><br /> Lesen von Eigenschaften|  
|Alle Abonnements verwalten|Berichte|Lesen von Eigenschaften<br /><br /> Lesen eines Abonnements<br /><br /> Erstellen eines Abonnements<br /><br /> Löschen eines Abonnements<br /><br /> Aktualisieren eines Abonnements|  
|Datenquellen verwalten|Ordner|Erstellen von Datenquellen|  
|Datenquellen verwalten|Datenquellen|Aktualisieren von Eigenschaften<br /><br /> Löschen von Updateinhalt<br /><br /> Lesen von Eigenschaften|  
|Ordner verwalten|Ordner|Erstellen von Ordnern<br /><br /> Löschen von Updateeigenschaften<br /><br /> Lesen von Eigenschaften|  
|Einzelne Abonnements verwalten|Berichte|Lesen von Eigenschaften<br /><br /> Erstellen von Abonnements<br /><br /> Löschen von Abonnements<br /><br /> Lesen von Abonnements<br /><br /> Aktualisieren von Abonnements|  
|Modelle verwalten|Ordner|Erstellen eines Modells|  
|Modelle verwalten|Modelle|Lesen von Eigenschaften<br /><br /> Lesen von Inhalt<br /><br /> Löschen von Updateinhalt<br /><br /> Lesen von Datenquellen<br /><br /> Aktualisieren von Datenquellen<br /><br /> Lesen von Autorisierungsrichtlinien für Modellelemente<br /><br /> Aktualisieren von Autorisierungsrichtlinien für Modellelemente<br /><br /> Löschen von Updateeigenschaften|  
|Berichtsverlauf verwalten|Berichte|Lesen von Eigenschaften<br /><br /> Erstellen eines Berichtsverlaufs<br /><br /> Löschen eines Berichtsverlaufs<br /><br /> Ausführen von Leserichtlinien<br /><br /> Aktualisieren von Richtlinien<br /><br /> Auflisten des Berichtsverlaufs|  
|Berichte verwalten|Ordner|Erstellen von Berichten<br /><br /> gilt auch für die Erstellung freigegebener Datasets|  
|Berichte verwalten|Berichte|Lesen von Eigenschaften<br /><br /> Löschen von Updateeigenschaften<br /><br /> Aktualisieren von Parametern<br /><br /> Lesen von Datenquellen<br /><br /> Aktualisieren von Datenquellen<br /><br /> Lesen von Berichtsdefinitionen<br /><br /> Aktualisieren von Berichtsdefinitionen<br /><br /> Ausführen von Leserichtlinien<br /><br /> Aktualisieren von Richtlinien|  
|Berichte verwalten|Freigegebene Datasets|Lesen von Eigenschaften<br /><br /> Löschen von Updateeigenschaften<br /><br /> Aktualisieren von Parametern<br /><br /> Lesen von Datenquellen<br /><br /> Aktualisieren von Datenquellen<br /><br /> Lesen von Berichtsdefinitionen<br /><br /> Aktualisieren von Berichtsdefinitionen<br /><br /> Ausführen von Leserichtlinien<br /><br /> Aktualisieren von Richtlinien|  
|Ressourcen verwalten|Ordner|Erstellen von Ressourcen|  
|Ressourcen verwalten|Ressourcen|Aktualisieren von Eigenschaften<br /><br /> Löschen von Updateinhalt<br /><br /> Lesen von Eigenschaften|  
|Ressourcen verwalten|Berichtsteile|Aktualisieren von Eigenschaften<br /><br /> Löschen von Updateinhalt<br /><br /> Lesen von Eigenschaften|  
|Sicherheit für einzelne Elemente festlegen|Berichte, Ressourcen, Datenquellen, freigegebene Datasets, Ordner|Lesen von Sicherheitsrichtlinien - Aktualisieren von Sicherheitsrichtlinien|  
|Datenquellen anzeigen|Datenquellen|Lesen von Inhalt<br /><br /> Lesen von Eigenschaften|  
|Ordner anzeigen|Ordner|Lesen von Eigenschaften<br /><br /> Ausführen und Anzeigen<br /><br /> Auflisten des Berichtsverlaufs|  
|Modelle anzeigen|Berichtsmodelle|Lesen von Eigenschaften<br /><br /> Lesen von Inhalt<br /><br /> Lesen von Datenquellen|  
|Berichte anzeigen|Berichte|Lesen von Inhalt<br /><br /> Lesen von Eigenschaften|  
|Berichte anzeigen|Freigegebene Datasets|Lesen von Inhalt<br /><br /> Lesen von Eigenschaften|  
|Ressourcen anzeigen|Ressourcen|Lesen von Inhalt<br /><br /> Lesen von Eigenschaften|  
|Ressourcen anzeigen|Berichtsteile|Lesen von Inhalt<br /><br /> Lesen von Eigenschaften|  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
