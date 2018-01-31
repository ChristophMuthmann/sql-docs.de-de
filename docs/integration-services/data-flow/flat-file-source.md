---
title: Flatfilequelle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.flatfilesource.f1
- sql13.dts.designer.flatfilesourceadapter.connection.f1
- sql13.dts.designer.flatfilesourceadapter.columns.f1
- sql13.dts.designer.flatfilesourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4bc2455f71ec0aa3f927249d50524cfb98f9b380
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="flat-file-source"></a>Flatfilequelle
  Die Flatfilequelle liest Daten aus einer Textdatei. Die Textdatei kann in einem Format mit Trennzeichen, fester Breite oder einem gemischten Format vorliegen.  
  
-   Beim Format mit Trennzeichen werden Spalten und Zeilen mithilfe von Spalten- und Zeilentrennzeichen definiert.  
  
-   Beim Format mit fester Breite werden Spalten und Zeilen mithilfe der Breite definiert. Dieses Format schließt außerdem ein Zeichen zur Auffüllung der Felder auf die maximale Breite ein.  
  
-   Beim Format mit einem rechten Flatterrand werden mithilfe der Breite alle Spalten definiert, außer der letzten Spalte, die durch das Zeilentrennzeichen getrennt wird.  
  
 Es gibt folgende Möglichkeiten, um die Flatfilequelle zu konfigurieren:  
  
-   Fügen Sie der Transformationsausgabe eine Zeile hinzu, die den Namen der Textdatei enthält, aus der die Flatfilequelle Daten extrahiert.  
  
