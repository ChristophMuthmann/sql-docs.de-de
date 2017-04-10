---
title: "Transformations-Editor f&#252;r Suche (Seite &#39;Fehlerausgabe&#39;) | Microsoft Docs"
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
  - "sql13.dts.designer.lookuptransformation.erroroutput.f1"
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Transformations-Editor f&#252;r Suche (Seite &#39;Fehlerausgabe&#39;)
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Transformations-Editor für Suche** geben Sie Optionen für die Fehlerbehandlung an.  
  
 Weitere Informationen zur Transformation für Suche finden Sie unter [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## enthalten  
 **Eingabe/Ausgabe**  
 Zeigt den Namen der Eingabe an.  
  
 **Column**  
 Wird nicht verwendet.  
  
 **Fehler**  
 Geben Sie an, welche Art von Fehler auftreten soll, wenn Zeilen ohne übereinstimmende Einträge im Verweisdataset behandelt werden:  
  
-   Den Fehler ignorieren und die Zeilen an eine Ausgabe weiterleiten.  
  
-   Die Zeilen an eine Fehlerausgabe weiterleiten.  
  
-   Die Komponente mit einem Fehler abbrechen.  
  
 Diese Option ist nicht verfügbar, wenn Sie in der Liste **Angeben, wie Zeilen ohne übereinstimmende Einträge behandelt werden sollen** den Eintrag **Zeilen an Ausgabe nicht übereinstimmender Einträge umleiten** auswählen. Diese Liste befindet sich auf der Seite **Allgemein** des Dialogfelds **Transformations-Editor für Suche** .  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Geben Sie an, was geschehen soll, wenn Daten abgeschnitten werden:  
  
-   Den Fehler ignorieren.  
  
-   Die Zeile umleiten.  
  
-   Die Komponente mit einem Fehler abbrechen.  
  
 **Description**  
 Zeigt die Beschreibung des Vorgangs an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Geben Sie an, was bei einem Fehler oder beim Abschneiden von Daten mit allen ausgewählten Zellen geschehen soll:  
  
-   Den Fehler ignorieren.  
  
-   Die Zeile umleiten.  
  
-   Die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  