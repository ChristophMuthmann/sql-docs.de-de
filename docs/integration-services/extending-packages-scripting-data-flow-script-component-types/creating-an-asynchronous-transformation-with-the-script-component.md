---
title: Erstellen einer asynchronen Transformation mit der Skriptkomponente | Microsoft Docs
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
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4da61e00337430a3eaef84e40f9f732a572cc45b
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>Erstellen einer asynchronen Transformation mit der Skriptkomponente
  Transformationskomponenten dienen im Datenfluss eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakets dazu, Daten auf dem Weg von der Quelle zum Ziel zu ändern und zu analysieren. Eine Transformation mit synchronen Ausgaben verarbeitet jede eingegebene Zeile, während sie die Komponente durchläuft. Eine Transformation mit asynchronen Ausgaben möglicherweise warten, bis die Fertigstellung ihrer Verarbeitung, bis die Transformation alle Eingabezeilen empfangen hat, oder die Transformation kann bestimmte Zeilen ausgeben, bevor sie alle Eingabezeilen empfangen hat. In diesem Thema wird eine asynchrone Transformation erläutert. Wenn die Verarbeitung eine synchrone Transformation erfordert, finden Sie unter [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md). Weitere Informationen zu den Unterschieden zwischen synchronen und asynchronen Komponenten finden Sie unter [Grundlegendes zu synchronen und asynchronen Transformationen](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Einen Überblick über die Skriptkomponente finden Sie unter [Extending the Data Flow mit der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 Die Skriptkomponente und der Infrastrukturcode, den sie generiert, erleichtern den Prozess der Entwicklung von benutzerdefinierten Datenflusskomponenten. Um die Funktionsweise der Skriptkomponente zu verstehen, Sie können es jedoch hilfreich, durch die Schritte zu lesen, die Sie befolgen müssen, bei der Entwicklung einer benutzerdefinierten Datenflusskomponente in der [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) Abschnitt, und insbesondere [Entwickeln einer benutzerdefinierten Transformationskomponente mit synchronen Ausgaben](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>Erste Schritte mit einer asynchronen Transformationskomponente  
 Wenn Sie eine Skriptkomponente hinzufügen, auf der Registerkarte Datenfluss des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer die **Skriptkomponententyp** Dialogfeld werden Sie aufgefordert, die Komponente als Quelle, Transformation oder Ziel vorzukonfigurieren. Wählen Sie in diesem Dialogfeld **Transformation**.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>Konfigurieren einer asynchronen Transformationskomponente im Metadatenentwurfsmodus  
 Nachdem Sie die Option zum Erstellen einer Transformationskomponente ausgewählt haben, konfigurieren Sie die Komponente mit der **Skript Transformations-Editor**. Weitere Informationen finden Sie unter [Configuring the Script Component in the Script Component Editor](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Um die Skriptsprache auszuwählen, die die Skriptkomponente verwenden, legen Sie die **ScriptLanguage** Eigenschaft auf die **Skript** auf der Seite der **Skript Transformations-Editor** Dialogfeld Box.  
  
> [!NOTE]  
>  Um die Standardskriptsprache für die Skriptkomponente festzulegen, verwenden die **Skriptsprache** auf die option der **allgemeine** auf der Seite der **Optionen** (Dialogfeld). Weitere Informationen finden Sie unter [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Eine Datenfluss-Transformationskomponente verfügt über eine Eingabe und unterstützt eine oder mehrere Ausgaben. Konfiguration der Eingaben und Ausgaben der Komponente ist einer der Schritte, die Sie im metadatenentwurfsmodus, mithilfe abschließen müssen der **Skript Transformations-Editor**, bevor Sie das benutzerdefinierte Skript schreiben.  
  
### <a name="configuring-input-columns"></a>Konfigurieren von Eingabespalten  
 Eine mit der Skriptkomponente erstellte Transformationskomponente verfügt über eine einzelne Eingabe.  
  
 Auf der **Eingabespalten** auf der Seite der **Skript Transformations-Editor**, die Spaltenliste zeigt die verfügbaren Spalten aus der Ausgabe der upstreamkomponente im Datenfluss. Markieren Sie die Spalten, die Sie transformieren oder durchlaufen möchten. Markieren Sie alle Spalten, die Sie an Ort und Stelle transformieren möchten, als Lesen/Schreiben.  
  
 Weitere Informationen zu den **Eingabespalten** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Seite "Spalten" Eingabe &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Konfigurieren von Eingaben, Ausgaben und Ausgabespalten  
 Eine Transformationskomponente unterstützt eine oder mehrere Ausgaben.  
  
 Häufig hat eine Transformation mit asynchronen Ausgaben zwei Ausgaben. Wenn Sie beispielsweise die Anzahl der Adressen in einer bestimmten Stadt zählen, sollten Sie die Adressdaten an einen Ausgang weitergeben, während Sie das Ergebnis der Aggregation an einen anderen Ausgang senden. Die Aggregationsausgabe erfordert auch eine neue Ausgabespalte.  
  
 Auf der **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor**, sehen Sie, dass eine einzelne Ausgabe standardmäßig erstellt wurde, aber es wurden keine Ausgabespalten erstellt. Auf dieser Seite des Editors können Sie die folgenden Elemente konfigurieren:  
  
-   Sie haben die Möglichkeit, eine oder mehrere zusätzliche Ausgaben zu erstellen, beispielsweise eine Ausgabe für das Ergebnis einer Aggregation. Verwenden der **Ausgabe hinzufügen** und **Ausgabe entfernen** Schaltflächen, um die Ausgaben der asynchronen Transformationskomponente zu verwalten. Legen Sie die **SynchronousInputID** -Eigenschaft jeder Ausgabe auf 0 (null), um anzugeben, dass die Ausgabe nicht nur einfach Daten von einer upstreamkomponente weitergibt oder sie direkt in den vorhandenen Zeilen und Spalten transformiert. Durch dies Einstellung werden die Ausgaben asynchron zur Eingabe.  
  
-   Sie können der Eingabe und den Ausgaben einen beschreibenden Namen geben. In der Skriptkomponente werden diese Namen verwendet, um die typisierten Accessoreigenschaften zu erzeugen, mit denen Sie auf die Eingabe und Ausgaben in Ihrem Skript verweisen.  
  
-   Häufig werden durch eine asynchrone Transformation dem Datenfluss Spalten hinzugefügt. Wenn die **SynchronousInputID** -Eigenschaft einer Ausgabe 0 (null) ist, gibt an, dass die Ausgabe nicht einfach Daten von einer upstreamkomponente weitergibt oder sie direkt in den vorhandenen Zeilen und Spalten transformiert werden, müssen Sie hinzufügen und konfigurieren Ausgabespalten explizit in der Ausgabe. Ausgabespalten haben nicht dieselben Namen wie die Eingabespalten, denen sie zugeordnet sind.  
  
-   Sie können weitere Spalten hinzufügen, um zusätzliche Informationen aufzunehmen. Sie müssen einen eigenen Code schreiben, um die zusätzlichen Spalten mit Daten aufzufüllen. Informationen zum Reproduzieren des Verhaltens einer Standardfehlerausgabe finden Sie unter [simulieren einer Fehlerausgabe für die Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Weitere Informationen zu den **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Eingaben und Ausgaben Seite &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Hinzufügen von Variablen  
 Treten vorhandenen Variablen, deren Werte, die Sie in Ihrem Skript verwenden möchten, können Sie sie in den Eigenschaftenfeldern ReadOnlyVariables und ReadWriteVariables hinzufügen, auf die **Skript** auf der Seite der **Skript Transformations-Editor** .  
  
 Wenn Sie mehrere Variablen in die Eigenschaftsfelder hinzufügen, trennen Sie die Variablennamen durch Kommas. Sie können auch mehrere Variablen auswählen, indem Sie auf die Auslassungspunkte (**...** ) neben dem **ReadOnlyVariables** und **ReadWriteVariables** Eigenschaftenfelder, und wählen Sie dann die Variablen in der **Variablen auswählen** Das Dialogfeld.  
  
 Allgemeine Informationen zur Verwendung von Variablen mit der Skriptkomponente finden Sie unter [Using Variables in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Weitere Informationen zu den **Skript** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Seite "Skript" &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>Skripterstellung für eine asynchrone Transformationskomponente im Codeentwurfsmodus  
 Nachdem Sie alle Metadaten für Ihre Komponente konfiguriert haben, können Sie das benutzerdefinierte Skript schreiben. In der **Skript Transformations-Editor**auf die **Skript** auf **Bearbeitungsskript** So öffnen die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE in dem Sie das benutzerdefinierte Skript hinzufügen können. Die verwendete Skriptsprache, die Sie verwenden, hängt davon ab, ob Sie ausgewählt [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual c# als Skriptsprache für die **ScriptLanguage** Eigenschaft auf die **Skript** Seite ".  
  
 Wichtige Informationen, die für alle Arten von Komponenten, die mithilfe der Skriptkomponente erstellt gilt, finden Sie unter [codieren und Debuggen der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Grundlegendes zum automatisch generierten Code  
 Wenn Sie die VSTA IDE öffnen, nach dem Erstellen und die Konfiguration einer Transformationskomponente die bearbeitbare **ScriptMain** Klasse wird im Codeeditor mit Stubs für die ProcessInputRow und die CreateNewOutputRows Methoden angezeigt. Die ScriptMain-Klasse ist, in dem Sie Ihren benutzerdefinierten Code schreiben und ProcessInputRow ist die wichtigste Methode in einer Transformationskomponente. Die **CreateNewOutputRows** -Methode werden in der Regel in einer Quellkomponente, die wie eine asynchrone Transformation ist insofern, dass beide Komponenten eigene Ausgabezeilen erstellen müssen.  
  
 Wenn Sie VSTA öffnen **Projektexplorer** Fenster können Sie sehen, dass die Skriptkomponente auch schreibgeschützte generiert hat **BufferWrapper** und **ComponentWrapper** Projektelemente . Die ScriptMain-Klasse erbt von der Klasse UserComponent in der **ComponentWrapper** -Projektelement.  
  
 Zur Laufzeit ruft das Datenflussmodul die PrimeOutput-Methode in der **UserComponent** Klasse, welche Außerkraftsetzungen der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> übergeordnete Klasse. Die PrimeOutput-Methode ruft wiederum die CreateNewOutputRows-Methode.  
  
 Als Nächstes ruft das Datenflussmodul die ProcessInput-Methode in der UserComponent-Klasse, die außer Kraft setzt die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> übergeordnete Klasse. Die ProcessInput-Methode wird wiederum durchläuft die Zeilen im Eingabepuffer und ruft die ProcessInputRow-Methode einmal für jede Zeile.  
  
### <a name="writing-your-custom-code"></a>Schreiben von benutzerdefiniertem Code  
 Zur Erstellung einer benutzerdefinierten asynchronen Transformationskomponente abzuschließen, müssen Sie die überschriebene ProcessInputRow-Methode verwenden, um die Daten in jeder Zeile des Eingabepuffers verarbeiten. Weil die Ausgaben nicht mit der Eingabe synchron sind, müssen Sie Datenzeilen explizit in die Ausgaben schreiben.  
  
 Bei einer asynchronen Transformation können Sie die AddRow-Methode zum Hinzufügen von Zeilen an die Ausgabe nach Bedarf aus, in die ProcessInputRow oder ProcessInput-Methode. Sie müssen nicht die CreateNewOutputRows-Methode verwenden. Wenn Sie eine einzelne Zeile der Ergebnisse, wie zum Beispiel aggregationsergebnisse, in eine bestimmte Ausgabe schreiben, können Sie die Ausgabezeile vorher mithilfe der Methode CreateNewOutputRows erstellen und füllen Sie seine Werte später nach Verarbeitung aller Eingabezeilen. Es ist jedoch nicht sinnvoll sein, mehrere Zeilen in der Methode CreateNewOutputRows erstellen, da die Skriptkomponente nur die aktuelle Zeile in eine Eingabe oder Ausgabe verwenden kann. Die Methode CreateNewOutputRows ist wichtiger bei einer Quellkomponente, an dem es keine Eingabezeilen sind zu verarbeiten.  
  
 Sie können auch die ProcessInput-Methode selbst überschreiben möchten, damit Sie zusätzliche vorbereitende oder abschließende Verarbeitungsvorgänge vor oder nach dem Sie den Eingabepuffer durchlaufen und Aufrufen von ProcessInputRow für jede Zeile ausführen können. Eines der Codebeispiele in diesem Thema überschreibt z. B. ProcessInput, um die Anzahl der Adressen in einer bestimmten Stadt als ProcessInputRow durchläuft Zeilen zählen**.** Das Beispiel schreibt den Zusammenfassungswert in die zweite Ausgabe, nachdem alle Zeilen verarbeitet wurden. Im Beispiel wird die Ausgabe ProcessInput abgeschlossen, weil die Ausgabepuffer nicht mehr verfügbar sind, wenn "PostExecute" aufgerufen wird.  
  
 Je nach Ihren Anforderungen können Sie auch Skript in ' PreExecute ' und ' PostExecute ' Methoden in der ScriptMain-Klasse, um vorbereitende oder abschließende Verarbeitungsvorgänge ausführen schreiben möchten.  
  
> [!NOTE]  
>  Wenn Sie eine benutzerdefinierte Datenflusskomponente von Grund auf neu entwickeln wurden, würde es wichtig sein, die PrimeOutput-Methode, um Verweise auf die Ausgabepuffer zwischenzuspeichern außer Kraft setzen, damit Sie Zeilen mit Daten später den Puffern hinzufügen konnte. In der Skriptkomponente, dies ist nicht erforderlich, da Sie eine automatisch generierte Klasse jeden Ausgabepuffer im haben die **BufferWrapper** -Projektelement.  
  
## <a name="example"></a>Beispiel  
 Dieses Beispiel zeigt die benutzerdefinierten Code, der in der ScriptMain-Klasse zum Erstellen einer asynchronen Transformationskomponente erforderlich ist.  
  
> [!NOTE]  
>  Diese Beispiele verwenden die **Person.Address** -Tabelle in der **AdventureWorks** Beispieldatenbank aus, und übergeben Sie die erste und die vierte Spalte, die **IntAddressID** und  **Nvarchar (30) City** Spalten, durch den Datenfluss. Die gleichen Daten werden in den Quellen-, Transformations- und Zielbeispielen in diesem Abschnitt verwendet. Zusätzliche Voraussetzungen und Annahmen werden für jedes Beispiel dokumentiert.  
  
 Dieses Beispiel zeigt eine asynchrone Transformationskomponente mit zwei Ausgaben. Diese Transformation durchläuft die **AddressID** und **City** Spalten, die eine Ausgabe, während die Anzahl der Adressen in einer bestimmten Stadt (Redmond, Washington, USA) gezählt, und klicken Sie dann Ausgaben der der Ergebniswert an eine zweite Ausgabe.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Fügen Sie der Datenfluss-Designeroberfläche eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Transformation.  
  
2.  Verbinden Sie die Ausgabe einer Quelle einer anderen Transformation mit der neuen Transformation im Designer. Geben Sie diese Ausgabe sollte Daten aus der **Person.Address** Tabelle mit den **AdventureWorks** -Beispieldatenbank, die enthält mindestens die **AddressID** und  **City** Spalten.  
  
3.  Öffnen der **Skript Transformations-Editor**. Auf der **Eingabespalten** Seite der **AddressID** und **City** Spalten.  
  
4.  Auf der **Eingaben und Ausgaben** , hinzufügen und Konfigurieren der **AddressID** und **City** Ausgabespalten auf die erste Ausgabe. Fügen Sie eine zweite Ausgabe hinzu, und fügen Sie eine Ausgabespalte für den Zusammenfassungswert in der zweiten Ausgabe hinzu. Setzen Sie die SynchronousInputID-Eigenschaft der ersten Ausgabe auf 0, weil in diesem Beispiel jede Eingabezeile explizit in die erste Ausgabe kopiert wird. Die SynchronousInputID-Eigenschaft der neu erstellten Ausgabe ist bereits auf 0 gesetzt.  
  
5.  Benennen Sie die Eingabe, die Ausgaben und die neue Ausgabespalte um, um ihnen beschreibendere Namen zu geben. Im Beispiel wird **"myaddressinput"** als Namen für die Eingabe und **"myaddressoutput"** und **Meinezusammenfassungsausgabe** für die Ausgaben und **meineredmond-Anzahl** für die Ausgabespalte in der zweiten Ausgabe.  
  
6.  Auf der **Skript** auf **Bearbeitungsskript** , und geben Sie das folgende Skript. Schließen Sie dann die skriptentwicklungsumgebung und den **Skript Transformations-Editor**.  
  
7.  Erstellen und konfigurieren Sie eine Zielkomponente für die erste Ausgabe, der erwartet, dass die **AddressID** und **City** Spalten, z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ziel oder die beispielzielkomponente im demonstriert [Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md),. Verbinden Sie dann die erste Ausgabe der Transformation, **"myaddressoutput"**, mit der Zielkomponente. Sie können eine Zieltabelle erstellen, durch Ausführen des folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl in der **AdventureWorks** Datenbank:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Erstellen Sie eine weitere Zielkomponente für die zweite Ausgabe, und konfigurieren Sie sie. Verbinden Sie dann die zweite Ausgabe der Transformation, **Meinezusammenfassungsausgabe**, mit der Zielkomponente. Da in der zweiten Ausgabe eine einzelne Zeile mit nur einem Wert geschrieben wird, können Sie mit einem Verbindungs-Manager für Flatfiles, der eine Verbindung zu einer neuen Datei mit einer Spalte herstellt, einfach ein Ziel konfigurieren. Im Beispiel wird diese Zielspalte namens **meineredmond-Anzahl**.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu synchronen und asynchronen Transformationen](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Entwickeln einer benutzerdefinierten Transformationskomponente mit asynchronen Ausgaben](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  

