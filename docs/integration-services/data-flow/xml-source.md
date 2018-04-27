---
title: XML-Quelle | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- sql13.dts.designer.xmlsource.f1
- sql13.dts.designer.xmlsourceadapter.connectionmanager.f1
- sql13.dts.designer.xmlsourceadapter.columns.f1
- sql13.dts.designer.xmlsourceadapter.erroroutput.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9e862605c34de37a9937cacd396a5fb645aac76c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="xml-source"></a>XML-Quelle
  Die XML-Quelle liest eine XML-Datendatei und füllt die Spalten in der Quellausgabe mit den Daten.  
  
 Die Daten in XML-Dateien schließen häufig hierarchische Beziehungen ein. Beispielsweise kann eine XML-Datendatei Kataloge und Katalogelemente darstellen. Bevor die Daten in den Datenfluss aufgenommen werden können, muss die Beziehung der Elemente in der XML-Datendatei bestimmt werden, und für jedes Dateielement muss eine Ausgabe generiert werden.  
  
## <a name="schemas"></a>Schemas  
 Die XML-Quelle verwendet ein Schema zum Interpretieren der XML-Daten. Die XML-Quelle unterstützt die Verwendung von XSD-Dateien (XML Schema Definition) oder Inlineschemas, um die XML-Daten in das Tabellenformat zu übersetzen. Wenn Sie die XML-Quelle mithilfe des Dialogfelds **Quellen-Editor für XML** konfigurieren, kann die Benutzeroberfläche XSD-Code von der angegebenen XML-Datendatei generieren.  
  
> [!NOTE]  
>  DTDs werden nicht unterstützt.  
  
 Von den Schemas wird nur ein einziger Namespace unterstützt. Schemaauflistungen werden nicht unterstützt.  
  
> [!NOTE]  
>  Die XML-Quelle überprüft die Daten in der XML-Datei nicht mit dem XSD-Code.  
  
