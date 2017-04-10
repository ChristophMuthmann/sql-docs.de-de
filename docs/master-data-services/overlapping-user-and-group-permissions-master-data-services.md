---
title: "&#220;berlappende Benutzer- und Gruppenberechtigungen (Master Data Services) | Microsoft Docs"
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
  - "Benutzer [Master Data Services], Auflösen von Berechtigungen"
  - "Berechtigungen [Master Data Services], Benutzer und Gruppen (Überlappungen)"
  - "Gruppen [Master Data Services], Auflösen von Berechtigungen"
ms.assetid: 31c3cf7d-17d4-4474-b6a7-ffcb9fc45b37
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# &#220;berlappende Benutzer- und Gruppenberechtigungen (Master Data Services)
  Benutzerberechtigungen basieren auf:  
  
-   Berechtigungen aus Gruppenmitgliedschaften  
  
-   Dem Benutzer explizit zugewiesenen Berechtigungen  
  
 Wenn ein Benutzer mehreren Gruppen angehört und diese Gruppen Zugriff auf [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] haben, gelten die folgenden Regeln:  
  
-   Mit **Verweigern** werden alle anderen Berechtigungen überschrieben. Wenn die Objektberechtigung in einer Gruppe **Verweigern** lautet, so ist diese Berechtigung effektiv.  
  
-   Die Zugriffsberechtigung setzt sich aus allen gültigen Gruppenberechtigungen zusammen. Wenn die Objektberechtigung in einer Gruppe **Erstellen** und in einer anderen Gruppe **Aktualisieren** lautet, so lautet die effektive Berechtigung **Erstellen** und **Aktualisieren**.  
  
 Diese Regeln gelten sowohl für die Registerkarte **Modelle** als auch für die Registerkarte **Hierarchieelemente**. Berechtigungen werden für jede Registerkarte aufgelöst und dann kombiniert. Weitere Informationen finden Sie unter [Vorgehensweise: Festlegen von Berechtigungen &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md).  
  
> [!NOTE]  
>  Sie können die Auflösung überlappender Benutzer- und Gruppenberechtigungen in der Benutzeroberfläche anzeigen. Sowohl die Registerkarte **Modelle** als auch die Registerkarte **Hierarchieelemente** verfügt über eine Dropdownliste, aus der Sie **Effektiv** auswählen können, um effektive Berechtigungen anzuzeigen.  
  
## Beispiel 1  
 ![mds_conc_user_group_ex_1](../master-data-services/media/mds-conc-user-group-ex-1.gif "mds_conc_user_group_ex_1")  
  
 Der Benutzer gehört der Gruppe 1 und der Gruppe 2 an.  
  
 Der Benutzer verfügt für die Entität „Product“ über die Berechtigung **Lesen**.  
  
 Gruppe 1 verfügt für die Entität „Product“ über die Berechtigung **Aktualisieren**.  
  
 Gruppe 2 verfügt für die Entität „Product“ über die Berechtigung **Lesen**.  
  
 Ergebnis: Die effektive Berechtigung des Benutzers für die Entität „Product“ lautet **Aktualisieren**.  
  
## Beispiel 2  
 ![mds_conc_user_group_ex_2](../master-data-services/media/mds-conc-user-group-ex-2.gif "mds_conc_user_group_ex_2")  
  
 Der Benutzer gehört der Gruppe 1 und der Gruppe 2 an.  
  
 Der Benutzer verfügt für die Entität „Product“ über die Berechtigung **Lesen**.  
  
 Gruppe 1 verfügt für die Entität „Product“ über die Berechtigung **Aktualisieren**.  
  
 Gruppe 2 verfügt für die Entität „Product“ über die Berechtigung **Verweigern**.  
  
 Ergebnis: Die effektive Berechtigung des Benutzers für die Entität „Product“ lautet **Verweigern**.  
  
## Beispiel 3  
 ![mds_conc_user_group_ex_3](../master-data-services/media/mds-conc-user-group-ex-3.gif "mds_conc_user_group_ex_3")  
  
 Der Benutzer gehört der Gruppe 1 und der Gruppe 2 an.  
  
 Der Benutzer verfügt für eine Gruppe von Elementen unter einem Hierarchieknoten über die Berechtigung **Aktualisieren**.  
  
 Gruppe 1 verfügt für eine Gruppe von Elementen unter einem Hierarchieknoten über die Berechtigung **Lesen**.  
  
 Gruppe 2 verfügt für eine Gruppe von Elementen unter einem Hierarchieknoten über die Berechtigung **Lesen**.  
  
 Ergebnis: Die effektive Berechtigung des Benutzers für die Elemente lautet **Aktualisieren**.  
  
## Siehe auch  
 [Vorgehensweise: Festlegen von Berechtigungen &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Überlappende Modell- und Elementberechtigungen &#40;Master Data Services&#41;](../master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  