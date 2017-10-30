---
title: Laden der Ausgabe eines lokalen Pakets | Microsoft Docs
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
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
caps.latest.revision: 66
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 41de742c987d9f043f3dd247ee84af6a3eaf365b
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="loading-the-output-of-a-local-package"></a>Laden der Ausgabe eines lokalen Pakets
  Clientanwendungen können die Ausgabe des lesen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Paketen, wenn die Ausgabe in gespeichert ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ziele mit [!INCLUDE[vstecado](../../includes/vstecado-md.md)], oder wenn die Ausgabe mithilfe der Klassen in in einem Flatfileziel gespeichert wird die **System.IO** Namespace. Eine Clientanwendung kann jedoch die Ausgabe eines Pakets auch direkt aus dem Arbeitsspeicher lesen, ohne dass hierfür ein Zwischenschritt zur persistenten Speicherung der Daten erforderlich ist. Der Schlüssel für diese Lösung ist die **Microsoft.SqlServer.Dts.DtsClient** datennamespace, der spezielle Implementierungen der enthält die **IDbConnection**, **IDbCommand**, und **IDbDataParameter** Schnittstellen aus der **"System.Data"** Namespace. Die Assembly, Microsoft.SqlServer.Dts.DtsClient.dll wird standardmäßig unter installiert **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**.  
  
> [!NOTE]  
>  In diesem Thema beschriebene Vorgehensweise erfordert, dass der DelayValidation-Eigenschaft des Datenflusstasks und alle übergeordneten Objekte auf den Standardwert des **"false"**.  
  
## <a name="description"></a>Description  
 In dieser Prozedur wird veranschaulicht, wie eine Clientanwendung in verwaltetem Code entwickelt wird, die die Ausgabe eines Pakets mit einem DataReader-Ziel direkt aus dem Arbeitsspeicher lädt. Die hier zusammengefassten Schritte werden in dem folgenden Codebeispiel veranschaulicht.  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>So laden Sie Datenpaketausgabe in eine Clientanwendung  
  
1.  Konfigurieren Sie in dem Paket ein DataReader-Ziel so, dass die Ausgabe empfangen wird, die in die Clientanwendung gelesen werden soll. Geben Sie dem DataReader-Ziel einen aussagekräftigen Namen, da Sie diesen Namen später in der Clientanwendung verwenden werden. Notieren Sie sich den Namen des DataReader-Ziels.  
  
2.  Legen Sie im Entwicklungsprojekt einen Verweis auf die **Microsoft.SqlServer.Dts.DtsClient** Namespace durch Assemblysuche **Microsoft.SqlServer.Dts.DtsClient.dll**. Standardmäßig wird diese Assembly im installiert **C:\Program Files\Microsoft SQL Server\100\DTS\Binn**. Importieren Sie den Namespace in Ihren Code mithilfe von C#- **Using** oder [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **Importe** Anweisung.  
  
3.  In Ihrem Code erstellen Sie ein Objekt des Typs **DtsClient.DtsConnection** mit einer Verbindungszeichenfolge, die die erforderlichen Befehlszeilenparameter enthält **dtexec.exe** zum Ausführen des Pakets. Weitere Informationen finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md). Öffnen Sie dann die Verbindung mit dieser Verbindungszeichenfolge an. Sie können auch die **Dtexecui** -Hilfsprogramms die erforderliche Verbindungszeichenfolge visuell zu erstellen.  
  
    > [!NOTE]  
    >  Im Beispielcode wird das Laden des Pakets aus dem Dateisystem mithilfe der `/FILE <path and filename>`-Syntax veranschaulicht. Aber auch Laden des Pakets aus der MSDB-Datenbank mithilfe von können die `/SQL <package name>` Syntax, oder aus der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Paketspeicher mithilfe der `/DTS \<folder name>\<package name>` Syntax.  
  
4.  Erstellen Sie ein Objekt des Typs **DtsClient.DtsCommand** , verwendet das zuvor erstellte **' dtsconnection '** und legen Sie dessen **CommandText** -Eigenschaft auf den Namen des DataReader Ziel des Pakets. Rufen Sie anschließend die **ExecuteReader** Methode für das Command-Objekt, um die Paketergebnisse in ein neues DataReader-Ziel zu laden.  
  
