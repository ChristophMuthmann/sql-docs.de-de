---
title: Vergleichen den Skripttask und Skriptkomponente | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], comparing to Script component
- Script component [Integration Services], comparing to Script task
ms.assetid: 4b73753a-4239-491b-b7a6-abc63ba83d2d
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0413b4b88a1f0326dad1ba261aea647cefd43302
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="comparing-the-script-task-and-the-script-component"></a>Vergleich zwischen Skripttask und Skriptkomponente
  Der Skripttask, verfügbar im Fenster Ablaufsteuerung von der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Designer und der Skriptkomponente im Fenster des Datenflusses zur Verfügung haben ganz verschiedene Zwecke in ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Paket. Der Task stellt ein allgemeines Ablaufsteuerungstool dar, während die Komponente als Quelle, Transformation oder Ziel im Datenfluss dient. Trotz ihres unterschiedlichen Zwecks verfügen der Skripttask und die Skriptkomponente jedoch über Gemeinsamkeiten hinsichtlich der verwendeten Codierungstools sowie der Objekte im Paket, die sie dem Entwickler bereitstellen. Die Unterschiede und Gemeinsamkeiten zu kennen, kann Ihnen dabei helfen, Task und Komponente effektiver einzusetzen.  
  
## <a name="similarities-between-the-script-task-and-the-script-component"></a>Gemeinsamkeiten zwischen Skripttask und Skriptkomponente  
 Skripttask und Skriptkomponente verfügen über folgende gemeinsame Funktionen:  
  
|Funktion|Description|  
|-------------|-----------------|  
|Zwei Entwurfszeitmodi|Bei Task und Komponente legen Sie zunächst im Editor Eigenschaften fest und wechseln anschließend in die Entwicklungsumgebung, um Code zu schreiben.|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)|Task und Komponente verwenden dieselbe VSTA IDE und unterstützen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# geschriebenen Code.|  
|Vorkompilierte Skripts|Ab [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] werden alle Skripts vorkompiliert. In früheren Versionen konnten Sie festlegen, ob Skripts vorkompiliert werden sollten.<br /><br /> Das Skript wird in binärem Code vorkompiliert. Dies ermöglicht eine schnellere Ausführung, vergrößert jedoch das Paket.|  
|Debuggen|Beim Debuggen in der Entwurfsumgebung unterstützen der Task und die Komponente Breakpoints und die schrittweise Ausführung von Code. Weitere Informationen finden Sie unter [codieren und Debuggen des Skripttasks](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) und [codieren und Debuggen der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).|  
  
## <a name="differences-between-the-script-task-and-the-script-component"></a>Unterschiede zwischen Skripttask und Skriptkomponente  
 Skripttask und Skriptkomponente weisen folgende wichtige Unterschiede auf:  
  
