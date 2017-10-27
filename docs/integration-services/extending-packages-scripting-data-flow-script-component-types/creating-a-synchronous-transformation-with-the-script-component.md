---
title: Erstellen einer synchronen Transformation mit der Skriptkomponente | Microsoft Docs
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
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d4a507c31f77449aba7eb884c39bf68c7c78581
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>Erstellen einer synchronen Transformation mit der Skriptkomponente
  Transformationskomponenten dienen im Datenfluss eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakets dazu, Daten auf dem Weg von der Quelle zum Ziel zu ändern und zu analysieren. Eine Transformation mit synchronen Ausgaben verarbeitet jede eingegebene Zeile, während sie die Komponente durchläuft. Eine Transformation mit asynchronen Ausgaben wartet, bis alle Eingabezeilen empfangen wurden, bevor die Verarbeitung abgeschlossen wird. In diesem Thema wird eine synchrone Transformation erläutert. Informationen über asynchrone Transformationen finden Sie unter [Erstellen einer asynchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md). Weitere Informationen zu den Unterschieden zwischen synchronen und asynchronen Komponenten finden Sie unter [Grundlegendes zu synchronen und asynchronen Transformationen](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Einen Überblick über die Skriptkomponente finden Sie unter [Extending the Data Flow mit der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 Die Skriptkomponente und der Infrastrukturcode, den sie generieren, erleichtern Ihnen die Entwicklung benutzerdefinierter Datenflusskomponenten deutlich. Um die Funktionsweise der Skriptkomponente zu verstehen, Sie können es jedoch hilfreich, lesen die Schritte, die Sie befolgen müssen, bei der Entwicklung einer benutzerdefinierten Datenflusskomponente im Abschnitt auf [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), und zwar insbesondere [Entwickeln einer benutzerdefinierten Transformationskomponente mit synchronen Ausgaben](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>Erste Schritte mit einer synchronen Transformationskomponente  
 Wenn Sie eine Skriptkomponente hinzufügen, um im Bereich Datenfluss des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer die **Skriptkomponententyp** Dialogfeld wird geöffnet und fordert Sie zum Auswählen eines Quelle, Ziel oder Transformation Komponententyps. Wählen Sie in diesem Dialogfeld **Transformation**.  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>Konfigurieren einer synchronen Transformationskomponente im Metadatenentwurfsmodus  
 Nachdem Sie die Option zum Erstellen einer Transformationskomponente ausgewählt haben, konfigurieren Sie die Komponente mit der **Skript Transformations-Editor**. Weitere Informationen finden Sie unter [Configuring the Script Component in the Script Component Editor](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Um die Skriptsprache für die Skriptkomponente festzulegen, legen Sie die **ScriptLanguage** Eigenschaft auf die **Skript** auf der Seite der **Skript Transformations-Editor**.  
  
> [!NOTE]  
>  Um die Standardskriptsprache für die Skriptkomponente festzulegen, verwenden die **Skriptsprache** auf die option der **allgemeine** auf der Seite der **Optionen** (Dialogfeld). Weitere Informationen finden Sie unter [emeine Seite](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Eine Datenfluss-Transformationskomponente verfügt über eine Eingabe und eine oder mehrere Ausgaben unterstützt. Konfigurieren die Eingaben und Ausgaben für die Komponente einer der Schritte, die Sie im metadatenentwurfsmodus müssen ist, mithilfe Abschließen der **Skript Transformations-Editor**, bevor Sie das benutzerdefinierte Skript schreiben.  
  
### <a name="configuring-input-columns"></a>Konfigurieren von Eingabespalten  
 Eine Transformationskomponente verfügt über eine Eingabe.  
  
 Auf der **Eingabespalten** auf der Seite der **Transformations-Editors für Skripterstellung,** die Spaltenliste zeigt die verfügbaren Spalten aus der Ausgabe der upstreamkomponente im Datenfluss. Markieren Sie die Spalten, die Sie transformieren oder durchlaufen möchten. Markieren Sie alle Spalten, die Sie an Ort und Stelle transformieren möchten, als Lesen/Schreiben.  
  
 Weitere Informationen zu den **Eingabespalten** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Seite "Spalten" Eingabe &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Konfigurieren von Eingaben, Ausgaben und Ausgabespalten  
 Eine Transformationskomponente unterstützt eine oder mehrere Ausgaben.  
  
 Auf der **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor**, sehen Sie, dass eine einzelne Ausgabe erstellt wurde, aber die Ausgabe keine Spalten enthält. Auf dieser Seite des Editors haben Sie die Möglichkeit, die folgenden Elemente zu konfigurieren.  
  
-   Erstellen Sie eine oder mehrere zusätzliche Ausgaben, beispielsweise eine simulierte Fehlerausgabe für Zeilen, die unerwartete Werte aufweisen. Verwenden der **Ausgabe hinzufügen** und **Ausgabe entfernen** Schaltflächen, um die Ausgaben der synchronen Transformationskomponente zu verwalten. Alle Eingabezeilen werden an alle verfügbaren Ausgaben weitergeleitet, außer Sie geben an, dass jede Zeile nur an eine der Ausgaben weitergeleitet werden soll. Sie angeben, dass Sie beabsichtigen, die Umleitung von Zeilen durch Angabe eines Werts ungleich NULL ganze Zahl, für die **"exclusiongroup"** -Eigenschaft der Ausgaben erreicht. In der spezifischen ganzzahligen Wert eingegeben **ExclusionGroup** zum Identifizieren der Ausgaben spielt keine Rolle, jedoch müssen Sie dieselbe ganze Zahl für die spezifische Ausgabegruppe durchgängig verwenden.  
  
    > [!NOTE]  
    >  Sie können auch eine Wert ungleich NULL **ExclusionGroup** Eigenschaftswert für eine einzelne Ausgabe, wenn Sie nicht alle Zeilen ausgeben möchten. Allerdings in diesem Fall müssen Sie explizit aufrufen der **DirectRowTo\<Outputbuffer >** Methode für jede Zeile, die an die Ausgabe gesendet werden soll.  
  
-   Zuweisen eines aussagekräftigeren Namens für Eingabe und Ausgaben In der Skriptkomponente werden diese Namen verwendet, um die typisierten Accessoreigenschaften zu erzeugen, mit denen Sie auf die Eingabe und Ausgaben in Ihrem Skript verweisen.  
  
-   Verändern Sie die Spalten für synchrone Transformationen nicht. Normalerweise werden bei einer synchronen Transformation dem Datenfluss keine Spalten hinzugefügt. Die Daten werden gleich im Puffer verändert, und der Puffer wird an die nächste Komponente im Datenfluss übergeben. Bei einer solchen Vorgehensweise müssen Sie den Transformationsausgaben keine Ausgabespalten explizit hinzufügen und diese dann konfigurieren. Die Ausgaben werden ohne explizit definierte Spalten im Editor angezeigt.  
  
-   Fügen Sie simulierten Fehlerausgaben neue Spalten für Fehler auf Zeilenebene hinzu. Üblicherweise haben mehrere Ausgaben in der gleichen **ExclusionGroup** haben den gleichen Satz von Ausgabespalten. Falls Sie eine simulierte Fehlerausgabe erstellen, sollten Sie jedoch mehrere Spalten hinzufügen, um Fehlerinformationen zu speichern. Informationen wie das Datenflussmodul Fehlerzeilen verarbeitet, finden Sie unter [mithilfe von Fehlerausgaben in einer Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md). Beachten Sie, dass Sie in der Skriptkomponente eigenen Code schreiben müssen, um geeignete Fehlerinformationen für die zusätzlichen Spalten zu erhalten. Weitere Informationen finden Sie unter [simulieren einer Fehlerausgabe für die Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Weitere Informationen zu den **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Eingaben und Ausgaben Seite &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Hinzufügen von Variablen  
 Wenn Sie vorhandene Variablen in Ihrem Skript verwenden möchten, können Sie diese im Hinzufügen der **ReadOnlyVariables** und **ReadWriteVariables** Eigenschaftsfeldern für die **Skript** auf der Seite der **Skript Transformations-Editor**.  
  
 Wenn Sie mehrere Variablen in die Eigenschaftsfelder hinzufügen, trennen Sie die Variablennamen durch Kommas. Sie können auch mehrere Variablen auswählen, indem Sie auf die Auslassungspunkte (**...** ) neben dem **ReadOnlyVariables** und **ReadWriteVariables** Eigenschaftenfelder, und wählen Sie dann die Variablen in der **Variablen auswählen** Das Dialogfeld.  
  
 Allgemeine Informationen zur Verwendung von Variablen mit der Skriptkomponente finden Sie unter [Using Variables in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Weitere Informationen zu den **Skript** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Seite "Skript" &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>Skripterstellung für eine synchrone Transformationskomponente im Codeentwurfsmodus  
 Nachdem Sie die Metadaten für Ihre Komponente konfiguriert haben, können Sie das benutzerdefinierte Skript schreiben. In der **Skript Transformations-Editor**auf die **Skript** auf **Bearbeitungsskript** So öffnen die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE in dem Sie das benutzerdefinierte Skript hinzufügen können. Die verwendete Skriptsprache, die Sie verwenden, hängt davon ab, ob Sie ausgewählt [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual c# als Skriptsprache für die **ScriptLanguage** Eigenschaft auf die **Skript** Seite ".  
  
 Wichtige Informationen, die für alle Arten von Komponenten, die mithilfe der Skriptkomponente erstellt gilt, finden Sie unter [codieren und Debuggen der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Grundlegendes zum automatisch generierten Code  
 Wenn Sie öffnen die VSTA IDE nach der Erstellung und Konfiguration einer Transformationskomponente die bearbeitbare **ScriptMain** Klasse angezeigt wird, im Codeeditor mit einem Stub für die **ProcessInputRow** Methode. Die **ScriptMain** Klasse ist, in dem Sie Ihren benutzerdefinierten Code schreiben und **ProcessInputRow** ist die wichtigste Methode in einer Transformationskomponente.  
  
 Wenn Sie öffnen die **Projektexplorer** Fenster in VSTA können Sie sehen, dass die Skriptkomponente auch schreibgeschützte generiert hat **BufferWrapper** und **ComponentWrapper** Projekt Elemente. Die **ScriptMain** Klasse erbt von der **UserComponent** -Klasse in der **ComponentWrapper** -Projektelement.  
  
 Zur Laufzeit ruft das Datenflussmodul die **ProcessInput** Methode in der **UserComponent** Klasse, welche Außerkraftsetzungen der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> übergeordnete Klasse. Die **ProcessInput** Methode durchläuft die Zeilen in den Eingabepuffer und ruft dann die **ProcessInputRow** Methode einmal für jede Zeile.  
  
### <a name="writing-your-custom-code"></a>Schreiben von benutzerdefiniertem Code  
 Eine Transformationskomponente mit synchronen Ausgaben ist die Datenflusskomponente, die am einfachsten geschrieben werden kann. Zum Beispiel besteht das später in diesem Thema dargestellte Beispiel mit einer einzigen Ausgabe aus dem folgenden benutzerdefinierten Code:  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 Zum Erstellen einer benutzerdefinierten synchronen Transformationskomponente fertig sind, verwenden Sie die überschriebene **ProcessInputRow** Methode, um die Daten in jeder Zeile des Eingabepuffers transformieren. Das Datenflussmodul leitet diesen Puffer an die nächste Komponente im Datenfluss weiter, sobald er voll ist.  
  
 Je nach Ihren Anforderungen auch empfiehlt zum Schreiben von Skript in die **PreExecute** und **"PostExecute"** in verfügbaren Methoden der **ScriptMain** -Klasse, ausführen Vorbereitende oder abschließende Verarbeitungsvorgänge.  
  
### <a name="working-with-multiple-outputs"></a>Arbeiten mit mehreren Ausgaben  
 Die Umleitung von Eingabezeilen an eine von zwei oder mehreren möglichen Ausgaben erfordert nicht viel mehr benutzerdefinierten Code als das Szenario mit einer einzigen Ausgabe, das bereits erläutert wurde. Zum Beispiel besteht das später in diesem Thema dargestellte Beispiel mit zwei Ausgaben aus dem folgenden benutzerdefinierten Code:  
  
```vb  
Row.City = UCase(Row.City)  
If Row.City = "REDMOND" Then  
    Row.DirectRowToMyRedmondAddresses()  
Else  
    Row.DirectRowToMyOtherAddresses()  
End If  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
if (Row.City=="REDMOND")  
{  
    Row.DirectRowToMyRedmondAddresses();  
}  
else  
{  
    Row.DirectRowToMyOtherAddresses();  
}  
```  
  
 In diesem Beispiel wird die Skriptkomponente generiert die **DirectRowTo\<OutputBufferX >** Methoden, basierend auf den Namen der Ausgaben, die Sie konfiguriert. Sie können ähnlichen Code verwenden, um Fehlerzeilen an eine simulierte Fehlerausgabe weiterzuleiten.  
  
## <a name="examples"></a>Beispiele  
 Die hier aufgeführten Beispiele veranschaulichen die benutzerdefinierten Code, der erforderlich ist, in der **ScriptMain** Klasse, um eine synchrone Transformationskomponente zu erstellen.  
  
> [!NOTE]  
>  Diese Beispiele verwenden die **Person.Address** -Tabelle in der **AdventureWorks** Beispieldatenbank aus, und übergeben Sie die erste und die vierte Spalte, die **IntAddressID** und  **Nvarchar (30) City** Spalten, durch den Datenfluss. Die gleichen Daten werden in den Quellen-, Transformations- und Zielbeispielen in diesem Abschnitt verwendet. Zusätzliche Voraussetzungen und Annahmen werden für jedes Beispiel dokumentiert.  
  
### <a name="single-output-synchronous-transformation-example"></a>Beispiel einer synchronen Transformation mit einer Ausgabe  
 Dieses Beispiel zeigt eine synchrone Transformationskomponente mit einer Ausgabe. Diese Transformation durchläuft die **AddressID** Spalte und konvertiert die **City** -Spalte in Großbuchstaben.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Fügen Sie der Datenfluss-Designeroberfläche eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Transformation.  
  
2.  Verbinden Sie die Ausgabe einer Quelle oder einer anderen Transformation mit der neuen Transformationskomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. Geben Sie diese Ausgabe sollte Daten aus der **Person.Address** Tabelle mit den **AdventureWorks** -Beispieldatenbank, die enthält die **AddressID** und **Stadt**  Spalten.  
  
3.  Öffnen der **Skript Transformations-Editor**. Auf der **Eingabespalten** Seite der **AddressID** und **City** Spalten. Markierung der **City** Spalte als Lese-/Schreibzugriff.  
  
4.  Auf der **Eingaben und Ausgaben** Seite, benennen Sie die Eingabe und Ausgabe aussagekräftigere Namen, z. B. **"myaddressinput"** und **"myaddressoutput"**. Beachten Sie, dass die **SynchronousInputID** entspricht der Ausgabe der **ID** der Eingabe. Sie müssen deshalb keine Ausgabespalten hinzufügen und konfigurieren.  
  
5.  Auf der **Skript** auf **Bearbeitungsskript** , und geben Sie das folgende Skript. Schließen Sie dann die skriptentwicklungsumgebung und den **Skript Transformations-Editor**.  
  
6.  Erstellen und konfigurieren Sie eine Zielkomponente, die **AddressID** und **City** Spalten, z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ziel oder die beispielzielkomponente, die im demonstriert[Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Verbinden Sie daraufhin die Ausgabe der Transformation mit der Zielkomponente. Sie können eine Zieltabelle erstellen, durch Ausführen des folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl in der **AdventureWorks** Datenbank:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  Führen Sie das Beispiel aus.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
    }  
  
}  
```  
  
### <a name="two-output-synchronous-transformation-example"></a>Beispiel einer synchronen Transformation mit zwei Ausgaben  
 Dieses Beispiel zeigt eine synchrone Transformationskomponente mit zwei Ausgaben. Diese Transformation durchläuft die **AddressID** Spalte und konvertiert die **City** -Spalte in Großbuchstaben. Wenn der Name der Stadt Redmond ist, wird die Zeile an eine bestimmte Ausgabe weitergeleitet, während alle anderen Zeilen zu einer anderen Ausgabe weitergeleitet werden.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Fügen Sie der Datenfluss-Designeroberfläche eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Transformation.  
  
2.  Verbinden Sie die Ausgabe einer Quelle oder einer anderen Transformation mit der neuen Transformationskomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. Geben Sie diese Ausgabe sollte Daten aus der **Person.Address** Tabelle mit den **AdventureWorks** -Beispieldatenbank, die enthält mindestens die **AddressID** und  **City** Spalten.  
  
3.  Öffnen der **Skript Transformations-Editor**. Auf der **Eingabespalten** Seite der **AddressID** und **City** Spalten. Markierung der **City** Spalte als Lese-/Schreibzugriff.  
  
4.  Auf der **Eingaben und Ausgaben** Seite, erstellen Sie eine zweite Ausgabe. Nachdem Sie die neue Ausgabe hinzugefügt haben, stellen Sie sicher, dass Sie festlegen, seine **SynchronousInputID** auf die **ID** der Eingabe. Diese Eigenschaft ist für die erste Ausgabe bereits festgelegt, die standardmäßig erstellt wird. Legen Sie für jede Ausgabe der **ExclusionGroup** -Eigenschaft auf denselben Wert ungleich 0 (null), um anzugeben, dass Sie die Eingabezeilen auf zwei sich gegenseitig ausschließende Ausgaben verteilt werden. Sie müssen den Ausgaben keine Ausgabezeilen hinzufügen.  
  
5.  Benennen Sie die Eingaben und Ausgaben aussagekräftigere Namen, z. B. **"myaddressinput"**, **MyRedmondAddresses**, und **MyOtherAddresses**.  
  
6.  Auf der **Skript** auf **Bearbeitungsskript** , und geben Sie das folgende Skript. Schließen Sie dann die skriptentwicklungsumgebung und den **Skript Transformations-Editor**.  
  
7.  Erstellen und konfigurieren Sie zwei Zielkomponenten für die die **AddressID** und **City** Spalten, z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ziel, ein Flatfileziel oder die beispielzielkomponente im demonstriert [Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Verbinden Sie daraufhin alle Ausgaben der Transformation mit einer der Zielkomponenten. Sie können Zieltabellen erstellen, durch Ausführen einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Befehl ähnlich dem folgenden (mit eindeutigen Tabellennamen) in der **AdventureWorks** Datenbank:  
  
    ```sql
    CREATE TABLE [Person].[Address2](  
        [AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL  
    ```  
  
8.  Führen Sie das Beispiel aus.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
        If Row.City = "REDMOND" Then  
            Row.DirectRowToMyRedmondAddresses()  
        Else  
            Row.DirectRowToMyOtherAddresses()  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
        if (Row.City == "REDMOND")  
        {  
            Row.DirectRowToMyRedmondAddresses();  
        }  
        else  
        {  
            Row.DirectRowToMyOtherAddresses();  
        }  
  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu synchronen und asynchronen Transformationen] (~/integration-services/understanding-synchronous-and-asynchronous-transformations.md   
 [Erstellen eine asynchrone Transformation mit der Skriptkomponente] (~/integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md   
 [Entwickeln einer benutzerdefinierten Transformationskomponente mit synchronen Ausgaben] (~/integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md  
  
  