-   Geben Sie an, ob die Flatfilequelle leere Zeichenfolgen in Spalten als NULL-Werte interpretiert.  
  
    > [!NOTE]  
    >  Für den von der Flatfilequelle verwendeten Verbindungs-Manager für Flatfiles muss die Verwendung eines Formats mit Trennzeichen konfiguriert werden, damit leere Zeichenfolgen als NULL-Werte interpretiert werden. Falls der Verbindungs-Manager ein Format mit fester Breite oder mit einem Flatterrand verwendet, können aus Leerzeichen bestehende Daten nicht als NULL-Werte interpretiert werden.  
  
 Die Ausgabespalte in der Ausgabe der Flatfilequelle schließt die FastParse-Eigenschaft ein. FastParse gibt an, ob die Spalte die schnelleren gebietsschemaneutralen Analyseroutinen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oder die gebietsschemabezogenen Standardanalyseroutinen verwendet. Weitere Informationen finden Sie unter [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) und [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013).  
  
 Ausgabespalten schließen auch UseBinaryFormat-Eigenschaft ein. Sie verwenden diese Eigenschaft, um Unterstützung für binäre Daten in Dateien zu implementieren, wie für Daten mit dem gepackten Dezimalformat. Standardmäßig ist UseBinaryFormat auf **FALSE**festgelegt. Wenn Sie ein Binärformat verwenden möchten, legen Sie UseBinaryFormat auf **TRUE** fest und den Datentyp in der Ausgabespalte auf **DT_BYTES**. Bei diesem Vorgang überspringt die Flatfilequelle die Datenkonvertierung und leitet die Daten durch die Ausgabespalte, wie sie ist. Sie können eine Transformation verwenden, wie „Abgeleitete Spalte“ oder „Datenkonvertierung“, um die **DT_BYTES** -Daten in einen anderen Datentyp umzuwandeln, oder Sie können ein benutzerdefiniertes Skript in eine Skripttransformation schreiben, um die Daten zu interpretieren. Sie können auch eine benutzerdefinierte Datenflusskomponente schreiben, um die Daten zu interpretieren. Weitere Informationen zu den Datentypen, die Sie in **DT_BYTES** umwandeln können, finden Sie unter [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Diese Quelle verwendet für den Zugriff auf die Textdatei einen Verbindungs-Manager für Flatfiles. Durch Festlegen von Eigenschaften im Verbindungs-Manager für Flatfiles können Sie Informationen zur Datei und zu jeder enthaltenen Spalte bereitstellen und angeben, wie die Flatfilequelle die Daten in der Textdatei behandeln soll. Beispielsweise können Sie die Zeichen angeben, mit denen Spalten und Zeilen in der Datei getrennt werden, sowie den Datentyp und die Länge jeder Spalte. Weitere Informationen finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Diese Quelle weist eine Ausgabe und eine Fehlerausgabe auf.  
  
## <a name="configuration-of-the-flat-file-source"></a>Konfiguration der Flatfilequelle  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften der Flatfile](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Weitere Informationen zum Festlegen der Eigenschaften einer Datenflusskomponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="flat-file-source-editor-connection-manager-page"></a>Quellen-Editor für Flatfiles (Seite Verbindungs-Manager)
  Wählen Sie auf der Seite **Verbindungs-Manager** des Dialogfelds **Quellen-Editor für Flatfiles** den Verbindungs-Manager aus, den die Flatfilequelle verwenden soll. Die Flatfilequelle liest die Daten aus einer Textdatei, die in den Formaten mit Trennzeichen, fester Breite oder mit gemischten Inhalten vorliegen kann.  
  
 Eine Flatfilequelle kann einen der folgenden Typen von Verbindungs-Manager verwenden:  
  
-   Einen Verbindungs-Manager für Flatfiles, wenn es sich bei der Quelle um eine einzelne Flatfile handelt. Weitere Informationen finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
-   Einen Verbindungs-Manager für mehrere Flatfiles, wenn es bei der Quelle um mehrere Flatfiles handelt und der Datenflusstask sich in einem Schleifencontainer wie dem For-Schleifencontainer befindet. In jeder Schleife des Containers werden von der Flatfilequelle Daten vom nächsten Dateinamen geladen, der vom Verbindungs-Manager für mehrere Flatfiles bereitgestellt wird. Weitere Informationen finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Tastatur  
 **Flat file connection manager**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus der Liste aus, oder erstellen Sie einen neuen Verbindungs-Manager, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Verbindungs-Manager-Editor für Flatfiles** einen neuen Verbindungs-Manager.  
  
 **NULL-Werte aus der Quelle als NULL-Werte im Datenfluss beibehalten**  
 Geben Sie an, ob NULL-Werte erhalten werden, wenn Daten extrahiert werden. Der Standardwert dieser Eigenschaft ist **false**. Wenn dieser Wert f**alse**ist, ersetzt die Flatfilequelle die NULL-Werte aus den Quelldaten mit entsprechenden Standardwerten für jede Spalte, z. B. mit leeren Zeichenfolgen in Zeichenfolgenspalten und Nullen in numerischen Spalten.  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Datenansicht** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
## <a name="flat-file-source-editor-columns-page"></a>Quellen-Editor für Flatfiles (Seite Spalten)
  Mithilfe des Knotens **Spalten** des Dialogfelds **Quellen-Editor für Flatfiles** können Sie jeder externen (Quell-)Spalte eine Ausgabespalte zuordnen.  
  
> [!NOTE]  
>  Die **FileNameColumnName** -Eigenschaft der Flatfilequelle und die **FastParse** -Eigenschaft ihrer Ausgabespalten sind nicht im **Quellen-Editor für Flatfiles**verfügbar, sie können jedoch mithilfe des Dialogfelds **Erweiterter Editor**festgelegt werden. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Flatfilequelle von [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
### <a name="options"></a>Tastatur  
 **Verfügbare externe Spalten**  
 Zeigt die Liste der in der Datenquelle verfügbaren externen Spalten an. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden.  
  
 **Externe Spalte**  
 Zeigt die externen (Quell-)Spalten in der Reihenfolge an, in der sie von dem Task gelesen werden. Sie können die Reihenfolge ändern, indem Sie zunächst die ausgewählten Spalten in der Tabelle löschen. Wählen Sie anschließend die externen Spalten in einer anderen Reihenfolge aus der Liste aus.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen an. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
## <a name="flat-file-source-editor-error-output-page"></a>Quellen-Editor für Flatfiles (Seite Fehlerausgabe)
  Mithilfe der Seite **Fehlerausgabe** im Dialogfeld **Quellen-Editor für Flatfiles** können Sie Fehlerbehandlungsoptionen auswählen und Eigenschaften für Fehlerausgabespalten festlegen.\  
  
### <a name="options"></a>Tastatur  
 **Eingabe/Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen (Quell-)Spalten an, die im Dialogfeld **Quellen-Editor für Flatfiles** auf der Seite **Verbindungs-Manager**ausgewählt wurden.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Flatfileziel](../../integration-services/data-flow/flat-file-destination.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  
