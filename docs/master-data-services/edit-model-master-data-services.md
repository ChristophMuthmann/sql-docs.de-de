---
title: "Bearbeiten eines Modells (Master Data Services) | Microsoft Docs"
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
  - "Modelle [Master Data Services], umbenennen"
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Bearbeiten eines Modells (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] können Sie den Namen und die Beschreibung eines Modells ändern und festlegen, wie viele Tage die Transaktionsprotokolle beibehalten werden.  
  
 Weitere Informationen finden Sie unter [Transaktionen &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### So ändern Sie ein Modell  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Modelle**.  
  
3.  Wählen Sie auf der Seite **Modelle verwalten** im Raster die Zeile des Modells aus, dessen Name oder Beschreibung Sie ändern möchten.  
  
4.  Klicken Sie auf **Bearbeiten**.  
  
5.  Geben Sie im Feld **Name** den neuen Namen für das Modell ein.  
  
6.  Geben Sie im Feld **Beschreibung** die aktualisierte Beschreibung des Modells ein.  
  
7.  Wählen Sie im Feld **Tage für Protokollbeibehaltung** eine der Optionen für die Aufbewahrung von Protokolldaten aus. Der Standardwert ist **Systemeinstellung**, was bedeutet, dass der Wert der Systemeinstellungen in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] übernommen wird. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
     Wählen Sie **NEIN** aus, um die Systemeinstellung zu überschreiben und Transaktionsprotokolldaten nicht zu entfernen. Wählen Sie **JA** aus, und legen Sie das Feld **Tage** auf „0“ fest, um die Protokolldaten aller vorherigen Tage zu entfernen und nur die Protokolldaten des aktuellen Tags aufzubewahren. Wählen Sie **JA** aus, und legen Sie das Feld **Tage** auf eine bestimmte Anzahl von Tagen fest, um die Protokolldaten für die angegebene Anzahl von Tagen aufzubewahren.  
  
8.  Klicken Sie auf **Modell speichern**.  
  
 Die Spalte **Status** im Raster zeigt den Status des Vorgangs für das Modell. Beim Klicken auf die Schaltfläche **Modell speichern** wird das Bild ![Updating](../master-data-services/media/mds-model-status-updating.png "Updating") angezeigt, das angibt, dass das Modell aktualisiert wird. Wenn beim Erstellen oder Bearbeiten eines Modells Fehler auftreten, wird das Bild ![Error](../master-data-services/media/mds-model-status-error.png "Error") angezeigt. Andernfalls lautet der Status „OK“, und das Bild ![OK](../master-data-services/media/mds-model-status-ok.png "OK") wird angezeigt.  
  
## Siehe auch  
 [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [Löschen eines Modells &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [Modelle &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
  