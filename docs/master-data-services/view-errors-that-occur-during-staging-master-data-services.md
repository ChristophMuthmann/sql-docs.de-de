---
title: "Anzeigen von Fehlern, die während des Stagings auftreten (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
caps.latest.revision: "8"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bdc53da2a9259930b326778bb8227996565d9c8c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="view-errors-that-occur-during-staging-master-data-services"></a>Anzeigen von Fehlern, die während des Stagings auftreten (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie Fehler anzeigen, die während des Stagingprozesses auftreten. In der Datenbank [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] gibt es zwei Sichten, die Fehler anzeigen:  
  
-   stg.viw_name_MemberErrorDetails für Blatt- oder konsolidierte Elementupdates.  
  
-   stg.viw_name_RelationshipErrorDetails für Hierarchiebeziehungsupdates.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   In der Datenbank [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] müssen Sie entweder für stg.viw_name_MemberErrorDetails oder stg.viw_name_RelationshipErrorDetails über SELECT-Berechtigungen verfügen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-view-staging-errors"></a>So zeigen Sie bereitstellende Fehler an  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung mit der [!INCLUDE[ssDE](../includes/ssde-md.md)] -Instanz für die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank her.  
  
2.  Öffnen Sie eine neue Abfrage.  
  
3.  Geben Sie den folgenden Text ein, und ersetzen Sie den Namen durch den Namen der Stagingtabelle, z. B. viw_Product_MemberErrorDetails.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  Führen Sie die Abfrage aus. Fehlerdetails werden im **ErrorDescription** -Feld angezeigt.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Weitere Informationen zu Fehlermeldungen finden Sie unter [Fehler des Stagingprozesses &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Problembehandlung des Stagingprozesses (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
