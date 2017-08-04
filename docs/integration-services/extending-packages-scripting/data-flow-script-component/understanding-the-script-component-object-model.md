---
title: Grundlegendes zu den Script Component Object Model | Microsoft Docs
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
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 09de00344fe94087b6287b07c4b1ffe933d27b7c
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="understanding-the-script-component-object-model"></a>Grundlegendes zum Skript-Komponentenobjektmodell
  Entsprechend der Anleitung unter [codieren und Debuggen der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md), skriptkomponentenprojekt enthält drei Projektelemente:  
  
1.  Die **ScriptMain** Element, das enthält die **ScriptMain** Klasse, die in dem Sie Ihren Code schreiben. Die **ScriptMain** Klasse erbt von der **UserComponent** Klasse.  
  
2.  Die **ComponentWrapper** Element, das enthält die **UserComponent** Klasse, eine Instanz von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> , enthält die Methoden und Eigenschaften, die Sie zum Verarbeiten von Daten und für die Interaktion mit dem Paket verwenden. Die **ComponentWrapper** -Element enthält auch **Verbindungen** und **Variablen** Auflistungsklassen.  
  
3.  Die **BufferWrapper** Element, das enthält Klassen, die von erben <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> für jedes Eingabe- und Ausgabe und typisierte Eigenschaften für jede Spalte.  
  
 Schreiben von Code in der **ScriptMain** Element, verwenden Sie die Objekte, Methoden und Eigenschaften, die in diesem Thema erläutert. Es werden nicht von jeder Komponente alle hier aufgeführten Methoden verwendet. Wenn sie jedoch verwendet werden, geschieht dies in der gezeigten Reihenfolge.  
  
 Die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse enthält keinen Implementierungscode für die in diesem Thema erläuterten Methoden. Es ist daher unnötig, aber ungefährlich, Ihrer eigenen Implementierung der Methode einen Aufruf der Basisklassenimplementierung hinzuzufügen.  
  
 Informationen dazu, wie die Methoden und Eigenschaften dieser Klassen in einem bestimmten Typ von Skriptkomponente verwenden, finden Sie im Abschnitt [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Die Beispielthemen enthalten auch vollständige Codebeispiele.  
  
## <a name="acquireconnections-method"></a>‚AcquireConnections’-Methode  
 Quellen und Ziele müssen im Allgemeinen eine Verbindung mit einer externen Datenquelle herstellen. Überschreiben Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse, um die Verbindung oder die Verbindungsinformationen von dem entsprechenden Verbindungs-Manager abzurufen.  
  
 Das folgende Beispiel gibt eine **System.Data.SqlClient.SqlConnection** aus einen ADO.NET-Verbindungs-Manager.  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 Im folgenden Beispiel gibt einen vollständigen Pfad und Dateinamen aus einem Flat File Connection Manager, und öffnet dann die Datei mithilfe einer **System.IO.StreamReader**.  
  
```vb  
Private textReader As StreamReader  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    Dim connMgr As IDTSConnectionManager100 = _  
        Me.Connections.MyFlatFileSrcConnectionManager  
    Dim exportedAddressFile As String = _  
        CType(connMgr.AcquireConnection(Nothing), String)  
    textReader = New StreamReader(exportedAddressFile)  
  
End Sub  
```  
  
## <a name="preexecute-method"></a>‚PreExecute’-Methode  
 Überschreiben Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PreExecute%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse immer dann, wenn Sie eine Verarbeitung nur einmal durchführen müssen, bevor Sie die Verarbeitung einer Datenzeile starten. In einem Ziel können Sie beispielsweise den parametrisierten Befehl, den das Ziel verwendet, so konfigurieren, dass jede Datenzeile in die Datenquelle eingefügt wird.  
  
```vb  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
...  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
```  
  
```csharp  
SqlConnection sqlConn;   
SqlCommand sqlCmd;   
SqlParameter sqlParam;   
  
public override void PreExecute()   
{   
  
    sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " + "VALUES(@addressid, @city)", sqlConn);   
    sqlParam = new SqlParameter("@addressid", SqlDbType.Int);   
    sqlCmd.Parameters.Add(sqlParam);   
    sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);   
    sqlCmd.Parameters.Add(sqlParam);   
  
}  
```  
  
## <a name="processing-inputs-and-outputs"></a>Verarbeiten von Eingaben und Ausgaben  
  
### <a name="processing-inputs"></a>Verarbeiten von Eingaben  
 Skriptkomponenten, die als Transformationen oder Ziele konfiguriert sind, weisen eine Eingabe auf.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>Bereitstellungen durch das ‚BufferWrapper’-Projektelement  
 Für die einzelnen Eingabeargumente sortiert, dass Sie konfiguriert haben, die **BufferWrapper** Projektelement enthält eine Klasse, die abgeleitet <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> und hat den gleichen Namen wie die Eingabe. Jede Eingabepufferklasse enthält die folgenden Eigenschaften, Funktionen und Methoden:  
  
-   Benannte, typisierte Accessoreigenschaften für jede ausgewählte Eingabespalte. Diese Eigenschaften sind schreibgeschützt oder Lese-/Schreibzugriff, je nach den **Verwendungstyp** für die Spalte angegeben wird, auf die **Eingabespalten** auf der Seite der **Skript Transformations-Editor**.  
  
-   Ein  **\<Spalte > _IsNull** input-Eigenschaft für jede ausgewählte Spalte. Diese Eigenschaft wird auch nur-Lese oder Lese-/Schreibzugriff, je nach den **Verwendungstyp** für die Spalte angegeben.  
  
-   Ein **DirectRowTo\<Outputbuffer >** -Methode für jede konfigurierte Ausgabe. Verwenden Sie diese Methoden beim Filtern von Zeilen in eine von mehreren Ausgaben in der gleichen **ExclusionGroup**.  
  
-   Ein **NextRow** Funktion, um die nächste Eingabezeile abzurufen und ein **EndOfRowset** Funktion, um zu bestimmen, ob der letzte Datenpuffer verarbeitet wurde. Diese Funktionen ist in der Regel nicht erforderlich, wenn Sie in implementierten eingabeverarbeitungsmethoden verwenden die **UserComponent** Basisklasse. Der nächste Abschnitt enthält weitere Informationen zu den **UserComponent** Basisklasse.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>Bereitstellungen durch das ‚ComponentWrapper’-Projektelement  
 Das ComponentWrapper-Projektelement enthält eine Klasse namens **UserComponent** abgeleitet, die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. Die **ScriptMain** Klasse, die in dem Sie Ihren benutzerdefinierten Code schreiben leitet sich wiederum von **UserComponent**. Die **UserComponent** Klasse enthält die folgenden Methoden:  
  
-   Eine überschriebene Implementierung von der **ProcessInput** Methode. Dies ist die Methode, dass das Modul ruft weiter zur Laufzeit nach der Datenfluss der **PreExecute** -Methode, und es kann mehrfach aufgerufen werden. **ProcessInput** übergibt die Verarbeitung an die  **\<Inputbuffer > _ProcessInput** Methode. Die **ProcessInput** Methode für das Ende des Eingabepuffers überprüft, und wenn das Ende des Puffers erreicht wurde, ruft Sie die überschreibbare **FinishOutputs** -Methode und die Private **MarkOutputsAsFinished** Methode. Die **MarkOutputsAsFinished** -Methode ruft dann **SetEndOfRowset** für den letzten Ausgabepuffer.  
  
-   Eine überschreibbare Implementierung von der  **\<Inputbuffer > _ProcessInput** Methode. Diese Standardimplementierung durchläuft einfach jede Eingabezeile und ruft  **\<Inputbuffer > _ProcessInputRow**.  
  
-   Eine überschreibbare Implementierung von der  **\<Inputbuffer > _ProcessInputRow** Methode. Der Standardimplementierung ist leer. Dies ist die Methode, die Sie normalerweise überschreiben, um den benutzerdefinierten Datenverarbeitungscode zu schreiben.  
  
#### <a name="what-your-custom-code-should-do"></a>Schritte, die der benutzerdefinierte Code ausführen sollte  
 Sie können die folgenden Methoden verwenden, beim Verarbeiten der Eingabe in die **ScriptMain** Klasse:  
  
-   Überschreiben Sie  **\<Inputbuffer > _ProcessInputRow** zum Verarbeiten der Daten in jeder Eingabezeile, beim Durchlaufen verändern.  
  
-   Überschreiben Sie  **\<Inputbuffer > _ProcessInput** nur, wenn Sie etwas zusätzliche beim Durchlaufen der Eingabezeilen tun. (Sie müssen z. B. für testen **EndOfRowset** auf um andere Maßnahmen zu ergreifen, nachdem alle Zeilen verarbeitet wurden.) Rufen Sie  **\<Inputbuffer > _ProcessInputRow** um die zeilenverarbeitung auszuführen.  
  
-   Überschreiben Sie **FinishOutputs** wenn etwas, um die Ausgaben erfordern, bevor sie geschlossen werden.  
  
 Die **ProcessInput** Methode wird sichergestellt, dass diese Methoden zu den entsprechenden Zeitpunkten aufgerufen werden.  
  
### <a name="processing-outputs"></a>Verarbeiten von Ausgaben  
 Skriptkomponenten, die als Quellen oder Transformationen konfiguriert sind, weisen mindestens eine Eingabe auf.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>Bereitstellungen durch das ‚BufferWrapper’-Projektelement  
 Für jede von Ihnen konfigurierte Ausgabe enthält das BufferWrapper-Projektelement eine Klasse, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> abgeleitet ist und denselben Namen hat wie die Ausgabe. Jede Eingabepufferklasse enthält die folgenden Eigenschaften und Methoden:  
  
-   Benannte, typisierte, lesegeschützte Accessoreigenschaften für jede ausgewählte Ausgabespalte.  
  
-   Ein lesegeschütztes  **\<Spalte > _IsNull** -Eigenschaft für jede ausgewählte Ausgabespalte, die Sie verwenden können, um den Spaltenwert auf festgelegt **null**.  
  
-   Ein **AddRow** Methode, um in den Ausgabepuffer eine leere neue Zeile hinzuzufügen.  
  
-   Ein **SetEndOfRowset** Methode, um das Datenflussmodul wissen, dass keine weiteren Datenpuffer erwartet werden. Es gibt auch eine **EndOfRowset** Funktion, um zu bestimmen, ob der aktuelle Puffer der letzte Datenpuffer ist. Diese Funktionen ist in der Regel nicht erforderlich, wenn Sie in implementierten eingabeverarbeitungsmethoden verwenden die **UserComponent** Basisklasse.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>Bereitstellungen durch das ‚ComponentWrapper’-Projektelement  
 Das ComponentWrapper-Projektelement enthält eine Klasse namens **UserComponent** abgeleitet, die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. Die **ScriptMain** Klasse, die in dem Sie Ihren benutzerdefinierten Code schreiben leitet sich wiederum von **UserComponent**. Die **UserComponent** Klasse enthält die folgenden Methoden:  
  
-   Eine überschriebene Implementierung von der **PrimeOutput** Methode. Das Datenflussmodul ruft diese Methode vor **ProcessInput** zur Laufzeit, und es wird nur einmal aufgerufen. **PrimeOutput** übergibt die Verarbeitung an die **CreateNewOutputRows** Methode. Klicken Sie dann, wenn die Komponente eine Quelle handelt (d. h. die Komponente weist keine Eingaben), **PrimeOutput** Ruft die überschreibbare **FinishOutputs** -Methode und die Private **MarkOutputsAsFinished** Methode. Die **MarkOutputsAsFinished** Methodenaufrufe **SetEndOfRowset** für den letzten Ausgabepuffer.  
  
-   Eine überschreibbare Implementierung von der **CreateNewOutputRows** Methode. Der Standardimplementierung ist leer. Dies ist die Methode, die Sie normalerweise überschreiben, um den benutzerdefinierten Datenverarbeitungscode zu schreiben.  
  
#### <a name="what-your-custom-code-should-do"></a>Schritte, die der benutzerdefinierte Code ausführen sollte  
 Sie können die folgenden Methoden zum Verarbeiten von Ausgaben in den **ScriptMain** Klasse:  
  
-   Überschreiben Sie **CreateNewOutputRows** nur beim Hinzufügen und Auffüllen können Ausgabezeilen vor der Verarbeitung der Eingabezeilen. Beispielsweise können Sie **CreateNewOutputRows** in einer Datenquelle, jedoch in einer Transformation mit asynchronen Ausgaben, Sie sollten Aufrufen **AddRow** während oder nach der Verarbeitung der Eingabedaten.  
  
-   Überschreiben Sie **FinishOutputs** wenn etwas, um die Ausgaben erfordern, bevor sie geschlossen werden.  
  
 Die **PrimeOutput** Methode wird sichergestellt, dass diese Methoden zu den entsprechenden Zeitpunkten aufgerufen werden.  
  
## <a name="postexecute-method"></a>‚PostExecute’-Methode  
 Überschreiben Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse immer dann, wenn Sie eine Verarbeitung nur einmal durchführen müssen, nachdem Sie die Datenzeilen verarbeitet haben. Beispielsweise sollten Sie in einer Datenquelle, schließen Sie die **System.Data.SqlClient.SqlDataReader** zum Laden von Daten in den Datenfluss verwendet haben.  
  
> [!IMPORTANT]  
>  Die Auflistung der **ReadWriteVariables** steht nur in der **"PostExecute"** Methode. Sie können daher den Wert einer Paketvariablen nicht direkt inkrementieren, während Sie jede Datenzeile verarbeiten. Stattdessen den Wert einer lokalen Variablen, und legen Sie den Wert der Paketvariablen auf den Wert der lokalen Variablen in der **"PostExecute"** Methode auf, nachdem alle Daten wurden verarbeitet.  
  
## <a name="releaseconnections-method"></a>‚ReleaseConnections’-Methode  
 Quellen und Ziele müssen in der Regel mit einer externen Datenquelle verbinden. Überschreiben Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse, um die vorher in der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A>-Methode geöffnete Verbindung zu schließen und freizugeben.  
  
```vb  
    Dim connMgr As IDTSConnectionManager100  
...  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
```  
  
```csharp  
IDTSConnectionManager100 connMgr;  
  
public override void ReleaseConnections()  
{  
  
    connMgr.ReleaseConnection(sqlConn);  
  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [Beim Codieren und Debuggen der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
