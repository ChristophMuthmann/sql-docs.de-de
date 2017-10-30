---
title: Configuring the Script Component in the Script Component Editor | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8488fcc7d402430f66b9b9018b31956a5a1d8383
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor
  Bevor Sie benutzerdefinierten Code in der Skriptkomponente schreiben, müssen, wählen Sie den Typ von Datenflusskomponente, die Sie erstellen möchten – Quelle, Transformation oder Ziel – und konfigurieren Sie der Komponente Metadaten und Eigenschaften in der **Skript Transformations-Editor**.  
  
## <a name="selecting-the-type-of-component-to-create"></a>Auswählen der zu erstellenden Komponentenart  
 Wenn Sie eine Skriptkomponente hinzufügen, um im Bereich Datenfluss des [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer die **Skriptkomponententyp** Dialogfeld wird angezeigt. Sie konfigurieren die Komponente vorab als Quelle, Transformation oder Ziel. Nachdem Sie diese erste Auswahl getroffen haben, können Sie weiterhin so konfigurieren Sie die Komponente in der **Skript Transformations-Editor**.  
  
 Um die Standardskriptsprache für die Skriptkomponente festzulegen, verwenden die **Skriptsprache** auf die option der **allgemeine** auf der Seite der **Optionen** (Dialogfeld). Weitere Informationen finden Sie unter [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
## <a name="understanding-the-two-design-time-modes"></a>Grundlegendes zu den beiden Entwurfszeitmodi  
 Im [!INCLUDE[ssIS](../../../includes/ssis-md.md)]-Designer weist die Skriptkomponente zwei Modi auf: Metadatenentwurfsmodus und Codeentwurfsmodus.  
  
 Beim Öffnen der **Skript Transformations-Editor**, die Komponente wird im metadatenentwurfsmodus. In diesem Modus können Sie Eingabespalten auswählen und Ausgaben sowie Ausgabespalten hinzufügen oder konfigurieren, aber Sie können keinen Code erstellen. Nachdem Sie die Metadaten der Komponente konfiguriert haben, können Sie zum Codeentwurfsmodus wechseln, um das Skript zu erstellen.  
  
 Wenn Sie zum codeentwurfsmodus durch Klicken auf wechseln **Bearbeitungsskript**, die Skriptkomponente sperrt Metadaten, um zu verhindern, dass zusätzliche Änderungen, und generiert dann automatisch Basiscode aus den Metadaten der Eingaben und Ausgaben. Nachdem der automatisch generierte Code vollständig ist, sind Sie in der Lage, den benutzerdefinierten Code einzugeben. Dieser verwendet die automatisch generierten Basisklassen, um Eingabezeilen zu verarbeiten, auf Puffer und Spalten in den Puffern zuzugreifen sowie Verbindungs-Manager und Variablen aus dem Paket abzurufen. Hierbei handelt es sich ausschließlich um stark typisierte Objekte.  
  
 Sie können zum Metadatenentwurfsmodus zurückwechseln, nachdem Sie den benutzerdefinierten Code im Codeentwurfsmodus eingegeben haben. Dadurch wird der von Ihnen geschriebene Code nicht gelöscht. Nachfolgende Änderungen an den Metadaten sorgen jedoch dafür, dass die Basisklasse neu generiert wird. Danach kann die Validierung der Komponente fehlschlagen, da Objekte, auf die der benutzerdefinierte Code verweist, möglicherweise nicht mehr existieren oder geändert wurden. In diesem Fall müssen Sie den Code manuell korrigieren, damit er anhand der neu generierten Basisklasse erfolgreich kompiliert werden kann.  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>Konfigurieren der Komponente im Metadatenentwurfsmodus  
 Im Metadatenentwurfsmodus können Sie Eingabespalten auswählen und Ausgaben sowie Ausgabespalten hinzufügen und konfigurieren, aber Sie können keinen Code erstellen. Wechseln Sie, nachdem Sie die Metadaten der Komponente konfiguriert haben, in den Codeentwurfsmodus, um das Skript zu erstellen.  
  
 Welche Eigenschaften Sie im benutzerdefinierten Editor konfigurieren müssen, hängt von der Nutzung der Skriptkomponente ab. Die Skriptkomponente kann als Quelle, Transformation oder Ziel konfiguriert werden. Abhängig von der Verwendungsweise der Komponente unterstützt sie entweder eine Eingabe und/oder Ausgaben. Der von Ihnen erstellte benutzerdefinierte Code verarbeitet die Eingabe- und Ausgabezeilen und -spalten.  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>Seite 'Eingabespalten' des Transformations-Editors für Skripterstellung  
 Die **Eingabespalten** auf der Seite der **Skript Transformations-Editor** für Transformationen und Ziele, nicht jedoch für Quellen angezeigt wird. Auf dieser Seite wählen Sie die Eingabespalten aus, die Sie für das benutzerdefinierte Skript verfügbar machen möchten, und legen Lese- oder Lese-/Schreibzugriff darauf fest.  
  
 Im Codeprojekt, das basierend auf diesen Metadaten erstellt wird, enthält das Projektelement BufferWrapper für jede Eingabe eine Klasse, die wiederum typisierte Accessoreigenschaften für jede ausgewählte Eingabespalte beinhaltet. Z. B., wenn Sie eine ganze Zahl auswählen **CustomerID** Spalte und eine Zeichenfolge **CustomerName** Spalte aus einer Eingabe namens **CustomerInput**, enthält das Projektelement BufferWrapper eine **CustomerInput** von abgeleitete Klasse <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>, und die **CustomerInput** Klasse macht eine Ganzzahleigenschaft, die mit dem Namen **CustomerID** und eine Zeichenfolgeneigenschaft, die mit dem Namen **CustomerName**. Diese Konvention macht es möglich, Code mit einer Typprüfung wie im folgenden Beispiel zu schreiben:  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 Weitere Informationen zum Konfigurieren von Eingabespalten für einen bestimmten Typ von Datenflusskomponente finden Sie im entsprechende Beispiel unter [Entwickeln von bestimmten Arten von Skriptkomponenten](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>Seite 'Eingaben und Ausgaben' des Transformations-Editors für Skripterstellung  
 Die **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor** für Quellen, Transformationen und Ziele angezeigt wird. Auf dieser Seite können Sie Ein- und Ausgaben sowie Ausgabespalten, die Sie im benutzerdefinierten Skript verwenden möchten, hinzufügen, entfernen und konfigurieren. Hierbei gelten folgende Einschränkungen:  
  
-   Wenn die Skriptkomponente als Quelle verwendet wird, hat sie keine Eingabe, unterstützt jedoch mehrere Ausgaben.  
  
-   Wenn die Skriptkomponente als Transformation verwendet wird, werden eine Eingabe und mehrere Ausgaben unterstützt.  
  
-   Wenn die Skriptkomponente als Ziel verwendet wird, unterstützt sie eine Eingabe, hat jedoch keine Ausgaben.  
  
 Im Codeprojekt, das basierend auf diesen Metadaten erstellt wird, enthält das Projektelement BufferWrapper für jede Ein- und Ausgabe eine Klasse. Angenommen, Sie erstellen eine Ausgabe mit dem Namen **CustomerOutput**, enthält das Projektelement BufferWrapper eine **CustomerOutput** von abgeleitete Klasse <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>, und die **CustomerOutput** Klasse enthält typisierte Accessoreigenschaften für jede erstellte Ausgabespalte.  
  
 Sie können Ausgabespalten nur auf Konfigurieren der **Eingaben und Ausgaben** Seite. Sie können die Eingabespalten für Transformationen und Ziele auswählen, auf die **Eingabespalten** Seite. Für Ausgabespalten weisen die im Projektelement BufferWrapper erstellten typisierten Accessoreigenschaften nur Schreibzugriff auf. Die Accessoreigenschaften für Eingabespalten werden schreibgeschützt sein oder Lese-/Schreibzugriff, je nach den Verwendungstyp, die Sie für jede Spalte ausgewählt haben, auf die **Eingabespalten** Seite.  
  
 Weitere Informationen zum Konfigurieren von Eingaben und Ausgaben für einen bestimmten Typ von Daten Datenflusskomponente finden Sie im entsprechende Beispiel unter [Entwickeln von bestimmten Arten von Skriptkomponenten](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
> [!NOTE]  
>  Zur automatischen Bearbeitung von Fehlerzeilen können Sie eine Ausgabe in der Skriptkomponente zwar nicht direkt als Fehlerausgabe konfigurieren, aber Sie können die Funktion einer Fehlerausgabe reproduzieren, indem Sie eine weitere Ausgabe erstellen und ein Skript verwenden, um Zeilen ggf. an diese Ausgabe weiterzuleiten. Weitere Informationen finden Sie unter [simulieren einer Fehlerausgabe für die Skriptkomponente](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>Eigenschaften 'ExclusionGroup' und 'SynchronousInputID' von Ausgaben  
 Die **ExclusionGroup** Eigenschaft hat einen Wert ungleich 0 (null) nur in Transformationen mit synchronen Ausgaben, wobei Codes Filter oder eine Verzweigung ausführt und wird jede Zeile an eine der Ausgaben, die ungleich NULL denselben **ExclusionGroup** Wert. Die Transformation kann Zeilen beispielsweise entweder an die Standard- oder eine Fehlerausgabe weiterleiten. Wenn Sie für dieses Szenario zusätzliche Ausgaben erstellen, stellen Sie sicher, zum Festlegen des Werts, der die **SynchronousInputID** Eigenschaft, um die ganze Zahl, die entspricht der **ID** der komponenteneingabe.  
  
 Die **SynchronousInputID** Eigenschaft hat einen Wert ungleich 0 (null) nur in Transformationen mit synchronen Ausgaben. Wenn der Wert dieser Eigenschaft null ist, bedeutet dies, dass die Ausgabe asynchron ist. Diese Eigenschaft sollte für eine synchrone Ausgabe, in denen Zeilen über übergeben werden der ausgewählten Ausgabe oder Ausgaben ohne neue Zeilen hinzuzufügen, enthalten die **ID** der komponenteneingabe.  
  
> [!NOTE]  
>  Wenn die **Skript Transformations-Editor** erstellt die erste Ausgabe, legt der **SynchronousInputID** -Eigenschaft die Ausgabe auf die **ID** der komponenteneingabe. Jedoch, wenn der Editor weitere Ausgaben erstellt, der-Editor setzt den **SynchronousInputID** -Eigenschaften dieser Ausgaben auf 0 (null).  
>   
>  Wenn Sie eine Komponente mit synchronen Ausgaben erstellen, muss jede Ausgabe haben seine **SynchronousInputID** -Eigenschaftensatz auf die **ID** der komponenteneingabe. Daher für jede Ausgabe, die der Editor erstellt werden, nachdem die erste Ausgabe haben, muss die **SynchronousInputID** Wert geändert wird, von 0 (null), um die **ID** der komponenteneingabe.  
>   
>  Wenn Sie eine Komponente mit asynchronen Ausgaben erstellen, muss jede Ausgabe haben seine **SynchronousInputID** -Eigenschaft auf 0 (null) festgelegt. Die erste Ausgabe müssen Sie daher ihre **SynchronousInputID** Wert geändert wird, aus der **ID** der komponenteneingabe auf 0 (null).  
  
 Ein Beispiel zum Weiterleiten von Zeilen an eine von zwei synchronen Ausgaben in der Skriptkomponente finden Sie unter [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md).  
  
### <a name="object-names-in-generated-script"></a>Objektnamen in generiertem Skript  
 Die Skriptkomponente analysiert die Namen von Ein- und Ausgaben sowie von Spalten in den Ein- und Ausgaben und generiert basierend auf diesen Namen Klassen und Eigenschaften im Projektelement BufferWrapper. Wenn die gefundenen Namen Zeichen beinhalten, die nicht auf den Unicode-Kategorien gehören **UppercaseLetter**, **LowercaseLetter**, **TitlecaseLetter**, **ModifierLetter**, **OtherLetter**, oder **DecimalDigitLetter**, werden die ungültigen Zeichen in den generierten Namen gelöscht. Beispielsweise Leerzeichen entfernt werden, die zwei Eingabespalten mit den Namen **FirstName** und [**Vorname**] beide so interpretiert, mit dem Spaltennamen **FirstName**, zu unvorhersehbaren Ergebnissen führt. Um eine solche Situation zu vermeiden, sollten die Namen von Ein- und Ausgaben sowie Eingabe- und Ausgabespalten, die von der Skriptkomponente verwendet werden, nur Zeichen aus den in diesem Abschnitt genannten Unicode-Kategorien enthalten.  
  
### <a name="script-page-of-the-script-transformation-editor"></a>Seite 'Skript' des Transformations-Editors für Skripterstellung  
 Auf der **Skript** auf der Seite der **Skripttask-Editor**, Sie weisen Sie einen eindeutigen Namen und eine Beschreibung für den Skripttask. Außerdem können Sie Werte für die folgenden Eigenschaften zuweisen.  
  
> [!NOTE]  
>  In [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] und höheren Versionen werden alle Skripts vorkompiliert. In früheren Versionen haben Sie angegeben, ob Skripts, durch Festlegen vorkompiliert sind einer **Precompile** Eigenschaft für den Task.  
  
#### <a name="validateexternalmetadata-property"></a>Eigenschaft 'ValidateExternalMetadata'  
 Der boolesche Wert, der die **' ValidateExternalMetadata '** -Eigenschaft gibt an, ob die Komponente Überprüfung anhand externer Datenquellen zur Entwurfszeit ausführen soll, oder gibt an, ob sie die Überprüfung bis zur Laufzeit verschieben soll. Standardmäßig ist der Wert dieser Eigenschaft **"true"**; d. h. die externe Metadaten wird sowohl zur Entwurfszeit und zur Laufzeit überprüft. Sie sollten zum Festlegen des Werts dieser Eigenschaft auf **"false"** bei eine externen Datenquelle steht nicht zur Entwurfszeit: z. B., wenn das Paket lädt die Quelle oder das Ziel nur zur Laufzeit erstellt.  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>Eigenschaften 'ReadOnlyVariables' und 'ReadWriteVariables'  
 Sie können kommagetrennte Listen vorhandener Variablen als Werte dieser Eigenschaften eingeben, um die Variablen für schreibgeschützten oder Lese-/Schreibzugriff im Code der Skriptkomponente verfügbar zu machen. Auf Variablen wird im Code über die Eigenschaften <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> und <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> der automatisch generierten Basisklasse zugegriffen. Weitere Informationen finden Sie unter [Using Variables in the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
> [!NOTE]  
>  Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 Sie können [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# als Programmiersprache für die Skriptkomponente auswählen.  
  
#### <a name="edit-script-button"></a>Schaltfläche 'Skript bearbeiten'  
 Die **Bearbeitungsskript** Schaltfläche öffnet die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE, in dem Sie das benutzerdefinierte Skript schreiben. Weitere Informationen finden Sie unter [codieren und Debuggen der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>Seite 'Verbindungs-Manager' des Transformations-Editors für Skripterstellung  
 Auf der **Verbindungs-Manager** auf der Seite der **Skript Transformations-Editor**, hinzufügen und Entfernen von Verbindungs-Manager, die Sie in Ihr benutzerdefiniertes Skript verwenden möchten. Normalerweise müssen Sie Verbindungs-Manager mit Verweisen versehen, wenn Sie eine Quell- oder Zielkomponente erstellen.  
  
 Im Code-Projekt, das generiert wird, auf der Grundlage dieser Metadaten, die **ComponentWrapper** Projektelement enthält eine **Verbindungen** Auflistungsklasse, die für jeden ausgewählten Verbindungs-Manager eine typisierte Accessoreigenschaft aufweist. Jede typisierte Accessoreigenschaft trägt denselben Namen wie der jeweilige Verbindungs-Manager und gibt einen Verweis auf den Verbindungs-Manager als Instanz von <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> zurück. Angenommen, wenn Sie einen Verbindungs-Manager mit dem Namen hinzugefügt haben `MyADONETConnection` auf die **Verbindungs-Manager** Seite des Editors können Sie einen Verweis auf den Verbindungs-Manager in Ihrem Skript abrufen, indem Sie mit dem folgenden Code:  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 Weitere Informationen finden Sie unter [Connecting to Data Sources in the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Beim Codieren und Debuggen der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