5.  Optional können Sie die Ausgabe des Pakets indirekt parametrisieren, indem Sie die Auflistung der **DtsDataParameter** Objekte auf der **DtsCommand** Objekt Werte an im Paket definierte Variablen übergeben. Innerhalb des Pakets können Sie diese Variablen als Abfrageparameter oder in Ausdrücken verwenden, um die an das DataReader-Ziel zurückgegebenen Ergebnisse zu beeinflussen. Sie müssen diese Variablen definieren, in das Paket in der **DtsClient** Namespace, bevor Sie sie mit verwenden können die **DtsDataParameter** Objekt von einer Clientanwendung. (Müssen Sie möglicherweise klicken Sie auf die **Variablenspalten** Symbolleisten-Schaltfläche in der **Variablen** Fenster zum Anzeigen der **Namespace** Spalte.) In Ihrem Client-Code beim Hinzufügen einer **DtsDataParameter** auf die **Parameter** Auflistung von der **DtsCommand**, lassen Sie den DtsClient-Namespaceverweis aus dem Variablennamen . Beispiel:  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  Rufen Sie die **lesen** -Methode des DataReader wiederholt Bedarf so durchlaufen Sie die Zeilen der Ausgabedaten. Verwenden Sie die Daten, oder speichern Sie die Daten zur späteren Verwendung in der Clientanwendung.  
  
    > [!IMPORTANT]  
    >  Die **lesen** dieser Implementierung des DataReader Methodenrückgabe **"true"** ein weiteres Mal, nachdem die letzte Zeile der Daten gelesen wurde. Dadurch ist es schwierig, den normalen Code zu verwenden, der dem DataReader durchläuft **lesen** gibt **"true"**. Wenn Ihr Code versucht, den DataReader oder die Verbindung nach dem Lesen der erwarteten Anzahl von Zeilen, ohne einen weiteren finalen Aufruf zum Schließen der **lesen** -Methode, der Code wird eine nicht behandelte Ausnahme ausgelöst. Jedoch, wenn Ihr Code versucht wird, zum Lesen von Daten bei dieser letzten Iteration durch eine Schleife beim **lesen** dennoch zurück **"true"** jedoch die letzte Zeile übergeben wurde, gibt der Code löst ein nicht behandeltes  **ApplicationException** mit der Meldung "die SSIS-IDataReader-Objekt liegt hinter dem Ende des Resultset." Dieses Verhalten unterscheidet sich von dem anderer DataReader-Implementierungen. Daher bei eine Schleife verwenden, um die Zeilen in dem DataReader zu lesen **lesen** gibt **"true"**, Sie müssen so schreiben Sie Code zum Abfangen, testen und verwerfen diese erwartete  **ApplicationException** auf der letzten erfolgreichen Aufruf der **lesen** Methode. Oder, wenn Sie die Anzahl der erwarteten Zeilen im Voraus wissen, können Sie die Zeilen verarbeiten, und rufen dann die **lesen** Methode noch einmal, bevor Sie den DataReader und die Verbindung schließen.  
  
7.  Rufen Sie die **Dispose** Methode der **DtsCommand** Objekt. Dies ist besonders wichtig, wenn Sie verwendet haben **DtsDataParameter** Objekte.  
  
8.  Schließen Sie den DataReader und die Verbindungsobjekte.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein Paket ausgeführt, das einen einzelnen Aggregatwert berechnet und den Wert in einem DataReader-Ziel speichert. Dieser Wert wird dann vom DataReader gelesen und in einem Textfeld in einem Windows Form angezeigt.  
  
 Beim Laden der Ausgabe eines Pakets in einer Clientanwendung müssen keine Parameter verwendet werden. Wenn Sie nicht, um einen Parameter zu verwenden möchten, können Sie die Verwendung der Variablen im weglassen der **DtsClient** Namespace, und lassen Sie den Code, verwendet der **DtsDataParameter** Objekt.  
  
#### <a name="to-create-the-test-package"></a>So erstellen Sie das Testpaket  
  
