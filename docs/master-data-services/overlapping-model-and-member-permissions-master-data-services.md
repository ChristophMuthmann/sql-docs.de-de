---
title: "&#220;berlappende Modell- und Elementberechtigungen (Master Data Services) | Microsoft Docs"
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
  - "Modelle [Master Data Services], effektive Berechtigungen"
  - "Berechtigungen [Master Data Services], Überlappungen für Modelle und Elemente"
  - "Elemente [Master Data Services], effektive Berechtigungen"
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# &#220;berlappende Modell- und Elementberechtigungen (Master Data Services)
  Die einem Element zugewiesene Berechtigung kann mit einer einem Modellobjekt zugewiesenen Berechtigung überlappen. Bei einer Überlappung tritt die restriktivere Berechtigung in Kraft.  
  
 Wenn ein Element über eine Berechtigung verfügt, die sich von der des zugehörigen Modellobjekts unterscheidet, gelten die folgenden Regeln:  
  
-   **Verweigern** überschreibt alle anderen Berechtigungen.  
  
-   **Admin** Berechtigung auf der Modellebene überschreibt alle anderen Berechtigungen und Zugriffsberechtigungen auf untergeordneten Ebenen alle (CRUD) geändert.  
  
-   Die effektive Zugriffsberechtigungen überschneidet sich mit Berechtigungen für Elemente und Attribute.  
  
     Wenn Berechtigungen umfassen z. B. **Erstellen** und **Update**, ist die Berechtigung für Attribute **Update**. Ist die effektive Berechtigung **Update**.  
  
 Das folgende Bild zeigt, welche Berechtigungen für einen einzelnen Attributwert wirksam werden, wenn Attributberechtigungen sich von Elementberechtigungen unterscheiden.  
  
 ![mds_conc_security_member_overlap_table](../master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## Beispiel 1  
 ![mds_conc_overlap_model_1](../master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 Auf der **Modelle** Registerkarte, um die Product-Entität hat **Update** zugewiesene Berechtigung. Diese Berechtigung wird von allen Attributen in der Entität geerbt.  
  
 Auf der **Hierarchieelemente** Registerkarte, um die unterkategorieknoten "Mountain Bikes" in einer abgeleiteten Hierarchie hat **Update** zugewiesene Berechtigung.  
  
 Ergebnis: In **Explorer**, der Benutzer hat **Update** Berechtigung für alle Attributwerte für alle Elemente im Knoten "Mountain Bikes". Alle anderen Elemente und Attribute werden ausgeblendet.  
  
 ![mds_conc_overlap_model_example_1](../master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## Beispiel 2  
 ![mds_conc_overlap_model_2](../master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 Auf der **Modelle** Registerkarte, um das Subcategory-Attribut hat **Update** zugewiesene Berechtigung.  
  
 Auf der **Hierarchieelemente** Registerkarte der unterkategorieknoten "Mountain Bikes" in einer abgeleiteten Hierarchie explizit zugewiesen **Lesen** Berechtigung.  
  
 Ergebnis: In **Explorer**, der Benutzer hat **Lesen** Berechtigung für die Subcategory-Attributwerte für die Elemente im Knoten "Mountain Bikes". Alle anderen Elemente und Attribute werden ausgeblendet.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## Beispiel 3  
 ![mds_conc_overlap_model_3](../master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 Auf der **Modelle** Registerkarte, um das Subcategory-Attribut hat **Lesen** zugewiesene Berechtigung.  
  
 Auf der **Hierarchieelemente** Registerkarte die Unterkategorie "Mountain Bikes" in einer abgeleiteten Hierarchie explizit zugewiesen **Update** Berechtigung.  
  
 Ergebnis: In **Explorer**, der Benutzer hat **Lesen** Berechtigung für die Attributwerte. Alle anderen Elemente und Attribute werden ausgeblendet.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## Siehe auch  
 [Bestimmen von Berechtigungen & #40; Master Data Services & #41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Überlappende Benutzer und Gruppenberechtigungen & #40; Master Data Services & #41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  