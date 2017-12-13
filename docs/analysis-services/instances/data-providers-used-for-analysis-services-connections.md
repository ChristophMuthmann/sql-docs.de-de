---
title: "Für Analysis Services-Verbindungen verwendete Datenanbieter | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 10f2596b6a2111fac89fc996bf6be521d7158f5d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>Für Analysis Services-Verbindungen verwendete Clientbibliotheken (Datenanbieter)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Analysis Services stellt drei Clientbibliotheken, auch bekannt als **Datenanbieter**für Server- und Datenzugriff von Tools und -Clientanwendungen. Tools wie SSMS und SSDT und Anwendungen, wie Power BI Desktop und Excel mit Analysis Services herstellen, mit diese Bibliotheken. Zwei der Clientbibliotheken, ADOMD.NET, und Analysis Services Management Objects (AMO), sind verwaltete Client-Bibliotheken. Der Analysis Services-OLE DB-Anbieter (MSOLAP DLL) ist eine native Client-Bibliothek. 
  
##  <a name="bkmk_downloadsite"></a>Herunterladen einer neuere Versionen  
 Die auf dem Clientcomputer installierte Version sollte mit der Hauptversion des Servers übereinstimmen, der die Daten bereitstellt. Wenn die Serverinstallation neuer als die auf den Arbeitsstationen im Netzwerk installierten Datenanbieter ist, müssen Sie u. U. neuere Bibliotheken installieren.  

Clientbibliotheken, die in früheren SQL Server-Feature Packs enthalten entsprechen auf die SQL-Version. Allerdings können sie nicht die neuesten sein. Herstellen einer Verbindung mit Azure Analysis Services erfordern eine höhere Versionen. Alle Versionen sind abwärtskompatibel.

Um die neuesten zu erhalten, finden Sie unter [Clientbibliotheken für Verbindungen mit Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers). 
  
## <a name="see-also"></a>Siehe auch  
 [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
