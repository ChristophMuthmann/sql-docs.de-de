---
title: "Transformations-Editor f&#252;r Ausdrucksextrahierung (Registerkarte Erweitert) | Microsoft Docs"
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
  - "sql13.dts.designer.termextraction.advanced.f1"
helpviewer_keywords: 
  - "Transformations-Editor für Ausdrucksextrahierung"
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Transformations-Editor f&#252;r Ausdrucksextrahierung (Registerkarte Erweitert)
  Auf der Registerkarte **Erweitert** des Dialogfelds **Transformations-Editor für Ausdrucksextrahierung** können Sie Eigenschaften für die Extrahierung angeben, wie z. B. Häufigkeit, Länge und ob Wörter oder Ausdrücke extrahiert werden sollen.  
  
 Weitere Informationen zur Transformation für Ausdrucksextrahierung finden Sie unter [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md).  
  
## enthalten  
 **Nomen**  
 Gibt an, dass durch die Transformation nur einzelne Nomen extrahiert werden.  
  
 **Nominaler Ausdruck**  
 Gibt an, dass durch die Transformation nur nominale Ausdrücke extrahiert werden.  
  
 **Nomen und nominaler Ausdruck**  
 Gibt an, dass durch die Transformation sowohl Nomen als auch nominale Ausdrücke extrahiert werden.  
  
 **Häufigkeit**  
 Gibt an, dass es sich bei dem Ergebnis um die Häufigkeit des Begriffs handelt.  
  
 **TFIDF**  
 Gibt an, dass es sich bei dem Ergebnis um den TFIDF-Wert des Begriffs handelt. Das TFIDF-Ergebnis ist das Produkt von Ausdruckshäufigkeit und umgekehrter Dokumenthäufigkeit, definiert als: TFIDF des Ausdrucks T = (Häufigkeit von T) * log((Anz. Zeilen in der Eingabe)/(Anz. Zeilen mit T))  
  
 **Schwellenwert für Häufigkeit**  
 Gibt in Form eines Zahlenwertes an, wie oft ein Wort oder ein Ausdruck vorkommen muss, bevor die Extrahierung erfolgt. Der Standardwert ist 2.  
  
 **Maximale Ausdruckslänge**  
 Gibt die maximale Länge des Ausdrucks in Worten an. Diese Option bezieht sich nur auf nominale Ausdrücke. Der Standardwert ist 12.  
  
 **Ausdrucksextrahierung mit Unterscheidung nach Groß-/Kleinschreibung verwenden**  
 Gibt an, ob bei der Extrahierung nach Groß-/Kleinschreibung unterschieden wird. Der Standardwert ist **False**.  
  
 **Fehlerausgabe konfigurieren**  
 Im Dialogfeld [Fehlerausgabe konfigurieren](../Topic/Configure%20Error%20Output.md) können Sie die Fehlerbehandlung bei Zeilen, die Fehler verursachen, angeben.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformations-Editor für Ausdrucksextrahierung &#40;Registerkarte „Ausdrucksextrahierung“&#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Transformations-Editor für Ausdrucksextrahierung &#40;Registerkarte „Ausschluss“&#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-exclusion-tab.md)   
 [Transformation für Ausdruckssuche](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
  