---
title: "Transformation zum Zuordnen der Zeichen | Microsoft Docs"
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
  - "sql13.dts.designer.charactertrans.f1"
helpviewer_keywords: 
  - "Sich gegenseitig ausschließende Zuordnungen [Integration Services]"
  - "Zuordnen von Daten [Integration Services]"
  - "Zeichenfolgenfunktionen (string functions)"
  - "Transformation zum Zuordnen der Zeichen [Integration Services]"
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# Transformation zum Zuordnen der Zeichen
  Die Transformation zum Zuordnen der Zeichen wendet Zeichenfolgenfunktionen, wie z. B. die Konvertierung von Klein- in Großbuchstaben, auf Zeichendaten an. Diese Transformation betrifft nur Spaltendaten mit einem Zeichenfolgen-Datentyp.  
  
 Die Transformation zum Zuordnen der Zeichen kann Spaltendaten direkt konvertieren oder der Transformationsausgabe eine Spalte hinzufügen und die konvertierten Daten in die neue Spalte einfügen. Sie können auf eine Eingabespalte verschiedene Zuordnungsvorgänge anwenden und die Ergebnisse verschiedenen Spalten hinzufügen. Konvertieren Sie z. B. eine Spalte in Groß- und Kleinbuchstaben, und fügen Sie die Ergebnisse zwei unterschiedlichen Spalten hinzu.  
  
 Die Zuordnung kann unter bestimmten Umständen das Abschneiden von Daten verursachen. Beispielsweise, wenn Einzelbytezeichen Zeichen mit einer Multibytedarstellung zugeordnet werden. Die Transformation zum Zuordnen der Zeichen schließt eine Fehlerausgabe ein, mit der abgeschnittene Daten an eine separate Ausgabe weitergeleitet werden können. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../../integration-services/data-flow/error-handling-in-data.md).  
  
 Diese Transformation weist eine Eingabe, eine Ausgabe und eine Fehlerausgabe auf.  
  
## Zuordnungsvorgänge  
 In der folgenden Tabelle sind die Zuordnungsvorgänge beschrieben, die von der Transformation zum Zuordnen der Zeichen unterstützt werden.  
  
|Vorgang|Description|  
|---------------|-----------------|  
|Byteumkehrung|Kehrt die Bytereihenfolge um.|  
|Normale Breite|Ordnet Zeichen halber Breite Zeichen normaler Breite zu.|  
|Halbe Breite|Ordnet Zeichen normaler Breite Zeichen halber Breite zu.|  
|Hiragana|Ordnet Katakanazeichen Hiraganazeichen zu.|  
|Katakana|Ordnet Hiraganazeichen Katakanazeichen zu.|  
|Linguistische Schreibweise|Wendet die linguistische Schreibweise anstelle der Systemregeln an. Die linguistische Schreibweise bezieht sich auf die Funktionalität der Win32 API für die einfache Unicode-Schreibweisenzuordnung von Türkisch und anderen Gebietsschemas.|  
|Kleinschreibung|Konvertiert Zeichen in Kleinbuchstaben.|  
|Chinesisch (vereinfacht)|Ordnet Zeichen in traditionellem Chinesisch Zeichen in vereinfachtem Chinesisch zu.|  
|Chinesisch (traditionell)|Ordnet Zeichen in vereinfachtem Chinesisch Zeichen in traditionellem Chinesisch zu.|  
|Großschreibung|Konvertiert Zeichen in Großbuchstaben.|  
  
## Zuordnungsvorgänge, die sich gegenseitig ausschließen  
 In einer Transformation können mehrere Vorgänge ausgeführt werden. Manche Zuordnungsvorgänge schließen sich jedoch gegenseitig aus. In der folgenden Tabelle sind die Einschränkungen aufgeführt, die bei der Verwendung mehrerer Vorgänge in derselben Spalte gelten. Vorgänge in den Spalten Vorgang A und Vorgang B schließen sich gegenseitig aus.  
  
|Vorgang A|Vorgang B|  
|-----------------|-----------------|  
|Kleinschreibung|Großschreibung|  
|Hiragana|Katakana|  
|Halbe Breite|Normale Breite|  
|Chinesisch (traditionell)|Chinesisch (vereinfacht)|  
|Kleinschreibung|Hiragana, Katakana, halbe Breite, normale Breite|  
|Großschreibung|Hiragana, Katakana, halbe Breite, normale Breite|  
  
## Konfiguration der Transformation zum Zuordnen der Zeichen  
 Es gibt folgende Möglichkeiten, um die Transformation zum Zuordnen der Zeichen zu konfigurieren:  
  
-   Geben Sie die zu konvertierenden Spalten an.  
  
-   Geben Sie die auf jede Spalte anzuwendenden Vorgänge an.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld **Transformations-Editor für Zeichenzuordnung** festlegen können, finden Sie unter [Character Map Transformation Editor](../../../integration-services/data-flow/transformations/character-map-transformation-editor.md).  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
  