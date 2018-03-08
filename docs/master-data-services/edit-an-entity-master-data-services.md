---
title: "Bearbeiten einer Entität (Master Data Services) | Microsoft-Dokumentation"
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
- entities [Master Data Services], changing name
ms.assetid: 6a5b9f14-6dfc-49d7-a771-e96461d4feae
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 80bb4a70c306371910e0059c2d9bbb7a7330d617
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="edit-an-entity-master-data-services"></a>Bearbeiten einer Entität (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie eine Entität bearbeiten.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-edit-an-entity"></a>So bearbeiten Sie eine Entität  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entitäten verwalten** im Raster die Zeile für die Entität aus, die Sie ändern möchten, und klicken Sie anschließend auf **Bearbeiten**.  
  
4.  Geben Sie im Feld **Name** den aktualisierten Namen für die Entität ein.  
  
5.  Geben Sie im Feld **Beschreibung** die aktualisierte Beschreibung der Entität ein.  
  
6.  Geben Sie im Feld **Name für Stagingtabellen** den aktualisierten Namen für die Stagingtabelle ein.  
  
7.  Wählen Sie für das Feld **Transaktionsprotokolltyp** den aktualisierten Transaktionsprotokolltyp in der Dropdownliste aus.  
  
     Weitere Informationen finden Sie unter [Ändern des Transaktionsprotokolltyps von Entitäten &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md).  
  
8.  Aktivieren oder deaktivieren Sie das Kontrollkästchen **Codewerte automatisch erstellen**.  
  
     Weitere Informationen finden Sie unter [Automatische Codeerstellung &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)  
  
9. Aktivieren oder deaktivieren Sie das Kontrollkästchen **Datenkomprimierung aktivieren**. Die Zeilenkomprimierung ist standardmäßig aktiviert.  
  
     Weitere Informationen finden Sie unter [Datenkomprimierung](../relational-databases/data-compression/data-compression.md).  
  
## <a name="status"></a>Status  
 Die Statusspalte im Raster zeigt den Status des Vorgangs für die Entität. Wenn Sie auf **Entität speichern**klicken, wird das folgende Bild angezeigt, das angibt, dass die Entität aktualisiert wird.  
  
 ![Symbol für Statusaktualisierung](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status")  
  
 Wenn beim Erstellen oder Bearbeiten einer Entität Fehler auftreten, wird das folgende Bild angezeigt.  
  
 ![Symbol für Fehlerstatus](../master-data-services/media/mds-statusicon-error.png "Icon for error status")  
  
 Falls der Status "OK" lautet, wird das folgende Bild angezeigt.  
  
 ![Symbol für den Status OK](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status")  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [Löschen einer Entität &#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)   
 [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
