---
title: Bearbeiten des Modells (Master Data Services) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- models [Master Data Services], changing name
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08291f09ed7bc172fe22534e82b79ecc47ce55e1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="edit-model-master-data-services"></a>Bearbeiten eines Modells (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] können Sie den Namen und die Beschreibung eines Modells ändern und festlegen, wie viele Tage die Transaktionsprotokolle beibehalten werden.  
  
 Weitere Informationen finden Sie unter [Transaktionen &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-change-a-model"></a>So ändern Sie ein Modell  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Modelle**.  
  
3.  Wählen Sie auf der Seite **Modelle verwalten** im Raster die Zeile des Modells aus, dessen Name oder Beschreibung Sie ändern möchten.  
  
4.  Klicken Sie auf **Bearbeiten**.  
  
5.  Geben Sie im Feld **Name** den neuen Namen für das Modell ein.  
  
6.  Geben Sie im Feld **Beschreibung** die aktualisierte Beschreibung des Modells ein.  
  
7.  Wählen Sie im Feld **Tage für Protokollbeibehaltung** eine der Optionen für die Aufbewahrung von Protokolldaten aus. Der Standardwert ist **Systemeinstellung**, was bedeutet, dass der Wert der Systemeinstellungen in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] übernommen wird. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
     Wählen Sie **NEIN** aus, um die Systemeinstellung zu überschreiben und Transaktionsprotokolldaten nicht zu entfernen. Wählen Sie **JA** aus, und legen Sie das Feld **Tage** auf „0“ fest, um die Protokolldaten aller vorherigen Tage zu entfernen und nur die Protokolldaten des aktuellen Tags aufzubewahren. Wählen Sie **JA** aus, und legen Sie das Feld **Tage** auf eine bestimmte Anzahl von Tagen fest, um die Protokolldaten für die angegebene Anzahl von Tagen aufzubewahren.  
  
8.  Klicken Sie auf **Modell speichern**.  
  
 Die Spalte **Status** im Raster zeigt den Status des Vorgangs für das Modell. Beim Klicken auf die **speichern Modell** Schaltfläche, die ![aktualisieren](../master-data-services/media/mds-model-status-updating.png "aktualisieren") Bild angezeigt, was bedeutet, dass das Modell aktualisiert wird. Treten Fehler beim Erstellen oder Bearbeiten eines Modells der ![Fehler](../master-data-services/media/mds-model-status-error.png "Fehler") Bild angezeigt. Andernfalls lautet der Status „OK“, und das Bild ![OK](../master-data-services/media/mds-model-status-ok.png "OK") angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie ein Modell &#40; Master Data Services &#41;](../master-data-services/create-a-model-master-data-services.md)   
 [Löschen eines Modells &#40; Master Data Services &#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [Modelle &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
  
