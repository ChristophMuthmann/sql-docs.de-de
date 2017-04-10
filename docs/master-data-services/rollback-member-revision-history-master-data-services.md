---
title: "Zur&#252;cksetzen des Elementrevisionsverlaufs (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
caps.latest.revision: 5
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 5
---
# Zur&#252;cksetzen des Elementrevisionsverlaufs (Master Data Services)
  Ein Elementrevisionsverlauf wird jedes Mal aufgezeichnet, wenn ein Element geändert wird. Sie können einen Elementrevisionsverlauf auf eine frühere Version zurücksetzen.  
  
## Erforderliche Komponenten  
  
-   Sie benötigen die Berechtigung, mindestens eines der Attribute des ausgewählten Elements zu aktualisieren. Wenn Sie einen Revisionsverlauf zurücksetzen, werden alle Attributwerte, die aktualisiert werden können, auf die vorherigen Versionswerte zurückgesetzt.  
  
-   Der Revisionsverlauf steht nur dann zur Verfügung, wenn der Transaktionsprotokolltyp der Entität "Element" ist.  
  
 **Zurücksetzen eines Elementrevisionsverlaufs**  
  
1.  Klicken Sie in Master Data Manager auf "Explorer".  
  
2.  Wählen Sie die Entität und das Element aus, das zurückgesetzt werden soll.  
  
3.  Klicken Sie auf **Verlauf anzeigen**.  
  
4.  Wählen Sie die Revision aus, die zurückgesetzt werden soll, und klicken Sie anschließend auf **Zurücksetzen**.  
  
## Siehe auch  
 [Elementrevisionsverlauf &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [Ändern des Transaktionsprotokolltyps von Entitäten &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  