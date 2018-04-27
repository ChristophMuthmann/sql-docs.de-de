---
title: Zusammenführen von Konflikten (Master Data Services) | Microsoft-Dokumentation
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
ms.assetid: 797219ad-5109-4666-94d3-dd1d59440a33
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16c2873058f4dc720572ba92142456fa78b1bed1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="merge-conflicts-master-data-services"></a>Konflikte zusammenführen [Master Data Services]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Wenn in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]Daten, die Sie veröffentlichen möchten, von einem anderen Benutzer geändert wurden, schlägt das Veröffentlichen mit einem Konfliktfehler fehl. Um diesen Fehler zu beheben, können Sie die Konflikte zusammenführen und die Änderungen erneut veröffentlichen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
-   Sie müssen mindestens die Berechtigung "Aktualisieren" für das Blattmodellobjekt für die Entität besitzen, die Sie aktualisieren.  
  
### <a name="to-merge-conflicts"></a>So führen Sie Konflikte zusammen  
  
1.  Aktualisieren Sie auf der Seite **Explorer** das Elementattribut.  
  
2.  Wenn das gleiche Elementattribut von einem anderen Benutzer geändert wurde, wird das Dialogfeld **Konflikte zusammenführen** angezeigt.  
  
3.  Im Dialogfeld **Konflikte zusammenführen** haben Sie folgende Möglichkeiten:  
  
    -   Sie können **Neueste** auswählen und auf **Anwenden** klicken, um die ausstehenden Änderungen rückgängig zu machen und die neueste Version vom Server herunterzuladen.  
  
    -   Sie können **Ursprüngliche** auswählen und auf **Anwenden** klicken, um die ursprüngliche Version auf das Arbeitsblatt anzuwenden.  
  
    -   Sie können **Ihre** auswählen und auf **Anwenden** klicken, um die vorhandenen lokalen Änderungen beizubehalten.  
  
4.  Nachdem Sie auf **Anwenden**geklickt haben, können Sie zusätzliche Änderungen vornehmen und erneut veröffentlichen. Sie können auch auf **Abbrechen** klicken, um die Aktualisierung abzubrechen und die neueste Version erneut vom Server herunterzuladen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Elemente &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
  
