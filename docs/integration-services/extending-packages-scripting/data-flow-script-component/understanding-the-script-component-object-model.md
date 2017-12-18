---
title: Grundlegendes zum Skript-Komponentenobjektmodell | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs: VB
helpviewer_keywords: Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fd9402f5ec9cdd85f2ccf45e09e4984b98ea1cc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="understanding-the-script-component-object-model"></a>Grundlegendes zum Skript-Komponentenobjektmodell
  Wie im Artikel [Coding and Debugging the Script Component (Codieren und Debuggen der Skriptkomponente)](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md) erläutert, enthält das Skriptkomponentenprojekt drei Projektelemente:  
  
1.  Das **ScriptMain**-Element, das die **ScriptMain**-Klasse enthält, in die Sie den Code schreiben. Die **ScriptMain**-Klasse erbt von der **UserComponent**-Klasse.  
  
2.  Das **ComponentWrapper**-Element, das die **UserComponent**-Klasse enthält, eine Instanz von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>, die die Methoden und Eigenschaften enthält, die Sie verwenden, um Daten zu verarbeiten und mit dem Paket zu interagieren. Das **ComponentWrapper**-Element enthält außerdem die Auflistungsklassen **Verbindungen** und **Variablen**.  
  
3.  Das **BufferWrapper**-Element, das Klassen enthält und von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> für jede Eingabe und Ausgabe sowie typisierte Eigenschaften für jede Spalte erbt.  
  
 Beim Schreiben des Codes in das **ScriptMain**-Element verwenden Sie die in diesem Artikel besprochenen Objekte, Methoden und Eigenschaften. Es werden nicht von jeder Komponente alle hier aufgeführten Methoden verwendet. Wenn sie jedoch verwendet werden, geschieht dies in der gezeigten Reihenfolge.  
  
 Die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse enthält keinen Implementierungscode für die in diesem Thema erläuterten Methoden. Es ist daher unnötig, aber ungefährlich, Ihrer eigenen Implementierung der Methode einen Aufruf der Basisklassenimplementierung hinzuzufügen.  
  
 Informationen darüber, wie die Methoden und Eigenschaften dieser Klassen in einem bestimmten Skriptkomponententyp zu verwenden sind, finden Sie im Abschnitt [Additional Script Component Examples (Zusätzliche Skriptkomponentenbeispiele)](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Die Beispielthemen enthalten auch vollständige Codebeispiele.  
  
## <a name="acquireconnections-method"></a>‚AcquireConnections’-Methode  
 Quellen und Ziele müssen im Allgemeinen eine Verbindung mit einer externen Datenquelle herstellen. Überschreiben Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse, um die Verbindung oder die Verbindungsinformationen von dem entsprechenden Verbindungs-Manager abzurufen.  
  
 Im folgenden Beispiel wird **System.Data.SqlClient.SqlConnection** von einem ADO.NET-Verbindungs-Manager zurückgegeben.  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 Das folgende Beispiel gibt einen vollständigen Pfad- und Dateinamen von einem Verbindungs-Manager für Flatfiles zurück und öffnet anschließend die Datei mithilfe von **System.IO.StreamReader**.  
  
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
 Für jede von Ihnen konfigurierte Ausgabe enthält das **BufferWrapper**-Projektelement eine Klasse, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> abgeleitet ist und denselben Namen hat wie die Eingabe. Jede Eingabepufferklasse enthält die folgenden Eigenschaften, Funktionen und Methoden:  
  
-   Benannte, typisierte Accessoreigenschaften für jede ausgewählte Eingabespalte. Diese Eigenschaften sind schreibgeschützt oder weisen Lese-/Schreibzugriff auf, abhängig von dem für die Spalte auf der Seite **Eingabespalten** des Dialogfelds **Transformations-Editor für Skripterstellung** angegebenen **Verwendungstyp**.  
  
-   Eine **\<column>_IsNull**-Eigenschaft für jede ausgewählte Eingabespalte. Diese Eigenschaft ist ebenfalls schreibgeschützt oder weist Lese-/Schreibzugriff auf, abhängig von dem für die Spalte angegebenen **Verwendungstyp**.  
  
-   Eine **DirectRowTo\<outputbuffer>**-Methode für jede konfigurierte Ausgabe. Sie verwenden diese Methoden beim Filtern von Zeilen in eine von mehreren Ausgaben in derselben **ExclusionGroup**.  
  
-   Eine **NextRow**-Funktion, um die nächste Eingabezeile abzurufen, und eine **EndOfRowset**-Funktion, um zu bestimmen, ob der letzte Datenpuffer verarbeitet wurde. Normalerweise benötigen Sie diese Funktionen nicht, wenn Sie die in der **UserComponent**-Basisklasse implementierten Eingabeverarbeitungsmethoden verwenden. Im nächsten Abschnitt finden Sie weitere Informationen über die **UserComponent**-Basisklasse.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>Bereitstellungen durch das ‚ComponentWrapper’-Projektelement  
 Das ComponentWrapper-Projektelement enthält eine Klasse mit dem Namen **UserComponent**, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> abgeleitet wird. Die **ScriptMain**-Klasse, in die Sie Ihren benutzerdefinierten Code schreiben, wird wiederum von **UserComponent** abgeleitet. Die **UserComponent**-Klasse enthält die folgenden Methoden:  
  
-   Eine überschriebene Implementierung der **ProcessInput**-Methode. Diese Methode wird vom Datenflussmodul zur Laufzeit direkt im Anschluss an die **PreExecute**-Methode aufgerufen, unter Umständen sogar mehrfach. **ProcessInput** übergibt die Verarbeitung an die **\<inputbuffer>_ProcessInput**-Methode. Anschließend sucht die**ProcessInput**-Methode nach dem Ende des Eingabepuffers. Wenn das Ende des Puffers erreicht wurde, ruft sie die überschreibbare**FinishOutputs**-Methode und die private **MarkOutputsAsFinished**-Methode auf. Die **MarkOutputsAsFinished**-Methode ruft dann auf dem letzten Ausgabepuffer **SetEndOfRowset** auf.  
  
-   Eine überschreibbare Implementierung der **\<inputbuffer>_ProcessInput**-Methode. Diese Standardimplementierung durchläuft jede Eingabezeile einmal und ruft **\<inputbuffer>_ProcessInputRow** auf.  
  
-   Eine überschreibbare Implementierung der **\<inputbuffer>_ProcessInputRow**-Methode. Der Standardimplementierung ist leer. Dies ist die Methode, die Sie normalerweise überschreiben, um den benutzerdefinierten Datenverarbeitungscode zu schreiben.  
  
#### <a name="what-your-custom-code-should-do"></a>Schritte, die der benutzerdefinierte Code ausführen sollte  
 Sie können mithilfe der folgenden Methoden Eingaben in die **ScriptMain**-Klasse verarbeiten:  
  
-   Überschreiben Sie **\<inputbuffer>_ProcessInputRow**, um die Daten in jeder Eingabezeile beim Durchlaufen zu verarbeiten.  
  
-   Überschreiben Sie **\<inputbuffer>_ProcessInput** nur dann, wenn Sie beim Durchlaufen der Eingabezeilen noch einen anderen Vorgang ausführen müssen. (Sie müssen beispielsweise **EndOfRowset** testen, um andere Maßnahmen zu ergreifen, nachdem alle Zeilen verarbeitet wurden.) Rufen Sie **\<inputbuffer>_ProcessInputRow** auf, um die Zeilenverarbeitung auszuführen.  
  
-   Überschreiben Sie **FinishOutputs**, wenn Sie einen Vorgang für die Ausgaben ausführen müssen, bevor sie geschlossen werden.  
  
 Die **ProcessInput**-Methode stellt sicher, dass diese Methoden zum jeweils richtigen Zeitpunkt aufgerufen werden.  
  
### <a name="processing-outputs"></a>Verarbeiten von Ausgaben  
 Skriptkomponenten, die als Quellen oder Transformationen konfiguriert sind, weisen mindestens eine Eingabe auf.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>Bereitstellungen durch das ‚BufferWrapper’-Projektelement  
 Für jede von Ihnen konfigurierte Ausgabe enthält das BufferWrapper-Projektelement eine Klasse, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> abgeleitet ist und denselben Namen hat wie die Ausgabe. Jede Eingabepufferklasse enthält die folgenden Eigenschaften und Methoden:  
  
-   Benannte, typisierte, lesegeschützte Accessoreigenschaften für jede ausgewählte Ausgabespalte.  
  
-   Eine lesegeschützte **\<column>_IsNull**-Eigenschaft für jede ausgewählte Ausgabespalte, die Sie zum Festlegen des Spaltenwerts auf **NULL** verwenden können.  
  
-   Eine **AddRow**-Methode, um dem Ausgabepuffer eine neue leere Zeile hinzuzufügen.  
  
-   Eine **SetEndOfRowset**-Methode, um dem Datenflussmodul mitzuteilen, dass keine weiteren Datenpuffer erwartet werden. Außerdem gibt es eine **EndOfRowset**-Funktion, um zu bestimmen, ob der aktuelle Puffer der letzte Datenpuffer ist. Normalerweise benötigen Sie diese Funktionen nicht, wenn Sie die in der **UserComponent**-Basisklasse implementierten Eingabeverarbeitungsmethoden verwenden.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>Bereitstellungen durch das ‚ComponentWrapper’-Projektelement  
 Das ComponentWrapper-Projektelement enthält eine Klasse mit dem Namen **UserComponent**, die von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> abgeleitet wird. Die **ScriptMain**-Klasse, in die Sie Ihren benutzerdefinierten Code schreiben, wird wiederum von **UserComponent** abgeleitet. Die **UserComponent**-Klasse enthält die folgenden Methoden:  
  
-   Eine überschriebene Implementierung der **PrimeOutput**-Methode. Diese Methode wird vom Datenflussmodul zur Laufzeit nur einmal vor **ProcessInput** aufgerufen. **PrimeOutput** übergibt die Verarbeitung an die **CreateNewOutputRows**-Methode. Wenn die Komponente eine Quelle ist (d.h. die Komponente weist keine Eingaben auf), ruft **PrimeOutput** die überschreibbare **FinishOutputs**-Methode und die private **MarkOutputsAsFinished**-Methode auf. Die **MarkOutputsAsFinished**-Methode ruft **SetEndOfRowset** auf dem letzten Ausgabepuffer auf.  
  
-   Eine überschreibbare Implementierung der **CreateNewOutputRows**-Methode. Der Standardimplementierung ist leer. Dies ist die Methode, die Sie normalerweise überschreiben, um den benutzerdefinierten Datenverarbeitungscode zu schreiben.  
  
#### <a name="what-your-custom-code-should-do"></a>Schritte, die der benutzerdefinierte Code ausführen sollte  
 Sie können mithilfe der folgenden Methoden Ausgaben in der **ScriptMain**-Klasse verarbeiten:  
  
-   Überschreiben Sie **CreateNewOutputRows** nur, wenn Sie Ausgabezeilen vor der Verarbeitung der Eingabezeilen hinzufügen und auffüllen können. Sie können beispielsweise **CreateNewOutputRows** in einer Quelle verwenden. In einer Transformation mit asynchronen Ausgaben sollten Sie jedoch **AddRow** während oder nach der Verarbeitung der Eingabedaten aufrufen.  
  
-   Überschreiben Sie **FinishOutputs**, wenn Sie einen Vorgang für die Ausgaben ausführen müssen, bevor sie geschlossen werden.  
  
 Die **PrimeOutput**-Methode stellt sicher, dass diese Methoden zum jeweils richtigen Zeitpunkt aufgerufen werden.  
  
## <a name="postexecute-method"></a>‚PostExecute’-Methode  
 Überschreiben Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse immer dann, wenn Sie eine Verarbeitung nur einmal durchführen müssen, nachdem Sie die Datenzeilen verarbeitet haben. In einer Quelle können Sie beispielsweise den von Ihnen zum Laden von Daten in den Datenfluss verwendeten **System.Data.SqlClient.SqlDataReader** schließen.  
  
> [!IMPORTANT]  
>  Die Auflistung von **ReadWriteVariables** ist nur in der **PostExecute**-Methode verfügbar. Sie können daher den Wert einer Paketvariablen nicht direkt inkrementieren, während Sie jede Datenzeile verarbeiten. Inkrementieren Sie stattdessen den Wert einer lokalen Variablen, und legen Sie den Wert der Paketvariablen auf den Wert der lokalen Variablen in der **PostExecute**-Methode fest, nachdem alle Daten verarbeitet wurden.  
  
## <a name="releaseconnections-method"></a>‚ReleaseConnections’-Methode  
 Quellen und Ziele müssen generell eine Verbindung mit einer externen Datenquelle herstellen. Überschreiben Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>-Basisklasse, um die vorher in der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A>-Methode geöffnete Verbindung zu schließen und freizugeben.  
  
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
 [Configuring the Script Component in the Script Component Editor (Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor)](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [Codieren und Debuggen der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
