---
title: "Überlappende Benutzer- und Gruppenberechtigungen (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- users [Master Data Services], resolving permissions
- permissions [Master Data Services], user and group overlaps
- groups [Master Data Services], resolving permissions
ms.assetid: 31c3cf7d-17d4-4474-b6a7-ffcb9fc45b37
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 1dcefd134dccc0ae8a7039758dcd987e09b90813
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="overlapping-user-and-group-permissions-master-data-services"></a>Überlappende Benutzer- und Gruppenberechtigungen (Master Data Services)
  Benutzerberechtigungen basieren auf:  
  
-   Berechtigungen aus Gruppenmitgliedschaften  
  
-   Dem Benutzer explizit zugewiesenen Berechtigungen  
  
 Wenn ein Benutzer mehreren Gruppen angehört und diese Gruppen Zugriff auf [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]haben, gelten die folgenden Regeln:  
  
-   Mit**Verweigern** werden alle anderen Berechtigungen überschrieben. Wenn die Objektberechtigung in einer Gruppe **Verweigern** lautet, so ist diese Berechtigung effektiv.  
  
-   Die Zugriffsberechtigung setzt sich aus allen gültigen Gruppenberechtigungen zusammen. Wenn die Objektberechtigung in einer Gruppe **Erstellen** und in einer anderen Gruppe **Aktualisieren** lautet, so lautet die effektive Berechtigung **Erstellen** und **Aktualisieren**.  
  
 Diese Regeln gelten sowohl für die Registerkarte **Modelle** als auch für die Registerkarte **Hierarchieelemente** . Berechtigungen werden für jede Registerkarte aufgelöst und dann kombiniert. Weitere Informationen finden Sie unter [Vorgehensweise: Festlegen von Berechtigungen &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md).  
  
> [!NOTE]  
>  Sie können die Auflösung überlappender Benutzer- und Gruppenberechtigungen in der Benutzeroberfläche anzeigen. Sowohl die Registerkarte **Modelle** als auch die Registerkarte **Hierarchieelemente** verfügt über eine Dropdownliste, aus der Sie **Effektiv** auswählen können, um effektive Berechtigungen anzuzeigen.  
  
## <a name="example-1"></a>Beispiel 1  
 ![mds_conc_user_group_ex_1](../master-data-services/media/mds-conc-user-group-ex-1.gif "mds_conc_user_group_ex_1")  
  
 Der Benutzer gehört der Gruppe 1 und der Gruppe 2 an.  
  
 Der Benutzer verfügt für die Entität „Product“ über die Berechtigung **Lesen** .  
  
 Gruppe 1 verfügt für die Entität „Product“ über die Berechtigung **Aktualisieren** .  
  
 Gruppe 2 verfügt für die Entität „Product“ über die Berechtigung **Lesen** .  
  
 Ergebnis: Die effektive Berechtigung des Benutzers für die Entität „Product“ lautet **Aktualisieren** .  
  
## <a name="example-2"></a>Beispiel 2  
 ![mds_conc_user_group_ex_2](../master-data-services/media/mds-conc-user-group-ex-2.gif "mds_conc_user_group_ex_2")  
  
 Der Benutzer gehört der Gruppe 1 und der Gruppe 2 an.  
  
 Der Benutzer verfügt für die Entität „Product“ über die Berechtigung **Lesen** .  
  
 Gruppe 1 verfügt für die Entität „Product“ über die Berechtigung **Aktualisieren** .  
  
 Gruppe 2 verfügt für die Entität „Product“ über die Berechtigung **Verweigern** .  
  
 Ergebnis: Die effektive Berechtigung des Benutzers für die Entität „Product“ lautet **Verweigern** .  
  
## <a name="example-3"></a>Beispiel 3  
 ![mds_conc_user_group_ex_3](../master-data-services/media/mds-conc-user-group-ex-3.gif "mds_conc_user_group_ex_3")  
  
 Der Benutzer gehört der Gruppe 1 und der Gruppe 2 an.  
  
 Der Benutzer verfügt für eine Gruppe von Elementen unter einem Hierarchieknoten über die Berechtigung **Aktualisieren** .  
  
 Gruppe 1 verfügt für eine Gruppe von Elementen unter einem Hierarchieknoten über die Berechtigung **Lesen** .  
  
 Gruppe 2 verfügt für eine Gruppe von Elementen unter einem Hierarchieknoten über die Berechtigung **Lesen** .  
  
 Ergebnis: Die effektive Berechtigung des Benutzers für die Elemente lautet **Aktualisieren** .  
  
## <a name="see-also"></a>Siehe auch  
 [Vorgehensweise: Festlegen von Berechtigungen &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Überlappende Modell- und Elementberechtigungen &#40;Master Data Services&#41;](../master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  

