---
title: Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs: VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
caps.latest.revision: "46"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ede9923efe50fa8accb4aab6b0455bf2823dfb75
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor
  Bevor Sie benutzerdefinierten Code in der Skriptkomponente schreiben, müssen Sie sich für eine Datenflusskomponente entscheiden (Quelle, Transformation oder Ziel) und anschließend die Metadaten und Eigenschaften der Komponente im **Transformations-Editor für Skripterstellung** konfigurieren.  
  
## <a name="selecting-the-type-of-component-to-create"></a>Auswählen der zu erstellenden Komponentenart  
 Wenn Sie zum Bereich Datenfluss des [!INCLUDE[ssIS](../../../includes/ssis-md.md)]-Designers eine Skriptkomponente hinzufügen, wird das Dialogfeld **Skriptkomponententyp auswählen** geöffnet. Sie konfigurieren die Komponente vorab als Quelle, Transformation oder Ziel. Nachdem Sie diese erste Auswahl getroffen haben, können Sie die Komponente im **Transformations-Editor für Skripterstellung** weiter konfigurieren.  
  
 Verwenden Sie im Dialogfeld **Optionen** auf der Seite **Allgemein** die Option **Skriptsprache**, um die Standardskriptsprache für die Skriptkomponente festzulegen. Weitere Informationen finden Sie unter [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
## <a name="understanding-the-two-design-time-modes"></a>Grundlegendes zu den beiden Entwurfszeitmodi  
 Im [!INCLUDE[ssIS](../../../includes/ssis-md.md)]-Designer weist die Skriptkomponente zwei Modi auf: Metadatenentwurfsmodus und Codeentwurfsmodus.  
  
 Wenn Sie den **Transformations-Editor für Skripterstellung** öffnen, befindet sich die Komponente im Metadatenentwurfsmodus. In diesem Modus können Sie Eingabespalten auswählen und Ausgaben sowie Ausgabespalten hinzufügen oder konfigurieren, aber Sie können keinen Code erstellen. Nachdem Sie die Metadaten der Komponente konfiguriert haben, können Sie zum Codeentwurfsmodus wechseln, um das Skript zu erstellen.  
  
 Wenn Sie durch Klicken auf **Skript bearbeiten** in den Codeentwurfsmodus wechseln, sperrt die Skriptkomponente die Metadaten, um weitere Änderungen zu verhindern, und erstellt anschließend aus den Metadaten der Ein- und Ausgaben automatisch Basiscode. Nachdem der automatisch generierte Code vollständig ist, sind Sie in der Lage, den benutzerdefinierten Code einzugeben. Dieser verwendet die automatisch generierten Basisklassen, um Eingabezeilen zu verarbeiten, auf Puffer und Spalten in den Puffern zuzugreifen sowie Verbindungs-Manager und Variablen aus dem Paket abzurufen. Hierbei handelt es sich ausschließlich um stark typisierte Objekte.  
  
 Sie können zum Metadatenentwurfsmodus zurückwechseln, nachdem Sie den benutzerdefinierten Code im Codeentwurfsmodus eingegeben haben. Dadurch wird der von Ihnen geschriebene Code nicht gelöscht. Nachfolgende Änderungen an den Metadaten sorgen jedoch dafür, dass die Basisklasse neu generiert wird. Danach kann die Validierung der Komponente fehlschlagen, da Objekte, auf die der benutzerdefinierte Code verweist, möglicherweise nicht mehr existieren oder geändert wurden. In diesem Fall müssen Sie den Code manuell korrigieren, damit er anhand der neu generierten Basisklasse erfolgreich kompiliert werden kann.  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>Konfigurieren der Komponente im Metadatenentwurfsmodus  
 Im Metadatenentwurfsmodus können Sie Eingabespalten auswählen und Ausgaben sowie Ausgabespalten hinzufügen und konfigurieren, aber Sie können keinen Code erstellen. Wechseln Sie, nachdem Sie die Metadaten der Komponente konfiguriert haben, in den Codeentwurfsmodus, um das Skript zu erstellen.  
  
 Welche Eigenschaften Sie im benutzerdefinierten Editor konfigurieren müssen, hängt von der Nutzung der Skriptkomponente ab. Die Skriptkomponente kann als Quelle, Transformation oder Ziel konfiguriert werden. Abhängig von der Verwendungsweise der Komponente unterstützt sie entweder eine Eingabe und/oder Ausgaben. Der von Ihnen erstellte benutzerdefinierte Code verarbeitet die Eingabe- und Ausgabezeilen und -spalten.  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>Seite 'Eingabespalten' des Transformations-Editors für Skripterstellung  
 Die Seite **Eingabespalten** im **Transformations-Editor für Skripterstellung** wird für Transformationen und Ziele, nicht jedoch für Quellen angezeigt. Auf dieser Seite wählen Sie die Eingabespalten aus, die Sie für das benutzerdefinierte Skript verfügbar machen möchten, und legen Lese- oder Lese-/Schreibzugriff darauf fest.  
  
 Im Codeprojekt, das basierend auf diesen Metadaten erstellt wird, enthält das Projektelement BufferWrapper für jede Eingabe eine Klasse, die wiederum typisierte Accessoreigenschaften für jede ausgewählte Eingabespalte beinhaltet. Wenn Sie beispielsweise eine ganzzahlige **CustomerID**-Spalte und eine **CustomerName**-Zeichenfolgenspalte aus einer Eingabe namens **CustomerInput** auswählen, enthält das Projektelement BufferWrapper eine **CustomerInput**-Klasse, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> abgeleitet ist. Die **CustomerInput**-Klasse stellt eine ganzzahlige Eigenschaft namens **CustomerID** und eine Zeichenfolgeneigenschaft namens **CustomerName** zur Verfügung. Diese Konvention macht es möglich, Code mit einer Typprüfung wie im folgenden Beispiel zu schreiben:  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 Weitere Informationen zum Konfigurieren von Eingabespalten für einen bestimmten Datenflusskomponententyp finden Sie im entsprechenden Beispiel unter [Developing Specific Types of Script Components (Entwickeln bestimmter Arten von Skriptkomponenten)](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>Seite 'Eingaben und Ausgaben' des Transformations-Editors für Skripterstellung  
 Die Seite **Eingaben und Ausgaben** im **Transformations-Editor für Skripterstellung** wird für Quellen, Transformationen und Ziele angezeigt. Auf dieser Seite können Sie Ein- und Ausgaben sowie Ausgabespalten, die Sie im benutzerdefinierten Skript verwenden möchten, hinzufügen, entfernen und konfigurieren. Hierbei gelten folgende Einschränkungen:  
  
-   Wenn die Skriptkomponente als Quelle verwendet wird, hat sie keine Eingabe, unterstützt jedoch mehrere Ausgaben.  
  
-   Wenn die Skriptkomponente als Transformation verwendet wird, werden eine Eingabe und mehrere Ausgaben unterstützt.  
  
-   Wenn die Skriptkomponente als Ziel verwendet wird, unterstützt sie eine Eingabe, hat jedoch keine Ausgaben.  
  
 Im Codeprojekt, das basierend auf diesen Metadaten erstellt wird, enthält das Projektelement BufferWrapper für jede Ein- und Ausgabe eine Klasse. Wenn Sie beispielsweise eine Ausgabe namens **CustomerOutput** erstellen, enthält das Projektelement BufferWrapper eine **CustomerOutput**-Klasse, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> abgeleitet ist. Die **CustomerOutput**-Klasse beinhaltet typisierte Accessoreigenschaften für jede erstellte Ausgabespalte.  
  
 Sie können Ausgabespalten nur auf der Seite **Eingaben und Ausgaben** konfigurieren. Eingabespalten für Transformationen und Ziele können Sie auf der Seite **Eingabespalten** auswählen. Für Ausgabespalten weisen die im Projektelement BufferWrapper erstellten typisierten Accessoreigenschaften nur Schreibzugriff auf. Die Accessoreigenschaften für Eingabespalten haben dagegen Lese- oder Lese-/Schreibzugriff, je nachdem, welche Nutzungsart Sie auf der Seite **Eingabespalten** für die jeweilige Spalte festgelegt haben.  
  
 Weitere Informationen zum Konfigurieren von Ein- und Ausgaben für einen bestimmten Datenflusskomponententyp finden Sie im entsprechenden Beispiel unter [Developing Specific Types of Script Components (Entwickeln bestimmter Arten von Skriptkomponenten)](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
> [!NOTE]  
>  Zur automatischen Bearbeitung von Fehlerzeilen können Sie eine Ausgabe in der Skriptkomponente zwar nicht direkt als Fehlerausgabe konfigurieren, aber Sie können die Funktion einer Fehlerausgabe reproduzieren, indem Sie eine weitere Ausgabe erstellen und ein Skript verwenden, um Zeilen ggf. an diese Ausgabe weiterzuleiten. Weitere Informationen finden Sie unter [Simulating an Error Output for the Script Component (Simulieren einer Fehlerausgabe für die Skriptkomponente)](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>Eigenschaften 'ExclusionGroup' und 'SynchronousInputID' von Ausgaben  
 Die **ExclusionGroup**-Eigenschaft hat nur in Transformationen mit synchronen Ausgaben einen Wert ungleich 0, in denen der Code einen Filter oder eine Verzweigung ausführt und jede Zeile an eine der Ausgaben weiterleitet, die denselben **ExclusionGroup**-Wert ungleich 0 aufweisen. Die Transformation kann Zeilen beispielsweise entweder an die Standard- oder eine Fehlerausgabe weiterleiten. Wenn Sie für dieses Szenario zusätzliche Ausgaben erstellen, achten Sie darauf, den Wert der **SynchronousInputID**-Eigenschaft auf die ganze Zahl festzulegen, die der **ID** der Komponenteneingabe entspricht.  
  
 Die **SynchronousInputID**-Eigenschaft verfügt nur in Transformationen mit synchronen Ausgaben über einen Wert ungleich 0. Wenn der Wert dieser Eigenschaft null ist, bedeutet dies, dass die Ausgabe asynchron ist. Für eine synchrone Ausgabe, bei der Zeilen an die gewählten Ausgaben übergeben werden, ohne neue Zeilen hinzuzufügen, sollte die Eigenschaft die **ID** der Komponenteneingabe enthalten.  
  
> [!NOTE]  
>  Wenn der **Transformations-Editor für Skripterstellung** die erste Ausgabe generiert, legt er die **SynchronousInputID**-Eigenschaft der Ausgabe auf die **ID** der Komponenteneingabe fest. Bei der Erstellung weiterer Ausgaben legt der Editor die **SynchronousInputID**-Eigenschaften dieser Ausgaben auf 0 fest.  
>   
>  Wenn Sie eine Komponente mit synchronen Ausgaben erstellen, muss die **SynchronousInputID**-Eigenschaft für jede Ausgabe auf die **ID** der Komponenteneingabe festgelegt sein. Daher muss für jede Ausgabe, die der Editor nach der ersten generiert, der **SynchronousInputID**-Wert von 0 in die **ID** der Komponenteneingabe geändert werden.  
>   
>  Wenn Sie eine Komponente mit asynchronen Ausgaben erstellen, muss die **SynchronousInputID**-Eigenschaft für jede Ausgabe auf 0 festgelegt sein. Daher muss für die erste Ausgabe der **SynchronousInputID**-Wert von der **ID** der Komponenteneingabe in 0 geändert werden.  
  
 Ein Beispiel für das Weiterleiten von Zeilen an eine von zwei synchronen Ausgaben in der Skriptkomponente finden Sie unter [Creating a Synchronous Transformation with the Script Component (Erstellen einer synchronen Transformation mit der Skriptkomponente)](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md).  
  
### <a name="object-names-in-generated-script"></a>Objektnamen in generiertem Skript  
 Die Skriptkomponente analysiert die Namen von Ein- und Ausgaben sowie von Spalten in den Ein- und Ausgaben und generiert basierend auf diesen Namen Klassen und Eigenschaften im Projektelement BufferWrapper. Wenn die gefundenen Namen Zeichen beinhalten, die nicht zu den Unicode-Kategorien **UppercaseLetter**, **LowercaseLetter**, **TitlecaseLetter**, **ModifierLetter**, **OtherLetter**, oder **DecimalDigitLetter** gehören, werden die ungültigen Zeichen in den generierten Namen gelöscht. Da beispielsweise Leerzeichen entfernt werden, werden zwei Eingabespalten mit den Namen **FirstName** und [**First Name**] beide so interpretiert, als trügen sie den Spaltennamen **FirstName**. Dies kann unvorhersehbare Ergebnisse zur Folge haben. Um eine solche Situation zu vermeiden, sollten die Namen von Ein- und Ausgaben sowie Eingabe- und Ausgabespalten, die von der Skriptkomponente verwendet werden, nur Zeichen aus den in diesem Abschnitt genannten Unicode-Kategorien enthalten.  
  
### <a name="script-page-of-the-script-transformation-editor"></a>Seite 'Skript' des Transformations-Editors für Skripterstellung  
 Auf der Seite **Skript** im **Skripttask-Editor** können Sie dem Skripttask einen eindeutigen Namen und eine Beschreibung zuweisen. Außerdem können Sie Werte für die folgenden Eigenschaften zuweisen.  
  
> [!NOTE]  
>  In [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] und höheren Versionen werden alle Skripts vorkompiliert. In vorherigen Versionen mussten Sie dafür die **Precompile**-Eigenschaft für den Task festlegen.  
  
#### <a name="validateexternalmetadata-property"></a>Eigenschaft 'ValidateExternalMetadata'  
 Der boolesche Wert der **ValidateExternalMetadata**-Eigenschaft gibt an, ob die Komponente zur Entwurfszeit eine Prüfung anhand externer Datenquellen ausführen oder diese Prüfung bis zur Laufzeit verschieben soll. Standardmäßig weist diese Eigenschaft den Wert **TRUE** auf, d.h. die externen Metadaten werden zur Entwurfs- und zur Laufzeit geprüft. Wenn eine externe Datenquelle zur Entwurfszeit nicht verfügbar ist, sollten Sie den Wert der Eigenschaft auf **FALSE** festlegen. Dies ist beispielsweise dann der Fall, wenn das Paket die Quelle erst zur Laufzeit herunterlädt oder das Ziel erst dann erstellt.  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>Eigenschaften 'ReadOnlyVariables' und 'ReadWriteVariables'  
 Sie können kommagetrennte Listen vorhandener Variablen als Werte dieser Eigenschaften eingeben, um die Variablen für schreibgeschützten oder Lese-/Schreibzugriff im Code der Skriptkomponente verfügbar zu machen. Auf Variablen wird im Code über die Eigenschaften <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> und <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> der automatisch generierten Basisklasse zugegriffen. Weitere Informationen finden Sie unter [Using Variables in the Script Component (Verwenden von Variablen in der Skriptkomponente)](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
> [!NOTE]  
>  Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 Sie können [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# als Programmiersprache für die Skriptkomponente auswählen.  
  
#### <a name="edit-script-button"></a>Schaltfläche 'Skript bearbeiten'  
 Die Schaltfläche **Skript bearbeiten** öffnet die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications-IDE (VSTA), in der Sie das benutzerdefinierte Skript schreiben. Weitere Informationen finden Sie unter [Coding and Debugging the Script Component (Codieren und Debuggen der Skriptkomponente)](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>Seite 'Verbindungs-Manager' des Transformations-Editors für Skripterstellung  
 Auf der Seite **Verbindungs-Manager** im **Transformations-Editor für Skripterstellung** können Sie Verbindungs-Manager hinzufügen und entfernen, die im benutzerdefinierten Skript verwendet werden sollen. Normalerweise müssen Sie Verbindungs-Manager mit Verweisen versehen, wenn Sie eine Quell- oder Zielkomponente erstellen.  
  
 Im Codeprojekt, das basierend auf diesen Metadaten erstellt wird, enthält das Projektelement **ComponentWrapper** eine **Connections**-Auflistungsklasse, die für jeden ausgewählten Verbindungs-Manager eine typisierte Accessoreigenschaft aufweist. Jede typisierte Accessoreigenschaft trägt denselben Namen wie der jeweilige Verbindungs-Manager und gibt einen Verweis auf den Verbindungs-Manager als Instanz von <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> zurück. Wenn Sie beispielsweise auf der Seite **Verbindungs-Manager** des Editors den Verbindungs-Manager `MyADONETConnection` hinzugefügt haben, können Sie mit dem folgenden Code einen Verweis auf diesen Verbindungs-Manager im Skript erhalten:  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 Weitere Informationen finden Sie unter [Connecting to Data Sources in the Script Component (Herstellen einer Verbindung mit Datenquellen in der Skriptkomponente)](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Codieren und Debuggen der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
