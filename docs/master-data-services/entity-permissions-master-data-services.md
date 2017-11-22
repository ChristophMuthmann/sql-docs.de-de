---
title: "Entitätsberechtigungen (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- entities [Master Data Services], permissions
- permissions [Master Data Services], entities
ms.assetid: 22785062-4faf-46ee-bffa-01cbd6d5a5b3
caps.latest.revision: "6"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba616e93dac142ea283a15640afec5f0acf6228c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="entity-permissions-master-data-services"></a>Entitätsberechtigungen (Master Data Services)
  Entitätsberechtigungen gelten für:  
  
-   Alle Attribute der Entität, einschließlich **Name** und **Code**für Blatt- und konsolidierte Elemente.  
  
-   Alle Auflistungen der Entität.  
  
-   Explizite Hierarchiemitgliedschaften und Beziehungen.  
  
 Wenn Sie über eine Berechtigung für eine Entität verfügen, können Sie der Entität, ihren expliziten Hierarchien und ihren Auflistungen Elemente hinzufügen bzw. Elemente daraus entfernen.  
  
> [!NOTE]  
>  Diese Berechtigungen gelten nur für den Funktionsbereich **Explorer** der Benutzeroberfläche.  
  
|Berechtigung|Description|  
|----------------|-----------------|  
|**Lesen**|Der Benutzer kann Elemente, Attribute, Hierarchiemitgliedschaften oder Sammlungszugehörigkeiten anzeigen.|  
|**Create**|Der Benutzer kann Elemente erstellen und während der Erstellung Attributwerte zuweisen.|  
|**Update**|Der Benutzer kann Elemente, Attribute, Hierarchiemitgliedschaften oder Sammlungszugehörigkeiten aktualisieren.|  
|**Delete**|Der Benutzer kann Elemente löschen.|  
|**Verweigern**|Der Zugriff auf die Entität wird vollständig verweigert.|  
  
 Die Berechtigungen zum Lesen, Erstellen, Aktualisieren und Löschen können miteinander kombiniert werden. Wenn Berechtigungen zum Erstellen, Aktualisieren und Löschen zugewiesen werden, wird die Leseberechtigung automatisch zugewiesen.  
  
## <a name="see-also"></a>Siehe auch  
 [Zuweisen von Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
