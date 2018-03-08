---
title: "Konflikte zusammenführen (MDS-Add-In für Excel) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf95978f-a2c5-4325-8606-dbd4e88741b8
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db3056898ea1d48d17fccd5518c184d1469d1640
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="merge-conflicts-mds-add-in-for-excel"></a>Konflikte zusammenführen (MDS-Add-In für Excel)
  Wenn das [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Add-In für Excel auf dem Server von einem anderen Benutzer geändert wurde, schlägt das Veröffentlichen mit einem Konfliktfehler fehl. Um diesen Fehler zu beheben, können Sie die Konflikte zusammenführen und die Änderungen erneut veröffentlichen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
-   Sie müssen mindestens die Berechtigung "Aktualisieren" für das Blattmodellobjekt für die Entität besitzen, die Sie aktualisieren.  
  
-   Im aktiven Arbeitsblatt müssen von MDS verwaltete Daten vorhanden sein.  
  
-   Das aktive Arbeitsblatt muss einen Konfliktfehler aufweisen, nachdem Sie versucht haben, Ihre Änderungen zu veröffentlichen.  
  
### <a name="to-merge-conflicts"></a>So führen Sie Konflikte zusammen  
  
1.  Wählen Sie im Arbeitsblatt die Zeile oder Zelle, die den Konfliktfehler aufweist.  
  
2.  Wählen Sie in der Menügruppe **Veröffentlichen und überprüfen** die Option **Konflikte zusammenführen** , um das Dialogfeld **Konflikte zusammenführen** zu öffnen.  
  
3.  Im Dialogfeld **Konflikte zusammenführen** haben Sie folgende Möglichkeiten:  
  
    -   Sie können **Neueste** auswählen und auf **Anwenden** klicken, um die ausstehenden Änderungen rückgängig zu machen und die neueste Version vom Server herunterzuladen.  
  
    -   Sie können **Ursprüngliche** auswählen und auf **Anwenden** klicken, um die ursprüngliche Version auf das Arbeitsblatt anzuwenden.  
  
    -   Sie können **Ihre** auswählen und auf **Anwenden** klicken, um die vorhandenen lokalen Änderungen beizubehalten.  
  
4.  Nachdem Sie auf **Anwenden**geklickt haben, können Sie zusätzliche Änderungen vornehmen und erneut veröffentlichen. Sie können auch auf **Abbrechen** klicken, um die Aktualisierung abzubrechen und die neueste Version erneut vom Server herunterzuladen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht: Importieren von Daten aus Excel &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
