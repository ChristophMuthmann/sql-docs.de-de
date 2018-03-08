---
title: Erstellen einer asynchronen Transformation mit der Skriptkomponente | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7a7d607fda10fa8e3ae020e6b702867e9f8ef0a2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>Erstellen einer asynchronen Transformation mit der Skriptkomponente
  Transformationskomponenten dienen im Datenfluss eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakets dazu, Daten auf dem Weg von der Quelle zum Ziel zu ändern und zu analysieren. Eine Transformation mit synchronen Ausgaben verarbeitet jede eingegebene Zeile, während sie die Komponente durchläuft. Eine Transformation mit asynchronen Ausgaben kann die Fertigstellung ihrer Verarbeitung abwarten, bis die Transformation alle Eingabezeilen empfangen hat. Die Transformation kann bestimmte Zeilen auch ausgeben, bevor sie alle Eingabezeilen empfangen hat. In diesem Thema wird eine asynchrone Transformation erläutert. Wenn die Verarbeitung eine synchrone Transformation erfordert, finden Sie weitere Informationen unter [Creating a Synchronous Transformation with the Script Component (Erstellen einer synchronen Transformation mit der Skriptkomponente)](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md). Weitere Informationen zu den Unterschieden zwischen synchronen und asynchronen Komponenten finden Sie unter [Understanding Synchronous and Asynchronous Transformations (Grundlegendes zu synchronen und asynchronen Transformationen)](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Eine Übersicht der Skriptkomponenten finden Sie unter [Extending the Data Flow with the Script Component (Erweitern des Datenflusses mit der Skriptkomponente)](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 Die Skriptkomponente und der Infrastrukturcode, den sie generiert, erleichtern den Prozess der Entwicklung von benutzerdefinierten Datenflusskomponenten. Zum Verständnis der Funktionsweise dieser Skriptkomponente kann es jedoch hilfreich sein, sich mit den im Abschnitt [Developing a Custom Data Flow Component (Entwickeln einer benutzerdefinierten Datenflusskomponente)](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) beschriebenen Schritten vertraut zu machen, die Sie bei der Entwicklung einer benutzerdefinierten Datenflusskomponente ausführen müssen, und zwar insbesondere mit [Developing a Custom Transformation Component with Synchronous Outputs (Entwickeln einer benutzerdefinierten Transformationskomponente mit synchronen Ausgaben)](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>Erste Schritte mit einer asynchronen Transformationskomponente  
 Wenn Sie auf der Registerkarte „Datenfluss“ des [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designers eine Skriptkomponente hinzufügen, wird das Dialogfeld **Skriptkomponententyp auswählen** geöffnet, in dem Sie zur Vorkonfiguration der Komponente als Quelle, Transformation oder Ziel aufgefordert werden. Wählen Sie in diesem Dialogfeld die Option **Transformation** aus.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>Konfigurieren einer asynchronen Transformationskomponente im Metadatenentwurfsmodus  
 Nachdem Sie die Option zur Erstellung einer Transformationskomponente ausgewählt haben, konfigurieren Sie die Komponente mit dem **Transformations-Editor für Skripterstellung**. Weitere Informationen finden Sie unter [Configuring the Script Component in the Script Component Editor (Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor)](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Legen Sie die **ScriptLanguage**-Eigenschaft auf der Seite **Skript** im Dialogfeld **Transformations-Editor für Skripterstellung** fest, um die Skriptsprache auszuwählen, die die Skriptkomponente verwendet.  
  
> [!NOTE]  
>  Verwenden Sie im Dialogfeld **Optionen** auf der Seite **Allgemein** die Option **Skriptsprache**, um die Standardskriptsprache für die Skriptkomponente festzulegen. Weitere Informationen finden Sie unter [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Eine Datenfluss-Transformationskomponente verfügt über eine Eingabe und unterstützt eine oder mehrere Ausgaben. Die Konfiguration der Eingaben und Ausgaben der Komponente ist einer der Schritte, die Sie mithilfe des **Transformations-Editors für Skripterstellung** im Metadatenentwurfsmodus ausführen müssen, bevor Sie das benutzerdefinierte Skript schreiben.  
  
### <a name="configuring-input-columns"></a>Konfigurieren von Eingabespalten  
 Eine mit der Skriptkomponente erstellte Transformationskomponente verfügt über eine einzelne Eingabe.  
  
 Die Spaltenliste auf der Seite **Eingabespalten** im **Transformations-Editor für Skripterstellung** zeigt die von der Ausgabe der Upstreamkomponente im Datenfluss verfügbaren Spalten. Markieren Sie die Spalten, die Sie transformieren oder durchlaufen möchten. Markieren Sie alle Spalten, die Sie an Ort und Stelle transformieren möchten, als Lesen/Schreiben.  
  
 Weitere Informationen über die Seite **Eingabespalten** im **Transformations-Editor für Skripterstellung** finden Sie unter [Script Transformation Editor (Input Columns Page) (Transformations-Editor für Skripterstellung (Seite „Eingabespalten“))](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Konfigurieren von Eingaben, Ausgaben und Ausgabespalten  
 Eine Transformationskomponente unterstützt eine oder mehrere Ausgaben.  
  
 Häufig hat eine Transformation mit asynchronen Ausgaben zwei Ausgaben. Wenn Sie beispielsweise die Anzahl der Adressen in einer bestimmten Stadt zählen, sollten Sie die Adressdaten an einen Ausgang weitergeben, während Sie das Ergebnis der Aggregation an einen anderen Ausgang senden. Die Aggregationsausgabe erfordert auch eine neue Ausgabespalte.  
  
 Auf der Seite **Eingaben und Ausgaben** im **Transformations-Editor für Skripterstellung** wird Ihnen angezeigt, dass standardmäßig eine Ausgabe, jedoch keine Ausgabespalten erstellt wurden. Auf dieser Seite des Editors können Sie die folgenden Elemente konfigurieren:  
  
-   Sie haben die Möglichkeit, eine oder mehrere zusätzliche Ausgaben zu erstellen, beispielsweise eine Ausgabe für das Ergebnis einer Aggregation. Verwenden Sie die Schaltflächen **Ausgabe hinzufügen** und **Ausgabe entfernen**, um die Ausgaben der asynchronen Transformationskomponente zu verwalten. Legen Sie die **SynchronousInputID**-Eigenschaft jeder Ausgabe auf 0 fest, um anzugeben, dass die Ausgabe nicht nur Daten von einer Upstreamkomponente weitergibt oder diese direkt in den vorhandenen Zeilen und Spalten transformiert. Durch dies Einstellung werden die Ausgaben asynchron zur Eingabe.  
  
-   Sie können der Eingabe und den Ausgaben einen beschreibenden Namen geben. In der Skriptkomponente werden diese Namen verwendet, um die typisierten Accessoreigenschaften zu erzeugen, mit denen Sie auf die Eingabe und Ausgaben in Ihrem Skript verweisen.  
  
-   Häufig werden durch eine asynchrone Transformation dem Datenfluss Spalten hinzugefügt. Wenn die **SynchronousInputID**-Eigenschaft einer Ausgabe 0 beträgt, wird dadurch angegeben, dass die Ausgabe nicht nur Daten von einer Upstreamkomponente weitergibt oder diese direkt in den vorhandenen Zeilen und Spalten transformiert, und Sie müssen in der Ausgabe explizit Ausgabespalten hinzufügen und diese konfigurieren. Ausgabespalten haben nicht dieselben Namen wie die Eingabespalten, denen sie zugeordnet sind.  
  
-   Sie können weitere Spalten hinzufügen, um zusätzliche Informationen aufzunehmen. Sie müssen einen eigenen Code schreiben, um die zusätzlichen Spalten mit Daten aufzufüllen. Weitere Informationen über das Reproduzieren des Verhaltens einer Standardfehlerausgabe finden Sie unter [Simulating an Error Output for the Script Component (Simulieren einer Fehlerausgabe für die Skriptkomponente)](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Weitere Informationen über die Seite **Eingaben und Ausgaben** im **Transformations-Editor für Skripterstellung** finden Sie unter [Script Transformation Editor (Inputs and Outputs Page) (Transformations-Editor für Skripterstellung (Seite „Eingaben und Ausgaben“))](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Hinzufügen von Variablen  
 Wenn Sie die Werte von vorhandenen Variablen in Ihrem Skript verwenden möchten, können Sie diese in den Eigenschaftenfeldern „ReadOnlyVariables“ und „ReadWriteVariables“ auf der Seite **Skript** im **Transformations-Editor für Skripterstellung** hinzufügen.  
  
 Wenn Sie mehrere Variablen in die Eigenschaftsfelder hinzufügen, trennen Sie die Variablennamen durch Kommas. Sie können auch mehrere Variablen auswählen, indem Sie auf die Schaltfläche mit den Auslassungszeichen (**…**) neben den Eigenschaftsfeldern für **ReadOnlyVariables** und **ReadWriteVariables** klicken und dann die Variablen im Dialogfeld **Variablen auswählen** festlegen.  
  
 Allgemeine Informationen über das Verwenden von Variablen mit der Skriptkomponente finden Sie unter [Using Variables in the Script Component (Verwenden von Variablen in der Skriptkomponente)](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Weitere Informationen über die Seite **Skript** im **Transformations-Editor für Skripterstellung** finden Sie unter [Script Transformation Editor (Script Page) (Transformations-Editor für Skripterstellung (Seite „Skript“))](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>Skripterstellung für eine asynchrone Transformationskomponente im Codeentwurfsmodus  
 Nachdem Sie alle Metadaten für Ihre Komponente konfiguriert haben, können Sie das benutzerdefinierte Skript schreiben. Klicken Sie auf der Seite **Skript** im **Transformations-Editor für Skripterstellung** auf **Skript bearbeiten**, um die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications-IDE (VSTA) zu öffnen und Ihr benutzerdefiniertes Skript hinzuzufügen. Welche Skriptsprache Sie verwenden, hängt davon ab, ob Sie auf der Seite **Skript** [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# als Skriptsprache für die **ScriptLanguage**-Eigenschaft festgelegt haben.  
  
 Wichtige Informationen, die alle Arten von Komponenten betreffen, die mithilfe der Skriptkomponente erstellt wurden, finden Sie unter [Coding and Debugging the Script Component (Codieren und Debuggen der Skriptkomponente)](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Grundlegendes zum automatisch generierten Code  
 Wenn Sie nach der Erstellung und Konfiguration einer Transformationskomponente die VSTA-IDE öffnen, wird die bearbeitbare **ScriptMain**-Klasse im Code-Editor mit einem Stub für die Methoden „ProcessInputRow“ und „CreateNewOutputRows“ angezeigt. Sie schreiben Ihren benutzerdefinierten Code in der ScriptMain-Klasse. „ProcessInputRow“ ist die wichtigste Methode in einer Transformationskomponente. Die **CreateNewOutputRows**-Methode wird eher in einer Quellkomponente verwendet, die insofern wie eine asynchrone Transformation funktioniert, dass beide Komponenten eigene Ausgabezeilen erstellen müssen.  
  
 Wenn Sie das Fenster **Projektexplorer** in VSTA öffnen, können Sie sehen, dass die Skriptkomponente auch schreibgeschützte **BufferWrapper**- und **ComponentWrapper**-Projektelemente generiert hat. Die ScriptMain-Klasse erbt von der UserComponent-Klasse im **ComponentWrapper**-Projektelement.  
  
 Zur Laufzeit ruft das Datenflussmodul die PrimeOutput-Methode in der **UserComponent**-Klasse auf, die die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A>-Methode der übergeordneten <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Klasse überschreibt. Die PrimeOutput-Methode ruft wiederum die CreateNewOutputRows-Methode auf.  
  
 Danach ruft das Datenflussmodul die ProcessInput-Methode in der UserComponent-Klasse auf, die die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A>-Methode der übergeordneten <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Klasse überschreibt. Die ProcessInput-Methode durchläuft die Zeilen im Eingabepuffer der Reihe nach und ruft für jede Zeile einmal die ProcessInputRow-Methode auf.  
  
### <a name="writing-your-custom-code"></a>Schreiben von benutzerdefiniertem Code  
 Sie müssen mit der überschriebenen ProcessInputRow-Methode die Daten in jeder Zeile des Eingabepuffers verarbeiten, um die Erstellung einer benutzerdefinierten asynchronen Transformationskomponente abzuschließen. Weil die Ausgaben nicht mit der Eingabe synchron sind, müssen Sie Datenzeilen explizit in die Ausgaben schreiben.  
  
 Bei einer asynchronen Transformation können Sie mit der AddRow-Methode der Ausgabe bei Bedarf Zeilen aus der Methode „ProcessInputRow“ oder „ProcessInput“ heraus hinzufügen. Sie müssen nicht die CreateNewOutputRows-Methode verwenden. Wenn Sie eine einzelne Ergebniszeile, z.B. Aggregationsergebnisse, in eine bestimmte Ausgabe schreiben, können Sie die Ausgabezeile vorher mithilfe der CreateNewOutputRows-Methode erstellen und ihre Werte später nach Verarbeitung aller Eingabezeilen auffüllen. Es ist jedoch nicht sinnvoll, in der CreateNewOutputRows-Methode mehrere Zeilen zu erstellen, weil mit der Skriptkomponente nur die aktuelle Zeile in einer Eingabe oder Ausgabe verwendet werden kann. Die CreateNewOutputRows-Methode ist bei einer Quellkomponente wichtiger, bei der keine Eingabezeilen zu verarbeiten sind.  
  
 Sie können auch die ProcessInput-Methode überschreiben, damit Sie zusätzliche vorbereitende oder abschließende Verarbeitungsvorgänge ausführen können, bevor oder nachdem Sie den Eingabepuffer durchlaufen und ProcessInputRow für jede Zeile aufrufen. Eines der Codebeispiele in diesem Artikel überschreibt beispielsweise ProcessInput, um die Anzahl von Adressen in einer bestimmten Stadt zu zählen, während ProcessInputRow die Zeilen durchläuft. Im Beispiel wird der Zusammenfassungswert in die zweite Ausgabe geschrieben, nachdem alle Zeilen verarbeitet wurden. In diesem Beispiel wird die Ausgabe in ProcessInput abgeschlossen, weil die Ausgabepuffer nicht mehr verfügbar sind, wenn PostExecute aufgerufen wird.  
  
 Je nach Anforderung können Sie auch Skript in den Methoden „PreExecute“ und „PostExecute“ schreiben, die in der ScriptMain-Klasse verfügbar sind, um vorbereitende oder abschließende Verarbeitungsvorgänge auszuführen.  
  
> [!NOTE]  
>  Wenn Sie eine benutzerdefinierte Datenflusskomponente von Grund auf erstellen, ist es wichtig, die PrimeOutput-Methode zu überschreiben, um Verweise auf die Ausgabepuffer zwischenzuspeichern, damit Sie den Puffern später Datenzeilen hinzufügen können. Dies ist in der Skriptkomponente nicht erforderlich, da dort eine automatisch generierte Klasse vorliegt, die jeden Ausgabepuffer im **BufferWrapper**-Projektelement darstellt.  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird der benutzerdefinierte Code veranschaulicht, der in der ScriptMain-Klasse zur Erstellung einer asynchronen Transformationskomponente erforderlich ist.  
  
> [!NOTE]  
>  In diesen Beispielen werden die erste und die vierte Spalte der Tabelle **Person.Address** in der Beispieldatenbank **AdventureWorks** verwendet, und die Spalten **intAddressID** und **nvarchar(30)City** werden durch den Datenfluss weitergeleitet. Die gleichen Daten werden in den Quellen-, Transformations- und Zielbeispielen in diesem Abschnitt verwendet. Zusätzliche Voraussetzungen und Annahmen werden für jedes Beispiel dokumentiert.  
  
 Dieses Beispiel zeigt eine asynchrone Transformationskomponente mit zwei Ausgaben. Bei dieser Transformation werden die Spalten **AddressID** und **City** an eine Ausgabe übergeben. Gleichzeitig wird die Anzahl von Adressen in einer bestimmten Stadt (Redmond, Washington, USA) gezählt, und der resultierende Wert wird an einer zweite Ausgabe ausgegeben.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Fügen Sie der Datenfluss-Designeroberfläche eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Transformation.  
  
2.  Verbinden Sie die Ausgabe einer Quelle einer anderen Transformation mit der neuen Transformation im Designer. Diese Ausgabe sollte Daten aus der Tabelle **Person.Address** der Beispieldatenbank **AdventureWorks** bereitstellen, die mindestens die Spalten **AddressID** und **City** enthält.  
  
3.  Öffnen Sie den **Transformations-Editor für Skripterstellung**. Wählen Sie auf der Seite **Eingabespalten** die Spalten **AddressID** und **City** aus.  
  
4.  Fügen Sie auf der Seite **Eingaben und Ausgaben** die Ausgabespalten **AddressID** und **City** hinzu, und konfigurieren Sie sie auf der ersten Ausgabe. Fügen Sie eine zweite Ausgabe hinzu, und fügen Sie eine Ausgabespalte für den Zusammenfassungswert in der zweiten Ausgabe hinzu. Setzen Sie die SynchronousInputID-Eigenschaft der ersten Ausgabe auf 0, weil in diesem Beispiel jede Eingabezeile explizit in die erste Ausgabe kopiert wird. Die SynchronousInputID-Eigenschaft der neu erstellten Ausgabe ist bereits auf 0 gesetzt.  
  
5.  Benennen Sie die Eingabe, die Ausgaben und die neue Ausgabespalte um, um ihnen beschreibendere Namen zu geben. Im Beispiel wird **MyAddressInput** als Name der Eingabe, **MyAddressOutput** und **MySummaryOutput** für die Ausgaben und **MyRedmondCount** für die Ausgabespalte in der zweiten Ausgabe verwendet.  
  
6.  Klicken Sie auf der Seite **Skript** auf **Skript bearbeiten**, und geben Sie das folgende Skript ein. Schließen Sie anschließend die Skriptentwicklungsumgebung und den **Transformations-Editor für Skripterstellung**.  
  
7.  Erstellen und konfigurieren Sie eine Zielkomponente für die erste Ausgabe, die die Spalten **AddressID** und **City** erwartet, z.B. ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ziel, oder die Beispielzielkomponente, die unter [Creating a Destination with the Script Component (Erstellen eines Ziels mit der Skriptkomponente)](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md) veranschaulicht wird. Verbinden Sie anschließend die erste Ausgabe der Transformation, **MyAddressOutput**, mit der Zielkomponente. Sie können eine Zieltabelle erstellen, indem Sie den folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Befehl in der **AdventureWorks**-Datenbank ausführen:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Erstellen Sie eine weitere Zielkomponente für die zweite Ausgabe, und konfigurieren Sie sie. Verbinden Sie dann die zweite Ausgabe der Transformation, **MySummaryOutput**, mit der Zielkomponente. Da in der zweiten Ausgabe eine einzelne Zeile mit nur einem Wert geschrieben wird, können Sie mit einem Verbindungs-Manager für Flatfiles, der eine Verbindung zu einer neuen Datei mit einer Spalte herstellt, einfach ein Ziel konfigurieren. Im Beispiel wird diese Zielspalte **MyRedmondCount** genannt.  
  
9. Führen Sie das Beispiel aus.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Private myRedmondAddressCount As Integer  
  
    Public Overrides Sub CreateNewOutputRows()  
  
        MySummaryOutputBuffer.AddRow()  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInput(ByVal Buffer As MyAddressInputBuffer)  
  
        While Buffer.NextRow()  
            MyAddressInput_ProcessInputRow(Buffer)  
        End While  
  
        If Buffer.EndOfRowset Then  
            MyAddressOutputBuffer.SetEndOfRowset()  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount  
            MySummaryOutputBuffer.SetEndOfRowset()  
        End If  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With MyAddressOutputBuffer  
            .AddRow()  
            .AddressID = Row.AddressID  
            .City = Row.City  
        End With  
  
        If Row.City.ToUpper = "REDMOND" Then  
            myRedmondAddressCount += 1  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    private int myRedmondAddressCount;  
  
    public override void CreateNewOutputRows()  
    {  
  
        MySummaryOutputBuffer.AddRow();  
  
    }  
  
    public override void MyAddressInput_ProcessInput(MyAddressInputBuffer Buffer)  
    {  
  
        while (Buffer.NextRow())  
        {  
            MyAddressInput_ProcessInputRow(Buffer);  
        }  
  
        if (Buffer.EndOfRowset())  
        {  
            MyAddressOutputBuffer.SetEndOfRowset();  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount;  
            MySummaryOutputBuffer.SetEndOfRowset();  
        }  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            MyAddressOutputBuffer.AddRow();  
            MyAddressOutputBuffer.AddressID = Row.AddressID;  
            MyAddressOutputBuffer.City = Row.City;  
        }  
  
        if (Row.City.ToUpper() == "REDMOND")  
        {  
            myRedmondAddressCount += 1;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Grundlegendes zu synchronen und asynchronen Transformationen](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Entwickeln einer benutzerdefinierten Transformationskomponente mit asynchronen Ausgaben](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
