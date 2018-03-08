---
title: Elemente (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- leaf members [Master Data Services]
- consolidated members [Master Data Services]
- consolidated members [Master Data Services], about consolidated members
- members [Master Data Services], about members
- leaf members [Master Data Services], about leaf members
- members [Master Data Services]
ms.assetid: 0fda32b9-677d-4ba2-bb28-f76f2383a30f
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 026efa6fe3e44bdfa50e300296bfe6df7d773bbc
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="members-master-data-services"></a>Elemente (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]sind Elemente die physischen Masterdaten. Ein Element kann z. B. ein Fahrrad mit der Modellbezeichnung Road-150 in einer Product-Entität oder ein bestimmter Kunde in einer Customer-Entität sein.  
  
## <a name="how-members-relate-to-other-model-objects"></a>Zusammenhang zwischen Elementen und anderen Modellobjekten  
 Sie können sich Elemente als Zeilen in einer Tabelle vorstellen. Verwandte Elemente sind in einer Entität enthalten, und jedes Element wird von Attributwerten definiert.  
  
 In diesem Beispiel stellt die Tabelle eine Entität, die Zeilen in der Tabelle die Elemente und die Spalten in der Tabelle die Attribute dar. Jede Zelle stellt einen Attributwert für ein bestimmtes Element dar.  
  
 ![Als Tabelle dargestellte Master Data Services-Entität](../master-data-services/media/mds-conc-entity-table.gif "Master Data Services Entity Represented as Table")  
  
## <a name="member-types"></a>Elementtypen  
 Es gibt drei Arten von Elementen: Blattelemente, konsolidierte Elemente und Sammlungselemente.  
  
 Blattelemente sind die Standardelemente in einer Entität.  
  
-   In abgeleiteten Hierarchien sind Blattelemente der einzige Typ des Elements. Blattelemente aus einer Entität werden als übergeordnete Elemente der Blattelemente aus einer anderen Entität verwendet.  
  
-   In expliziten Hierarchien sind Blattelemente die niedrigste Ebene und können nicht über untergeordnete Elemente verfügen.  
  
 Konsolidierte Elemente sind nur vorhanden, wenn explizite Hierarchien und Auflistungen für die Entität aktiviert sind.  
  
-   Abgeleitete Hierarchien enthalten keine konsolidierten Elemente.  
  
-   In expliziten Hierarchien können konsolidierte Elemente übergeordnete Elemente anderer Elemente innerhalb der Hierarchie sein, oder sie können untergeordnete Elemente sein.  
  
## <a name="use-hierarchies-and-collections-to-organize-members"></a>Organisieren von Elementen mithilfe von Hierarchien und Auflistungen  
 Hierarchien und Auflistungen können verwendet werden, um Elemente für die Berichterstellung oder Analyse zu gruppieren. Weitere Informationen finden Sie unter [Hierarchien &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md) und [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md).  
  
## <a name="member-example"></a>Beispiel für ein Element  
 Im folgenden Beispiel schließt jedes Element einen Attributwert Name, Code, Subcategory StandardCost, ListPrice und FilePhoto ein.  
  
 ![Entitätstabelle für Fahrradprodukte](../master-data-services/media/mds-conc-entity-table-w-data.gif "Bike Product Entity Table")  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie ein Blattelement.|[Erstellen eines Blattelements &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Erstellen Sie ein neues konsolidiertes Element.|[Erstellen eines konsolidierten Elements &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)|  
|Löschen Sie ein vorhandenes Element oder eine Auflistung.|[Löschen eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)|  
|Reaktivieren Sie ein gelöschtes Element oder eine Auflistung.|[Reaktivieren eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)|  
|Aktualisieren Sie die Attributwerte eines Elements.|[Ändern des Attributtyps &#40;MDS-Add-In für Excel&#41;](../master-data-services/microsoft-excel-add-in/change-the-attribute-type-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Übersicht über Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [Attribute &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
-   [Hierarchien &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md)  
  
-   [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [Blattberechtigungen &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)  
  
 
-   [Filteroperatoren &#40;Master Data Services&#41;](../master-data-services/filter-operators-master-data-services.md)  
  
  
