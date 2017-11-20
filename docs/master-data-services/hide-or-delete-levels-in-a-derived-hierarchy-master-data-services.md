---
title: "Ausblenden oder Löschen von Ebenen in einer abgeleiteten Hierarchie (Master Data Services) | Microsoft-Dokumentation"
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
- derived hierarchies, hiding levels
- derived hierarchies, deleting levels
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a4d70ee875bdd39ee4ff79c7ce19cad426c677b6
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="hide-or-delete-levels-in-a-derived-hierarchy-master-data-services"></a>Ausblenden oder Löschen von Ebenen in einer abgeleiteten Hierarchie (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie eine Ebene in einer abgeleiteten Hierarchie ausblenden, wenn die Ebene zur Gruppierung benötigt wird, aber nicht angezeigt werden soll. Löschen Sie eine Ebene, wenn Sie sie nicht zur Gruppierung verwenden möchten.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-hide-or-delete-levels-in-a-derived-hierarchy"></a>So löschen oder blenden Sie Ebenen in einer abgeleiteten Hierarchie aus  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Abgeleitete Hierarchien**.  
  
3.  Wählen Sie auf der Seite **Verwaltung abgeleiteter Hierarchien** aus der Liste **Modell** ein Modell aus.  
  
4.  Wählen Sie die Zeile der abgeleiteten Hierarchie aus, die Sie bearbeiten möchten.  
  
5.  Klicken Sie auf **Bearbeiten**.  
  
6.  Im Bereich **Aktuelle Ebenen** :  
  
    -   Um eine Ebene auszublenden, klicken Sie auf eine andere als die oberste oder unterste Ebene. Wählen Sie aus der Liste **Sichtbar** den Eintrag **Nein**aus. Klicken Sie dann auf **Ausgewähltes Hierarchieelement speichern**.  
  
    -   Um die oberste Ebene zu löschen, klicken Sie auf **Ausgewähltes Hierarchieelement löschen**. Klicken Sie im Bestätigungsdialogfeld auf **OK**. Sie können nur die oberste Ebene löschen.  
  
## <a name="see-also"></a>Siehe auch  
    
 [Abgeleitete Hierarchien &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  

