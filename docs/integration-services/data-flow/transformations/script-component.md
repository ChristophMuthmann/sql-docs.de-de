---
title: "Skript für Komponente | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- sql13.dts.designer.scriptcomponentdetails.f1
- sql13.dts.designer.scriptcomponent.f1
- sql13.dts.designer.scriptcomponent.connections.f1
- sql13.dts.designer.scriptcomponent.inputcolumn.f1
- sql13.dts.designer.scriptcomponent.columnproperties.f1
- sql13.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
caps.latest.revision: 70
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: e7b0923968137a76b68d0324223ffbb61e7443b9
ms.contentlocale: de-de
ms.lasthandoff: 08/19/2017

---
# <a name="script-component"></a>Skriptkomponente
  Die Skriptkomponente hostet Skripts und ermöglicht einem Paket benutzerdefinierten Skriptcode einzuschließen und benutzerdefinierten Skriptcode auszuführen. Die Skriptkomponente kann in Paketen für folgende Zwecke verwendet werden:  
  
-   Anwenden mehrerer Transformationen auf Daten, statt mehrere Transformationen im Datenfluss zu verwenden. Beispielsweise können mit einem Skript die Werte in zwei Spalten hinzugefügt und dann der Mittelwert der Summe berechnet werden.  
  
-   Zugreifen auf Geschäftsregeln in einer vorhandenen .NET-Assembly. Beispielsweise kann ein Skript eine Geschäftsregel anwenden, die den gültigen Wertebereich einer **Income** -Spalte angibt.  
  
