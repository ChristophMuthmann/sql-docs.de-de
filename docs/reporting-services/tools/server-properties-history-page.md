---
title: "Servereigenschaften (Seite „Verlauf“)|Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 66744654fac383f2390109a01f8d4cb7b502bf7a
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="server-properties-history-page"></a>Servereigenschaften (Seite Verlauf)
  Verwenden Sie diese [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Seite in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] als Standardwert für die Anzahl von Kopien der Berichtsverläufe, die Sie beibehalten möchten. Mithilfe eines Standardwertes werden erste Grenzwerte für den Berichtsverlauf für alle Berichte festgelegt. Sie können diese Werte für die jeweiligen Berichte anpassen.  
  
 Der Berichtsverlauf ist eine Auflistung von Berichtsmomentaufnahmen, die die zum Zeitpunkt der Erstellung der Momentaufnahme aktuellen Berichtsdaten und die Layouts enthalten. Mithilfe des Berichtsverlaufs können Sie die Kopie eines Berichts, so wie er zu einem bestimmten Zeitpunkt erstellt wurde, aufbewahren. Sie können den Berichtsverlauf für einzelne Berichte erstellen und verwalten, die auf einem Berichtsserver ausgeführt werden, der für den einheitlichen Modus oder den integrierten SharePoint-Modus konfiguriert ist.  
  
 Die Momentaufnahmen des Berichtsverlaufs werden in der Berichtsserverdatenbank gespeichert. Wenn Sie eine unbegrenzte Zahl von Momentaufnahmen speichern, müssen Sie regelmäßig die Größe der Datenbank überprüfen, um sicherzustellen, dass ihre Größe nicht allzu schnell wächst oder zu viel Speicherplatz belegt wird.  
  
 So öffnen Sie diese Seite
 1) Starten Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Stellen Sie eine Verbindung mit einer Berichtsserverinstanz her.
 3) Klicken Sie mit der rechten Maustaste auf den Berichtsservernamen, und wählen Sie **Eigenschaften**aus.
 4) Klicken Sie auf **Verlauf** , um diese Seite zu öffnen.  
  
## <a name="options"></a>enthalten  
 **Beliebig viele Momentaufnahmen im Berichtsverlauf speichern**  
 Alle Berichtsverlaufs-Momentaufnahmen werden beibehalten. Sie müssen die Momentaufnahmen manuell löschen, um die Größe des Berichtsverlaufs zu verringern.  
  
 **Max. Anzahl von Kopien des Berichtsverlaufs**  
 Es wird eine festgelegte Anzahl von Berichtsverlaufs-Momentaufnahmen beibehalten. Wenn der Grenzwert erreicht ist, werden ältere Kopien aus dem Berichtsverlauf entfernt, um Platz für neue Kopien zu erhalten.  
  
 Wenn Sie den Berichtsverlauf zu einem späteren Zeitpunkt einschränken und der vorhandene Berichtsverlauf den angegebenen Grenzwert übersteigt, verringert der Berichtsserver den vorhandenen Berichtsverlauf auf den neuen Grenzwert. Die ältesten Berichtsmomentaufnahmen werden zuerst gelöscht. Falls der Berichtsverlauf leer ist oder unter dem Grenzwert liegt, werden neue Berichtsmomentaufnahmen hinzugefügt. Ist der Grenzwert erreicht, wird die älteste Momentaufnahme gelöscht, sobald eine neue Berichtsmomentaufnahme hinzugefügt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen von Berichtsservereigenschaften &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Vorgehensweise: Herstellen einer Verbindung mit einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Berichtsserver im Management Studio (F1-Hilfe)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  

