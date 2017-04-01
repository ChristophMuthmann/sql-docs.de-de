---
title: "Erstellen eines Berichtsverlaufs (Reporting Services im integrierten SharePoint-Modus) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Berichtsverlauf [Reporting Services], SharePoint"
ms.assetid: e57ec746-05ae-4ff6-8e39-6cde87310daa
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 12
---
# Erstellen eines Berichtsverlaufs (Reporting Services im integrierten SharePoint-Modus)
  Der Berichtsverlauf stellt eine Auflistung von Berichtsmomentaufnahmen dar, die Sie im Laufe der Zeit erstellen. Jede Momentaufnahme ist eine Kopie des Berichts in dem Zustand, in dem er zum Zeitpunkt der Momentaufnahme vorlag. Er enthält das Layout und die Daten, die für den Bericht aktuell waren, als die Momentaufnahme erstellt wurde. Renderinginformationen werden nicht mit der Momentaufnahme gespeichert. Wenn Sie eine Momentaufnahme im Berichtsverlauf öffnen, wird er in HTML-Code im Berichts-Viewer-Webpart geöffnet. Nachdem er gerendert wurde, können Sie ihn in andere Anwendungsformate exportieren.  
  
 Damit ein Berichtsverlauf erstellt werden kann, muss der Bericht unbeaufsichtigt ausgeführt werden können (d. h., der Bericht muss vom Berichtsserver ohne Benutzerinteraktion ausgeführt werden können). Sie müssen über die Berechtigung zum Bearbeiten von Elementen für die Bibliothek, die den Bericht beinhaltet, verfügen. Zum Anzeigen und Löschen des Berichtsverlaufs müssen Sie über die Berechtigung zum Anzeigen von Versionen oder zum Löschen von Versionen verfügen.  
  
### So erstellen Sie eine Momentaufnahme oder den Berichtsverlauf  
  
1.  Zeigen Sie auf den Bericht.  
  
2.  Klicken Sie darauf, um den Pfeil nach unten anzuzeigen, und wählen Sie dann **Berichtsverlauf anzeigen**aus.  
  
3.  Klicken Sie auf **Neue Momentaufnahme**. Ist die Schaltfläche nicht sichtbar, sind Sie nicht zum Erstellen von Momentaufnahmen im Berichtsverlauf berechtigt.  
  
4.  Wählen Sie die soeben erstellte Momentaufnahme in der Liste aus, um ihn anzuzeigen. Jede Momentaufnahme wird durch einen Timestamp identifiziert, der angibt, wann die Momentaufnahme erstellt wurde. Sie können die Momentaufnahme nicht umbenennen, ihn nicht an eine andere Position verschieben und ihn nicht ändern.  
  
### So planen Sie den Berichtsverlauf  
  
1.  Zeigen Sie auf den Bericht.  
  
2.  Klicken Sie darauf, um den Pfeil nach unten anzuzeigen, und wählen Sie dann **Verarbeitungsoptionen verwalten**aus.  
  
3.  Klicken Sie unter **Optionen für Verlaufsmomentaufnahmen**auf **Berichtsverlaufs-Momentaufnahmen nach einem Zeitplan erstellen**.  
  
4.  Wenn ein freigegebener Zeitplan vorhanden ist, der die gewünschten Zeitplaninformationen enthält, klicken Sie auf **Nach einem freigegebenen Zeitplan** , und wählen Sie den gewünschten Zeitplan aus. Andernfalls klicken Sie auf **Nach einem benutzerdefinierten Zeitplan**, und klicken Sie dann auf **Konfigurieren** , um Optionen zum Erstellen des Berichtsverlaufs nach einem sich wiederholenden Zeitplan anzugeben.  
  
### So erstellen Sie einen Berichtsverlauf, wenn Daten in einem Bericht aktualisiert werden  
  
1.  Zeigen Sie auf den Bericht.  
  
2.  Klicken Sie darauf, um den Pfeil nach unten anzuzeigen, und wählen Sie dann **Verarbeitungsoptionen verwalten**aus.  
  
3.  Klicken Sie unter **Optionen für Verlaufsmomentaufnahmen**auf **Alle Berichtsdaten-Momentaufnahmen im Berichtsverlauf speichern**.  
  
## Siehe auch  
 [Festlegen von Verarbeitungsoptionen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
  