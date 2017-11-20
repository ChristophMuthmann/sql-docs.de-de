---
title: Erstellen einer expliziten Hierarchie (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/01/2016
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
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 1bbc9d8a78915c3be4a5530c3d47909505dea599
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>Erstellen einer expliziten Hierarchie (Master Data Services)
  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine explizite Hierarchie, wenn Sie eine unregelmäßige Hierarchie benötigen, in der Elemente auf jeder Ebene vorhanden sein können. Explizite Hierarchien enthalten Elemente aus einer einzelnen Entität.  
  
 Wenn Sie eine explizite Hierarchie erstellt haben, können Sie dieser im Funktionsbereich **Explorer** Elemente hinzufügen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Die Entität muss für explizite Hierarchien und Auflistungen aktiviert werden.  
  
### <a name="to-create-an-explicit-hierarchy"></a>So erstellen Sie eine explizite Hierarchie  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** im Raster die Zeile der Entität aus, für die Sie eine explizite Hierarchie erstellen möchten.  
  
4.  Klicken Sie auf **explizite Hierarchien**.  
  
5.  Klicken Sie auf der Seite **Manage Explicit Hierarchy** (Explizite Hierarchie verwalten) auf **Add**(Hinzufügen).  
  
6.  Geben Sie im Feld **Name** einen Namen für die Hierarchie ein.  
  
7.  Optional können Sie das Kontrollkästchen für **Obligatorische Hierarchie** deaktivieren, um die Hierarchie als nicht obligatorische Hierarchie zu erstellen. Weitere Informationen zu Hierarchietypen finden Sie unter [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md).  
  
8.  Klicken Sie auf **Speichern**.  
  
## <a name="grid-columns"></a>Rasterspalten  
 Für jede erstellte explizite Hierarchie wird dem Raster eine Zeile mit sieben Spalten hinzugefügt. Die Spalten werden im Folgenden beschrieben.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|Status|Der Status der Entität. Wenn Sie auf **Speichern** klicken, wird das folgende Bild angezeigt, das angibt, dass die Entität aktualisiert wird.<br /><br /> ![Symbol für Statusaktualisierung](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status")<br /><br /> Wenn beim Erstellen oder Bearbeiten einer Entität Fehler auftreten, wird das folgende Bild angezeigt.<br /><br /> ![Symbol für Fehlerstatus](../master-data-services/media/mds-statusicon-error.png "Icon for error status")<br /><br /> Falls der Status „OK“ lautet, wird das folgende Bild angezeigt.<br /><br /> ![Symbol für den Status OK](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status")|  
|Name|Der explizite Name der Hierarchie.|  
|Obligatorisch|Gibt an, ob die explizite Hierarchie erforderlich ist.|  
|Erstellt von|Der Benutzername des Benutzers, der die explizite Hierarchie erstellt hat.|  
|Erstellt am|Das Datum und die Uhrzeit der Erstellung der expliziten Hierarchie.|  
|Aktualisiert von|Der Benutzername des Benutzers, der die explizite Hierarchie zuletzt aktualisiert hat.|  
|Aktualisiert am|Das Datum und die Uhrzeit der letzten Aktualisierung der expliziten Hierarchie.|  
  
## <a name="next-steps"></a>Nächste Schritte  
  
-   [Erstellen eines konsolidierten Elements &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)  
  
  
  
## <a name="see-also"></a>Siehe auch  
 [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [Abgeleitete Hierarchien mit expliziten Abschlüssen &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Ändern des Namens einer expliziten Hierarchie &#40;Master Data Services&#41;](../master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  