-   Verwenden benutzerdefinierter Formeln und Funktionen zusätzlich zu den Funktionen und Operatoren der Ausdrucksgrammatik von [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Überprüfen Sie z. B. Kreditkartennummern mithilfe der LUHN-Formel.  
  
-   Überprüfen von Spaltendaten und Auslassen von Datensätzen mit ungültigen Daten. Beispielsweise kann ein Skript auswerten, ob eine Portogebühr angemessen ist, und Datensätze mit extrem hohen oder niedrigen Beträgen auslassen.  
  
 Die Skriptkomponente ist eine schnelle und einfache Möglichkeit, um benutzerdefinierte Funktionen in einen Datenfluss einzuschließen. Wenn Sie jedoch den Skriptcode in mehreren Paketen wiederverwenden möchten, sollten Sie nicht die Skriptkomponente verwenden, sondern eine benutzerdefinierte Komponente programmieren. Weitere Informationen finden Sie unter [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
> [!NOTE]  
>  Wenn die Skriptkomponente ein Skript enthält, das versucht, den Wert einer Spalte zu lesen, die NULL ist, kommt es bei der Ausführung des Pakets zu einem Fehler der Skriptkomponente. Es wird die Verwendung der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> -Methode im Skript empfohlen, um zu bestimmen, ob die Spalte NULL ist, bevor versucht wird, den Spaltenwert zu lesen.  
  
 Die Skriptkomponente kann als Quelle, als Transformation oder als Ziel verwendet werden. Diese Komponente unterstützt eine Eingabe und mehrere Ausgaben. Abhängig von der Verwendungsweise der Komponente unterstützt sie entweder eine Eingabe und/oder Ausgaben. Das Skript wird von jeder Zeile in der Eingabe oder Ausgabe aufgerufen.  
  
-   Wenn die Skriptkomponente als Quelle verwendet wird, werden mehrere Ausgaben unterstützt.  
  
-   Wenn die Skriptkomponente als Transformation verwendet wird, werden eine Eingabe und mehrere Ausgaben unterstützt.  
  
-   Wenn die Skriptkomponente als Ziel verwendet wird, wird eine Eingabe unterstützt.  
  
 Fehlerausgaben werden von der Skriptkomponente nicht unterstützt.  
  
 Nachdem Sie entschieden haben, dass die Skriptkomponente für Ihr Paket geeignet ist, müssen Sie die Eingaben und Ausgaben konfigurieren, das Skript entwickeln, das von der Komponente verwendet wird, und die Komponente konfigurieren.  
  
## <a name="understanding-the-script-component-modes"></a>Grundlegendes zu den Skriptkomponentenmodi  
 Im [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer weist die Skriptkomponente zwei Modi auf: Metadatenentwurfsmodus und Codeentwurfsmodus. Im Metadatenentwurfsmodus können Sie Eingaben und Ausgaben der Skriptkomponente hinzufügen und ändern, aber Sie können keinen Code erstellen. Nachdem Sie alle Eingaben und Ausgaben konfiguriert haben, wechseln Sie zum Codeentwurfsmodus, um das Skript zu erstellen. Die Skriptkomponente generiert von den Metadaten der Eingaben und Ausgaben automatisch Basiscode. Wenn Sie die Metadaten ändern, nachdem die Skriptkomponente den Basiscode generiert hat, kann es sein, dass der Code nicht mehr kompiliert wird, weil der aktualisierte Basiscode mit Ihrem Code inkompatibel ist.  
  
## <a name="writing-the-script-that-the-component-uses"></a>Erstellen des von der Komponente verwendeten Skripts  
 Die Skriptkomponente verwendet [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] -Tools für Anwendungen (VSTA) als Umgebung zum Erstellen der Skripts. Sie greifen auf VSTA im **Transformations-Editor für Skripterstellung**zu. Weitere Informationen finden Sie unter [Transformations-Editor für Skripterstellung &#40;Seite Skript&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 Die Skriptkomponente stellt ein VSTA-Projekt bereit, das eine automatisch generierte Klasse namens ScriptMain generiert, die die Komponentenmetadaten darstellt. Wenn z. B. die Skriptkomponente als Transformation mit drei Ausgaben verwendet wird, enthält ScriptMain eine Methode für jede Ausgabe. ScriptMain ist der Einstiegspunkt in das Skript.  
  
 VSTA enthält alle Standardfunktionen der [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] -Umgebung, z. B. den [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] -Editor mit Farbcodierung, IntelliSense und den Objektkatalog. Das von der Skriptkomponente verwendete Skript wird in der Paketdefinition gespeichert. Wenn Sie das Paket entwerfen, wird der Skriptcode vorübergehend in eine Projektdatei geschrieben.  
  
 VSTA unterstützt die Programmiersprachen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# und [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic.  
  
 Informationen zum Programmieren der Skriptkomponente finden Sie unter [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md). Detailliertere Informationen zum Konfigurieren der Skriptkomponente als Quelle, Transformation oder Ziel finden Sie unter [Developing Specific Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md). Zusätzliche Beispiele, welche die Verwendung der Skriptkomponente veranschaulichen (wie z. B. ODBC-Ziele), finden Sie unter [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
> [!NOTE]  
>  Anders als in früheren Versionen, in denen Sie angeben konnten, ob die Skripts vorkompiliert sind, werden in [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] und nachfolgenden Versionen alle Skripts vorkompiliert. Wenn ein Skript vorkompiliert ist, wird das Sprachmodul zur Laufzeit nicht geladen, und das Paket wird schneller ausgeführt. Kompilierte binäre Dateien belegen jedoch erheblich mehr Speicherplatz.  
  
## <a name="configuring-the-script-component"></a>Konfigurieren der Skriptkomponente  
 Es gibt folgende Möglichkeiten, um die Skriptkomponente zu konfigurieren:  
  
-   Wählen Sie die Eingabespalten aus, auf die verwiesen werden kann.  
  
    > [!NOTE]  
    >  Sie können nur einen Eingang konfigurieren, wenn Sie den [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer verwenden.  
  
-   Stellen Sie das Skript bereit, das von der Komponente ausgeführt wird.  
  
-   Geben Sie die Skriptsprache an.  
  
-   Stellen Sie durch Trennzeichen getrennte Listen mit schreibgeschützten Variablen und Lese-/Schreibvariablen bereit.  
  
-   Fügen Sie mehr Ausgaben hinzu, und fügen Sie Ausgabespalten hinzu, denen das Skript Werte zuweist.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
### <a name="configuring-the-script-component-in-the-designer"></a>Konfigurieren der Skriptkomponente im Designer  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>Programmgesteuertes Konfigurieren der Skriptkomponente im Designer  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Fenster **Eigenschaften** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="select-script-component-type"></a>Skriptkomponententyp auswählen
  Mithilfe des Dialogfelds **Skriptkomponententyp auswählen** können Sie angeben, ob eine Skripttransformation mit einer Vorkonfiguration als Quelle, Transformation oder Ziel verwendet wird.  
  
 Weitere Informationen zur Skriptkomponente finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Weitere Informationen zur Programmierung der Skriptkomponente finden Sie unter [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>enthalten  
 Ihre Auswahl zwischen **Quelle**, **Ziel**und **Transformation** beeinflusst die Konfiguration der Skripttransformation und die Seiten des Transformations-Editors für die Skripterstellung.  
  
## <a name="script-transformation-editor-connection-managers-page"></a>Transformations-Editor für Skripterstellung (Seite Verbindungs-Manager)
  Auf der Seite **Verbindungs-Manager** von **Transformations-Editor für Skripterstellung** können Sie Verbindungen angeben, die vom Skript verwendet werden.  
  
 Weitere Informationen zur Skriptkomponente finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Weitere Informationen zur Programmierung der Skriptkomponente finden Sie unter [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>enthalten  
 **Connection managers**  
 Zeigen Sie die Liste der Verbindungen an, die durch das Skript verwendet werden können.  
  
 **Name**  
 Geben Sie einen eindeutigen aussagekräftigen Namen für die Verbindung ein.  
  
 **Verbindungs-Manager**  
 Wählen Sie aus der Liste der verfügbaren Verbindungs-Manager, oder wählen Sie  **\<neue Verbindung >** So öffnen die **SSIS-Verbindungs-Manager hinzufügen** (Dialogfeld).  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung für die Verbindung ein.  
  
 **Hinzufügen**  
 Fügen Sie der Liste **Verbindungs-Manager** eine weitere Verbindung hinzu.  
  
 **Entfernen**  
 Entfernen Sie die ausgewählte Verbindung aus der Liste **Verbindungs-Manager** .  
  
## <a name="script-transformation-editor-input-columns-page"></a>Transformations-Editor für Skripterstellung (Seite Eingabespalten)
  Legen Sie mithilfe der Seite **Eingabespalten** des Dialogfelds **Transformations-Editor für Skripterstellung** die Eigenschaften für Eingabespalten fest.  
  
> [!NOTE]  
>  Für Quellkomponenten, die Ausgaben, aber keine Eingaben haben, wird die Seite **Eingabespalten** nicht angezeigt.  
  
 Weitere Informationen zur Skriptkomponente finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Weitere Informationen zur Programmierung der Skriptkomponente finden Sie unter [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>enthalten  
 **Eingabename**  
 Wählen Sie eine Option aus der Liste der verfügbaren Eingaben aus.  
  
 **Verfügbare Eingabespalten**  
 Geben Sie mithilfe der Kontrollkästchen die Spalten an, die von der Skripttransformation verwendet werden.  
  
 **Eingabespalte**  
 Wählen Sie für jede Zeile eine Spalte aus der Liste der verfügbaren Eingabespalten aus. Ihre Auswahl wird entsprechend in der Auswahl der Kontrollkästchen in der Tabelle **Verfügbare Eingabespalten**deutlich.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Eingabespalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 **Verwendungstyp**  
 Geben Sie an, ob die Skripttransformation jede Spalte als **ReadOnly** oder **ReadWrite**behandeln soll.  
  
## <a name="script-transformation-editor-inputs-and-outputs-page"></a>Transformations-Editor für Skripterstellung (Seiten Eingaben und Ausgaben)
  Auf der Seite **Eingaben und Ausgaben** des Dialogfelds **Transformations-Editor für Skripterstellung** können Sie Ein- und Ausgaben für die Skripterstellung hinzufügen, entfernen oder konfigurieren.  
  
> [!NOTE]  
>  Für Quellkomponenten sind keine Eingaben, sondern nur Ausgaben, und für Zielkomponenten keine Ausgaben, sondern nur Eingaben vorhanden. Transformationen verfügen über Ein- und Ausgaben.  
  
 Weitere Informationen zur Skriptkomponente finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Weitere Informationen zur Programmierung der Skriptkomponente finden Sie unter [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>enthalten  
 **Inputs and outputs**  
 Wählen Sie auf der linken Seite eine Eingabe oder Ausgabe, um die entsprechenden Eigenschaften in der Tabelle auf der rechten Seite anzuzeigen. Welche Eigenschaften bearbeitet werden können, ist von der getroffenen Auswahl abhängig. Viele dieser Eigenschaften sind schreibgeschützt. Weitere Informationen zu den einzelnen Eigenschaften finden Sie unter den folgenden Themen.  
  
 [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 **Ausgabe hinzufügen**  
 Fügen Sie der Liste eine weitere Ausgabe hinzu.  
  
 **Spalte hinzufügen**  
 Wählen Sie einen Ordner aus, in den die neue Ausgabespalte platziert werden soll, und fügen Sie anschließend die Spalte hinzu, indem Sie auf **Spalte hinzufügen**klicken.  
  
 **Ausgabe entfernen**  
 Wählen Sie eine Ausgabe aus, und entfernen Sie sie dann, indem Sie auf **Ausgabe entfernen**klicken.  
  
 **Spalte entfernen**  
 Wählen Sie eine Spalte aus, und entfernen Sie sie dann, indem Sie auf **Spalte entfernen**klicken.  
  
## <a name="script-transformation-editor-script-page"></a>Transformations-Editor für Skripterstellung (Seite Skript)
  Auf der Registerkarte **Skript** des Dialogfelds **Transformations-Editor für Skripterstellung** können Sie ein Skript und verknüpfte Eigenschaften angeben.  
  
 Weitere Informationen zur Skriptkomponente finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Weitere Informationen zur Programmierung der Skriptkomponente finden Sie unter [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>enthalten  
 **Eigenschaften**  
 Zeigt die Skripttransformationseigenschaften an und ermöglicht Änderungen. Viele dieser Eigenschaften sind schreibgeschützt. Die folgenden Eigenschaften können Sie ändern:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Description**|Beschreibt den Zweck der Skripttransformation.|  
|**LocaleID**|Gibt das Gebietsschema für die Bereitstellung regionsspezifischer Informationen für das Bestellen sowie für Datums- und Zeitformate an.|  
|**Name**|Geben Sie einen aussagekräftigen Namen für die Komponente ein.|  
|**ValidateExternalMetadata**|Zeigt an, ob von der Skripttransformation zur Entwurfszeit Spaltenmetadaten mithilfe externer Datenquellen überprüft werden. Bei dem Wert **false** wird die Überprüfung bis zur Ausführungszeit verzögert.|  
|**ReadOnlyVariables**|Geben Sie eine durch Trennzeichen getrennte Liste von Variablen für den schreibgeschützten Zugriff durch die Skripttransformation ein.<br /><br /> Hinweis: Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.|  
|**ReadWriteVariables**|Geben Sie eine durch Trennzeichen getrennte Liste von Variablen für den Lese-/Schreibzugriff durch die Skripttransformation ein.<br /><br /> Hinweis: Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.|  
|**ScriptLanguage**|Wählen Sie die Skriptsprache aus, die von der Skriptkomponente verwendet werden soll.<br /><br /> Um die Standardskriptsprache für Skriptkomponenten und Skripttasks festzulegen, verwenden Sie im Dialogfeld **Optionen** auf der Seite **Allgemein** die Option **Skriptsprache** .|  
|**UserComponentTypeName**|Gibt die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> -Klasse und die **Microsoft.SqlServer.TxScript** -Assembly an, die die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Infrastruktur unterstützen.|  
  
 **Skript bearbeiten**  
 Verwenden Sie [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] -Tools für Anwendungen (VSTA), um ein Skript zu erstellen oder zu ändern.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
  
  