## <a name="xml-source-editor"></a>Quellen-Editor für XML  
 Die Daten in XML-Dateien schließen häufig hierarchische Beziehungen ein. Im Dialogfeld **Quellen-Editor für XML** wird das angegebene Schema zum Generieren der XML-Quellausgaben verwendet. Sie können eine XSD-Datei angeben, ein Inlineschema verwenden oder XSD-Code von der angegebenen XML-Datendatei generieren. Das Schema muss zur Entwurfszeit verfügbar sein.  
  
 Die XML-Quelle generiert von den XML-Daten Tabellenstrukturen, indem sie eine Ausgabe für jedes Element erstellt, das andere Elemente in den XML-Dateien enthält. Wenn z. B. die XML-Daten Kataloge und Katalogelemente darstellen, erstellt die XML-Quelle eine Ausgabe für Kataloge und eine Ausgabe für jeden Elementtyp, der in den Katalogen enthalten ist. Die Ausgabe jedes Elements enthält Ausgabespalten für die Attribute dieses Elements.  
  
 Um Informationen zur hierarchischen Beziehung der Daten in den Ausgaben bereitzustellen, fügt die XML-Quelle in den Ausgaben eine Spalte hinzu, die das übergeordnete Element für jedes untergeordnete Element identifiziert. Für das Beispiel der Kataloge mit unterschiedlichen Elementtypen hätte jedes Element einen Spaltenwert, der den zugehörigen Katalog identifiziert.  
  
 Die XML-Quelle erstellt für jedes Element eine Ausgabe, aber es ist nicht erforderlich alle Ausgaben zu verwenden. Sie können jede Ausgabe löschen, die Sie nicht verwenden möchten, oder sie einfach nicht mit einer Downstreamkomponente verbinden.  
  
 Die XML-Quelle generiert außerdem die Ausgabenamen, um sicherzustellen, dass die Namen eindeutig sind. Es könnte sich um lange Namen handeln, mit denen die Ausgaben für Sie nicht sinnvoll identifiziert werden. Sie können die Ausgaben umbenennen, vorausgesetzt die Namen bleiben eindeutig. Außerdem können Sie den Datentyp und die Länge der Ausgabespalten ändern.  
  
 Für jede Ausgabe fügt die XML-Quelle eine Fehlerausgabe hinzu. Standardmäßig weisen die Spalten in Fehlerausgaben den Unicode-Zeichenfolgen-Datentyp (DT_WSTR) mit einer Länge von 255 auf. Sie können jedoch die Spalten in den Fehlerausgaben konfigurieren, indem Sie deren Datentyp und Länge ändern.  
  
 Falls die XML-Datendatei Elemente enthält, die nicht im XSD-Code vorhanden sind, werden diese ignoriert und es wird keine Ausgabe dafür generiert. Wenn andererseits in der XML-Datendatei Elemente fehlen, die im XSD-Code dargestellt sind, enthält die Ausgabe Spalten mit NULL-Werten.  
  
 Wenn die Daten aus der XML-Datendatei extrahiert werden, werden sie in einen Datentyp von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] konvertiert. Die XML-Quelle kann XML-Daten jedoch nicht in die Datentypen DT_TIME2 oder DT_DBTIMESTAMP2 konvertieren, da diese Datentypen nicht von der Quelle unterstützt werden. Weitere Informationen finden Sie unter [Integration Services Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Im XSD-Code oder Inlineschema kann der Datentyp für Elemente angegeben sein. Andernfalls weist der **Quellen-Editor für XML** der Spalte in der Ausgabe, die das Element enthält, den Unicode-Zeichenfolgen-Datentyp (DT_WSTR) zu und legt als Spaltenlänge 255 Zeichen fest.  
  
 Wenn im Schema die maximale Länge eines Elements angegeben ist, wird die Länge der Ausgabespalte auf diesen Wert festgelegt. Ist die maximale Länge größer als die Länge, die von dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentyp unterstützt wird, in den das Element konvertiert wird, werden die Daten auf die maximale Länge des Datentyps abgeschnitten. Besitzt z. B. eine Zeichenfolge die Länge 5000, wird sie auf 4000 Zeichen abgeschnitten, da die maximale Länge des DT_WSTR-Datentyps 4000 Zeichen beträgt. Ebenso werden Bytedaten auf 8000 Zeichen, die maximale Länge des DT_BYTES-Datentyps, abgeschnitten. Wenn im Schema keine maximale Länge angegeben ist, wird die Standardlänge von Spalten mit einem der Datentypen auf 255 festgelegt. Das Abschneiden von Daten in der XML-Quelle wird auf die gleiche Weise gehandhabt wie das Abschneiden in anderen Datenflusskomponenten. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).  
  
 Sie können den Datentyp und die Spaltenlänge ändern. Weitere Informationen finden Sie unter [Integration Services Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="configuration-of-the-xml-source"></a>Konfiguration der XML-Quelle  
 Die XML-Quelle unterstützt drei verschiedene Datenzugriffsmodi. Sie können den Dateispeicherort der XML-Datendatei, eine Variable mit dem Dateispeicherort oder eine Variable mit den XML-Daten angeben.  
  
 Die XML-Quelle schließt die benutzerdefinierten Eigenschaften **XMLData** und **XMLSchemaDefinition** ein, die beim Laden des Pakets mithilfe von Eigenschaftsausdrücken aktualisiert werden können. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften der XML-Quelle](../../integration-services/data-flow/xml-source-custom-properties.md).  
  
 Die XML-Quelle unterstützt mehrere reguläre Ausgaben und Fehlerausgaben.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] schließt das Dialogfeld **Quellen-Editor für XML**zum Konfigurieren der XML-Quelle ein. Dieses Dialogfeld steht im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zur Verfügung.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften der XML-Quelle](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen der Eigenschaften anzuzeigen:  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="xml-source-editor-connection-manager-page"></a>Quellen-Editor für XML (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** in **Quellen-Editor für XML** können Sie eine XML-Datei und die XML-Schemadefinition (XSD) angeben, mit der die XML-Daten transformiert werden.  
  
### <a name="static-options"></a>Statische Optionen  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|value|Description|  
|-----------|-----------------|  
|XML-Dateispeicherort|Ruft Daten aus einer XML-Datei ab.|  
|XML-Datei aus Variable|Gibt den XML-Dateinamen in einer Variablen an.<br /><br /> **Verwandte Informationen:** [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|XML-Daten aus Variable|Ruft XML-Daten aus einer Variablen ab.|  
  
 **Inlineschema verwenden**  
 Gibt an, ob die XML-Quelldaten das XSD-Schema enthalten, mit dem die Struktur und die Daten definiert und überprüft werden.  
  
 **XSD-Speicherort**  
 Geben Sie den Pfad und den Dateinamen der XSD-Schemadatei ein, oder suchen Sie die Datei, indem Sie auf die Schaltfläche **Durchsuchen**klicken.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie die XSD-Schemadatei suchen.  
  
 **XSD-Code generieren**  
 Mithilfe des Dialogfelds **Speichern unter** können Sie einen Speicherort für die automatisch generierte XSD-Schemadatei auswählen. Der Editor leitet das Schema aus der Struktur der XML-Daten ab.  
  
### <a name="data-access-mode-dynamic-options"></a>Dynamische Optionen (Datenzugriffsmodus)  
  
#### <a name="data-access-mode--xml-file-location"></a>Datenzugriffsmodus = Speicherort der XML-Datei  
 **XML-Speicherort**  
 Geben Sie den Pfad und den Dateinamen der XML-Datendatei ein, oder suchen Sie die Datei, indem Sie auf die Schaltfläche **Durchsuchen**klicken.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie die XML-Datendatei suchen.  
  
#### <a name="data-access-mode--xml-file-from-variable"></a>Datenzugriffsmodus = XML-Datei aus Variable  
 **Variablenname**  
 Wählt die Variable aus, die den Pfad und den Dateinamen der XML-Datei enthält.  
  
#### <a name="data-access-mode--xml-data-from-variable"></a>Datenzugriffsmodus = XML-Daten aus Variable  
 **Variablenname**  
 Wählt die Variable aus, die die XML-Daten enthält.  
  
## <a name="xml-source-editor-columns-page"></a>Quellen-Editor für XML (Seite Spalten)
  Mithilfe des Knotens **Spalten** im Dialogfeld **Quellen-Editor für XML** können Sie einer externen (Quell-)Spalte eine Ausgabespalte zuordnen.  
  
### <a name="options"></a>Tastatur  
 **Verfügbare externe Spalten**  
 Zeigt die Liste der in der Datenquelle verfügbaren externen Spalten an. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden.  
  
 **Externe Spalte**  
 Zeigt die externen (Quell-)Spalten in der Reihenfolge an, in der sie von dem Task gelesen werden. Sie können die Reihenfolge ändern, indem Sie zunächst die ausgewählten Spalten in der im Editor angezeigten Tabelle löschen. Wählen Sie anschließend die externen Spalten in einer anderen Reihenfolge aus der Liste aus.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen an. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
## <a name="xml-source-editor-error-output-page"></a>Quellen-Editor für XML (Seite Fehlerausgabe)
  Mithilfe der Seite **Fehlerausgabe** des Dialogfelds **Quellen-Editor für XML** können Sie Fehlerbehandlungsoptionen auswählen und Eigenschaften für Fehlerausgabespalten festlegen.  
  
### <a name="options"></a>Tastatur  
 **Eingabe/Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen (Quell-)Spalten an, die im Dialogfeld **Quellen-Editor für XML** auf der Seite **Verbindungs-Manager**ausgewählt wurden.  
  
 **Fehler**  
 Gibt an, was bei Auftreten eines Fehlers geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Gibt an, was im Falle einer Kürzung geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Beschreibung**  
 Zeigt die Beschreibung des Fehlers an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Gibt an, was im Falle eines Fehlers oder einer Kürzung mit den ausgewählten Zellen geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Extrahieren von Daten mithilfe der XML-Quelle](../../integration-services/data-flow/extract-data-by-using-the-xml-source.md)  
