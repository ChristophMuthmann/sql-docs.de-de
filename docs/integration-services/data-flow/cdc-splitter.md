---
title: CDC-Splitter | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.designer.cdcsplitter.f1
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b07701fd3644368e5b47d983850ceefffa491930
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="cdc-splitter"></a>CDC-Splitter
  Der CDC-Splitter teilt einen einzelnen Fluss von Änderungszeilen aus einem CDC-Quelldatenfluss in unterschiedliche Datenflüsse für Einfüge-, Update und Löschvorgänge auf. Der Datenfluss wird basierend auf der erforderlichen Spalte `__$operation` und seinen Standardwerten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Änderungstabellen geteilt.  
  
|Wert des Vorgangs|Ausgabe|Description|  
|------------------------|------------|-----------------|  
|1|DELETE|Gelöschte Zeile|  
|2|Insert|Eingefügte Zeile (nicht verfügbar bei Verwendung des CDC-Modus **Net with merge** )|  
|3|Update|Zeile vor Update (nur bei Verwendung des CDC-Modus **All with Old Values** verfügbar)|  
|4|Update|Zeile nach Update (folgt auf die Zeile vor Update)|  
|5|Update|Mergezeile (nur bei Verwendung des CDC-Modus **Net with merge** verfügbar)|  
|Andere|Fehler||  
  
 Sie können den Splitter verwenden, um vordefinierte INSERT-, DELETE- und UPDATE-Ausgaben zur weiteren Verarbeitung zu verbinden.  
  
 Die CDC-Splittertransformation weist eine normale Eingabe und eine Fehlerausgabe auf.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Die CDC-Splittertransformation weist eine Fehlerausgabe auf. Eingabezeilen mit einem ungültigen Wert für die Spalte $operation werden als fehlerhaft angesehen und gemäß der **ErrorRowDisposition** -Eigenschaft der Eingabe behandelt.  
  
 Die Komponentenfehlerausgabe enthält die folgenden Ausgabespalten:  
  
-   **Fehlercode**: Auf 1 festgelegt.  
  
-   **Fehlerspalte**: Die Quellspalte, die den Fehler verursacht (für Konvertierungsfehler).  
  
-   **Fehlerzeilenspalten**: Die Eingabespalten der Zeile, die den Fehler verursacht hat.  
  
## <a name="configuring-the-cdc-splitter"></a>Konfigurieren des CDC-Splitters  
 Für den CDC-Splitter sind keine konfigurierbaren Eigenschaften vorhanden.  
  
 Weitere Informationen zur Verwendung des CDC-Splitters finden Sie unter CDC-Komponenten für Microsoft SQL Server Integration Services.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können.  
  
 So öffnen Sie das Dialogfeld **Erweiterter Editor** :  
  
-   Klicken Sie auf dem Bildschirm **Datenfluss** des [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Projekts mit der rechten Maustaste auf den CDC-Splitter, und wählen Sie **Erweiterten Editor anzeigen**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Weiterleiten des CDC-Datenstroms gemäß Änderungstyp](../../integration-services/data-flow/direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  
