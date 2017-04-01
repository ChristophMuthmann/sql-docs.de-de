---
title: "Elemente (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Blattelemente [Master Data Services]"
  - "Konsolidierte Elemente [Master Data Services]"
  - "Konsolidierte Elemente [Master Data Services], Informationen zu konsolidierten Elementen"
  - "Elemente [Master Data Services], Informationen zu Elementen"
  - "Blattelemente [Master Data Services], Informationen zu Blattelementen"
  - "Elemente [Master Data Services]"
ms.assetid: 0fda32b9-677d-4ba2-bb28-f76f2383a30f
caps.latest.revision: 16
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# Elemente (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]sind Elemente die physischen Masterdaten. Ein Element kann z. B. ein Fahrrad mit der Modellbezeichnung Road-150 in einer Product-Entität oder ein bestimmter Kunde in einer Customer-Entität sein.  
  
## Zusammenhang zwischen Elementen und anderen Modellobjekten  
 Sie können sich Elemente als Zeilen in einer Tabelle vorstellen. Verwandte Elemente sind in einer Entität enthalten, und jedes Element wird von Attributwerten definiert.  
  
 In diesem Beispiel stellt die Tabelle eine Entität, die Zeilen in der Tabelle die Elemente und die Spalten in der Tabelle die Attribute dar. Jede Zelle stellt einen Attributwert für ein bestimmtes Element dar.  
  
 ![Als Tabelle dargestellte Master Data Services-Entität](../master-data-services/media/mds-conc-entity-table.gif "Als Tabelle dargestellte Master Data Services-Entität")  
  
## Elementtypen  
 Es gibt drei Arten von Elementen: Blattelemente, konsolidierte Elemente und Sammlungselemente.  
  
 Blattelemente sind die Standardelemente in einer Entität.  
  
-   In abgeleiteten Hierarchien sind Blattelemente der einzige Typ des Elements. Blattelemente aus einer Entität werden als übergeordnete Elemente der Blattelemente aus einer anderen Entität verwendet.  
  
-   In expliziten Hierarchien sind Blattelemente die niedrigste Ebene und können nicht über untergeordnete Elemente verfügen.  
  
 Konsolidierte Elemente sind nur vorhanden, wenn explizite Hierarchien und Auflistungen für die Entität aktiviert sind.  
  
-   Abgeleitete Hierarchien enthalten keine konsolidierten Elemente.  
  
-   In expliziten Hierarchien können konsolidierte Elemente übergeordnete Elemente anderer Elemente innerhalb der Hierarchie sein, oder sie können untergeordnete Elemente sein.  
  
## Organisieren von Elementen mithilfe von Hierarchien und Auflistungen  
 Hierarchien und Auflistungen können verwendet werden, um Elemente für die Berichterstellung oder Analyse zu gruppieren. Weitere Informationen finden Sie unter [Hierarchien &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md) und [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md).  
  
## Beispiel für ein Element  
 Im folgenden Beispiel schließt jedes Element einen Attributwert Name, Code, Subcategory StandardCost, ListPrice und FilePhoto ein.  
  
 ![Entitätstabelle für Fahrradprodukte](../master-data-services/media/mds-conc-entity-table-w-data.gif "Entitätstabelle für Fahrradprodukte")  
  
## Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie ein Blattelement.|[Erstellen eines Blattelements &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Erstellen Sie ein neues konsolidiertes Element.|[Erstellen eines konsolidierten Elements &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)|  
|Löschen Sie ein vorhandenes Element oder eine Auflistung.|[Löschen eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)|  
|Reaktivieren Sie ein gelöschtes Element oder eine Auflistung.|[Reaktivieren eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)|  
|Aktualisieren Sie die Attributwerte eines Elements.|[Ändern des Attributtyps &#40;MDS-Add-In für Excel&#41;](../master-data-services/microsoft-excel-add-in/change-the-attribute-type-mds-add-in-for-excel.md)|  
|Verschieben Sie Elemente innerhalb einer Hierarchie.|[Verschieben von Elementen innerhalb einer Hierarchie &#40;Master Data Services&#41;](../Topic/Move%20Members%20within%20a%20Hierarchy%20\(Master%20Data%20Services\).md)|  
|Beheben von Konflikten beim Zusammenführen.|[Konflikte zusammenführen &#40;Master Data Services&#41;](../master-data-services/merge-conflicts-master-data-services.md)|  
  
## Verwandte Inhalte  
  
-   [Übersicht über Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [Attribute &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
-   [Hierarchien &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md)  
  
-   [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [Blattberechtigungen &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)  
  
-   [Konsolidierte Berechtigungen &#40;Master Data Services&#41;](../Topic/Consolidated%20Permissions%20\(Master%20Data%20Services\).md)  
  
-   [Filteroperatoren &#40;Master Data Services&#41;](../master-data-services/filter-operators-master-data-services.md)  
  
  