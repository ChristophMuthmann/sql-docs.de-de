---
title: Working with Excel Files with the Script Task | Microsoft Docs
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
- Script task [Integration Services], Excel files
- Script task [Integration Services], examples
- Excel [Integration Services]
ms.assetid: b8fa110a-2c9c-4f5a-8fe1-305555640e44
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 46bf53c35663393ad600f02600961cf0295386bf
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-excel-files-with-the-script-task"></a>Arbeiten mit Excel-Dateien mit dem Skripttask
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt den Excel-Verbindungs-Manager, die Excel-Quelle und das Excel-Ziel zum Arbeiten mit den in Kalkulationstabellen gespeicherten Daten im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel-Dateiformat bereit. Die in diesem Thema beschriebenen Verfahren verwenden den Skripttask zum Abrufen von Informationen über verfügbare Excel-Datenbanken (Arbeitsmappendateien) und -Tabellen (Arbeitsmappen und benannte Bereiche). Diese Beispiele können leicht geändert werden, um mit einer der anderen vom [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB-Anbieter unterstützten dateibasierten Datenquellen zu arbeiten.  
  
 [Konfigurieren eines Pakets zum Testen der Beispiele](#configuring)  
  
 [Beispiel 1: Überprüfen Sie, ob eine Excel-Datei vorhanden ist.](#example1)  
  
 [Beispiel 2: Überprüfen Sie, ob eine Excel-Tabelle vorhanden ist.](#example2)  
  
 [Beispiel 3: Abrufen einer Liste von Excel-Dateien in einem Ordner](#example3)  
  
 [Beispiel 4: Abrufen einer Liste von Tabellen in einer Excel-Datei](#example4)  
  
 [Zum Anzeigen der Ergebnisse der Beispiele](#testing)  
  
> [!NOTE]  
>  Wenn Sie einen Task erstellen möchten, den Sie einfacher in mehreren Paketen wiederverwenden können, empfiehlt es sich, den Code in diesem Skripttaskbeispiel als Ausgangspunkt für einen benutzerdefinierten Task zu verwenden. Weitere Informationen finden Sie unter [Entwickeln eines benutzerdefinierten Tasks](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
##  <a name="configuring"></a>Konfigurieren eines Pakets zum Testen der Beispiele  
 Sie können ein einzelnes Paket konfigurieren, um alle Beispiele in diesem Thema zu testen. In den Beispielen werden oft die gleichen Paketvariablen und die gleichen [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Klassen verwendet.  
  
#### <a name="to-configure-a-package-for-use-with-the-examples-in-this-topic"></a>So konfigurieren Sie ein Paket zur Verwendung mit den in diesem Thema beschriebenen Beispielen  
  
1.  Erstellen Sie in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ein neues [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]-Projekt, und öffnen Sie das Standardpaket für die Bearbeitung.  
  
2.  **Variablen**. Öffnen der **Variablen** Fenster und definieren Sie die folgenden Variablen:  
  
    -   `ExcelFile`, des Typs **Zeichenfolge**. Geben Sie den vollständigen Pfad zu einer vorhandenen Excel-Arbeitsmappe und den zugehörigen Dateinamen ein.  
  
    -   `ExcelTable`, des Typs **Zeichenfolge**. Geben Sie den Namen eines vorhandenen Arbeitsblatts oder eines benannten Bereichs in der Arbeitsmappe ein, der im Wert der `ExcelFile`-Variablen genannt wird. Bei diesem Wert wird die Groß-/Kleinschreibung beachtet.  
  
    -   `ExcelFileExists`, des Typs **booleschen**.  
  
    -   `ExcelTableExists`, des Typs **booleschen**.  
  
    -   `ExcelFolder`, des Typs **Zeichenfolge**. Geben Sie den vollständigen Pfad eines Ordners ein, der mindestens eine Excel-Arbeitsmappe enthält.  
  
    -   `ExcelFiles`, des Typs **Objekt**.  
  
    -   `ExcelTables`, des Typs **Objekt**.  
  
3.  **Imports-Anweisungen**. Für die meisten Codebeispiele müssen am Anfang der Skriptdatei einer oder beide der folgenden [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Namespaces importiert werden:  
  
    -   **System.IO**, für Dateisystemvorgänge.  
  
    -   **"System.Data.OleDb"**, um Excel-Dateien als Datenquellen zu öffnen.  
  
4.  **Verweise**. Die Codebeispiele, die Schemainformationen aus Excel-Dateien gelesen erfordern einen zusätzlichen Verweis im skriptprojekt für den **"System.xml"** Namespace.  
  
5.  Legen Sie die Standardskriptsprache für die Skriptkomponente mithilfe der **Skriptsprache** option die **allgemeine** auf der Seite der **Optionen** (Dialogfeld). Weitere Informationen finden Sie unter [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
##  <a name="example1"></a>Beschreibung zu Beispiel 1: Überprüfen Sie, ob eine Excel-Datei vorhanden ist.  
 In diesem Beispiel wird überprüft, ob die von der `ExcelFile`-Variable angegebene Excel-Arbeitsmappendatei vorhanden ist. Daraufhin wird der boolesche Wert der `ExcelFileExists`-Variable auf das Ergebnis festgelegt. Sie können diesen booleschen Wert im Workflow des Pakets zur Verzweigung verwenden.  
  
#### <a name="to-configure-this-script-task-example"></a>So konfigurieren Sie dieses Skripttaskbeispiel  
  
1.  Das Paket einen neuen Skripttask hinzu, und ändern Sie den Namen in **ExcelFileExists**.  
  
2.  In der **Skripttask-Editor**auf die **Skript** auf **ReadOnlyVariables** , und geben Sie den Eigenschaftswert mit einer der folgenden Methoden:  
  
    -   Typ **ExcelFile**.  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** wählen Sie im Dialogfeld die **ExcelFile** Variable.  
  
3.  Klicken Sie auf **ReadWriteVariables** , und geben Sie den Eigenschaftswert mit einer der folgenden Methoden:  
  
    -   Typ **ExcelFileExists**.  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** wählen Sie im Dialogfeld die **ExcelFileExists** Variable.  
  
4.  Klicken Sie auf **Bearbeitungsskript** auf den Skripteditor zu öffnen.  
  
5.  Hinzufügen einer **Importe** -Anweisung für die **System.IO** -Namespace am Anfang der Skriptdatei.  
  
6.  Fügen Sie den folgenden Code hinzu.  
  
### <a name="example-1-code"></a>Beispiel 1-Code  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    If File.Exists(fileToTest) Then  
      Dts.Variables("ExcelFileExists").Value = True  
    Else  
      Dts.Variables("ExcelFileExists").Value = False  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    string fileToTest;  
  
    fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
    if (File.Exists(fileToTest))  
    {  
      Dts.Variables["ExcelFileExists"].Value = true;  
    }  
    else  
    {  
      Dts.Variables["ExcelFileExists"].Value = false;  
    }  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
##  <a name="example2"></a>Beschreibung zu Beispiel 2: Überprüfen Sie, ob eine Excel-Tabelle vorhanden ist.  
 In diesem Beispiel wird überprüft, ob das in der `ExcelTable`-Variable angegebene Excel-Arbeitsblatt bzw. der benannte Bereich in der Excel-Arbeitsmappendatei vorhanden ist, die in der `ExcelFile`-Variable angegeben wurde. Daraufhin wird der boolesche Wert der `ExcelTableExists`-Variable auf das Ergebnis festgelegt. Sie können diesen booleschen Wert im Workflow des Pakets zur Verzweigung verwenden.  
  
#### <a name="to-configure-this-script-task-example"></a>So konfigurieren Sie dieses Skripttaskbeispiel  
  
1.  Das Paket einen neuen Skripttask hinzu, und ändern Sie den Namen in **ExcelTableExists**.  
  
2.  In der **Skripttask-Editor**auf die **Skript** auf **ReadOnlyVariables** , und geben Sie den Eigenschaftswert mit einer der folgenden Methoden:  
  
    -   Typ **ExcelTable** und **ExcelFile** durch Kommas getrennt**.**  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** wählen Sie im Dialogfeld die **ExcelTable** und **ExcelFile** Variablen.  
  
3.  Klicken Sie auf **ReadWriteVariables** , und geben Sie den Eigenschaftswert mit einer der folgenden Methoden:  
  
    -   Typ **ExcelTableExists**.  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** wählen Sie im Dialogfeld die **ExcelTableExists** Variable.  
  
4.  Klicken Sie auf **Bearbeitungsskript** auf den Skripteditor zu öffnen.  
  
5.  Hinzufügen eines Verweises auf die **"System.xml"** Assembly im skriptprojekt.  
  
6.  Hinzufügen **Importe** -Anweisungen für die **System.IO** und **"System.Data.OleDb"** Namespaces am Anfang der Skriptdatei.  
  
7.  Fügen Sie den folgenden Code hinzu.  
  
### <a name="example-2-code"></a>Beispiel 2-Code  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
    Dim tableToTest As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim excelTables As DataTable  
    Dim excelTable As DataRow  
    Dim currentTable As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    tableToTest = Dts.Variables("ExcelTable").Value.ToString  
  
    Dts.Variables("ExcelTableExists").Value = False  
    If File.Exists(fileToTest) Then  
      connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=" & fileToTest & _  
        ";Extended Properties=Excel 8.0"  
      excelConnection = New OleDbConnection(connectionString)  
      excelConnection.Open()  
      excelTables = excelConnection.GetSchema("Tables")  
      For Each excelTable In excelTables.Rows  
        currentTable = excelTable.Item("TABLE_NAME").ToString  
        If currentTable = tableToTest Then  
          Dts.Variables("ExcelTableExists").Value = True  
        End If  
      Next  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
    public void Main()  
        {  
            string fileToTest;  
            string tableToTest;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable excelTables;  
            string currentTable;  
  
            fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
            tableToTest = Dts.Variables["ExcelTable"].Value.ToString();  
  
            Dts.Variables["ExcelTableExists"].Value = false;  
            if (File.Exists(fileToTest))  
            {  
                connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" +  
                "Data Source=" + fileToTest + ";Extended Properties=Excel 8.0";  
                excelConnection = new OleDbConnection(connectionString);  
                excelConnection.Open();  
                excelTables = excelConnection.GetSchema("Tables");  
                foreach (DataRow excelTable in excelTables.Rows)  
                {  
                    currentTable = excelTable["TABLE_NAME"].ToString();  
                    if (currentTable == tableToTest)  
                    {  
                        Dts.Variables["ExcelTableExists"].Value = true;  
                    }  
                }  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
}  
```  
  
##  <a name="example3"></a>Beschreibung zu Beispiel 3: Abrufen einer Liste von Excel-Dateien in einem Ordner  
 In diesem Beispiel wird ein Array mit der Liste der Excel-Dateien aus dem Ordner gefüllt, der im Wert der `ExcelFolder`-Variable angegeben wurde. Das Array wird daraufhin in die `ExcelFiles`-Variable kopiert. Mithilfe des Foreach-Enumerators für Daten aus Variablen können die Dateien in dem Array durchlaufen werden.  
  
#### <a name="to-configure-this-script-task-example"></a>So konfigurieren Sie dieses Skripttaskbeispiel  
  
1.  Das Paket einen neuen Skripttask hinzu, und ändern Sie den Namen in **GetExcelFiles**.  
  
2.  Öffnen der **Skripttask-Editor**auf die **Skript** auf **ReadOnlyVariables** , und geben Sie den Eigenschaftswert mit einer der folgenden Methoden:  
  
    -   Typ **ExcelFolder**  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** Dialogfeld wählen die Variable ExcelFolder.  
  
3.  Klicken Sie auf **ReadWriteVariables** , und geben Sie den Eigenschaftswert mit einer der folgenden Methoden:  
  
    -   Typ **ExcelFiles**.  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** Dialogfeld wählen die Variable ExcelFiles.  
  
4.  Klicken Sie auf **Bearbeitungsskript** auf den Skripteditor zu öffnen.  
  
5.  Hinzufügen einer **Importe** -Anweisung für die **System.IO** -Namespace am Anfang der Skriptdatei.  
  
6.  Fügen Sie den folgenden Code hinzu.  
  
### <a name="example-3-code"></a>Beispiel 3-Code  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const FILE_PATTERN As String = "*.xls"  
  
    Dim excelFolder As String  
    Dim excelFiles As String()  
  
    excelFolder = Dts.Variables("ExcelFolder").Value.ToString  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN)  
  
    Dts.Variables("ExcelFiles").Value = excelFiles  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    const string FILE_PATTERN = "*.xls";  
  
    string excelFolder;  
    string[] excelFiles;  
  
    excelFolder = Dts.Variables["ExcelFolder"].Value.ToString();  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN);  
  
    Dts.Variables["ExcelFiles"].Value = excelFiles;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
### <a name="alternate-solution"></a>Alternative Lösung  
 Anstelle eines Skripttasks können Sie zum Sammeln einer Liste von Excel-Arbeitsmappen in einem Array auch den Foreach-Dateienumerator verwenden, um alle Excel-Dateien in einem Ordner zu durchlaufen. Weitere Informationen finden Sie unter [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
##  <a name="example4"></a>Beschreibung zu Beispiel 4: Abrufen einer Liste von Tabellen in einer Excel-Datei  
 In diesem Beispiel wird ein Array mit der Liste der Arbeitsmappen und benannten Bereiche in der Excel-Arbeitsmappendatei gefüllt, der im Wert der `ExcelFile`-Variable angegeben wurde. Das Array wird daraufhin in die `ExcelTables`-Variable kopiert. Mithilfe des Foreach-Enumerators für Daten aus Variablen können die Tabellen in dem Array durchlaufen werden.  
  
> [!NOTE]  
>  Die Liste der Tabellen in einer Excel-Arbeitsmappe schließt sowohl Arbeitsmappen (diese weisen das Suffix $ auf) als auch benannte Bereiche ein. Wenn Sie die Liste nach nur Arbeitsmappen oder nach nur benannten Bereichen filtern müssen, müssen Sie zu diesem Zweck möglicherweise zusätzlichen Code hinzufügen.  
  
#### <a name="to-configure-this-script-task-example"></a>So konfigurieren Sie dieses Skripttaskbeispiel  
  
1.  Das Paket einen neuen Skripttask hinzu, und ändern Sie den Namen in **GetExcelTables**.  
  
2.  Öffnen der **Skripttask-Editor**auf die **Skript** auf **ReadOnlyVariables** , und geben Sie den Eigenschaftswert mit einer der folgenden Methoden:  
  
    -   Typ **ExcelFile**.  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** Dialogfeld Feld, wählen Sie die Variable ExcelFile.  
  
3.  Klicken Sie auf **ReadWriteVariables** , und geben Sie den Eigenschaftswert mit einer der folgenden Methoden:  
  
    -   Typ **ExcelTables**.  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** Dialogfeld wählen die ExcelTablesvariable.  
  
4.  Klicken Sie auf **Bearbeitungsskript** auf den Skripteditor zu öffnen.  
  
5.  Hinzufügen eines Verweises auf die **"System.xml"** Namespace im skriptprojekt.  
  
6.  Hinzufügen einer **Importe** -Anweisung für die **"System.Data.OleDb"** -Namespace am Anfang der Skriptdatei.  
  
7.  Fügen Sie den folgenden Code hinzu.  
  
### <a name="example-4-code"></a>Code zu Beispiel 4  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim excelFile As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim tablesInFile As DataTable  
    Dim tableCount As Integer = 0  
    Dim tableInFile As DataRow  
    Dim currentTable As String  
    Dim tableIndex As Integer = 0  
  
    Dim excelTables As String()  
  
    excelFile = Dts.Variables("ExcelFile").Value.ToString  
    connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=" & excelFile & _  
        ";Extended Properties=Excel 8.0"  
    excelConnection = New OleDbConnection(connectionString)  
    excelConnection.Open()  
    tablesInFile = excelConnection.GetSchema("Tables")  
    tableCount = tablesInFile.Rows.Count  
    ReDim excelTables(tableCount - 1)  
    For Each tableInFile In tablesInFile.Rows  
      currentTable = tableInFile.Item("TABLE_NAME").ToString  
      excelTables(tableIndex) = currentTable  
      tableIndex += 1  
    Next  
  
    Dts.Variables("ExcelTables").Value = excelTables  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            string excelFile;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable tablesInFile;  
            int tableCount = 0;  
            string currentTable;  
            int tableIndex = 0;  
  
            string[] excelTables = new string[5];  
  
            excelFile = Dts.Variables["ExcelFile"].Value.ToString();  
            connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" +  
                "Data Source=" + excelFile + ";Extended Properties=Excel 8.0";  
            excelConnection = new OleDbConnection(connectionString);  
            excelConnection.Open();  
            tablesInFile = excelConnection.GetSchema("Tables");  
            tableCount = tablesInFile.Rows.Count;  
  
            foreach (DataRow tableInFile in tablesInFile.Rows)  
            {  
                currentTable = tableInFile["TABLE_NAME"].ToString();  
                excelTables[tableIndex] = currentTable;  
                tableIndex += 1;  
            }  
  
            Dts.Variables["ExcelTables"].Value = excelTables;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
### <a name="alternate-solution"></a>Alternative Lösung  
 Anstelle eines Skripttasks können Sie zum Sammeln einer Liste von Excel-Arbeitsmappen in einem Array auch den Enumerator für das Foreach-ADO.NET-Schemarowset verwenden, um alle Tabellen (d. h. Arbeitsmappen und benannte Bereiche) in einer Excel-Arbeitsmappendatei zu durchlaufen. Weitere Informationen finden Sie unter [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
##  <a name="testing"></a>Zum Anzeigen der Ergebnisse der Beispiele  
 Wenn Sie alle Beispiele dieses Themas im selben Paket konfiguriert haben, können Sie alle Skripttasks mit einem zusätzlichen Skripttask verbinden, der die Ausgaben aller Beispiele anzeigt.  
  
#### <a name="to-configure-a-script-task-to-display-the-output-of-the-examples-in-this-topic"></a>So konfigurieren Sie einen Skripttask zum Anzeigen der Ausgabe der in diesem Thema behandelten Beispiele  
  
1.  Das Paket einen neuen Skripttask hinzu, und ändern Sie den Namen in **DisplayResults**.  
  
2.  Verbinden Sie alle vier beispielskripttasks miteinander, damit jede Aufgabe ausgeführt wird, nach dem erfolgreichen des vorhergehenden Tasks Abschluss, und verbinden Sie den vierten Beispieltask mit dem **DisplayResults** Aufgabe.  
  
3.  Öffnen der **DisplayResults** Aufgabe der **Skripttask-Editor**.  
  
4.  Auf der **Skript** auf **ReadOnlyVariables** und verwenden Sie eine der folgenden Methoden alle sieben aufgeführten Variablen hinzufügen [Konfigurieren eines Pakets zum Testen der Beispiele](#configuring):  
  
    -   Geben Sie den Namen jeder Variable durch Trennzeichen getrennt ein.  
  
         -oder-  
  
    -   Klicken Sie auf die Auslassungspunkte (**...** ) Schaltfläche neben dem Eigenschaftsfeld, und in der **Variablen auswählen** (Dialogfeld), die Variablen.  
  
5.  Klicken Sie auf **Bearbeitungsskript** auf den Skripteditor zu öffnen.  
  
6.  Hinzufügen **Importe** -Anweisungen für die **Microsoft.VisualBasic** und **"System.Windows.Forms"** Namespaces am Anfang der Skriptdatei.  
  
7.  Fügen Sie den folgenden Code hinzu.  
  
8.  Führen Sie das Paket aus, und überprüfen Sie die in dem Meldungsfeld angezeigten Ergebnisse.  
  
### <a name="code-to-display-the-results"></a>Code zum Anzeigen der Ergebnisse  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const EOL As String = ControlChars.CrLf  
  
    Dim results As String  
    Dim filesInFolder As String()  
    Dim fileInFolder As String  
    Dim tablesInFile As String()  
    Dim tableInFile As String  
  
    results = _  
      "Final values of variables:" & EOL & _  
      "ExcelFile: " & Dts.Variables("ExcelFile").Value.ToString & EOL & _  
      "ExcelFileExists: " & Dts.Variables("ExcelFileExists").Value.ToString & EOL & _  
      "ExcelTable: " & Dts.Variables("ExcelTable").Value.ToString & EOL & _  
      "ExcelTableExists: " & Dts.Variables("ExcelTableExists").Value.ToString & EOL & _  
      "ExcelFolder: " & Dts.Variables("ExcelFolder").Value.ToString & EOL & _  
      EOL  
  
    results &= "Excel files in folder: " & EOL  
    filesInFolder = DirectCast(Dts.Variables("ExcelFiles").Value, String())  
    For Each fileInFolder In filesInFolder  
      results &= " " & fileInFolder & EOL  
    Next  
    results &= EOL  
  
    results &= "Excel tables in file: " & EOL  
    tablesInFile = DirectCast(Dts.Variables("ExcelTables").Value, String())  
    For Each tableInFile In tablesInFile  
      results &= " " & tableInFile & EOL  
    Next  
  
    MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information)  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            const string EOL = "\r";  
  
            string results;  
            string[] filesInFolder;  
            //string fileInFolder;  
            string[] tablesInFile;  
            //string tableInFile;  
  
            results = "Final values of variables:" + EOL + "ExcelFile: " + Dts.Variables["ExcelFile"].Value.ToString() + EOL + "ExcelFileExists: " + Dts.Variables["ExcelFileExists"].Value.ToString() + EOL + "ExcelTable: " + Dts.Variables["ExcelTable"].Value.ToString() + EOL + "ExcelTableExists: " + Dts.Variables["ExcelTableExists"].Value.ToString() + EOL + "ExcelFolder: " + Dts.Variables["ExcelFolder"].Value.ToString() + EOL + EOL;  
  
            results += "Excel files in folder: " + EOL;  
            filesInFolder = (string[])(Dts.Variables["ExcelFiles"].Value);  
            foreach (string fileInFolder in filesInFolder)  
            {  
                results += " " + fileInFolder + EOL;  
            }  
            results += EOL;  
  
            results += "Excel tables in file: " + EOL;  
            tablesInFile = (string[])(Dts.Variables["ExcelTables"].Value);  
            foreach (string tableInFile in tablesInFile)  
            {  
                results += " " + tableInFile + EOL;  
            }  
  
            MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  

