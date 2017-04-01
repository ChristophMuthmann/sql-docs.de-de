---
title: "Abgeleitete Hierarchien mit expliziten Abschl&#252;ssen (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Hierarchien [Master Data Services], abgeleitete Hierarchien mit expliziten Abschlüssen"
  - "Explizite Hierarchien, abgeleitete Hierarchien mit expliziten Abschlüssen"
  - "Abgeleitete Hierarchien, abgeleitete Hierarchien mit expliziten Abschlüssen"
ms.assetid: 6a82ff66-c137-4757-99bb-787d189b4295
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Abgeleitete Hierarchien mit expliziten Abschl&#252;ssen (Master Data Services)
  Wenn in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]die Ebenen aus einer expliziten Hierarchie als oberste Ebenen einer abgeleiteten Hierarchie verwendet werden, wird dies als abgeleitete Hierarchie mit explizitem Abschluss bezeichnet.  
  
 Die explizite Hierarchie muss auf der gleichen Entität wie die Entität am oberen Ende der abgeleiteten Hierarchie basieren.  
  
 In der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]-Benutzeroberfläche erstellen Sie diesen Hierarchietyp durch Ziehen einer expliziten Hierarchie in die oberste Ebene einer abgeleiteten Hierarchie.  
  
 ![mds_conc_explicit_cap_UI_structure](../master-data-services/media/mds-conc-explicit-cap-ui-structure.gif "mds_conc_explicit_cap_UI_structure")  
  
## Beispiel für eine abgeleitete Hierarchie mit explizitem Abschluss  
 In diesem Beispiel stammen die Elemente in der expliziten Hierarchie aus der Entität Subcategory. In der abgeleiteten Hierarchie stammen die Elemente der obersten Ebene auch aus der Entität Unterkategorie.  
  
 ![mds_conc_explicit_cap_UI_example](../master-data-services/media/mds-conc-explicit-cap-ui-example.gif "mds_conc_explicit_cap_UI_example")  
  
 Durch die Verwendung der expliziten Hierarchie am oberen Rand einer abgeleiteten Hierarchie wird die abgeleitete Hierarchie unregelmäßig.  
  
## Regeln  
  
-   Sie können nicht mehr als eine explizite Hierarchie in einer abgeleiteten Hierarchie mit explizitem Abschluss haben.  
  
-   Sie können die gleiche explizite Hierarchie als Abschluss für mehrere abgeleitete Hierarchien verwenden.  
  
-   Sie können keine Hierarchieelementberechtigungen an abgeleitete Hierarchien mit expliziten Abschlüssen zuweisen. Wenn Sie der expliziten Hierarchie oder der abgeleiteten Hierarchie einzeln Berechtigungen zuweisen, wirken sich die Berechtigungen auf beide Hierarchien aus.  
  
## Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie eine abgeleitete Hierarchie.|[Erstellen einer abgeleiteten Hierarchie &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Erstellen Sie eine explizite Hierarchie.|[Erstellen einer expliziten Hierarchie &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Löschen Sie eine vorhandene abgeleitete Hierarchie.|[Löschen einer abgeleiteten Hierarchie &#40;Master Data Services&#41;](../master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
|||  
  
## Verwandte Inhalte  
  
-   [Abgeleitete Hierarchien &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  