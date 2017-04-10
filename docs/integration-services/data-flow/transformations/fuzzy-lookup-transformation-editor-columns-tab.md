---
title: "Transformations-Editor f&#252;r Fuzzysuche (Registerkarte Spalten) | Microsoft Docs"
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
  - "sql13.dts.designer.fuzzylookuptransformation.columns.f1"
helpviewer_keywords: 
  - "Transformations-Editor für Fuzzysuche"
ms.assetid: aaf45327-79e9-4760-9b4d-546ace91b5b4
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Transformations-Editor f&#252;r Fuzzysuche (Registerkarte Spalten)
  Auf der Registerkarte **Spalten** des Dialogfelds **Transformations-Editor für Fuzzysuche** können Sie die Eigenschaften für die Eingabe- und Ausgabespalten festlegen.  
  
 Weitere Informationen zur Transformation für Fuzzysuche finden Sie unter [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
## enthalten  
 **Verfügbare Eingabespalten**  
 Um Eingabespalten mit verfügbaren Suchspalten zu verbinden, ziehen Sie diese auf die Suchspalten. Diese Spalten müssen übereinstimmende, unterstützte Datentypen aufweisen. Wählen Sie eine Zuordnungszeile aus, und klicken Sie mit der rechten Maustaste darauf, um die Zuordnungen im Dialogfeld [Beziehungen erstellen](../../../integration-services/data-flow/transformations/create-relationships.md) zu bearbeiten.  
  
 **Name**  
 Zeigen Sie die Namen der verfügbaren Eingabespalten an.  
  
 **Pass-Through**  
 Geben Sie an, ob die Eingabespalten in der Ausgabe der Transformation eingeschlossen sein sollen.  
  
 **Verfügbare Suchspalten**  
 Wählen Sie mithilfe der Kontrollkästchen die Spalten aus, für die die Fuzzysuchvorgänge ausgeführt werden sollen.  
  
 **Suchspalte**  
 Wählen Sie Suchspalten aus der Liste der verfügbaren Spalten der Verweistabelle aus. Ihre Auswahl wird entsprechend in der Auswahl der Kontrollkästchen in der **Verfügbare Suchspalten** -Tabelle deutlich. Durch das Auswählen einer Spalte in der **Verfügbare Suchspalten** -Tabelle wird eine Ausgabespalte erstellt, die den Spaltenwert der Verweistabelle für jede übereinstimmende Zeile enthält, die zurückgegeben wird.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für die Ausgabe der einzelnen Suchspalten ein. Standardmäßig wird der Name der Suchspalte mit einem angefügten numerischen Indexwert verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformations-Editor für Fuzzysuche &#40;Registerkarte „Verweistabelle“&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Transformations-Editor für Fuzzysuche &#40;Registerkarte „Erweitert“&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  