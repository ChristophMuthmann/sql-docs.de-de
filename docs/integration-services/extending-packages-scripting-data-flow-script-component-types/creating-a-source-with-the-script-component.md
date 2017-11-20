---
title: Erstellen einer Datenquelle mit der Skriptkomponente | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4944c3d5752da21fed90f16a38a33b4fad41515
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-source-with-the-script-component"></a>Erstellen einer Quelle mit der Skriptkomponente
  Quellkomponenten dienen im Datenfluss eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakets dazu, Daten aus einer Datenquelle zu laden, um sie an Downstreamtransformationen und -ziele zu übergeben. Gewöhnlich stellen Sie über einen vorhandenen Verbindungs-Manager eine Verbindung mit der Datenquelle her.  
  
 Einen Überblick über die Skriptkomponente finden Sie unter [Extending the Data Flow mit der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 Die Skriptkomponente und der Infrastrukturcode, den sie generieren, erleichtern Ihnen die Entwicklung benutzerdefinierter Datenflusskomponenten deutlich. Um die Funktionsweise der Skriptkomponente zu verstehen, kann es jedoch hilfreich sein, sich mit den Schritten, die bei der Entwicklung einer benutzerdefinierten Datenflusskomponente durchlaufen werden, vertraut zu machen. Finden Sie im Abschnitt [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), insbesondere im Thema [Entwickeln einer benutzerdefinierten Quellkomponente](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md).  
  
## <a name="getting-started-with-a-source-component"></a>Erste Schritte mit einer Quellkomponente  
 Wenn Sie eine Skriptkomponente hinzufügen, um im Bereich Datenfluss des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer die **Skriptkomponententyp** Dialogfeld wird geöffnet und fordert Sie zum Auswählen einer Quelle, Ziel oder Transformation Skript. Wählen Sie in diesem Dialogfeld **Quelle**.  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>Konfigurieren einer Quellkomponente im Metadatenentwurfsmodus  
 Nach der Auswahl eine Quellkomponente zu erstellen, konfigurieren Sie die Komponente, mit der **Skript Transformations-Editor**. Weitere Informationen finden Sie unter [Configuring the Script Component in the Script Component Editor](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Eine Datenflussquellkomponente verfügt über keine Eingaben und unterstützt eine oder mehrere Ausgaben. Konfiguration der Ausgaben für die Komponente einer der Schritte, die Sie im metadatenentwurfsmodus müssen ist, mithilfe Abschließen der **Skript Transformations-Editor**, bevor Sie das benutzerdefinierte Skript schreiben.  
  
 Sie können auch die Skriptsprache angeben, durch Festlegen der **ScriptLanguage** Eigenschaft auf die **Skript** auf der Seite der **Skript Transformations-Editor**.  
  
> [!NOTE]  
>  Um die Standardskriptsprache für Skriptkomponenten und Skripttasks festzulegen, verwenden die **Skriptsprache** auf die option der **allgemeine** auf der Seite der **Optionen** (Dialogfeld). Weitere Informationen finden Sie unter [General Page](~/integration-services/control-flow/script-task-editor-general-page.md).  
  
### <a name="adding-connection-managers"></a>Hinzufügen von Verbindungs-Managern  
 Eine Quellkomponente verwendet normalerweise einen vorhandenen Verbindungs-Manager zum Herstellen einer Verbindung mit der Datenquelle, aus der Daten in den Datenfluss geladen werden. Auf der **Verbindungs-Manager** auf der Seite der **Skript Transformations-Editor**, klicken Sie auf **hinzufügen** geeigneten Verbindungs-Manager hinzufügen.  
  
 Ein Verbindungs-Manager ist jedoch nur eine praktische Einheit, die Daten kapselt und speichert, die sie benötigt, um eine Verbindung mit einer bestimmten Art von Datenquelle herzustellen. Sie müssen, um Daten zu laden und zu speichern sowie möglicherweise auch um eine Verbindung mit der Datenquelle herzustellen und diese zu beenden, eigenen benutzerdefinierten Code schreiben.  
  
 Allgemeine Informationen zur Verwendung von Verbindungs-Manager mit der Skriptkomponente finden Sie unter [Connecting to Data Sources in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Weitere Informationen zu den **Verbindungs-Manager** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Verbindungsseite-Manager &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-outputs-and-output-columns"></a>Konfigurieren von Ausgaben und Ausgabespalten  
 Eine Quellkomponente verfügt über keine Eingaben und unterstützt eine oder mehrere Ausgaben. Auf der **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor**, eine einzelne Ausgabe standardmäßig erstellt wurde, aber es wurden keine Ausgabespalten erstellt. Auf dieser Seite des Editors haben Sie die Möglichkeit, die folgenden Elemente zu konfigurieren.  
  
-   Sie müssen Ausgabespalten für jede Ausgabe manuell hinzufügen und konfigurieren. Wählen Sie den ausgabespaltenordner für jede Ausgabe, und klicken Sie dann mithilfe der **Add Column** und **Spalte entfernen** Schaltflächen, um die Ausgabespalten für jede Ausgabe der Quellkomponente zu verwalten. Die Namen, die Sie den Ausgabespalten hier zuweisen, verwenden Sie später mithilfe der typisierten Accessoreigenschaften, die im automatisch generierten Code erstellt wurden, für Verweise im Skript.  
  
-   Sie haben die Möglichkeit, eine oder mehrere zusätzliche Ausgaben zu erstellen, beispielsweise eine simulierte Fehlerausgabe für Zeilen, die unerwartete Werte aufweisen. Verwenden der **Ausgabe hinzufügen** und **Ausgabe entfernen** Schaltflächen, um die Ausgaben der Quellkomponente zu verwalten. Alle Eingabezeilen werden an alle verfügbaren Ausgaben weitergeleitet, es sei denn, Sie auch einen identischen Wert ungleich NULL für angeben der **ExclusionGroup** -Eigenschaft der Ausgaben für jede Zeile nur eine der Ausgaben weiterleiten, die denselben, möchten **ExclusionGroup** Wert. Der spezifische ganzzahlige Wert ausgewählt werden, zum Identifizieren der **ExclusionGroup** spielt keine Rolle.  
  
    > [!NOTE]  
    >  Sie können auch eine Wert ungleich NULL **ExclusionGroup** Eigenschaftswert für eine einzelne Ausgabe, wenn Sie nicht alle Zeilen ausgeben möchten. In diesem Fall jedoch müssen Sie explizit aufrufen der **DirectRowTo\<Outputbuffer >** Methode für jede Zeile, die an die Ausgabe gesendet werden soll.  
  
-   Sie können allen Ausgaben einen Anzeigenamen zuweisen. Sie verwenden die Namen der Ausgaben in Ihrem Skript später für Verweise mithilfe der typisierten Accessoreigenschaften, die im automatisch generierten Code erstellt wurden.  
  
-   Üblicherweise haben mehrere Ausgaben in der gleichen **ExclusionGroup** haben die gleichen Ausgabespalten. Falls Sie eine simulierte Fehlerausgabe erstellen, sollten Sie jedoch mehrere Spalten hinzufügen, um Fehlerinformationen zu speichern. Informationen wie das Datenflussmodul Fehlerzeilen verarbeitet, finden Sie unter [mithilfe von Fehlerausgaben in einer Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md). In der Skriptkomponente müssen Sie hingegen eigenen Code schreiben, um geeignete Fehlerinformationen für die zusätzlichen Spalten zu erhalten. Weitere Informationen finden Sie unter [simulieren einer Fehlerausgabe für die Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Weitere Informationen zu den **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Eingaben und Ausgaben Seite &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Hinzufügen von Variablen  
 Treten vorhandenen Variablen, deren Werte, die Sie in Ihrem Skript verwenden möchten, können Sie diese im Hinzufügen der **ReadOnlyVariables** und **ReadWriteVariables** Eigenschaftsfeldern für die **Skript** auf der Seite der **Skript Transformations-Editor**.  
  
 Wenn Sie mehrere Variablen in die Eigenschaftenfelder eingeben, trennen Sie die Variablennamen durch Kommas. Sie können auch mehrere Variablen eingeben, indem Sie auf die Auslassungspunkte (**...** ) neben dem **ReadOnlyVariables** und **ReadWriteVariables** Eigenschaftenfelder und Auswählen von Variablen in der **Variablen auswählen** (Dialogfeld) .  
  
 Allgemeine Informationen zur Verwendung von Variablen mit der Skriptkomponente finden Sie unter [Using Variables in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Weitere Informationen zu den **Skript** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Seite "Skript" &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>Schreiben einer Quellkomponente im Codeentwurfsmodus  
 Nachdem Sie die Metadaten für Ihre Komponente konfiguriert haben, öffnen Sie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE, das benutzerdefinierte Skript zu codieren. Um VSTA zu öffnen, klicken Sie auf **Bearbeitungsskript** auf die **Skript** auf der Seite der **Skript Transformations-Editor**. Sie können das Skript schreiben, indem Sie entweder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#-, abhängig von der Skriptsprache für ausgewählte der **ScriptLanguage** Eigenschaft.  
  
 Wichtige Informationen, die für alle Arten von Komponenten, die mithilfe der Skriptkomponente erstellt gilt, finden Sie unter [codieren und Debuggen der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Grundlegendes zum automatisch generierten Code  
 Wenn Sie die VSTA IDE öffnen, nach dem Erstellen und Konfigurieren einer Quellkomponente die bearbeitbare **ScriptMain** Klasse wird im Code-Editor angezeigt. Sie Ihren benutzerdefinierten Code schreiben, der **ScriptMain** Klasse.  
  
 Die **ScriptMain** -Klasse schließt einen Stub für die **CreateNewOutputRows** Methode. Die **CreateNewOutputRows** ist die wichtigste Methode in einer Quellkomponente.  
  
 Wenn Sie öffnen die **Projektexplorer** Fenster in VSTA können Sie sehen, dass die Skriptkomponente auch schreibgeschützte generiert hat **BufferWrapper** und **ComponentWrapper** Projekt Elemente. Die **ScriptMain** Klasse erbt von **UserComponent** -Klasse in der **ComponentWrapper** -Projektelement.  
  
 Zur Laufzeit ruft das Datenflussmodul die **PrimeOutput** Methode in der **UserComponent** Klasse, welche Außerkraftsetzungen der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> übergeordnete Klasse. Die **PrimeOutput** -Methode ruft ihrerseits die folgenden Methoden:  
  
1.  Die **CreateNewOutputRows** -Methode, die Sie in überschreiben **ScriptMain** zum Hinzufügen von Zeilen aus der Datenquelle an die Ausgabe Puffern, deren zunächst leer.  
  
2.  Die **FinishOutputs** Methode, die standardmäßig leer ist. Überschreiben Sie diese Methode in **ScriptMain** um Verarbeitungsschritte auszuführen, die zum Abschluss der Ausgabe erforderlich sind.  
  
3.  Die Private **MarkOutputsAsFinished** aufruft der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> übergeordnete Klasse, um das Datenflussmodul mitzuteilen, dass die Ausgabe abgeschlossen ist. Sie müssen keine Aufrufen **SetEndOfRowset** explizit in Ihrem eigenen Code.  
  
### <a name="writing-your-custom-code"></a>Schreiben von benutzerdefiniertem Code  
 Zum Erstellen einer benutzerdefinierten Quellkomponente fertig sind, möchten Sie möglicherweise Schreiben von Skripts in den folgenden Methoden zur Verfügung, in der **ScriptMain** Klasse.  
  
1.  Überschreiben Sie die **' acquireconnections '** Methode, um eine Verbindung mit der externen Datenquelle herstellen. Extrahieren Sie das Verbindungsobjekt bzw. die erforderlichen Verbindungsinformationen vom Verbindungs-Manager.  
  
2.  Überschreiben Sie die **PreExecute** -Methode zum Laden von Daten, wenn Sie alle Quelldaten gleichzeitig laden können. Sie können z. B. Ausführen eine **"SqlCommand"** für ein [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank, und Laden Sie alle Quelldaten gleichzeitig in eine **SqlDataReader**. Wenn Sie zu einem Zeitpunkt (z. B. beim Lesen einer Textdatei) die Quelldaten zeilenweise laden müssen, können Sie die Daten laden, wie Sie Zeilen in durchlaufen **CreateNewOutputRows**.  
  
3.  Verwenden Sie die überschriebene **CreateNewOutputRows** -Methode leere Ausgabepuffer neue Zeilen hinzu und füllen Sie die Werte der einzelnen Spalten in den neuen Ausgabezeilen. Verwenden der **AddRow** Methode der einzelnen Ausgabepuffer eine leere neue Zeile hinzufügen, und legen Sie dann die Werte der einzelnen Spalten. Üblicherweise kopieren Sie die Werte aus den Spalten, die aus der externen Quelle geladen werden.  
  
4.  Überschreiben Sie die **"PostExecute"** Methode, um die Verarbeitung der Daten abzuschließen. Sie können z. B. schließen die **SqlDataReader** , dass Sie zum Laden von Daten verwendet.  
  
5.  Überschreiben Sie die **' releaseconnections '** Methode aus der externen Datenquelle zu trennen, falls erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen die benutzerdefinierten Code, der erforderlich ist, in der **ScriptMain** Klasse, um die Erstellung einer Quellkomponente.  
  
> [!NOTE]  
>  Diese Beispiele verwenden die **Person.Address** -Tabelle in der **AdventureWorks** Beispieldatenbank aus, und übergeben Sie die erste und die vierte Spalte, die **IntAddressID** und  **Nvarchar (30) City** Spalten, durch den Datenfluss. Die gleichen Daten werden in den Quellen-, Transformations- und Zielbeispielen in diesem Abschnitt verwendet. Zusätzliche Voraussetzungen und Annahmen werden für jedes Beispiel dokumentiert.  
  
### <a name="adonet-source-example"></a>ADO.NET-Quellenbeispiel  
 Dieses Beispiel zeigt eine Quellkomponente, die einen vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Verbindungs-Manager zum Laden von Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle in den Datenfluss.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Erstellen einer [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Verbindungs-Manager verwendet die **SqlClient** Anbieter zur Verbindung mit der **AdventureWorks** Datenbank.  
  
2.  Fügen Sie der Datenfluss-Designeroberfläche eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Quelle.  
  
3.  Öffnen der **Skript Transformations-Editor**. Auf der **Eingaben und Ausgaben** Seite, die der standardmäßigen Ausgabe einen aussagekräftigeren Namen, z. B. **"myaddressoutput"**, hinzufügen und konfigurieren Sie die beiden Ausgabespalten **AddressID**und **City**.  
  
    > [!NOTE]  
    >  Achten Sie darauf, dass Sie den Datentyp ändern die **City** Ausgabespalte in DT_WSTR.  
  
4.  Auf der **Verbindungs-Manager** hinzufügen oder erstellen, die [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Verbindungs-Manager, und geben sie einen Namen wie z. B. **"myadonetconnection"**.  
  
5.  Auf der **Skript** auf **Bearbeitungsskript** , und geben Sie das folgende Skript. Schließen Sie dann die skriptentwicklungsumgebung und den **Skript Transformations-Editor**.  
  
6.  Erstellen und konfigurieren Sie eine Zielkomponente, z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ziel oder die beispielzielkomponente, die [Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md), der erwartet, dass die  **AddressID** und **City** Spalten. Stellen Sie anschließend eine Verbindung der Quellkomponente mit dem Ziel her. (Sie können eine Quelle ohne Transformationen direkt mit einem Ziel verbinden.) Sie können eine Zieltabelle erstellen, durch Ausführen des folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl in der **AdventureWorks** Datenbank:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  Führen Sie das Beispiel aus.  
  
    ```vb  
    Imports System.Data.SqlClient  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim connMgr As IDTSConnectionManager100  
        Dim sqlConn As SqlConnection  
        Dim sqlReader As SqlDataReader  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            connMgr = Me.Connections.MyADONETConnection  
            sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim cmd As New SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn)  
            sqlReader = cmd.ExecuteReader  
  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Do While sqlReader.Read  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = sqlReader.GetInt32(0)  
                    .City = sqlReader.GetString(1)  
                End With  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
  
            sqlReader.Close()  
  
        End Sub  
  
        Public Overrides Sub ReleaseConnections()  
  
            connMgr.ReleaseConnection(sqlConn)  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.Data.SqlClient;  
    public class ScriptMain:  
        UserComponent  
  
    {  
        IDTSConnectionManager100 connMgr;  
        SqlConnection sqlConn;  
        SqlDataReader sqlReader;  
  
        public override void AcquireConnections(object Transaction)  
        {  
            connMgr = this.Connections.MyADONETConnection;  
            sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
  
            SqlCommand cmd = new SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn);  
            sqlReader = cmd.ExecuteReader();  
  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            while (sqlReader.Read())  
            {  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = sqlReader.GetInt32(0);  
                    MyAddressOutputBuffer.City = sqlReader.GetString(1);  
                }  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            sqlReader.Close();  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            connMgr.ReleaseConnection(sqlConn);  
  
        }  
  
    }  
    ```  
  
### <a name="flat-file-source-example"></a>Flatfilequellenbeispiel  
 Diese Beispiel zeigt eine Quellkomponente, die einen vorhandenen Verbindungs-Manager für Flatfiles zum Laden von Daten aus einer Flatfile in den Datenfluss einsetzt. Die Flatfilequelldaten werden durch einen Export aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Verwenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import / Export-Assistenten zum Exportieren der **Person.Address** Tabelle aus der **AdventureWorks** -Beispieldatenbank in eine kommagetrennte Flatfile. In diesem Beispiel wird der Dateiname ExportedAddresses.txt verwendet.  
  
2.  Erstellen Sie einen Verbindungs-Manager für Flatfiles, der eine Verbindung mit der exportierten Datendatei herstellt.  
  
3.  Fügen Sie der Datenfluss-Designeroberfläche eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Quelle.  
  
4.  Öffnen der **Skript Transformations-Editor**. Auf der **Eingaben und Ausgaben** Seite, die der standardmäßigen Ausgabe einen aussagekräftigeren Namen, z. B. **"myaddressoutput"**. Hinzufügen und konfigurieren Sie die beiden Ausgabespalten **AddressID** und **City**.  
  
5.  Auf der **Verbindungs-Manager** Seite, hinzufügen oder den Flatfile-Verbindungs-Manager erstellen, verwenden einen beschreibenden Namen wie z. B. **"myflatfilesrcconnectionmanager"**.  
  
6.  Auf der **Skript** auf **Bearbeitungsskript** , und geben Sie das folgende Skript. Schließen Sie dann die skriptentwicklungsumgebung und den **Skript Transformations-Editor**.  
  
7.  Erstellen und konfigurieren Sie eine Zielkomponente, z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ziel oder die beispielzielkomponente, die [Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Stellen Sie anschließend eine Verbindung der Quellkomponente mit dem Ziel her. (Sie können eine Quelle ohne Transformationen direkt mit einem Ziel verbinden.) Sie können eine Zieltabelle erstellen, durch Ausführen des folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl in der **AdventureWorks** Datenbank:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Führen Sie das Beispiel aus.  
  
    ```vb  
    Imports System.IO  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Private textReader As StreamReader  
        Private exportedAddressFile As String  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connMgr As IDTSConnectionManager100 = _  
                Me.Connections.MyFlatFileSrcConnectionManager  
            exportedAddressFile = _  
                CType(connMgr.AcquireConnection(Nothing), String)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
            MyBase.PreExecute()  
            textReader = New StreamReader(exportedAddressFile)  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Dim nextLine As String  
            Dim columns As String()  
  
            Dim delimiters As Char()  
            delimiters = ",".ToCharArray  
  
            nextLine = textReader.ReadLine  
            Do While nextLine IsNot Nothing  
                columns = nextLine.Split(delimiters)  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = columns(0)  
                    .City = columns(3)  
                End With  
                nextLine = textReader.ReadLine  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
            MyBase.PostExecute()  
            textReader.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.IO;  
    public class ScriptMain:  
        UserComponent  
  
    {  
        private StreamReader textReader;  
        private string exportedAddressFile;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileSrcConnectionManager;  
            exportedAddressFile = (string)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
            base.PreExecute();  
            textReader = new StreamReader(exportedAddressFile);  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            string nextLine;  
            string[] columns;  
  
            char[] delimiters;  
            delimiters = ",".ToCharArray();  
  
            nextLine = textReader.ReadLine();  
            while (nextLine != null)  
            {  
                columns = nextLine.Split(delimiters);  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = columns[0];  
                    MyAddressOutputBuffer.City = columns[3];  
                }  
                nextLine = textReader.ReadLine();  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            base.PostExecute();  
            textReader.Close();  
  
        }  
  
    }  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [Entwickeln einer benutzerdefinierten Quellkomponente](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  