1.  Erstellen Sie ein neues [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket. Im Beispielcode wird "DtsClientWParamPkg.dtsx" als Name des Pakets verwendet.  
  
2.  Fügen Sie eine Variable der Typzeichenfolge im DtsClient-Namespace hinzu. Der Beispielscode verwendet "Country" als den Namen der Variablen. (Müssen Sie möglicherweise klicken Sie auf die **Variablenspalten** Symbolleisten-Schaltfläche in der **Variablen** Fenster zum Anzeigen der **Namespace** Spalte.)  
  
3.  Fügen Sie einen OLE DB-Verbindungs-Manager hinzu, der eine Verbindung zu der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Beispieldatenbank herstellt.  
  
4.  Fügen Sie dem Paket einen Datenflusstask hinzu, und wechseln Sie zur Datenfluss-Entwurfsoberfläche.  
  
5.  Fügen Sie dem Datenfluss eine OLE DB-Quelle hinzu, und konfigurieren Sie sie so, dass der zuvor erstellte OLE DB-Verbindungs-Manager verwendet werden kann, den Sie vorher erstellt haben. Fügen Sie auch den folgenden SQL-Befehl hinzu:  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  Klicken Sie auf **Parameter** und in der **Abfrageparameter festlegen** Dialogfeld Feld, das den einzelnen Eingabeparameter in der Abfrage, Parameter0, der Dtsclient-Variablen zuordnen.  
  
7.  Fügen Sie dem Datenfluss eine Transformation für das Aggregieren hinzu, und verbinden Sie die Ausgabe der OLE DB-Quelle mit der Transformation. Öffnen Sie den Transformations-Editor für Aggregieren, und konfigurieren Sie diesen so, dass alle Eingabespalten (*) gezählt werden und der Aggregatwert mit dem Alias "CustomerCount" ausgegeben wird.  
  
8.  Fügen Sie dem Datenfluss ein DatenReader-Ziel hinzu, und verbinden Sie die Ausgabe der Transformation für das Aggregieren mit dem DataReader-Ziel. Im Beispielcode wird "DataReaderDest" als Name des DataReader verwendet. Wählen Sie die einzelne verfügbare Eingabespalte, CustomerCount, für das Ziel aus.  
  
9. Speichern Sie das Paket. Die anschließend erstellte Testanwendung führt das Paket aus und ruft seine Ausgabe direkt vom Arbeitsspeicher ab.  
  
#### <a name="to-create-the-test-application"></a>So erstellen Sie die Testanwendung  
  
1.  Erstellen Sie eine neue Windows Forms-Anwendung.  
  
2.  Hinzufügen eines Verweises auf die **Microsoft.SqlServer.Dts.DtsClient** Namespace zu suchen und die Assembly mit dem gleichen Namen in **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**.  
  
3.  Kopieren Sie den folgenden Beispielcode, und fügen Sie ihn in das Codemodul für das Formular ein.  
  
4.  Ändern Sie den Wert, der die **DtexecArgs** -Variablen so, dass diese enthält die erforderlichen Befehlszeilenparameter **dtexec.exe** zum Ausführen des Pakets. Im Beispielcode wird das Paket aus dem Dateisystem geladen.  
  
5.  Ändern Sie den Wert, der die **DataReaderName** -Variablen so, dass diese enthält des Namens des DataReader-Ziels im Paket.  
  
6.  Setzen Sie eine Schaltfläche und ein Textfeld in das Formular. Im Beispielcode wird **BtnRun** als den Namen der Schaltfläche und **TxtResults** als den Namen des Textfelds.  
  
7.  Führen Sie die Anwendung aus, und klicken Sie auf die Schaltfläche. Nach einer kurzen Pause während der Ausführung des Pakets sollte der von dem Paket berechnete Aggregatwert (die Anzahl von Kunden in Kanada) im Textfeld auf dem Formular angezeigt werden.  
  
### <a name="sample-code"></a>Beispielcode  
  
```vb  
Imports System.Data  
Imports Microsoft.SqlServer.Dts.DtsClient  
  
Public Class Form1  
  
  Private Sub btnRun_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnRun.Click  
  
    Dim dtexecArgs As String  
    Dim dataReaderName As String  
    Dim countryName As String  
  
    Dim dtsConnection As DtsConnection  
    Dim dtsCommand As DtsCommand  
    Dim dtsDataReader As IDataReader  
    Dim dtsParameter As DtsDataParameter  
  
    Windows.Forms.Cursor.Current = Cursors.WaitCursor  
  
    dtexecArgs = "/FILE ""C:\...\DtsClientWParamPkg.dtsx"""  
    dataReaderName = "DataReaderDest"  
    countryName = "Canada"  
  
    dtsConnection = New DtsConnection()  
    With dtsConnection  
      .ConnectionString = dtexecArgs  
      .Open()  
    End With  
  
    dtsCommand = New DtsCommand(dtsConnection)  
    dtsCommand.CommandText = dataReaderName  
  
    dtsParameter = New DtsDataParameter("Country", DbType.String)  
    dtsParameter.Direction = ParameterDirection.Input  
    dtsCommand.Parameters.Add(dtsParameter)  
  
    dtsParameter.Value = countryName  
  
    dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default)  
  
    With dtsDataReader  
      .Read()  
      txtResults.Text = .GetInt32(0).ToString("N0")  
    End With  
  
    'After reaching the end of data rows,  
    ' call the Read method one more time.  
    Try  
      dtsDataReader.Read()  
    Catch ex As Exception  
      MessageBox.Show("Exception on final call to Read method:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception on final call to Read method", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    ' The following method is a best practice, and is  
    '  required when using DtsDataParameter objects.  
    dtsCommand.Dispose()  
  
    Try  
      dtsDataReader.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing DataReader:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing DataReader", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Try  
      dtsConnection.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing connection:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing connection", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Windows.Forms.Cursor.Current = Cursors.Default  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Data;  
using Microsoft.SqlServer.Dts.DtsClient;  
  
namespace DtsClientWParamCS  
{  
  public partial class Form1 : Form  
  {  
    public Form1()  
    {  
      InitializeComponent();  
      this.btnRun.Click += new System.EventHandler(this.btnRun_Click);  
    }  
  
    private void btnRun_Click(object sender, EventArgs e)  
    {  
      string dtexecArgs;  
      string dataReaderName;  
      string countryName;  
  
      DtsConnection dtsConnection;  
      DtsCommand dtsCommand;  
      IDataReader dtsDataReader;  
      DtsDataParameter dtsParameter;  
  
      Cursor.Current = Cursors.WaitCursor;  
  
      dtexecArgs = @"/FILE ""C:\...\DtsClientWParamPkg.dtsx""";  
      dataReaderName = "DataReaderDest";  
      countryName = "Canada";  
  
      dtsConnection = new DtsConnection();  
      {  
        dtsConnection.ConnectionString = dtexecArgs;  
        dtsConnection.Open();  
      }  
  
      dtsCommand = new DtsCommand(dtsConnection);  
      dtsCommand.CommandText = dataReaderName;  
  
      dtsParameter = new DtsDataParameter("Country", DbType.String);  
      dtsParameter.Direction = ParameterDirection.Input;  
      dtsCommand.Parameters.Add(dtsParameter);  
  
      dtsParameter.Value = countryName;  
  
      dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default);  
  
      {  
        dtsDataReader.Read();  
        txtResults.Text = dtsDataReader.GetInt32(0).ToString("N0");  
      }  
  
      //After reaching the end of data rows,  
      // call the Read method one more time.  
      try  
      {  
        dtsDataReader.Read();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception on final call to Read method:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception on final call to Read method", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      // The following method is a best practice, and is  
      //  required when using DtsDataParameter objects.  
      dtsCommand.Dispose();  
  
      try  
      {  
        dtsDataReader.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing DataReader:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing DataReader", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      try  
      {  
        dtsConnection.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing connection:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing connection", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      Cursor.Current = Cursors.Default;  
  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Unterschieden zwischen lokalen und Remote-Ausführung](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Programmgesteuerten laden und Ausführen eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Programmgesteuertes Laden und Ausführen eines Remotepakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  

