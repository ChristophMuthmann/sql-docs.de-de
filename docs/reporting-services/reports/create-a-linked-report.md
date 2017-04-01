---
title: "Erstellen eines verkn&#252;pften Berichts | Microsoft Docs"
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
  - "Verknüpfte Berichte [Reporting Services], erstellen"
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
caps.latest.revision: 44
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 44
---
# Erstellen eines verkn&#252;pften Berichts
  Ein verknüpfter Bericht ist ein Berichtsserverelement, das einen Zugriffspunkt auf einen vorhandenen Bericht bereitstellt. Grundsätzlich ist er mit einer Programmverknüpfung vergleichbar, die Sie verwenden, um ein Programm auszuführen oder eine Datei zu öffnen.  
  
 Ein verknüpfter Bericht wird von einem vorhandenen Bericht abgeleitet und behält die Berichtsdefinition des Originals bei. Ein verknüpfter Bericht erbt immer das Berichtslayout und die Datenquelleneigenschaften des ursprünglichen Berichts. Alle anderen Eigenschaften und Einstellungen können sich von denen des ursprünglichen Berichts unterscheiden, einschließlich Sicherheit, Parameter, Speicherort, Abonnements und Zeitpläne.  
  
 Sie können einen verknüpften Bericht erstellen, wenn Sie zusätzliche Versionen eines vorhandenen Berichts erstellen möchten. Beispielsweise könnten Sie einen einzelnen regionalen Vertriebsbericht verwenden, um regionsspezifische Berichte für alle Vertriebsgebiete zu erstellen.  
  
 Obwohl verknüpfte Berichte in der Regel auf parametrisierten Berichten basieren, ist kein parametrisierter Bericht erforderlich. Sie können immer dann verknüpfte Berichte erstellen, wenn Sie einen vorhandenen Bericht mit anderen Einstellungen bereitstellen möchten.  
  
### So erstellen Sie einen verknüpften Bericht  
  
1.  Navigieren Sie im Berichts-Manager zum Ordner, der den Bericht enthält, zu dem Sie einen Link erstellen möchten, und öffnen Sie dann das Menü Optionen und klicken Sie auf **Verknüpften Bericht erstellen**.  
  
2.  Geben Sie einen Namen für den neuen verknüpften Bericht ein. Geben Sie optional eine Beschreibung ein.  
  
3.  Um einen anderen Ordner für den Bericht auszuwählen, klicken Sie auf **Speicherort ändern**. Klicken Sie auf den Ordner, den Sie verwenden möchten, oder geben Sie den Ordnernamen im Feld **Speicherort** ein. [!INCLUDE[clickOK](../../includes/clickok-md.md)] Wenn Sie keinen anderen Ordner auswählen, wird der verknüpfte Bericht im aktuellen Ordner (in dem der Bericht, auf dem er basiert, gespeichert ist) erstellt.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Der verknüpfte Bericht wird geöffnet.  
  
     Das Symbol für einen verknüpften Bericht unterscheidet sich von anderen Elementen, die von einem Berichtsserver verwaltet werden. Das folgende Symbol steht für einen verknüpften Bericht:  
  
     ![Verknüpfter Bericht (Symbol)](../../reporting-services/report-server/media/hlp-16linked.png "Verknüpfter Bericht (Symbol)")  
  
## Siehe auch  
 [Öffnen und Schließen eines Berichts &#40;Berichts-Manager&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Neuer verknüpfter Bericht (Seite) &#40;Berichts-Manager&#41;](../Topic/New%20Linked%20Report%20Page%20\(Report%20Manager\).md)   
 [Speicherort für Elemente auswählen (Seite) &#40;Berichts-Manager&#41;](../Topic/Choose%20Item%20Location%20Page%20\(Report%20Manager\).md)   
 [Allgemeine Eigenschaften (Seite) &#40;Berichte, Berichts-Manager&#41;](../Topic/General%20Properties%20Page,%20Reports%20\(Report%20Manager\).md)   
 [Konzepte von Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  