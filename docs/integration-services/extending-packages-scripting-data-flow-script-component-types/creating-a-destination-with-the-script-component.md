---
title: Erstellen eines Ziels mit der Skriptkomponente | Microsoft Docs
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
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7680aac73590f92eadd615b9d164967e61877664
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-destination-with-the-script-component"></a>Erstellen eines Ziels mit der Skriptkomponente
  Zielkomponenten dienen im Datenfluss eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakets dazu, von Upstreamquellen empfangene Daten und Transformationen in einer Datenquelle zu speichern. Gewöhnlich stellt die Zielkomponente über einen vorhandenen Verbindungs-Manager eine Verbindung mit der Datenquelle her.  
  
 Einen Überblick über die Skriptkomponente finden Sie unter [Extending the Data Flow mit der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 Die Skriptkomponente und der Infrastrukturcode, den sie generieren, erleichtern Ihnen die Entwicklung benutzerdefinierter Datenflusskomponenten deutlich. Jedoch, um die Funktionsweise der Skriptkomponente zu verstehen, Sie finden es vielleicht hilfreich, lesen die Schritte für die Entwicklung von benutzerdefinierten Datenflusskomponenten in der [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) Abschnitt, und zwar insbesondere [Entwickeln einer benutzerdefinierten Zielkomponente](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md).  
  
## <a name="getting-started-with-a-destination-component"></a>Erste Schritte mit einer Zielkomponente  
 Wenn Sie eine Skriptkomponente hinzufügen, auf der Registerkarte Datenfluss des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer die **Skriptkomponententyp** Dialogfeld wird geöffnet und fordert Sie zum Auswählen einer **Quelle**, **Ziel** , oder **Transformation** Skript. Wählen Sie in diesem Dialogfeld **Ziel**.  
  
 Verbinden Sie anschließend die Ausgabe einer Transformation mit der Zielkomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. Für Tests können Sie ohne Transformationen direkt eine Quelle mit einem Ziel verbinden.  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>Konfigurieren einer Zielkomponente im Metadatenentwurfsmodus  
 Nachdem Sie die Option zum Erstellen einer Zielkomponente ausgewählt haben, konfigurieren Sie die Komponente mit der **Skript Transformations-Editor**. Weitere Informationen finden Sie unter [Configuring the Script Component in the Script Component Editor](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Um die Skriptsprache auszuwählen, die das skriptziel verwenden wird, legen Sie die **ScriptLanguage** Eigenschaft auf die **Skript** auf der Seite der **Skript Transformations-Editor** Das Dialogfeld.  
  
> [!NOTE]  
>  Um die Standardskriptsprache für die Skriptkomponente festzulegen, verwenden die **Skriptsprache** auf die option der **allgemeine** auf der Seite der **Optionen** (Dialogfeld). Weitere Informationen finden Sie unter [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Eine Datenflusszielkomponente verfügt über eine Eingabe und keine Ausgaben. Konfiguration der Eingabe für die Komponente einer der Schritte, die Sie im metadatenentwurfsmodus müssen ist, mithilfe Abschließen der **Skript Transformations-Editor**, bevor Sie das benutzerdefinierte Skript schreiben.  
  
### <a name="adding-connection-managers"></a>Hinzufügen von Verbindungs-Managern  
 Eine Zielkomponente verwendet normalerweise einen vorhandenen Verbindungs-Manager zum Herstellen einer Verbindung mit der Datenquelle, in der sie die Daten aus dem Datenfluss speichert. Auf der **Verbindungs-Manager** auf der Seite der **Skript Transformations-Editor**, klicken Sie auf **hinzufügen** geeigneten Verbindungs-Manager hinzufügen.  
  
 Ein Verbindungs-Manager ist jedoch nur eine praktische Einheit, die die Informationen kapselt und speichert, die benötigt werden, um eine Verbindung mit einem bestimmten Datenquellentyp herzustellen. Um Daten zu laden und zu speichern und möglicherweise auch eine Verbindung mit der Datenquelle herzustellen und diese zu beenden, müssen Sie Ihren eigenen benutzerdefinierten Code schreiben.  
  
 Allgemeine Informationen zur Verwendung von Verbindungs-Manager mit der Skriptkomponente finden Sie unter [Connecting to Data Sources in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Weitere Informationen zu den **Verbindungs-Manager** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Verbindungsseite-Manager &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>Konfigurieren von Eingaben und Eingabespalten  
 Eine Zielkomponente verfügt über eine Eingabe und keine Ausgaben.  
  
 Auf der **Eingabespalten** auf der Seite der **Skript Transformations-Editor**, die Spaltenliste zeigt die verfügbaren Spalten aus der Ausgabe der upstreamkomponente im Datenfluss. Wählen Sie die Spalten aus, die Sie speichern möchten.  
  
 Weitere Informationen zu den **Eingabespalten** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Seite "Spalten" Eingabe &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
 Die **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor** wird eine einzelne Eingabe, die Sie umbenennen können. Verwenden Sie die im automatisch generierten Code erstellte Accessoreigenschaft, um mit dem Namen in Ihrem Skript auf die Eingabe zu verweisen.  
  
 Weitere Informationen zu den **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Eingaben und Ausgaben Seite &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Hinzufügen von Variablen  
 Wenn Sie vorhandene Variablen in Ihrem Skript verwenden möchten, können Sie diese im Hinzufügen der **ReadOnlyVariables** und **ReadWriteVariables** Eigenschaftsfeldern für die **Skript** auf der Seite der **Skript Transformations-Editor**.  
  
 Wenn Sie mehrere Variablen in die Eigenschaftsfelder hinzufügen, trennen Sie die Variablennamen durch Kommas. Sie können auch mehrere Variablen auswählen, indem Sie auf die Auslassungspunkte (**...** ) neben dem **ReadOnlyVariables** und **ReadWriteVariables** Eigenschaftenfelder, und wählen Sie dann die Variablen in der **Variablen auswählen** Das Dialogfeld.  
  
 Allgemeine Informationen zur Verwendung von Variablen mit der Skriptkomponente finden Sie unter [Using Variables in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Weitere Informationen zu den **Skript** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Skript Transformations-Editor &#40; Seite "Skript" &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>Schreiben einer Zielkomponente im Codeentwurfsmodus  
 Nachdem Sie die Metadaten für Ihre Komponente konfiguriert haben, können Sie das benutzerdefinierte Skript schreiben. In der **Skript Transformations-Editor**auf die **Skript** auf **Bearbeitungsskript** So öffnen die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE in dem Sie das benutzerdefinierte Skript hinzufügen können. Die verwendete Skriptsprache, die Sie verwenden, hängt davon ab, ob Sie ausgewählt [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual c# als Skriptsprache für die **ScriptLanguage** Eigenschaft auf die **Skript** Seite ".  
  
 Wichtige Informationen, die für alle Arten von Komponenten, die mithilfe der Skriptkomponente erstellt gilt, finden Sie unter [codieren und Debuggen der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Grundlegendes zum automatisch generierten Code  
 Wenn Sie öffnen die VSTA IDE nach der Erstellung und Konfiguration einer Zielkomponente, die bearbeitet werden **ScriptMain** Klasse angezeigt wird, im Codeeditor mit einem Stub für die **ProcessInputRow** Methode. Die **ScriptMain** Klasse ist, in dem Sie Ihren benutzerdefinierten Code schreiben und **ProcessInputRow** ist die wichtigste Methode in einer Zielkomponente.  
  
 Wenn Sie öffnen die **Projektexplorer** Fenster in VSTA können Sie sehen, dass die Skriptkomponente auch schreibgeschützte generiert hat **BufferWrapper** und **ComponentWrapper** Projekt Elemente. Die **ScriptMain** Klasse erbt von **UserComponent** -Klasse in der **ComponentWrapper** -Projektelement.  
  
 Zur Laufzeit ruft das Datenflussmodul die **ProcessInput** Methode in der **UserComponent** Klasse, welche Außerkraftsetzungen der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> übergeordnete Klasse. Die **ProcessInput** Methode durchläuft die Zeilen in den Eingabepuffer und ruft dann die **ProcessInputRow** Methode einmal für jede Zeile.  
  
### <a name="writing-your-custom-code"></a>Schreiben von benutzerdefiniertem Code  
 Zum Erstellen einer benutzerdefinierten Zielkomponente fertig sind, möchten Sie möglicherweise Schreiben von Skripts in den folgenden Methoden zur Verfügung, in der **ScriptMain** Klasse.  
  
1.  Überschreiben Sie die **' acquireconnections '** Methode, um eine Verbindung mit der externen Datenquelle herstellen. Extrahieren Sie das Verbindungsobjekt bzw. die erforderlichen Verbindungsinformationen vom Verbindungs-Manager.  
  
2.  Überschreiben Sie die **PreExecute** Methode So bereiten Sie die Daten zu speichern. Beispielsweise sollten Sie zum Erstellen und Konfigurieren einer **"SqlCommand"** und die Parameter in dieser Methode.  
  
3.  Verwenden Sie die überschriebene **ProcessInputRow** Methode, um jede Eingabezeile an die externe Datenquelle zu kopieren. Z. B. für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ziel, können Sie die Spaltenwerte in den Parametern des Kopieren einer **"SqlCommand"** und führen Sie den Befehl jeweils einmal für jede Zeile. Für ein Flatfileziel können Sie die Werte für jede Spalte zum Schreiben einer **StreamWriter**, die Werte durch Spaltentrennzeichen voneinander getrennt.  
  
4.  Überschreiben Sie die **"PostExecute"** Methode, um aus der externen Datenquelle zu trennen, falls erforderlich, und alle weiteren erforderlichen Cleanups ausführen.  
  
## <a name="examples"></a>Beispiele  
 Die nachstehenden Beispielen wird Code, der erforderlich ist, in der **ScriptMain** Klasse zur Erstellung einer Zielkomponente.  
  
> [!NOTE]  
>  Diese Beispiele verwenden die **Person.Address** -Tabelle in der **AdventureWorks** Beispieldatenbank aus, und übergeben Sie die erste und die vierte Spalte, die **Int*AddressID*** und **Nvarchar (30) City** Spalten, durch den Datenfluss. Die gleichen Daten werden in den Quellen-, Transformations- und Zielbeispielen in diesem Abschnitt verwendet. Zusätzliche Voraussetzungen und Annahmen werden für jedes Beispiel dokumentiert.  
  
### <a name="adonet-destination-example"></a>Beispiel ADO.NET-Ziel  
 Dieses Beispiel zeigt eine Zielkomponente, die einen vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Verbindungs-Manager zum Speichern von Daten aus dem Datenfluss in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.  
  
 Wenn Sie den Beispielcode ausführen möchten, müssen Sie das Paket und die Komponente folgendermaßen konfigurieren:  
  
1.  Erstellen einer [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Verbindungs-Manager verwendet die **SqlClient** Anbieter zur Verbindung mit der **AdventureWorks** Datenbank.  
  
2.  Erstellen Sie eine Zieltabelle durch Ausführen des folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl in der **AdventureWorks** Datenbank:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Fügen Sie der Oberfläche des Datenfluss-Designers eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Ziel.  
  
4.  Verbinden Sie die Ausgabe einer Upstreamquelle oder Transformation mit der Zielkomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. (Sie können eine Quelle ohne Transformationen direkt mit einem Ziel verbinden.) Geben Sie diese Ausgabe sollte Daten aus der **Person.Address** Tabelle mit den **AdventureWorks** -Beispieldatenbank, die enthält mindestens die **AddressID** und  **City** Spalten.  
  
5.  Öffnen der **Skript Transformations-Editor**. Auf der **Eingabespalten** Seite der **AddressID** und **City** Eingabespalten verwendet werden sollen.  
  
6.  Auf der **Eingaben und Ausgaben** Seite, benennen Sie die Eingabe einen aussagekräftigeren Namen wie z. B. **"myaddressinput"**.  
  
7.  Auf der **Verbindungs-Manager** hinzufügen oder erstellen, die [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Verbindungs-Manager mit einem Namen wie **Meinadonetverbindungsmanager**.  
  
8.  Auf der **Skript** auf **Bearbeitungsskript** , und geben Sie das folgende Skript. Schließen Sie dann die Skriptentwicklungsumgebung.  
  
9. Schließen der **Skript Transformations-Editor** und führen Sie das Beispiel.  
  
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
  
1.  Erstellen Sie einen Verbindungs-Manager für Flatfiles, der eine Verbindung mit einer Zieldatei herstellt. Die Datei muss nicht vorhanden sein; sie wird durch die Zielkomponente erstellt. Konfigurieren Sie die Zieldatei als durch Trennzeichen getrennte Datei enthält die **AddressID** und **City** Spalten.  
  
2.  Fügen Sie der Oberfläche des Datenfluss-Designers eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Ziel.  
  
3.  Verbinden Sie die Ausgabe einer Upstreamquelle oder Transformation mit der Zielkomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. (Sie können eine Quelle ohne Transformationen direkt mit einem Ziel verbinden.) Geben Sie diese Ausgabe sollte Daten aus der **Person.Address** Tabelle mit der **AdventureWorks** Beispieldatenbank und enthalten sollte mindestens die **AddressID** und **City** Spalten.  
  
4.  Öffnen der **Skript Transformations-Editor**. Auf der **Eingabespalten** Seite der **AddressID** und **City** Spalten.  
  
5.  Auf der **Eingaben und Ausgaben** Seite, benennen Sie die Eingabe einen aussagekräftigeren Namen, z. B. **"myaddressinput"**.  
  
6.  Auf der **Verbindungs-Manager** Seite, hinzufügen oder Erstellen der Flatfile-Verbindungs-Manager mit einem aussagekräftigen Namen wie z. B. **MyFlatFileDestConnectionManager**.  
  
7.  Auf der **Skript** auf **Bearbeitungsskript** , und geben Sie das folgende Skript. Schließen Sie dann die Skriptentwicklungsumgebung.  
  
8.  Schließen der **Skript Transformations-Editor** und führen Sie das Beispiel.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Datenquelle mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [Entwickeln einer benutzerdefinierten Zielkomponente](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  

