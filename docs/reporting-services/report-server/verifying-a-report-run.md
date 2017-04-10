---
title: "&#220;berpr&#252;fen einer Berichtsausf&#252;hrung | Microsoft Docs"
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
  - "Überwachen [Reporting Services]"
  - "Überwachen der Berichtsausführung"
  - "Protokolle [Reporting Services], Überprüfen der Berichtsausführung"
  - "Berichtsausführungsdaten [Reporting Services]"
  - "Statusinformationen [Reporting Services]"
  - "Berichtsverarbeitung [Reporting Services] Überprüfen der Ausführung"
  - "Prüfen der Berichtsausführung"
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
caps.latest.revision: 37
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 37
---
# &#220;berpr&#252;fen einer Berichtsausf&#252;hrung
  Mit Protokolldateien oder den Statusinformationen, die zusammen mit einem Bericht im Berichts-Manager angezeigt werden, können Sie Informationen zum Status der Berichtsverarbeitung anzeigen.  
  
## Quellen für Berichtausführungsdaten  
 Die Berichtsausführungsprotokolle stellen umfangreiche Informationen zur Berichtsausführung bereit. Hierzu zählen der Name des Berichts, der Name des Benutzers, der den Bericht ausgeführt hat, der Zeitpunkt der Berichtsausführung sowie die verwendete Übermittlungserweiterung für die Weitergabe des Berichts. Um diese Daten anzuzeigen und zu analysieren, kopieren Sie das Berichtsausführungsprotokoll in Datenbanktabellen, für die problemlos Abfragen ausgeführt und Berichte erstellt werden können.  
  
 Protokolldateien enthalten eine Vielzahl von Einträgen zur Berichtsausführung und zu anderen Serveraktivitäten. Da Protokolldateien so viele Daten enthalten, sollten Sie den Berichts-Manager verwenden, wenn Sie nur überprüfen möchten, wann der Bericht zuletzt ausgeführt wurde. Falls Sie zusätzliche Informationen benötigen, müssen Sie die Protokolldateien ansehen.  
  
> [!NOTE]  
>  Im Berichts-Manager werden die Verarbeitungszeiten von Berichten, die bei Bedarf ausgeführt wurden, nicht angezeigt.  
  
 In der folgenden Tabelle ist beschrieben, wie Sie das Datum und die Uhrzeit der Verarbeitung für verschiedene Berichtstypen anzeigen.  
  
|Berichtstyp|Datum und Uhrzeit ist hier zu finden|Vorgehensweise zum Anzeigen der Informationen|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|Ein Bericht, der als Berichtsmomentaufnahme ausgeführt wird.|Auf der Seite Inhalt. Weitere Informationen finden Sie unter [Inhalt &#40;Seite, Berichts-Manager&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md).|1) Suchen Sie den Ordner, in dem der Bericht gespeichert ist.<br /><br /> 2) Wählen Sie für den Ordner die Sicht „Details“ aus.<br /><br /> 3) Notieren Sie sich das Datum und die Uhrzeit in der Spalte **Wann ausgeführt**.|  
|Eine Momentaufnahme im Berichtsverlauf.|Auf der Eigenschaftenseite Verlauf. Weitere Informationen finden Sie unter [Momentaufnahmeoptionen (Eigenschaftenseite) &#40;Berichts-Manager&#41;](../Topic/Snapshot%20Options%20Properties%20Page%20\(Report%20Manager\).md).|1) Öffnen Sie den Bericht.<br /><br /> 2) Klicken Sie auf die Seite **Eigenschaften**.<br /><br /> 3) Klicken Sie auf die Registerkarte **Verlauf**.<br /><br /> 4) Notieren Sie sich das Datum und die Uhrzeit in der Spalte **Wann ausgeführt**.|  
|Ein zwischengespeicherter Bericht.|Im Zeitplan, der zum Erstellen und Aktualisieren des zwischengespeicherten Berichts verwendet wird.|1) Öffnen Sie den Bericht.<br /><br /> 2) Klicken Sie auf die Seite **Eigenschaften**.<br /><br /> 3) Klicken Sie auf die Registerkarte **Ausführung**.<br /><br /> 4) Öffnen Sie den Zeitplan.|  
  
## Siehe auch  
 [Reporting Services-Protokolldateien und Quellen](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  