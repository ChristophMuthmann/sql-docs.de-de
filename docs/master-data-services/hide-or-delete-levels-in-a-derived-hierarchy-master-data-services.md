---
title: Ausblenden oder Löschen von Ebenen in einer abgeleiteten Hierarchie (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- derived hierarchies, hiding levels
- derived hierarchies, deleting levels
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad60fc09d7e1640a48955260ce0f16a8d07e1fac
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="hide-or-delete-levels-in-a-derived-hierarchy-master-data-services"></a>Ausblenden oder Löschen von Ebenen in einer abgeleiteten Hierarchie (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie eine Ebene in einer abgeleiteten Hierarchie ausblenden, wenn die Ebene zur Gruppierung benötigt wird, aber nicht angezeigt werden soll. Löschen Sie eine Ebene, wenn Sie sie nicht zur Gruppierung verwenden möchten.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-hide-or-delete-levels-in-a-derived-hierarchy"></a>So löschen oder blenden Sie Ebenen in einer abgeleiteten Hierarchie aus  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Abgeleitete Hierarchien**.  
  
3.  Wählen Sie auf der Seite **Verwaltung abgeleiteter Hierarchien** aus der Liste **Modell** ein Modell aus.  
  
4.  Wählen Sie die Zeile der abgeleiteten Hierarchie aus, die Sie bearbeiten möchten.  
  
5.  Klicken Sie auf **Bearbeiten**.  
  
6.  Im Bereich **Aktuelle Ebenen** :  
  
    -   Um eine Ebene auszublenden, klicken Sie auf eine andere als die oberste oder unterste Ebene. Wählen Sie aus der Liste **Sichtbar** den Eintrag **Nein**aus. Klicken Sie dann auf **Ausgewähltes Hierarchieelement speichern**.  
  
    -   Um die oberste Ebene zu löschen, klicken Sie auf **Ausgewähltes Hierarchieelement löschen**. Klicken Sie im Bestätigungsdialogfeld auf **OK**. Sie können nur die oberste Ebene löschen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
    
 [Abgeleitete Hierarchien &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
