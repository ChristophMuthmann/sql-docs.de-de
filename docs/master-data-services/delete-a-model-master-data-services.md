---
title: "L&#246;schen eines Modells (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Löschen von Modellen [Master Data Services]"
  - "Modelle [Master Data Services], Löschen von Modellen"
ms.assetid: f0ad3cc4-aed7-47c8-94bc-2971fe9fe871
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# L&#246;schen eines Modells (Master Data Services)
  Löschen Sie ein Modell, um das Modell und alle zugehörigen Daten aus [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]zu entfernen.  
  
> [!NOTE]  
>  Nach Abschluss dieser Prozedur sind alle Objekte und alle Daten aus allen Versionen des Modells permanent gelöscht.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### So löschen Sie ein Modell  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Modelle**.  
  
3.  Wählen Sie auf der Seite **Modelle verwalten** im Raster die Zeile des Modells aus, das Sie löschen möchten.  
  
4.  Klicken Sie auf **Löschen**.  
  
5.  Klicken Sie im Bestätigungsdialogfeld auf **OK**.  
  
6.  Klicken Sie im zusätzlichen Bestätigungsdialogfeld auf **OK**.  
  
 Die Spalte **Status** im Raster zeigt den Status des Vorgangs für das Modell. Beim Klicken auf die Schaltfläche **Modell speichern** wird das Bild ![Updating](../master-data-services/media/mds-model-status-updating.png "Updating") angezeigt, das angibt, dass das Modell aktualisiert wird. Wenn beim Erstellen oder Bearbeiten eines Modells Fehler auftreten, wird das Bild ![Error](../master-data-services/media/mds-model-status-error.png "Error") angezeigt. Andernfalls lautet der Status „OK“, und das Bild ![OK](../master-data-services/media/mds-model-status-ok.png "OK") wird angezeigt.  
  
## Siehe auch  
 [Modelle &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)  
  
  