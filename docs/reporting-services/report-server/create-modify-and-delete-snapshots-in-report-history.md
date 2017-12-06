---
title: "Erstellen, Ändern und Löschen von Momentaufnahmen im Berichtsverlauf | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [Reporting Services]
- report snapshots [Reporting Services]
ms.assetid: 5aebbbfa-a8db-462d-8ab9-746fad9525f0
caps.latest.revision: "40"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 725cf2ab029fcaa7385a1321f4c7bacc3fcc008c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="create-modify-and-delete-snapshots-in-report-history"></a>Erstellen, Ändern und Löschen von Momentaufnahmen im Berichtsverlauf
  Der Berichtsverlauf ist eine Auflistung von Berichtsmomentaufnahmen. Zum Verwalten des Berichtsverlaufs können Sie Momentaufnahmen hinzufügen und löschen oder Eigenschaften zur Speicherung des Berichtsverlaufs ändern. Der Berichtsverlauf kann manuell oder nach einem Zeitplan erstellt werden.  
  
 Zum Erstellen des Berichtsverlaufs muss Ihre Rollenzuweisung die Aufgabe "Berichtsverlauf verwalten" enthalten. Zum Anzeigen des Berichtsverlaufs muss Ihre Rollenzuweisung die Aufgabe "Berichte anzeigen" enthalten. Der Berichtsverlauf ist für alle Benutzer mit Zugriff auf den Bericht verfügbar. Es ist nicht möglich, den Berichtsverlauf für bestimmte Benutzer selektiv zu aktivieren oder zu deaktivieren.  
  
 Momentaufnahmen im Berichtsverlauf werden nach dem Erstellungsdatum und der Erstellungsuhrzeit identifiziert. Das Datum und die Uhrzeit basieren auf dem Zeitpunkt der Ausführung der Abfrage.  
  
## <a name="creating-snapshots-in-report-history"></a>Erstellen von Momentaufnahmen im Berichtsverlauf  
 Momentaufnahmen können manuell oder in geplanten Intervallen für jeden Bericht erstellt werden, der unbeaufsichtigt ausgeführt werden kann. Zur unbeaufsichtigten Ausführung muss der Bericht gespeicherte Anmeldeinformationen oder keine Anmeldeinformationen verwenden. Wenn darüber hinaus im Bericht Parameter verwendet werden, müssen Sie Standardwerte für die Ausführung des Berichts angeben. Auf den Eigenschaftenseiten für den Bericht können Sie gespeicherte Anmeldeinformationen und Parameterwerte angeben. Weitere Informationen finden Sie unter [Parameter Eigenschaftenseite (Berichts-Manager)](http://msdn.microsoft.com/library/ebb53598-2378-46ae-8935-d5192f8ea49a).  
  
 Beim Erstellen eines Berichtsmomentaufnahmen werden die folgenden Elemente zusammen mit der Berichtsmomentaufnahme in der Berichtsserver-Datenbank gespeichert:  
  
-   Das Resultset (die Daten im Bericht, die über die auf der Eigenschaftenseite Datenquellen des Berichts angegebenen Anmeldeinformationen abgerufen werden).  
  
-   Die zugrunde liegende Berichtsdefinition zu dem Zeitpunkt, zu dem die Momentaufnahme erstellt wurde. Falls die Berichtsdefinition nach dem Generieren der Momentaufnahme geändert wird, werden diese Änderungen für die Momentaufnahme nicht berücksichtigt.  
  
-   Parameterwerte, mit denen das Resultset abgerufen oder gefiltert wird.  
  
-   Eingebettete Ressourcen, wie z. B. Bilder. Externe Ressourcen, die mit einem Bericht verknüpft sind, werden nicht zusammen mit der Berichtsmomentaufnahme gespeichert.  
  
 Von den Einstellungen hängt es ab, wie der Berichtsverlauf erstellt und wie viele Berichtsmomentaufnahmen gespeichert werden können.  
  
 Falls für einen Bericht ein Fehler gemeldet wird, wird keine Momentaufnahme erstellt. Berichte, die trotz angezeigter Warnungen weiter ausgeführt werden, können zum Generieren von Momentaufnahmen verwendet werden.  
  
## <a name="modifying-properties-and-deleting-report-history"></a>Ändern von Eigenschaften und Löschen des Berichtsverlaufs  
 Eine erstellte Berichtsmomentaufnahme kann nicht mehr geändert werden. Sie können jedoch die Eigenschaften so ändern, dass der Berichtsverlauf gelöscht wird.  
  
 Es gibt die folgenden Methoden, um den Berichtsverlauf zu löschen:  
  
-   Manuelles Löschen einzelner Momentaufnahmen oder einer Gruppe von Momentaufnahmen.  
  
     Momentaufnahmen können auf der Seite Verlauf im Berichts-Manager gelöscht werden. Navigieren Sie zum Bericht, klicken Sie auf Verlauf, aktivieren Sie das Kontrollkästchen neben den Momentaufnahmen, die Sie löschen möchten, und klicken Sie dann auf **Löschen**.  
  
-   Senken des Grenzwertes für den Berichtsverlauf, um die Anzahl der gespeicherten Momentaufnahmen zu reduzieren. Der Grenzwert für den Berichtsverlauf kann für den Berichtsserver oder für bestimmte Berichte festgelegt werden. Wenn der Grenzwert verringert wird, werden die ältesten Momentaufnahmen aus dem Verlauf gelöscht.  
  
 Es ist nicht möglich, alle auf einem Berichtsserver gespeicherten Berichtsverläufe in einem Massenvorgang zu löschen.  
  
 Der Berichtsverlauf wird beim Löschen eines Berichts ebenfalls gelöscht. Wenn Sie z. B. einen monatlichen Umsatzbericht löschen, weil Sie ihn durch eine neuere Version ersetzen, werden alle zugehörigen Berichtsverläufe ebenfalls gelöscht. Beim Verschieben eines Berichts werden auch alle Berichtsverläufe verschoben.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Berichtsverlaufs &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-server/create-report-history-reporting-services-in-sharepoint-integrated-mode.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Verwalten von Berichtsserverinhalten &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Hinzufügen einer Momentaufnahme zum Berichtsverlauf &#40;Berichts-Manager&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Einschränken des Berichtsverlaufs (Berichts-Manager)](../../reporting-services/reports/limit-report-history-report-manager.md)  
  
  
