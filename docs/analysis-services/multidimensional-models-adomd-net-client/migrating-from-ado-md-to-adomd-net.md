---
title: Migrieren von ADO MD zu ADOMD.NET | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, migrating to
- migrating ADO MD to ADOMD.NET
- ADO MD migration [ADOMD.NET]
ms.assetid: 8c760db3-c475-468e-948d-e5f599d985ad
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f487a18b188dad430c88531e82e747e9edf349f2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="migrating-from-ado-md-to-adomdnet"></a>Migrieren von ADO MD zu ADOMD.NET
  Die ADOMD.NET-Bibliothek ist ähnlich wie die ADO MD-Bibliothek (ActiveX Data Objects Multidimensional) eine Erweiterung der ADO-Bibliothek (ActiveX Data Objects), die verwendet wird, um auf mehrdimensionale Daten in COM-basierten (Component Object Model) Clientanwendungen zuzugreifen. ADO MD bietet einen einfachen Zugriff auf mehrdimensionale Daten aus nicht verwalteten Sprachen, wie C++ und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. ADOMD.NET bietet einen leichten Zugriff auf analytische (sowohl mehrdimensional als auch Data Mining) Daten aus verwalteten Sprachen, wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] C# und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET. Darüber hinaus stellt ADOMD.NET ein verbessertes Metadaten-Objektmodell bereit.  
  
 Die Migration bestehender Clientanwendungen von ADO MD auf ADOMD.NET ist leicht. Allerdings gibt es diverse wichtige Unterschiede in Bezug auf die Migration:  
  
 **Konnektivität und Datenzugriff für Clientanwendungen bereitstellen**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Erfordert Verweise auf sowohl Adodb.dll als auch Adomd.dll.|Erfordert einen einzelnen Verweis auf Microsoft.AnalysisServices.AdomdClient.dll.|  
  
 Zusätzlich zum Zugriff auf Metadaten stellt die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Klasse Konnektivitätsunterstützung bereit.  
  
 **Zum Abrufen von Metadaten für mehrdimensionale Objekte**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Verwenden Sie die Katalog-Klasse.|Verwenden Sie die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A>-Eigenschaft von <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.|  
  
 **Um Abfragen auszuführen, und geben Cellset-Objekte zurück**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Verwenden Sie die CellSet-Klasse.|Verwenden Sie die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Klasse.|  
  
 **Zugriff auf die Metadaten, die verwendet wird, um ein Cellset anzuzeigen**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Verwenden Sie die Position-Klasse.|Verwenden Sie die Objekte <xref:Microsoft.AnalysisServices.AdomdClient.Set> und <xref:Microsoft.AnalysisServices.AdomdClient.Tuple>.|  
  
> [!NOTE]  
>  Die <xref:Microsoft.AnalysisServices.AdomdClient.Position>-Klasse wird aus Gründen der Abwärtskompatibilität unterstützt.  
  
 **Miningmodell-Metadaten abrufen**  
 In ADO MD stehen keine Klassen zur Verfügung. Verwenden Sie in ADOMD.NET eine der Datamining-Auflistungen aus:  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> enthält eine Liste aller Miningmodelle in der Datenquelle.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> stellt Informationen über die verfügbaren Mining-Algorithmen bereit.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> macht Informationen über die Mining-Strukturen auf dem Server verfügbar.  
  
 Um diese Unterschiede herauszustellen, vergleicht das folgende Migrationsbeispiel eine bestehende ADO MD-Anwendung mit einer entsprechenden ADOMD.NET-Anwendung.  
  
## <a name="looking-at-a-migration-example"></a>Anschauen eines Migrationsbeispiels  
 Sowohl die vorhandenen ADO MD- als auch die entsprechenden ADOMD.NET-Codebeispiele, die in diesem Abschnitt angegeben sind, führen die gleichen Gruppen an Aktionen aus: Erstellen einer Verbindung, Ausführen einer MDX-Anweisung (Multidimensional Expressions) und Abrufen von Metadaten und Daten. Allerdings verwenden diese beiden Codesätze nicht die gleichen Objekte zur Ausführung dieser Tasks.  
  
