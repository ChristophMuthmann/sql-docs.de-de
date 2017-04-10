---
title: "Create a Consolidated Member (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "creating consolidated members [Master Data Services]"
  - "members [Master Data Services], creating consolidated members"
  - "Konsolidierte Elemente [Master Data Services], erstellen"
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
caps.latest.revision: 12
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 11
---
# Create a Consolidated Member (Master Data Services)
  Erstellen Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]ein konsolidiertes Element, wenn Sie einen übergeordneten Knoten für eine explizite Hierarchie wollen. Wenn Sie Daten in einer Massenoperation hinzufügen möchten, verwenden Sie stattdessen die Stagingtabellen. Weitere Informationen finden Sie unter [Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md).  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
-   Sie müssen mindestens die Berechtigung **Aktualisieren** für das konsolidierte Modellobjekt für die Entität besitzen, der Sie ein Element hinzufügen, sowie die Berechtigung **Erstellen** für den konsolidierten Typ unter der Entität.  
  
### So erstellen Sie ein konsolidiertes Element  
  
1.  Wählen Sie auf der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Startseite aus der Liste **Modell** ein Modell aus.  
  
2.  Wählen Sie aus der Liste **Version** eine Version aus.  
  
3.  Klicken Sie auf **Explorer**.  
  
4.  Zeigen Sie auf der Menüleiste auf **Hierarchien** , und klicken Sie auf den Namen der Hierarchie, der Sie ein konsolidiertes Element hinzufügen möchten.  
  
5.  Aktivieren Sie über dem Raster die Option **Konsolidierte Elemente** oder **Alle konsolidierten Elemente in der Hierarchie** .  
  
6.  Wählen Sie im linken Bereich einen Stammknoten oder ein konsolidiertes Element aus, unter dem Sie ein konsolidiertes Element erstellen möchten.  
  
7.  Klicken Sie auf **Hinzufügen**.  
  
8.  Vervollständigen Sie im Bereich rechts die Felder.  
  
9. Optional. Geben Sie im Feld **Anmerkungen** einen Kommentar dazu ein, warum das Element hinzugefügt wurde. Alle Benutzer, die Zugriff auf das Element haben, können die Anmerkung anzeigen.  
  
10. Klicken Sie auf **OK**.  
  
## Nächste Schritte  
  
-   [Verschieben von Elementen innerhalb einer Hierarchie &#40;Master Data Services&#41;](../Topic/Move%20Members%20within%20a%20Hierarchy%20\(Master%20Data%20Services\).md)  
  
## Siehe auch  
 [Erstellen einer expliziten Hierarchie &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Erstellen eines Blattelements &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)   
 [Elemente &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  