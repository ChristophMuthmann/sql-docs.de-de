---
title: Transformation zum Zuordnen der Zeichen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.charactertrans.f1
- sql13.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
caps.latest.revision: "42"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34c666dc86e9026c5981a6a45f32fc06759de061
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="character-map-transformation"></a>Transformation zum Zuordnen der Zeichen
  Die Transformation zum Zuordnen der Zeichen wendet Zeichenfolgenfunktionen, wie z. B. die Konvertierung von Klein- in Großbuchstaben, auf Zeichendaten an. Diese Transformation betrifft nur Spaltendaten mit einem Zeichenfolgen-Datentyp.  
  
 Die Transformation zum Zuordnen der Zeichen kann Spaltendaten direkt konvertieren oder der Transformationsausgabe eine Spalte hinzufügen und die konvertierten Daten in die neue Spalte einfügen. Sie können auf eine Eingabespalte verschiedene Zuordnungsvorgänge anwenden und die Ergebnisse verschiedenen Spalten hinzufügen. Konvertieren Sie z. B. eine Spalte in Groß- und Kleinbuchstaben, und fügen Sie die Ergebnisse zwei unterschiedlichen Spalten hinzu.  
  
 Die Zuordnung kann unter bestimmten Umständen das Abschneiden von Daten verursachen. Beispielsweise, wenn Einzelbytezeichen Zeichen mit einer Multibytedarstellung zugeordnet werden. Die Transformation zum Zuordnen der Zeichen schließt eine Fehlerausgabe ein, mit der abgeschnittene Daten an eine separate Ausgabe weitergeleitet werden können. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../../integration-services/data-flow/error-handling-in-data.md).  
  
 Diese Transformation weist eine Eingabe, eine Ausgabe und eine Fehlerausgabe auf.  
  
## <a name="mapping-operations"></a>Zuordnungsvorgänge  
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
  
## <a name="mutually-exclusive-mapping-operations"></a>Zuordnungsvorgänge, die sich gegenseitig ausschließen  
 In einer Transformation können mehrere Vorgänge ausgeführt werden. Manche Zuordnungsvorgänge schließen sich jedoch gegenseitig aus. In der folgenden Tabelle sind die Einschränkungen aufgeführt, die bei der Verwendung mehrerer Vorgänge in derselben Spalte gelten. Vorgänge in den Spalten Vorgang A und Vorgang B schließen sich gegenseitig aus.  
  
|Vorgang A|Vorgang B|  
|-----------------|-----------------|  
|Kleinschreibung|Großschreibung|  
|Hiragana|Katakana|  
|Halbe Breite|Normale Breite|  
|Chinesisch (traditionell)|Chinesisch (vereinfacht)|  
|Kleinschreibung|Hiragana, Katakana, halbe Breite, normale Breite|  
|Großschreibung|Hiragana, Katakana, halbe Breite, normale Breite|  
  
## <a name="configuration-of-the-character-map-transformation"></a>Konfiguration der Transformation zum Zuordnen der Zeichen  
 Es gibt folgende Möglichkeiten, um die Transformation zum Zuordnen der Zeichen zu konfigurieren:  
  
-   Geben Sie die zu konvertierenden Spalten an.  
  
-   Geben Sie die auf jede Spalte anzuwendenden Vorgänge an.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="character-map-transformation-editor"></a>Transformations-Editor für Zeichenzuordnung
  Im Dialogfeld **Transformations-Editor für Zeichenzuordnung** können Sie die auf Spaltendaten anwendbaren Zeichenfolgenfunktionen auswählen und angeben, ob eine Zuordnung direkt geändert oder als neue Spalte hinzugefügt werden soll.  
  
### <a name="options"></a>enthalten  
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
 Im Dialogfeld [Fehlerausgabe konfigurieren](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) können Sie für die Transformation verfügbare Optionen zur Fehlerbehandlung angeben.  
  
  
