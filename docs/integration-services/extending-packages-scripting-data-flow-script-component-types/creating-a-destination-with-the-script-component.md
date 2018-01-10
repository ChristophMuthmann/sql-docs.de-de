---
title: Erstellen eines Ziels mit der Skriptkomponente | Microsoft-Dokumentation
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
applies_to: SQL Server 2016 Preview
dev_langs: VB
helpviewer_keywords:
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
caps.latest.revision: "57"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d9037d604503ba2a0d5443e94f11638035369ce3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="creating-a-destination-with-the-script-component"></a>Erstellen eines Ziels mit der Skriptkomponente
  Zielkomponenten dienen im Datenfluss eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakets dazu, von Upstreamquellen empfangene Daten und Transformationen in einer Datenquelle zu speichern. Gewöhnlich stellt die Zielkomponente über einen vorhandenen Verbindungs-Manager eine Verbindung mit der Datenquelle her.  
  
 Eine Übersicht der Skriptkomponenten finden Sie unter [Extending the Data Flow with the Script Component (Erweitern des Datenflusses mit der Skriptkomponente)](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 Die Skriptkomponente und der Infrastrukturcode, den sie generieren, erleichtern Ihnen die Entwicklung benutzerdefinierter Datenflusskomponenten deutlich. Zum Verständnis der Funktionsweise dieser Skriptkomponente kann es jedoch hilfreich sein, sich mit den im Abschnitt [Developing a Custom Data Flow Component (Entwickeln einer benutzerdefinierten Datenflusskomponente)](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) beschriebenen Schritten für die Entwicklung einer benutzerdefinierten Datenflusskomponente vertraut zu machen, und zwar insbesondere mit [Developing a Custom Destination Component (Entwickeln einer benutzerdefinierten Zielkomponente)](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md).  
  
## <a name="getting-started-with-a-destination-component"></a>Erste Schritte mit einer Zielkomponente  
 Wenn Sie zur Registerkarte „Datenfluss“ des [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designers eine Skriptkomponente hinzufügen, wird das Dialogfeld **Skriptkomponententyp auswählen** geöffnet, und Sie werden zur Auswahl des Skripts **Quelle**, **Ziel** oder **Transformation** aufgefordert. Wählen Sie in diesem Dialogfeld **Ziel** aus.  
  
 Verbinden Sie anschließend die Ausgabe einer Transformation mit der Zielkomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. Für Tests können Sie ohne Transformationen direkt eine Quelle mit einem Ziel verbinden.  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>Konfigurieren einer Zielkomponente im Metadatenentwurfsmodus  
 Nachdem Sie die Option zur Erstellung einer Zielkomponente ausgewählt haben, konfigurieren Sie die Komponente mit dem **Transformations-Editor für Skripterstellung**. Weitere Informationen finden Sie unter [Configuring the Script Component in the Script Component Editor (Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor)](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Legen Sie die **ScriptLanguage**-Eigenschaft auf der Seite **Skript** im Dialogfeld **Transformations-Editor für Skripterstellung** fest, um die Skriptsprache auszuwählen, die das Skriptziel verwenden soll.  
  
> [!NOTE]  
>  Verwenden Sie im Dialogfeld **Optionen** auf der Seite **Allgemein** die Option **Skriptsprache**, um die Standardskriptsprache für die Skriptkomponente festzulegen. Weitere Informationen finden Sie unter [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Eine Datenflusszielkomponente verfügt über eine Eingabe und keine Ausgaben. Die Konfiguration der Eingabe für die Komponente ist einer der Schritte, den Sie mit dem **Transformations-Editor für Skripterstellung** im Metadatenentwurfsmodus abschließen müssen, bevor Sie das benutzerdefinierte Skript schreiben.  
  
### <a name="adding-connection-managers"></a>Hinzufügen von Verbindungs-Managern  
 Eine Zielkomponente verwendet normalerweise einen vorhandenen Verbindungs-Manager zum Herstellen einer Verbindung mit der Datenquelle, in der sie die Daten aus dem Datenfluss speichert. Klicken Sie im **Transformations-Editor für Skripterstellung** auf der Seite **Verbindungs-Manager** auf **Hinzufügen**, um den passenden Verbindungs-Manager hinzuzufügen.  
  
 Ein Verbindungs-Manager ist jedoch nur eine praktische Einheit, die die Informationen kapselt und speichert, die benötigt werden, um eine Verbindung mit einem bestimmten Datenquellentyp herzustellen. Um Daten zu laden und zu speichern und möglicherweise auch eine Verbindung mit der Datenquelle herzustellen und diese zu beenden, müssen Sie Ihren eigenen benutzerdefinierten Code schreiben.  
  
 Allgemeine Informationen zum Verwenden von Verbindungs-Managern mit der Skriptkomponente finden Sie unter [Connecting to Data Sources in the Script Component (Herstellen einer Verbindung mit Datenquellen in der Skriptkomponente)](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Weitere Informationen über die Seite **Verbindungs-Manager** im **Transformations-Editor für Skripterstellung** finden Sie unter [Script Transformation Editor (Connection Managers Page) (Transformations-Editor für Skripterstellung (Seite „Verbindungs-Manager“))](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>Konfigurieren von Eingaben und Eingabespalten  
 Eine Zielkomponente verfügt über eine Eingabe und keine Ausgaben.  
  
 Die Spaltenliste auf der Seite **Eingabespalten** im **Transformations-Editor für Skripterstellung** zeigt die von der Ausgabe der Upstreamkomponente im Datenfluss verfügbaren Spalten an. Wählen Sie die Spalten aus, die Sie speichern möchten.  
  
 Weitere Informationen über die Seite **Eingabespalten** im **Transformations-Editor für Skripterstellung** finden Sie unter [Script Transformation Editor (Input Columns Page) (Transformations-Editor für Skripterstellung (Seite „Eingabespalten“))](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
 Auf der Seite **Eingaben und Ausgaben** im **Transformations-Editor für Skripterstellung** wird eine einzelne Eingabe angezeigt, die Sie umbenennen können. Verwenden Sie die im automatisch generierten Code erstellte Accessoreigenschaft, um mit dem Namen in Ihrem Skript auf die Eingabe zu verweisen.  
  
 Weitere Informationen über die Seite **Eingaben und Ausgaben** im **Transformations-Editor für Skripterstellung** finden Sie unter [Script Transformation Editor (Inputs and Outputs Page) (Transformations-Editor für Skripterstellung (Seite „Eingaben und Ausgaben“))](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Hinzufügen von Variablen  
 Wenn Sie die vorhandenen Variablen in Ihrem Skript verwenden möchten, können Sie diese in den Eigenschaftsfeldern **ReadOnlyVariables** und **ReadWriteVariables** auf der Seite **Skript** im **Transformations-Editor für Skripterstellung** hinzufügen.  
  
 Wenn Sie mehrere Variablen in die Eigenschaftsfelder hinzufügen, trennen Sie die Variablennamen durch Kommas. Sie können auch mehrere Variablen auswählen, indem Sie auf die Schaltfläche mit den Auslassungszeichen (**…**) neben den Eigenschaftsfeldern für **ReadOnlyVariables** und **ReadWriteVariables** klicken und dann die Variablen im Dialogfeld **Variablen auswählen** festlegen.  
  
 Allgemeine Informationen über das Verwenden von Variablen mit der Skriptkomponente finden Sie unter [Using Variables in the Script Component (Verwenden von Variablen in der Skriptkomponente)](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Weitere Informationen über die Seite **Skript** im **Transformations-Editor für Skripterstellung** finden Sie unter [Script Transformation Editor (Script Page) (Transformations-Editor für Skripterstellung (Seite „Skript“))](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>Schreiben einer Zielkomponente im Codeentwurfsmodus  
 Nachdem Sie die Metadaten für Ihre Komponente konfiguriert haben, können Sie das benutzerdefinierte Skript schreiben. Klicken Sie auf der Seite **Skript** im **Transformations-Editor für Skripterstellung** auf **Skript bearbeiten**, um die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications-IDE (VSTA) zu öffnen und Ihr benutzerdefiniertes Skript hinzuzufügen. Welche Skriptsprache Sie verwenden, hängt davon ab, ob Sie auf der Seite **Skript** [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# als Skriptsprache für die **ScriptLanguage**-Eigenschaft festgelegt haben.  
  
 Wichtige Informationen, die alle Arten von Komponenten betreffen, die mithilfe der Skriptkomponente erstellt wurden, finden Sie unter [Coding and Debugging the Script Component (Codieren und Debuggen der Skriptkomponente)](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Grundlegendes zum automatisch generierten Code  
 Wenn Sie nach der Erstellung und Konfiguration einer Zielkomponente die VSTA-IDE öffnen, wird die bearbeitbare **ScriptMain**-Klasse im Code-Editor mit einem Stub für die **ProcessInputRow**-Methode angezeigt. Sie schreiben Ihren benutzerdefinierten Code in der **ScriptMain**-Klasse. **ProcessInputRow** ist die wichtigste Methode in einer Zielkomponente.  
  
 Wenn Sie das Fenster **Projektexplorer** in VSTA öffnen, können Sie sehen, dass die Skriptkomponente auch schreibgeschützte **BufferWrapper**- und **ComponentWrapper**-Projektelemente generiert hat. Die **ScriptMain**-Klasse erbt von der **UserComponent**-Klasse im **ComponentWrapper**-Projektelement.  
  
 Zur Laufzeit ruft das Datenflussmodul die **ProcessInput**-Methode in der **UserComponent**-Klasse auf, die die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A>-Methode der übergeordneten <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Klasse überschreibt. Die **ProcessInput**-Methode durchläuft die Zeilen im Eingabepuffer der Reihe nach und ruft für jede Zeile einmal die **ProcessInputRow**-Methode auf.  
  
### <a name="writing-your-custom-code"></a>Schreiben von benutzerdefiniertem Code  
 Sie sollten Skript in den folgenden Methoden schreiben, die in der **ScriptMain**-Klasse verfügbar sind, um das Erstellen einer benutzerdefinierten Zielkomponente abzuschließen.  
  
1.  Überschreiben Sie die **AcquireConnections**-Methode, um eine Verbindung mit der externen Datenquelle herzustellen. Extrahieren Sie das Verbindungsobjekt bzw. die erforderlichen Verbindungsinformationen vom Verbindungs-Manager.  
  
2.  Überschreiben Sie als Vorbereitung auf die Speicherung der Daten die **PreExecute**-Methode. Zum Beispiel sollten Sie **SqlCommand** und die entsprechenden Parameter in dieser Methode erstellen und konfigurieren.  
  
3.  Verwenden Sie die überschriebene **ProcessInputRow**-Methode, um jede Eingabezeile in die externe Datenquelle zu kopieren. Zum Beispiel können Sie für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ziel die Spaltenwerte in die Parameter von **SqlCommand** kopieren und den Befehl jeweils einmal pro Zeile ausführen. Für ein Flatfileziel können Sie die Werte für jede Spalte in einen **StreamWriter** schreiben, wobei die Werte durch Spaltentrennzeichen voneinander getrennt werden.  
  
4.  Überschreiben Sie bei Bedarf zur Trennung von der externen Datenbank und um alle weiteren erforderlichen Cleanups durchzuführen die **PostExecute**-Methode.  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen wird der Code veranschaulicht, der in der **ScriptMain**-Klasse zur Erstellung einer Zielkomponente erforderlich ist.  
  
> [!NOTE]  
>  In diesen Beispielen werden die erste und die vierte Spalte der Tabelle **Person.Address** in der Beispieldatenbank **AdventureWorks** verwendet, und die Spalten **int*AddressID*** und **nvarchar(30)City** werden durch den Datenfluss weitergeleitet. Die gleichen Daten werden in den Quellen-, Transformations- und Zielbeispielen in diesem Abschnitt verwendet. Zusätzliche Voraussetzungen und Annahmen werden für jedes Beispiel dokumentiert.  
  
### <a name="adonet-destination-example"></a>Beispiel ADO.NET-Ziel  
 Dieses Beispiel zeigt eine Zielkomponente, die einen vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager zum Speichern von Daten aus dem Datenfluss in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle verwendet.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Erstellen Sie einen [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager, der mithilfe des **SqlClient**-Anbieters eine Verbindung mit der **AdventureWorks**-Datenbank herstellt.  
  
2.  Erstellen Sie eine Zieltabelle, indem Sie den folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Befehl in der **AdventureWorks**-Datenbank ausführen:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Fügen Sie der Oberfläche des Datenfluss-Designers eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Ziel.  
  
4.  Verbinden Sie die Ausgabe einer Upstreamquelle oder Transformation mit der Zielkomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. (Sie können eine Quelle ohne Transformationen direkt mit einem Ziel verbinden.) Diese Ausgabe sollte Daten aus der Tabelle **Person.Address** der Beispieldatenbank **AdventureWorks** bereitstellen, die mindestens die Spalten **AddressID** und **City** enthält.  
  
5.  Öffnen Sie den **Transformations-Editor für Skripterstellung**. Wählen Sie auf der Seite **Eingabespalten** die Eingabespalten **AddressID** und **City** aus.  
  
6.  Geben Sie der Eingabe auf der Seite **Eingaben und Ausgaben** einen aussagekräftigeren Namen, z.B. **MyAddressInput**.  
  
7.  Fügen Sie auf der Seite **Verbindungs-Manager** den [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager mit einem Namen wie **MyADONETConnectionManager** hinzu, oder erstellen Sie diesen.  
  
8.  Klicken Sie auf der Seite **Skript** auf **Skript bearbeiten**, und geben Sie das folgende Skript ein. Schließen Sie dann die Skriptentwicklungsumgebung.  
  
9. Schließen Sie den **Transformations-Editor für Skripterstellung**, und führen Sie das Beispiel aus.  
  
```vb  
Imports System.Data.SqlClient  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim connMgr As IDTSConnectionManager100  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        connMgr = Me.Connections.MyADONETConnectionManager  
        sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
        With sqlCmd  
            .Parameters("@addressid").Value = Row.AddressID  
            .Parameters("@city").Value = Row.City  
            .ExecuteNonQuery()  
        End With  
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
    SqlCommand sqlCmd;  
    SqlParameter sqlParam;  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        connMgr = this.Connections.MyADONETConnectionManager;  
        sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " +  
            "VALUES(@addressid, @city)", sqlConn);  
        sqlParam = new SqlParameter("@addressid", SqlDbType.Int);  
        sqlCmd.Parameters.Add(sqlParam);  
        sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);  
        sqlCmd.Parameters.Add(sqlParam);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
        {  
            sqlCmd.Parameters["@addressid"].Value = Row.AddressID;  
            sqlCmd.Parameters["@city"].Value = Row.City;  
            sqlCmd.ExecuteNonQuery();  
        }  
    }  
  
    public override void ReleaseConnections()  
    {  
  
        connMgr.ReleaseConnection(sqlConn);  
  
    }  
  
}  
```  
  
### <a name="flat-file-destination-example"></a>Beispiel für das Flatfileziel  
 Dieses Beispiel zeigt eine Zielkomponente, die einen vorhandenen Verbindungs-Manager für Flatfiles zum Speichern von Daten aus einem Datenfluss in eine Flatfile verwendet.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Erstellen Sie einen Verbindungs-Manager für Flatfiles, der eine Verbindung mit einer Zieldatei herstellt. Die Datei muss nicht vorhanden sein; sie wird durch die Zielkomponente erstellt. Konfigurieren Sie die Zieldatei als durch Trennzeichen getrennte Datei, die die Spalten **AddressID** und **City** enthält.  
  
2.  Fügen Sie der Oberfläche des Datenfluss-Designers eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Ziel.  
  
3.  Verbinden Sie die Ausgabe einer Upstreamquelle oder Transformation mit der Zielkomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. (Sie können eine Quelle ohne Transformationen direkt mit einem Ziel verbinden.) Diese Ausgabe sollte Daten aus der Tabelle **Person.Address** der Beispieldatenbank **AdventureWorks** bereitstellen, und mindestens die Spalten **AddressID** und **City** enthalten.  
  
4.  Öffnen Sie den **Transformations-Editor für Skripterstellung**. Wählen Sie auf der Seite **Eingabespalten** die Spalten **AddressID** und **City** aus.  
  
5.  Geben Sie der Eingabe auf der Seite **Eingaben und Ausgaben** einen aussagekräftigeren Namen, z.B. **MyAddressInput**.  
  
6.  Fügen Sie auf der Seite **Verbindungs-Manager** den Verbindungs-Manager für Flatfiles mit einem aussagekräftigen Namen hinzu, z.B. **MyFlatFileDestConnectionManager**, oder erstellen Sie diesen.  
  
7.  Klicken Sie auf der Seite **Skript** auf **Skript bearbeiten**, und geben Sie das folgende Skript ein. Schließen Sie dann die Skriptentwicklungsumgebung.  
  
8.  Schließen Sie den **Transformations-Editor für Skripterstellung**, und führen Sie das Beispiel aus.  
  
```vb  
Imports System.IO  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim copiedAddressFile As String  
    Private textWriter As StreamWriter  
    Private columnDelimiter As String = ","  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        Dim connMgr As IDTSConnectionManager100 = _  
            Me.Connections.MyFlatFileDestConnectionManager  
        copiedAddressFile = CType(connMgr.AcquireConnection(Nothing), String)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        textWriter = New StreamWriter(copiedAddressFile, False)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With textWriter  
            If Not Row.AddressID_IsNull Then  
                .Write(Row.AddressID)  
            End If  
            .Write(columnDelimiter)  
            If Not Row.City_IsNull Then  
                .Write(Row.City)  
            End If  
            .WriteLine()  
        End With  
  
    End Sub  
  
    Public Overrides Sub PostExecute()  
  
        textWriter.Close()  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.IO;  
public class ScriptMain:  
    UserComponent  
  
{  
    string copiedAddressFile;  
    private StreamWriter textWriter;  
    private string columnDelimiter = ",";  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileDestConnectionManager;  
        copiedAddressFile = (string) connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        textWriter = new StreamWriter(copiedAddressFile, false);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            if (!Row.AddressID_IsNull)  
            {  
                textWriter.Write(Row.AddressID);  
            }  
            textWriter.Write(columnDelimiter);  
            if (!Row.City_IsNull)  
            {  
                textWriter.Write(Row.City);  
            }  
            textWriter.WriteLine();  
        }  
  
    }  
  
    public override void PostExecute()  
    {  
  
        textWriter.Close();  
  
    }  
  
}  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Creating a Source with the Script Component (Erstellen einer Quelle mit der Skriptkomponente)](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [Entwickeln einer benutzerdefinierten Zielkomponente](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
