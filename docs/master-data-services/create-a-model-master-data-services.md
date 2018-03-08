---
title: Erstellen eines Modells (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
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
- models [Master Data Services], creating models
- creating models [Master Data Services]
ms.assetid: 9bb3b3b3-bde8-44aa-ad62-eaae21188141
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e49ea38d232782f4c98e1ff5e2084daee1f39cd
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="create-a-model-master-data-services"></a>Erstellen eines Modells (Master Data Services)
  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]ein Modell, das Modellobjekte enthalten soll.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-create-a-model"></a>So erstellen Sie ein Modul  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Modelle**.  
  
3.  Klicken Sie auf der Seite **Modelle verwalten** auf **Hinzufügen**. Auf der rechten Seite wird ein Panel angezeigt.  
  
4.  Geben Sie im Feld **Name** den Namen des Modells ein.  
  
5.  (Optional) Geben Sie im Feld **Beschreibung** die Modellbeschreibung ein.  
  
6.  Wählen Sie im Feld **Tage für Protokollbeibehaltung** eine der Optionen für die Aufbewahrung von Protokolldaten aus. Der Standardwert ist **Systemeinstellung**, was bedeutet, dass der Wert der Systemeinstellungen in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] übernommen wird. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
     Wählen Sie **NEIN** aus, um die Systemeinstellung zu überschreiben und Transaktionsprotokolldaten nicht zu entfernen. Wählen Sie **JA** aus, und legen Sie das Feld **Tage** auf „0“ fest, um die Protokolldaten aller vorherigen Tage zu entfernen und nur die Protokolldaten des aktuellen Tags aufzubewahren. Wählen Sie **JA** aus, und legen Sie das Feld **Tage** auf eine bestimmte Anzahl von Tagen fest, um die Protokolldaten für die angegebene Anzahl von Tagen aufzubewahren.  
  
7.  Optional können Sie **Entität mit demselben Namen wie das Modell erstellen** auswählen, um eine Entität mit dem gleichen Namen wie das Modell zu erstellen.  
  
8.  Klicken Sie auf **Modell speichern**.  
  
 Für jedes erstellte Modell wird dem Raster eine Zeile mit acht Spalten hinzugefügt. Die acht Spalten lauten:  
  
-   **Status**: Der Status des Modells. Beim Klicken auf die Schaltfläche **Modell speichern** wird das Bild ![Aktualisieren](../master-data-services/media/mds-model-status-updating.png "Updating") angezeigt, das angibt, dass das Modell aktualisiert wird. Wenn beim Erstellen oder Bearbeiten eines Modells Fehler auftreten, wird das Bild ![Fehler](../master-data-services/media/mds-model-status-error.png "Error") angezeigt. Andernfalls lautet der Status „OK“, und das Bild ![OK](../master-data-services/media/mds-model-status-ok.png "OK") angezeigt.  
  
-   **Name**: Der Name des Modells.  
  
-   **Beschreibung**: Die Beschreibung des Modells.  
  
-   **Tage für Protokollbeibehaltung**: Die Beibehaltungsdauer des Protokolls für das Modell in Tagen.  
  
-   **Erstellt von**: Der Benutzername des Benutzers, der das Modell erstellt hat.  
  
-   **Erstellungsdatum und -uhrzeit**: Das Datum und die Uhrzeit der Erstellung des Modells.  
  
-   **Aktualisiert von**: Der Benutzername des Benutzers, der das Modell zuletzt aktualisiert hat.  
  
-   **Aktualisierungsdatum und -uhrzeit**: Das Datum und die Uhrzeit der letzten Aktualisierung des Modells.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [Erstellen einer Entität &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Modelle &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)   
 [Löschen eines Modells &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [Bearbeiten eines Modells &#40;Master Data Services&#41;](../master-data-services/edit-model-master-data-services.md)   
 [Transaktionen &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
  
