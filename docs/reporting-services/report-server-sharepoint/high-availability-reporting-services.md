---
title: "Hochverfügbarkeit in SQL Server Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: f17a051f774ee2ae97eaf6c3ad1cb1468dd9c280
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="high-availability-in-sql-server-reporting-services"></a>Hochverfügbarkeit in SQL Server Reporting Services

Ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver ist ein statusloser Server, auf dem Anwendungsdaten, Inhalt, Eigenschaften und Sitzungsinformationen in zwei relationalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken gespeichert werden. Die beste Art, die Verfügbarkeit der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionalität sicherzustellen, ist folgende Vorgehensweise:  
  
-   Verwenden Sie die Funktionen der Hochverfügbarkeit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] zur Maximierung der Betriebszeit der Berichtsserver-Datenbanken. Bei der Konfiguration einer [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz für die Ausführung in einem Failovercluster können Sie diese Instanz wählen, wenn Sie eine Berichtsserver-Datenbank erstellen.  
  
-   Verwenden Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Datenbanken und für Datenquellen, wenn möglich. Weitere Informationen finden Sie unter [Reporting Services mit Always On-Verfügbarkeitsgruppen](../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md).  
  
-   Konfigurieren Sie mehrere Berichtsserver für die Ausführung in einer Bereitstellung für horizontales Skalieren, in der alle Server eine gemeinsame Berichtsserver-Datenbank verwenden. Die Bereitstellung mehrerer Berichtsserverinstanzen (vorzugsweise auf verschiedenen Servern) in einer Bereitstellung für horizontales Skalieren kann für die Sicherstellung eines unterbrechungsfreien Diensts für den Fall, dass eine Berichtsserverinstanz abstürzt, sorgen.  
  
 Eine Bereitstellung für horizontales Skalieren bietet eine Möglichkeit, eine Datenbank freizugeben. Wenn ein Berichtsserver abstürzt, arbeiten andere in derselben Bereitstellung vorhandene Server weiter.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ist nicht clusterabhängig. Eine Bereitstellung für horizontales Skalieren liefert an sich keinen Lastenausgleich. Es werden keine Verarbeitungslasten auf einem Berichtsserver erkannt und neue Verarbeitungsanforderungen nicht an den am geringsten ausgelasteten Server geschickt. Fehlgeschlagene Verarbeitungsanforderungen werden nicht erneut weitergeleitet. Für die Nutzung von Lastenausgleichsfunktionen müssen Sie den Lastenausgleich für die Webserver konfigurieren, auf denen die Berichtsserver gehostet werden, und anschließend die Berichtsserver in einer Bereitstellung für horizontales Skalieren so konfigurieren, dass sie dieselbe Berichtsserver-Datenbank verwenden.  
  
 Der Report Server-Webdienst und der Windows-Dienst sind nahtlos integriert und werden zusammen als eine Berichtsserverinstanz ausgeführt. Die Verfügbarkeit für einen Dienst kann nicht unabhängig von der des anderen konfiguriert werden.  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
