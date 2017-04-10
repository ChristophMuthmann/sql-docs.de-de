---
title: "Quellen-Editor f&#252;r Flatfiles (Seite Spalten) | Microsoft Docs"
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
  - "sql13.dts.designer.flatfilesourceadapter.columns.f1"
helpviewer_keywords: 
  - "Quellen-Editor für Flatfiles"
ms.assetid: b5af5f65-c087-44fd-b5ae-d0441245fef2
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Quellen-Editor f&#252;r Flatfiles (Seite Spalten)
  Mithilfe des Knotens **Spalten** des Dialogfelds **Quellen-Editor für Flatfiles** können Sie jeder externen (Quell-)Spalte eine Ausgabespalte zuordnen.  
  
> [!NOTE]  
>  Die **FileNameColumnName** -Eigenschaft der Flatfilequelle und die **FastParse** -Eigenschaft ihrer Ausgabespalten sind nicht im **Quellen-Editor für Flatfiles**verfügbar, sie können jedoch mithilfe des Dialogfelds **Erweiterter Editor**festgelegt werden. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Flatfilequelle von [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Weitere Informationen zur Flatfilequelle finden Sie unter [Flat File Source](../../integration-services/data-flow/flat-file-source.md).  
  
## enthalten  
 **Verfügbare externe Spalten**  
 Zeigt die Liste der in der Datenquelle verfügbaren externen Spalten an. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden.  
  
 **Externe Spalte**  
 Zeigt die externen (Quell-)Spalten in der Reihenfolge an, in der sie von dem Task gelesen werden. Sie können die Reihenfolge ändern, indem Sie zunächst die ausgewählten Spalten in der Tabelle löschen. Wählen Sie anschließend die externen Spalten in einer anderen Reihenfolge aus der Liste aus.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen an. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Quellen-Editor für Flatfiles &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/flat-file-source-editor-connection-manager-page.md)   
 [Quellen-Editor für Flatfiles &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/flat-file-source-editor-error-output-page.md)   
 [Verbindungs-Manager für Flatfiles](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  