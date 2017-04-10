---
title: "Transformations-Editor f&#252;r Sortierung | Microsoft Docs"
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
  - "sql13.dts.designer.sorttransformation.f1"
helpviewer_keywords: 
  - "Transformations-Editor für Sortierung"
ms.assetid: 8ae23970-49a9-4d6d-9f15-c7074783347c
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Transformations-Editor f&#252;r Sortierung
  Mithilfe des Dialogfelds **Transformations-Editor für Sortierung** können Sie die zu sortierenden Spalten auswählen, die Sortierreihenfolge festlegen und angeben, ob Duplikate entfernt werden.  
  
 Weitere Informationen zur Transformation zum Sortieren finden Sie unter [Sort Transformation](../../../integration-services/data-flow/transformations/sort-transformation.md).  
  
## enthalten  
 **Verfügbare Eingabespalten**  
 Geben Sie mithilfe der Kontrollkästchen die zu sortierenden Spalten an.  
  
 **Name**  
 Zeigen Sie den Namen jeder verfügbaren Eingabespalte an.  
  
 **Passthrough**  
 Geben Sie an, ob die Spalte in der sortierten Ausgabe eingeschlossen werden soll.  
  
 **Eingabespalte**  
 Wählen Sie für jede Zeile eine Spalte aus der Liste der verfügbaren Eingabespalten aus. Ihre Auswahl wird entsprechend in der Auswahl der Kontrollkästchen in der **Verfügbare Eingabespalten** -Tabelle deutlich.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Eingabespalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 **Sortiertyp**  
 Geben Sie an, ob in aufsteigender oder absteigender Reihenfolge sortiert wird.  
  
 **Sortierreihenfolge**  
 Geben Sie die Reihenfolge an, in der die Spalten sortiert werden. Diese Einstellung muss manuell für jede Spalte vorgenommen werden.  
  
 **Vergleichsflags**  
 Weitere Informationen zu den Optionen für das Vergleichen von Zeichenfolgen finden Sie unter [Vergleichen von Zeichenfolgendaten](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Zeilen mit doppelten Sortierwerten entfernen**  
 Geben Sie an, ob die Transformation doppelte Zeilen in die Transformationsausgabe kopiert oder einen einzelnen Eintrag für alle Duplikate erstellt, basierend auf den angegebenen Optionen für den Zeichenfolgenvergleich.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  