|Funktion|Skripttask|Skriptkomponente|  
|-------------|-----------------|----------------------|  
|Ablaufsteuerung/Datenfluss|Der Skripttask wird auf der Registerkarte Ablaufsteuerung des Designers konfiguriert und außerhalb des Paketdatenflusses ausgeführt.|Die Skriptkomponente wird auf der Seite Datenfluss des Designers konfiguriert und stellt eine Quelle, Transformation oder ein Ziel im Datenflusstask dar.|  
|Zweck|Ein Skripttask kann fast jede allgemeine Aufgabe ausführen.|Sie müssen festlegen, ob Sie mit der Skriptkomponente eine Quelle, Transformation oder ein Ziel erstellen möchten.|  
|Ausführung|Ein Skripttask führt benutzerdefinierten Code an einem bestimmten Punkt im Paketworkflow aus. Er wird nur einmal ausgeführt, sofern Sie ihn nicht in einem Schleifencontainer oder Ereignishandler platzieren.|Auch eine Skriptkomponente wird einmal ausgeführt. Sie führt aber ihre Verarbeitungsroutine meist für jede Datenzeile im Datenfluss aus.|  
|Editor|Die **Skripttask-Editor** hat drei Seiten: **allgemeine**, **Skript**, und **Ausdrücke**. Nur die **ReadOnlyVariables** und **ReadWriteVariables**, und **ScriptLanguage** Eigenschaften wirken sich direkt auf den Code, den Sie schreiben können.|Die **Skript Transformations-Editor** hat bis zu vier Seiten: **Eingabespalten**, **Eingaben und Ausgaben**, **Skript**, und **Verbindungs-Manager**. Die Metadaten und Eigenschaften, die Sie auf diesen Seiten konfigurieren, legen die Member der Basisklassen fest, die für Sie bei der Codierung automatisch generiert werden.|  
|Interaktion mit dem Paket|In den Code für einen Skripttask geschrieben wurden, verwenden Sie die **Dts** Eigenschaft zum Zugriff auf andere Funktionen des Pakets. Die **Dts** Eigenschaft ist ein Mitglied der **ScriptMain** Klasse.|Im Skriptkomponentencode verwenden Sie typisierte Accessoreigenschaften für den Zugriff auf bestimmte Paketfunktionen wie Variablen und Verbindungs-Manager.<br /><br /> Die **PreExecute** Methode kann nur für schreibgeschützte Variablen zugreifen. Die **"PostExecute"** Methode kann Zugriff auf beide schreibgeschützten und Lese-/schreibvariablen.<br /><br /> Weitere Informationen zu diesen Methoden finden Sie unter [codieren und Debuggen der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).|  
|Verwenden von Variablen|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> Eigenschaft von der **Dts** Objekt, um auf Variablen zuzugreifen, die über der Aufgabe zur Verfügung stehen <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> und <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> Eigenschaften. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Dts.Variables(“MyStringVariable”).Value.ToString`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = Dts.Variables["MyStringVariable"].Value.ToString();`|Die Skriptkomponente verwendet typisierte Accessoreigenschaften der automatisch generierten Basisklasse, die aus den <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A>- und <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A>-Eigenschaften der Komponente erstellt werden. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Me.Variables.MyStringVariable`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = this.Variables.MyStringVariable;`|  
|Verwenden von Verbindungen|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> Eigenschaft von der **Dts** Objekt, das im Paket definierte Verbindungs-Manager für den Zugriff. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim myFlatFileConnection As String` <br /> `myFlatFileConnection = _     DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _     String)`<br /><br /> [C#]<br /><br /> `string myFlatFileConnection;` <br /> `myFlatFileConnection = (Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);`|Die Skriptkomponente verwendet typisierte Accessoreigenschaften der automatisch generierten Basisklasse, die aus der Liste von Verbindungs-Managern erstellt werden, die vom Benutzer auf der Seite Verbindungs-Manager des Editors eingegeben wurden. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim connMgr As IDTSConnectionManager100` <br /> `connMgr = Me.Connections.MyADONETConnection`<br /><br /> [C#]<br /><br /> `IDTSConnectionManager100 connMgr;` <br /> `connMgr = this.Connections.MyADONETConnection;`|  
|Auslösen von Ereignissen|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> Eigenschaft von der **Dts** Objekt zum Auslösen von Ereignissen. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", _     ex.Message & ControlChars.CrLf & ex.StackTrace, _     "", 0)`<br /><br /> [C#]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", ex.Message + "\r" + ex.StackTrace, "", 0);`|Die Skriptkomponente löst Fehler, Warnungen und Informationsmeldungen mithilfe der Methoden der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>-Schnittstelle, die von der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>-Eigenschaft zurückgegeben werden, aus. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim myMetadata as IDTSComponentMetaData100 myMetaData = Me.ComponentMetaData myMetaData.FireError(...)`|  
|Protokollierung|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> Methode der **Dts** bei aktivierten Protokollanbietern zu protokollieren von Informationen zum Objekt. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte Dts.Log("Test Log Event", _     0, _     bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0];` <br /> `Dts.Log("Test Log Event", 0, bt);`|Die Skriptkomponente verwendet die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>-Methode der automatisch generierten Basisklasse, um Informationen bei aktivierten Protokollanbietern zu protokollieren. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte`<br /><br /> `Me.Log("Test Log Event", _`<br /><br /> `0, _`<br /><br /> `bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0]; this.Log("Test Log Event", 0, bt);`|  
|Zurückgeben von Ergebnissen|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> -Eigenschaft und dem optionalen <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> Eigenschaft von der **Dts** Objekt benachrichtigt die Laufzeit über die Ergebnisse.|Die Skriptkomponente wird als Teil des Datenflusstasks ausgeführt und erstellt keine Ergebnisberichte mit einer dieser Eigenschaften.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweitern Sie das Paket mit dem Skripttask](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Erweitern des Datenflusses mit der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
  
  
