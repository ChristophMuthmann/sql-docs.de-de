---
title: Genehmigung erforderlich (Master Data Services) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b475a53d-269d-49f3-bb42-965c555f80be
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f73510c38944126f65567dcb0e6a8b97ec2498e0
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

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
  
  
