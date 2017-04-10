---
title: "Transformations-Editor f&#252;r Zeichenzuordnung | Microsoft Docs"
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
  - "sql13.dts.designer.charactermaptransformation.f1"
helpviewer_keywords: 
  - "Transformations-Editor für Zeichenzuordnung"
ms.assetid: 3f1dbcf9-9cca-4606-bdcc-7ea6ad48cdf3
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Transformations-Editor f&#252;r Zeichenzuordnung
  Im Dialogfeld **Transformations-Editor für Zeichenzuordnung** können Sie die auf Spaltendaten anwendbaren Zeichenfolgenfunktionen auswählen und angeben, ob eine Zuordnung direkt geändert oder als neue Spalte hinzugefügt werden soll.  
  
 Weitere Informationen zur Transformation zum Zuordnen der Zeichen finden Sie unter [Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md).  
  
## enthalten  
 **Verfügbare Eingabespalten**  
 Wählen Sie mithilfe der Kontrollkästchen die Spalten aus, die mithilfe von Zeichenfolgenfunktionen transformiert werden sollen. Die getroffene Auswahl wird in der nachfolgenden Tabelle angezeigt.  
  
 **Eingabespalte**  
 Zeigen Sie die in obiger Tabelle ausgewählten Eingabespalten an. Sie können eine Auswahl auch ändern oder entfernen, indem Sie die Liste der verfügbaren Eingabespalten verwenden.  
  
 **Ziel**  
 Geben Sie an, ob Sie die Ergebnisse der Zeichenfolgenfunktionen direkt in der vorhandenen Spalte speichern möchten, oder ob Sie die geänderten Daten in einer neuen Spalte speichern möchten.  
  
|Wert|Description|  
|-----------|-----------------|  
|Neue Spalte|Speichern Sie die Daten in einer neuen Spalte. Weisen Sie der Spalte unter **Ausgabealias**einen Namen zu.|  
|Direkte Änderung|Speichern Sie die geänderten Daten in der vorhandenen Spalte.|  
  
 **Vorgang**  
 Wählen Sie in der Liste die Zeichenfolgenfunktionen aus, die auf Spaltendaten angewendet werden sollen.  
  
|Wert|Description|  
|-----------|-----------------|  
|Kleinschreibung|In Kleinschreibung konvertieren.|  
|Großschreibung|In Großschreibung konvertieren.|  
|Byteumkehrung|In umgekehrte Bytereihenfolge konvertieren.|  
|Hiragana|Japanische Katakana-Zeichen in Hiragana-Zeichen konvertieren.|  
|Katakana|Japanische Hiragana-Zeichen in Katakana-Zeichen konvertieren.|  
|Halbe Breite|Zeichen normaler Breite in Zeichen halber Breite konvertieren.|  
|Normale Breite|Zeichen halber Breite in Zeichen normaler Breite konvertieren.|  
|Linguistische Schreibweise|Wenden Sie statt der Systemregeln die Regeln der linguistischen Schreibweise an (die mit Unicode bereitgestellte einfache Zuordnung der Schreibweise für Türkisch und andere Gebietsschemas).|  
|Chinesisch (vereinfacht)|Konvertieren Sie traditionelle chinesische Zeichen in vereinfachte chinesische Zeichen.|  
|Chinesisch (traditionell)|Konvertieren Sie vereinfachte chinesische Zeichen in traditionelle chinesische Zeichen.|  
  
 **Ausgabealias**  
 Geben Sie einen Alias für jede Spalte ein. Der Standard lautet **Copy of** , gefolgt vom Namen der Eingabespalte. Sie können jedoch auch einen eindeutigen, beschreibenden Namen auswählen.  
  
 **Fehlerausgabe konfigurieren**  
 Im Dialogfeld [Fehlerausgabe konfigurieren](../Topic/Configure%20Error%20Output.md) können Sie für die Transformation verfügbare Optionen zur Fehlerbehandlung angeben.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  