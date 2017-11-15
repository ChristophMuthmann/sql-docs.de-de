---
title: Sperren einer Version (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- versions [Master Data Services], locking
- locking versions [Master Data Services]
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51bec90f7dc9f99a1119a7d2face450d3831f0a4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lock-a-version-master-data-services"></a>Sperren einer Version (Master Data Services)
  Sperren Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine Version eines Modells, um Änderungen an den Elementen des Modells und den Attributen zu verhindern.  
  
> [!NOTE]  
>  Wenn eine Version gesperrt ist, können Administratorbenutzer und Modelladministratoren weiterhin Elemente hinzuzufügen, bearbeiten und entfernen. Andere Benutzer mit Berechtigungen für das Modell können die Elemente jedoch nur anzeigen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Der Status der Version muss **Öffnen**sein.  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Versionsverwaltung" zuzugreifen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-lock-a-version"></a>So sperren Sie eine Version  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Versionsverwaltung**.  
  
2.  Wählen Sie auf der Seite **Versionen verwalten** die Zeile für die Version aus, die Sie sperren möchten.  
  
3.  Klicken Sie auf **Sperren**.  
  
4.  Klicken Sie im Bestätigungsdialogfeld auf **OK**.  
  
## <a name="next-steps"></a>Nächste Schritte  
  
-   [Überprüfen einer Version anhand von Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [Durchführen eines Commits für eine Version &#40;Master Data Services&#41;](../master-data-services/commit-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Versionen &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Entsperren einer Version &#40;Master Data Services&#41;](../master-data-services/unlock-a-version-master-data-services.md)  
  
  
