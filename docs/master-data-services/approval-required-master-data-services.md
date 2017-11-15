---
title: Genehmigung erforderlich (Master Data Services) | Microsoft-Dokumentation
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b475a53d-269d-49f3-bb42-965c555f80be
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 518f9ecd8a23a026aa200b0788782a48eb682ddd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="approval-required-master-data-services"></a>Genehmigung erforderlich (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]kann der Administrator eine Entität auf „Genehmigung erforderlich“ festlegen. Alle Änderungen an dieser Entität müssen dann von einem der Entitätsadministratoren überprüft und genehmigt werden.  
  
> [!NOTE]  
>  Änderungen an Blattelementen müssen genehmigt werden. Bei Änderungen an veralteten expliziten Hierarchien und Sammlungen wird die Genehmigung umgangen.  
>   
>  Bei Änderungen, die vom Stagingtabellenprozess vorgenommen werden, wird die Genehmigung umgangen.  
>   
>  Bei Änderungen, die durch eine Geschäftsregel vorgenommen werden, wird die Genehmigung umgangen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich der Systemverwaltung zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)  
  
-   Eine Entität muss vorhanden sein. Weitere Informationen finden Sie unter [Erstellen einer Entität &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="to-enable-approval-required-for-an-entity"></a>So aktivieren Sie „Genehmigung erforderlich“ für eine Entität  
  
1.  Klicken Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** im Raster die Zeile für die Entität aus, für die Sie  **Genehmigung erforderlich** aktivieren möchten.  
  
4.  Klicken Sie auf **Bearbeiten**, wählen Sie **Genehmigung erforderlich**, und klicken Sie dann auf **Speichern**.  
  
## <a name="see-also"></a>Siehe auch  
 [Changesets &#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md)  
  
  
