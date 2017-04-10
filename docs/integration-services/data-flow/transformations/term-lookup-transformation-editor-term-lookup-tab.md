---
title: "Transformations-Editor f&#252;r Ausdruckssuche (Registerkarte Ausdruckssuche) | Microsoft Docs"
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
  - "sql13.dts.designer.termlookup.termlookup.f1"
helpviewer_keywords: 
  - "Transformations-Editor für Ausdruckssuche"
ms.assetid: 245d3466-d51f-4073-978a-694a8d9dfaec
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Transformations-Editor f&#252;r Ausdruckssuche (Registerkarte Ausdruckssuche)
  Mithilfe der Registerkarte **Ausdruckssuche** des Dialogfelds **Transformations-Editor für Ausdruckssuche** können Sie eine Eingabespalte einer Suchspalte in einer Verweistabelle zuordnen und einen Alias für jede Ausgabespalte bereitstellen.  
  
 Weitere Informationen zur Transformation für Ausdruckssuche finden Sie unter [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
## enthalten  
 **Verfügbare Eingabespalten**  
 Wählen Sie mithilfe der Kontrollkästchen die Eingabespalten aus, die unverändert an die Ausgabe weitergegeben werden. Ziehen Sie eine Eingabespalte auf die Liste **Verfügbare Verweisspalten** , um sie einer Suchspalte in der Verweistabelle zuzuordnen. Die Eingabe- und Suchspalten müssen übereinstimmende, unterstützte Datentypen haben, entweder DT_NTEXT oder DT_WSTR. Wählen Sie eine Zuordnungszeile aus, und klicken Sie mit der rechten Maustaste darauf, um die Zuordnungen im Dialogfeld [Beziehungen erstellen](../../../integration-services/data-flow/transformations/create-relationships.md) zu bearbeiten.  
  
 **Verfügbare Verweisspalten**  
 Zeigen Sie die verfügbaren Spalten in der Verweistabelle an. Wählen Sie die Spalte aus, die die Liste der Ausdrücke enthält, für die nach einer Übereinstimmung gesucht wird.  
  
 **Pass-Through-Spalte**  
 Wählen Sie Spalten aus der Liste der verfügbaren Eingabespalten aus. Ihre Auswahl wird entsprechend in der Auswahl der Kontrollkästchen in der **Verfügbare Eingabespalten** -Tabelle deutlich.  
  
 **Alias der Ausgabespalte**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 **Fehlerausgabe konfigurieren**  
 Auf der Registerkarte [Fehlerausgabe konfigurieren](../Topic/Configure%20Error%20Output.md) können Sie die Optionen zur Fehlerbehandlung von Zeilen angeben, die Fehler verursachen.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformations-Editor für Ausdruckssuche &#40;Registerkarte „Verweistabelle“&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-reference-table-tab.md)   
 [Transformations-Editor für Ausdruckssuche &#40;Registerkarte Erweitert&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-advanced-tab.md)   
 [Transformation für Ausdrucksextrahierung](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
  