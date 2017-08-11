---
title: "Hohe Verfügbarkeit (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], Reporting Services
- high availability [Reporting Services]
- Reporting Services, high availability
ms.assetid: 50e0813f-f591-4688-9cd1-e6389a3808e5
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b4b2d373dfc2467e10a9a6ee79d98aa3a690bd4c
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="high-availability-reporting-services"></a>Hohe Verfügbarkeit (Reporting Services)
  Ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver ist ein statusloser Server, auf dem Anwendungsdaten, Inhalt, Eigenschaften und Sitzungsinformationen in zwei relationalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken gespeichert werden. Die beste Art, die Verfügbarkeit der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionalität sicherzustellen, ist folgende Vorgehensweise:  
  
-   Verwenden Sie die Funktionen der hohen Verfügbarkeit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] zur Maximierung der Betriebszeit der Berichtsserver-Datenbanken. Bei der Konfiguration einer [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz für die Ausführung in einem Failovercluster können Sie diese Instanz wählen, wenn Sie eine Berichtsserver-Datenbank erstellen.  
  
-   Verwenden Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Datenbanken und für Datenquellen, wenn möglich. Weitere Informationen finden Sie unter [Reporting Services mit AlwaysOn-Verfügbarkeitsgruppen &#40; SQLServer &#41; ](../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md).  
  
-   Konfigurieren Sie mehrere Berichtsserver für die Ausführung in einer Bereitstellung für horizontales Skalieren, in der alle Server eine gemeinsame Berichtsserver-Datenbank verwenden. Die Bereitstellung mehrerer Berichtsserverinstanzen (vorzugsweise auf verschiedenen Servern) in einer Bereitstellung für horizontales Skalieren kann für die Sicherstellung eines unterbrechungsfreien Diensts für den Fall, dass eine Berichtsserverinstanz abstürzt, sorgen.  
  
 Eine Bereitstellung für horizontales Skalieren bietet eine Möglichkeit, eine Datenbank freizugeben. Wenn ein Berichtsserver abstürzt, arbeiten andere in derselben Bereitstellung vorhandene Server weiter.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ist nicht clusterabhängig. Eine Bereitstellung für horizontales Skalieren liefert an sich keinen Lastenausgleich. Es werden keine Verarbeitungslasten auf einem Berichtsserver erkannt und neue Verarbeitungsanforderungen nicht an den am geringsten ausgelasteten Server geschickt. Fehlgeschlagene Verarbeitungsanforderungen werden nicht erneut weitergeleitet. Für die Nutzung von Lastenausgleichsfunktionen müssen Sie den Lastenausgleich für die Webserver konfigurieren, auf denen die Berichtsserver gehostet werden, und anschließend die Berichtsserver in einer Bereitstellung für horizontales Skalieren so konfigurieren, dass sie dieselbe Berichtsserver-Datenbank verwenden.  
  
 Der Report Server-Webdienst und der Windows-Dienst sind nahtlos integriert und werden zusammen als eine Berichtsserverinstanz ausgeführt. Die Verfügbarkeit für einen Dienst kann nicht unabhängig von der des anderen konfiguriert werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Lösungen mit hoher Verfügbarkeit &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Bereitstellung für dezentrales Skalieren – Reporting Services im einheitlichen Modus &#40; Konfigurations-Manager &#41;](http://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c)  
  
  
