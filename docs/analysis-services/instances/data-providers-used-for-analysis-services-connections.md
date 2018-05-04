---
title: Für Analysis Services-Verbindungen verwendete Datenanbieter | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7703bda267a7b646bf6ccbbfee98c7401599f3a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>Für Analysis Services-Verbindungen verwendete Clientbibliotheken (Datenanbieter)
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services stellt drei Clientbibliotheken, auch bekannt als **Datenanbieter**für Server- und Datenzugriff von Tools und -Clientanwendungen. Tools wie SSMS und SSDT und Anwendungen, wie Power BI Desktop und Excel mit Analysis Services herstellen, mit diese Bibliotheken. Zwei der Clientbibliotheken, ADOMD.NET, und Analysis Services Management Objects (AMO), sind verwaltete Client-Bibliotheken. Der Analysis Services-OLE DB-Anbieter (MSOLAP DLL) ist eine native Client-Bibliothek. -Clientbibliotheken sind für SQL Server Analysis Services und Azure Analysis Services identisch.
  
##  <a name="bkmk_downloadsite"></a> Herunterladen einer neuere Versionen  
 Auf einem Clientcomputer installierte Version übereinstimmen, die Hauptversion des Servers, der die Daten bereitstellt. Wenn die Serverinstallation neuer als die auf den Arbeitsstationen im Netzwerk installierten Datenanbieter ist, müssen Sie u. U. neuere Bibliotheken installieren.  

Clientbibliotheken, die in früheren SQL Server-Feature Packs enthalten entsprechen auf die SQL-Version. Allerdings können sie nicht die neuesten sein. Herstellen einer Verbindung mit Azure Analysis Services erfordern eine höhere Versionen. Alle Versionen sind abwärtskompatibel.

Um die neuesten zu erhalten, finden Sie unter [Clientbibliotheken für Verbindungen mit Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers). 
  
## <a name="see-also"></a>Siehe auch  
 [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
