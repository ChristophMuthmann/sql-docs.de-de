---
title: "CDC-Splitter | Microsoft Docs"
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
  - "sql13.ssis.designer.cdcsplitter.f1"
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# CDC-Splitter
  Der CDC-Splitter teilt einen einzelnen Fluss von Änderungszeilen aus einem CDC-Quelldatenfluss in unterschiedliche Datenflüsse für Einfüge-, Update und Löschvorgänge auf. Der Datenfluss wird basierend auf der erforderlichen Spalte `__$operation` und seinen Standardwerten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Änderungstabellen geteilt.  
  
|Wert des Vorgangs|Ausgabe|Description|  
|------------------------|------------|-----------------|  
|1|Delete|Gelöschte Zeile|  
|2|Insert|Eingefügte Zeile (nicht verfügbar bei Verwendung des CDC-Modus **Net with merge**)|  
|3|Update|Zeile vor Update (nur bei Verwendung des CDC-Modus **All with Old Values** verfügbar)|  
|4|Update|Zeile nach Update (folgt auf die Zeile vor Update)|  
|5|Update|Mergezeile (nur bei Verwendung des CDC-Modus **Net with merge** verfügbar)|  
|Andere|Fehler||  
  
 Sie können den Splitter verwenden, um vordefinierte INSERT-, DELETE- und UPDATE-Ausgaben zur weiteren Verarbeitung zu verbinden.  
  
 Die CDC-Splittertransformation weist eine normale Eingabe und eine Fehlerausgabe auf.  
  
## Fehlerbehandlung  
 Die CDC-Splittertransformation weist eine Fehlerausgabe auf. Eingabezeilen mit einem ungültigen Wert für die Spalte $operation werden als fehlerhaft angesehen und gemäß der **ErrorRowDisposition** -Eigenschaft der Eingabe behandelt.  
  
 Die Komponentenfehlerausgabe enthält die folgenden Ausgabespalten:  
  
-   **Fehlercode**: Auf 1 festgelegt.  
  
-   **Fehlerspalte**: Die Quellspalte, die den Fehler verursacht (für Konvertierungsfehler).  
  
-   **Fehlerzeilenspalten**: Die Eingabespalten der Zeile, die den Fehler verursacht hat.  
  
## Konfigurieren des CDC-Splitters  
 Für den CDC-Splitter sind keine konfigurierbaren Eigenschaften vorhanden.  
  
 Weitere Informationen zur Verwendung des CDC-Splitters finden Sie unter CDC-Komponenten für Microsoft SQL Server Integration Services.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können.  
  
 So öffnen Sie das Dialogfeld **Erweiterter Editor** :  
  
-   Klicken Sie auf dem Bildschirm **Datenfluss** des [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Projekts mit der rechten Maustaste auf den CDC-Splitter, und wählen Sie **Erweiterten Editor anzeigen**.  
  
## Siehe auch  
 [Weiterleiten des CDC-Datenstroms gemäß Änderungstyp](../../integration-services/data-flow/direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  