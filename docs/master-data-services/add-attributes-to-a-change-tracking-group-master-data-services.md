---
title: "Hinzufügen von Attributen zu einer Änderungsnachverfolgungsgruppe (Master Data Services) | Microsoft-Dokumentation"
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
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 468d6712a515336fb60717ed1ba5c46cf644ca49
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>Hinzufügen von Attributen zu einer Änderungsnachverfolgungsgruppe (Master Data Services)
  Fügen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]einer Änderungsnachverfolgungsgruppe Attribute hinzu, wenn Sie Änderungen an den Werten des Attributs nachverfolgen möchten.  
  
> [!NOTE]  
>  Nachdem Sie einer Änderungsnachverfolgungsgruppe ein Attribut hinzugefügt haben, wird das Attribut in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank als geändert markiert, wenn die Werte für das Attribut geändert werden. Erstellen Sie eine Geschäftsregel, um auf der Grundlage der Änderung zu handeln.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Attribute müssen vorhanden sein, um sie der Änderungsnachverfolgungsgruppe hinzufügen zu können. Weitere Informationen finden Sie unter [Erstellen eines Textattributs &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>So fügen Sie einer Änderungnachverfolgungsgruppe Attribute hinzu  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** die Zeile der Entität aus, für die Sie ein Attribut erstellen möchten.  
  
4.  Klicken Sie auf **Attribute**.  
  
5.  Fügen Sie auf der Seite **Attribute verwalten** einen der folgenden Schritte aus.  
  
    -   Wenn das Attribut für Blattelemente bestimmt ist, wählen Sie **Blatt** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für konsolidierte Elemente bestimmt ist, wählen Sie **Konsolidiert** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für Sammlungen bestimmt ist, wählen Sie **Sammlung** im Listenfeld **Elementtypen** aus.  
  
6.  Wählen Sie die Zeile für das Attribut, das Sie bearbeiten möchten, und klicken Sie anschließend auf **Bearbeiten**.  
  
7.  Aktivieren Sie das Kontrollkästchen **Änderungsverfolgung aktivieren** .  
  
8.  Geben Sie im Feld **Änderungsverfolgungsgruppe** eine Zahl für die Gruppe ein.  
  
9. Klicken Sie auf **Attribut speichern**.  
  
     Für das bearbeitete Attribut wird die Spalte **Änderungsnachverfolgungsgruppe aktivieren** des Rasters geändert zu **Ja (Gruppe: Gruppennummer eingegeben)**.  
  
10. Wiederholen Sie diese Prozedur für alle Attribute, die Sie in die Gruppe einschließen möchten. Verwenden Sie die gleiche Änderungsnachverfolgungs-Gruppennummer für jedes Attribut in der Gruppe.  
  
## <a name="next-steps"></a>Nächste Schritte  
  
-   [Initiieren von Aktionen auf der Grundlage von Attributwertänderungen &#40;Master Data Services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Textattributs &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [Erstellen eines domänenbasierten Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  

