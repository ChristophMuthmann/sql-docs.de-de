---
title: "Sichtbarmachen einer Attributgruppe für Benutzer (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d9b4e9b3fb165d2aa8c445daa5d38c7a8d81ed03
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>Sichtbarmachen einer Attributgruppe für Benutzer (Master Data Services)
  Machen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] eine Attributgruppe für Benutzer oder Gruppen sichtbar, wenn Sie möchten, dass Benutzer im Funktionsbereich **Explorer** oberhalb des Rasters Registerkarten verwenden können.  
  
 Beim Erstellen einer Attributgruppe wird diese automatisch für alle Benutzer bis auf den Ersteller ausgeblendet.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Es muss mindestens eine Attributgruppe vorhanden sein. Weitere Informationen finden Sie unter [Create an Attribute Group &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md).  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>So machen Sie eine Attributgruppe für Benutzer sichtbar  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** im Raster die Zeile der Entität aus, für die Sie die Attributgruppe bearbeiten möchten.  
  
4.  Klicken Sie auf **Attributgruppen**.  
  
5.  Wählen Sie auf der Seite **Attributgruppen verwalten** den Elementtyp in der Dropdownliste **Member Types** (Elementtypen) aus, um **Blatt**, **Konsolidiert** oder **Sammlung**abhängig vom Typ der Gruppe, die Sie sichtbar machen möchten, zu erweitern.  
  
6.  Wählen Sie im Raster die Attributgruppe aus, die Sie bearbeiten möchten, und klicken Sie anschließend auf **Bearbeiten**.  
  
7.  Klicken Sie im Feld **Verfügbar** auf einen Benutzer oder eine Gruppe, und klicken Sie auf den Pfeil für **Hinzufügen** . Klicken Sie auf den Pfeil für **Alle hinzufügen** , um alles hinzuzufügen.  
  
8.  Klicken Sie auf **Speichern**.  
  
## <a name="see-also"></a>Siehe auch  
 [Attributgruppen &#40; Master Data Services &#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [Erstellen Sie eine Attributgruppe aus &#40; Master Data Services &#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
