---
title: "Rendern von Berichtsverlaufs-Momentaufnahmen mit URL-Zugriff | Microsoft Docs"
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
  - "URL-Zugriff [Reporting Services], Berichtsverlauf"
  - "Verlaufsmomentaufnahmen [Reporting Services]"
  - "Verlaufsdaten [Reporting Services]"
  - "Momentaufnahmen [Reporting Services], URL-Zugriff"
  - "Momentaufnahmen [Reporting Services], Rendern des Berichtsverlaufs"
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# Rendern von Berichtsverlaufs-Momentaufnahmen mit URL-Zugriff
  Sie können einen Bericht auf der Grundlage einer Berichtsverlaufs-Momentaufnahme rendern, indem Sie den Parameter *rs:Snapshot* angeben und seinen Wert auf eine gültige Momentaufnahme-ID festlegen. Der Parameterwert hat das Format YYYY-MM-DDTHH:MM:SS und basiert auf dem ISO-Standard 8601 (Standard International Organization for Standardization).  
  
 Wenn Sie diesen Parameter weglassen, wird der Bericht gemäß den Optionseinstellungen für die Berichtsausführung und Cacheverwaltung des Berichtsservers gerendert. Weitere Informationen zur Ausführung von Berichten finden Sie unter [Festlegen von Berichtsverarbeitungseigenschaften](../reporting-services/report-server/set-report-processing-properties.md).  
  
## Beispiel  
 Das folgende Beispiel zeigt eine URL, die eine Berichtsverlaufs-Momentaufnahme abruft:  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## Siehe auch  
 [URL-Zugriff &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL-Zugriffsparameterverweis](../reporting-services/url-access-parameter-reference.md)  
  
  