### <a name="existing-ado-md-code"></a>Vorhandener ADO MD-Code  
 Die folgende, aus der ADO MD 2.8-Dokumentation entliehene Codebeispiel ist in geschrieben [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic® 6.0 und verwendet ADO MD zu veranschaulichen, wie eine Verbindung herstellen und Abfragen einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle. Dieses ADO MD-Beispiel verwendet die folgenden Objekte:  
  
-   Erstellt eine Verbindung aus einem **Katalog** Objekt.  
  
-   Führt die MDX (Multidimensional Expressions)-Anweisung mithilfe der **Cellset** Objekt.  
  
-   Ruft die Metadaten und Daten aus der **Position** Objekt abgerufen, die von der **Cellset** Objekt.  
  
```  
Private Sub cmdCellSettoDebugWindow_Click()  
Dim cat As New ADOMD.Catalog  
Dim cst As New ADOMD.Cellset  
Dim i As Integer  
Dim j As Integer  
Dim k As Integer  
Dim strServer As String  
Dim strSource As String  
Dim strColumnHeader As String  
Dim strRowText As String  
  
On Error GoTo Error_cmdCellSettoDebugWindow_Click  
Screen.MousePointer = vbHourglass  
'*-----------------------------------------------------------------------  
'* Set server to local host.  
'*-----------------------------------------------------------------------  
    strServer = "LOCALHOST"  
  
'*-----------------------------------------------------------------------  
'* Set MDX query string source.  
'*-----------------------------------------------------------------------  
    strSource = strSource & "SELECT "  
    strSource = strSource & "{[Measures].members} ON COLUMNS,"  
    strSource = strSource & _  
        "NON EMPTY [Store].[Store City].members ON ROWS"  
    strSource = strSource & " FROM Sales"  
  
'*-----------------------------------------------------------------------  
'* Set active connection.  
'*-----------------------------------------------------------------------  
        cat.ActiveConnection = "Data Source=" & strServer & _  
            ";Provider=msolap;"  
  
'*-----------------------------------------------------------------------  
'* Set cellset source to MDX query string.  
'*-----------------------------------------------------------------------  
        cst.Source = strSource  
  
'*-----------------------------------------------------------------------  
'* Set cellset active connection to current connection  
'*-----------------------------------------------------------------------  
    Set cst.ActiveConnection = cat.ActiveConnection  
  
'*-----------------------------------------------------------------------  
'* Open cellset.  
'*-----------------------------------------------------------------------  
    cst.Open  
  
'*-----------------------------------------------------------------------  
'* Allow space for row header text.  
'*-----------------------------------------------------------------------  
strColumnHeader = vbTab & vbTab & vbTab & vbTab & vbTab & vbTab  
  
'*-----------------------------------------------------------------------  
'* Loop through column headers.  
'*-----------------------------------------------------------------------  
       For i = 0 To cst.Axes(0).Positions.Count - 1  
            strColumnHeader = strColumnHeader & _  
                cst.Axes(0).Positions(i).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
       Next  
       Debug.Print vbTab & strColumnHeader & vbCrLf  
  
'*-----------------------------------------------------------------------  
'* Loop through row headers and provide data for each row.  
'*-----------------------------------------------------------------------  
        strRowText = ""  
        For j = 0 To cst.Axes(1).Positions.Count - 1  
            strRowText = strRowText & _  
                cst.Axes(1).Positions(j).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
            For k = 0 To cst.Axes(0).Positions.Count - 1  
                strRowText = strRowText & cst(k, j).FormattedValue & _  
                    vbTab & vbTab & vbTab & vbTab  
            Next  
            Debug.Print strRowText & vbCrLf  
            strRowText = ""  
        Next  
  
    Screen.MousePointer = vbDefault  
Exit Sub  
  
Error_cmdCellSettoDebugWindow_Click:  
   Beep  
   Screen.MousePointer = vbDefault  
   MsgBox "The following error has occurred:" & vbCrLf & _  
      Err.Description, vbCritical, " Error!"  
   Exit Sub  
End Sub  
```  
  
### <a name="equivalent-adomdnet-code"></a>Entsprechender ADOMD.NET-Code  
 Das folgende, in Visual Basic .NET und mittels ADOMD.NET geschriebene Beispiel veranschaulicht, wie die gleichen Aktionen ausgeführt werden wie bei dem zuvor genannten Visual Basic 6.0-Beispiel. Der Hauptunterschied zwischen dem folgenden Beispiel und dem zuvor genannten ADO MD-Beispiel liegt in den Objekten, die verwendet werden, um die Aktionen auszuführen. Das ADOMD.NET-Beispiel verwendet die folgenden Objekte:  
  
-   Erstellt eine Verbindung mit einer **AdomdConnection** Objekt.  
  
-   Führt die MDX-Anweisung mithilfe einer **AdomdCommand** Objekt.  
  
-   Ruft die Metadaten und Daten aus der **festgelegt** Objekt abgerufen, die von der **Cellset** Objekt.  
  
```  
Private Sub DisplayCellSetInOutputWindow()  
    Dim conn As AdomdConnection  
    Dim cmd As AdomdCommand  
    Dim cst As CellSet  
    Dim i As Integer  
    Dim j As Integer  
    Dim k As Integer  
    Dim strServer As String = "LOCALHOST"  
    Dim strSource As String = "SELECT [Measures].members ON COLUMNS, " & _  
        "NON EMPTY [Store].[Store City].members ON ROWS FROM SALES"  
    Dim strOutput As New System.IO.StringWriter  
  
    '*-----------------------------------------------------------------------  
    '* Open connection.  
    '*-----------------------------------------------------------------------  
    Try  
        ' Create a new AdomdConnection object, providing the connection  
        ' string.  
        conn = New AdomdConnection("Data Source=" & strServer & _  
        ";Provider=msolap;")  
        ' Open the connection.  
        conn.Open()  
    Catch ex As Exception  
        Throw New ApplicationException( _  
            "An error occurred while connecting.")  
    End Try  
  
    Try  
    '*-----------------------------------------------------------------------  
    '* Open cellset.  
    '*-----------------------------------------------------------------------  
        ' Create a new AdomdCommand object, providing the MDX query string.  
        cmd = New AdomdCommand(strSource, conn)  
        ' Run the command and return a CellSet object.  
        cst = cmd.ExecuteCellSet()  
  
    '*-----------------------------------------------------------------------  
    '* Concatenate output.  
    '*-----------------------------------------------------------------------  
  
    ' Include spacing to account for row headers.  
    strOutput.Write(vbTab, 6)  
  
    ' Iterate through the first axis of the CellSet object and  
    ' retrieve column headers.  
    For i = 0 To cst.Axes(0).Set.Tuples.Count - 1  
        strOutput.Write(cst.Axes(0).Set.Tuples(i).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
    Next  
    strOutput.WriteLine()  
  
    ' Iterate through the second axis of the CellSet object and  
    ' retrieve row headers and cell data.  
    For j = 0 To cst.Axes(1).Set.Tuples.Count - 1  
        ' Append the row header.  
        strOutput.Write(cst.Axes(1).Set.Tuples(j).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
  
        ' Append the cell data for that row.  
        For k = 0 To cst.Axes(0).Set.Tuples.Count - 1  
            strOutput.Write(cst.Cells(k, j).FormattedValue)  
            strOutput.Write(vbTab, 4)  
        Next  
        strOutput.WriteLine()  
    Next  
  
    ' Display the output.  
    Debug.WriteLine(strOutput.ToString)  
  
    '*-----------------------------------------------------------------------  
    '* Release resources.  
    '*-----------------------------------------------------------------------  
        conn.Close()  
    Catch ex As Exception  
        ' Ignore or handle errors.  
    Finally  
        cst = Nothing  
        cmd = Nothing  
        conn = Nothing  
    End Try  
End Sub  
```  
  
  

