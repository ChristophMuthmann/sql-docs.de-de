---
title: "Quellen-Editor f&#252;r CDC (Seite Spalten) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.cdcsource.columns.f1"
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Quellen-Editor f&#252;r CDC (Seite Spalten)
  Auf der Seite **Spalten** des Dialogfelds **Quellen-Editor für CDC** können Sie jeder externen Spalte (Quellspalte) eine Ausgabespalte zuordnen.  
  
 Weitere Informationen zur CDC-Quelle finden Sie unter [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## Aufgabenliste  
 **So öffnen Sie die Seite "Spalten" des Quellen-Editors für CDC**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die CDC-Quelle enthält.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die CDC-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für CDC**auf **Spalten**.  
  
## enthalten  
 **Verfügbare externe Spalten**  
 Eine Liste der in der Datenquelle verfügbaren externen Spalten. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden. Wählen Sie die zu verwendenden Spalten in der Datenquelle aus. Die ausgewählten Spalten werden der Liste **Externe Spalte** in der Reihenfolge hinzugefügt, in der Sie sie auswählen.  
  
 **Externe Spalte**  
 Eine Ansicht der externen Spalten (Quellspalten) in der Reihenfolge, in der sie angezeigt werden, wenn Sie Komponenten konfigurieren, die Daten aus der CDC-Quelle verwenden. Sie können diese Reihenfolge ändern, indem Sie zunächst die ausgewählten Spalten in der Liste **Verfügbare externe Spalten** löschen und anschließend die externen Spalten in einer anderen Reihenfolge in der Liste auswählen. Die ausgewählten Spalten werden der Liste **Externe Spalte** in der Reihenfolge hinzugefügt, in der Sie sie auswählen.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen ein. Standardmäßig wird der Name der ausgewählten externen Spalte (Quellspalte) verwendet, Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der eingegebene Name wird im SSIS-Designer angezeigt.  
  
## Siehe auch  
 [Quellen-Editor für CDC &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [Quellen-Editor für CDC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  