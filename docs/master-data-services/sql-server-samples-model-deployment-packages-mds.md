---
title: 'SQL Server-Beispiele: Modellieren Bereitstellungspakete (MDS) | Microsoft Docs'
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
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7a031ba18c6782cdd73ae31ef395bc2ecdcf102
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>SQL Server-Beispiele: Modellbereitstellungspakete (MDS)
  Beispiele von Modellpaketen mit Daten sind in der Installation von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]enthalten. Der Standardspeicherort für diese Dateien Paket ist \<Laufwerk > \Programme\Microsoft SQL Server\130\Master Data services\samples\packages verwendet.  
  
 Eine Anleitung zum Bereitstellen der Beispielmodellpakete finden Sie unter [Bereitstellen von Beispielmodelle und Daten](../master-data-services/master-data-services-installation-and-configuration.md#deploySample). Stellen Sie diese Beispielmodellpakete mit dem [MDSModelDeploy-Tool](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)bereit.  
  
> [!IMPORTANT]  
>  **Beispiel-Updates in[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
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
 

 
 In Master Data Services ist ein Paket eine XML-Datei, die eine zur Bereitstellung geeignete Modellstruktur und optional die Daten aus dem Modell enthält. Verschieben Sie Kopien von Modellen mithilfe von Modellpaketen von einer MDS-Umgebung in eine andere, oder erstellen Sie neue Modelle in Ihrer vorhandenen [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Umgebung.  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellen eines Modellbereitstellungspakets mit MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  

