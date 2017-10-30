---
title: "Konflikte zusammenführen (MDS-Add-In für Excel) | Microsoft-Dokumentation"
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
ms.assetid: cf95978f-a2c5-4325-8606-dbd4e88741b8
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 9814c347b8a0f63fd63625149b55098b1df3896c
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="merge-conflicts-mds-add-in-for-excel"></a>Konflikte zusammenführen (MDS-Add-In für Excel)
  Wenn das [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Add-In für Excel auf dem Server von einem anderen Benutzer geändert wurde, schlägt das Veröffentlichen mit einem Konfliktfehler fehl. Um diesen Fehler zu beheben, können Sie die Konflikte zusammenführen und die Änderungen erneut veröffentlichen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
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
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht: Importieren von Daten aus Excel &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  

