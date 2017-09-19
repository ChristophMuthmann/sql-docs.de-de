---
title: 'SQL Server-Beispiele: Modellbereitstellungspakete (MDS) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Master Data Services
- Beispiel
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
caps.latest.revision: 21
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: bda0dbc730e24017dfc1978e691d3da654a15149
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>SQL Server-Beispiele: Modellbereitstellungspakete (MDS)
  Beispiele von Modellpaketen mit Daten sind in der Installation von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]enthalten. Der Standardspeicherort für die Pakete ist \<Laufwerk>\Programme\Microsoft SQL Server\130\Master Data Services\Samples\Packages.  
  
 Eine Anleitung zum Bereitstellen der Beispielmodellpakete finden Sie unter [Bereitstellen von Beispielmodelle und Daten](../master-data-services/master-data-services-installation-and-configuration.md#deploySample). Stellen Sie diese Beispielmodellpakete mit dem [MDSModelDeploy-Tool](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)bereit.  
  
> [!IMPORTANT]  
>  **Beispiel-Updates in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
>   
>  Die Beispielpakete wurden aktualisiert, um die folgenden neuen Funktionen zu unterstützen.  
>   
>  -   m:n-Beziehungen anzeigen  
>   
>      Weitere Informationen finden Sie unter [Eine m:n-Beziehung in einem Beispielmodell](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md#M2MSample).  

> -   Schränken Sie zulässige Werte für domänenbasierte Attribute ein.  
>   
>      Weitere Informationen finden Sie unter [Erstellen eines domänenbasierten Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md).  
> -   Genehmigung für Änderungen an Entitäten anfordern  
>   
>      Weitere Informationen finden Sie unter [Genehmigung erforderlich &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md).  
> -   Geschäftsregeln mit Not- und Else-Operatoren verwenden  
>   
>      Weitere Informationen finden Sie unter [Beispiele für Geschäftsregeln](../master-data-services/business-rule-examples-master-data-services.md).  
> -   Benutzerdefinierten Index implementieren  
>   
>      Weitere Informationen finden Sie unter [Benutzerdefinierter Index &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
 

 
 In Master Data Services ist ein Paket eine XML-Datei, die eine zur Bereitstellung geeignete Modellstruktur enthält und optional Daten vom Modell. Verschieben Sie Kopien von Modellen mithilfe von Modellpaketen von einer MDS-Umgebung in eine andere, oder erstellen Sie neue Modelle in Ihrer vorhandenen [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Umgebung.  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellen eines Modellbereitstellungspakets mit MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  

