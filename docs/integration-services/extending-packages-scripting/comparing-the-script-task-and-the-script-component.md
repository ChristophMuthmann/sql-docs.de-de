---
title: Vergleich zwischen Skripttask und Skriptkomponente | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs: VB
helpviewer_keywords:
- Script task [Integration Services], comparing to Script component
- Script component [Integration Services], comparing to Script task
ms.assetid: 4b73753a-4239-491b-b7a6-abc63ba83d2d
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b361124960eb0ed7ef7482277ccf35df44443cb6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="comparing-the-script-task-and-the-script-component"></a>Vergleich zwischen Skripttask und Skriptkomponente
  Der Skripttask, der im Fenster „Ablaufsteuerung“ des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Designers zur Verfügung steht, und die Skriptkomponente im Fenster „Datenfluss“ dienen in einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket völlig unterschiedlichen Zwecken. Der Task stellt ein allgemeines Ablaufsteuerungstool dar, während die Komponente als Quelle, Transformation oder Ziel im Datenfluss dient. Trotz ihres unterschiedlichen Zwecks verfügen der Skripttask und die Skriptkomponente jedoch über Gemeinsamkeiten hinsichtlich der verwendeten Codierungstools sowie der Objekte im Paket, die sie dem Entwickler bereitstellen. Die Unterschiede und Gemeinsamkeiten zu kennen, kann Ihnen dabei helfen, Task und Komponente effektiver einzusetzen.  
  
## <a name="similarities-between-the-script-task-and-the-script-component"></a>Gemeinsamkeiten zwischen Skripttask und Skriptkomponente  
 Skripttask und Skriptkomponente verfügen über folgende gemeinsame Funktionen:  
  
|Funktion|Description|  
|-------------|-----------------|  
|Zwei Entwurfszeitmodi|Bei Task und Komponente legen Sie zunächst im Editor Eigenschaften fest und wechseln anschließend in die Entwicklungsumgebung, um Code zu schreiben.|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)|Task und Komponente verwenden dieselbe VSTA IDE und unterstützen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# geschriebenen Code.|  
|Vorkompilierte Skripts|Ab [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] werden alle Skripts vorkompiliert. In früheren Versionen konnten Sie festlegen, ob Skripts vorkompiliert werden sollten.<br /><br /> Das Skript wird in binärem Code vorkompiliert. Dies ermöglicht eine schnellere Ausführung, vergrößert jedoch das Paket.|  
|Debuggen|Beim Debuggen in der Entwurfsumgebung unterstützen der Task und die Komponente Breakpoints und die schrittweise Ausführung von Code. Weitere Informationen finden Sie unter [Coding and Debugging the Script Task](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) (Codieren und Debuggen des Skripttasks) und [Coding and Debugging the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md) (Codieren und Debuggen der Skriptkomponente).|  
  
## <a name="differences-between-the-script-task-and-the-script-component"></a>Unterschiede zwischen Skripttask und Skriptkomponente  
 Skripttask und Skriptkomponente weisen folgende wichtige Unterschiede auf:  
  
|Funktion|Skripttask|Skriptkomponente|  
|-------------|-----------------|----------------------|  
|Ablaufsteuerung/Datenfluss|Der Skripttask wird auf der Registerkarte Ablaufsteuerung des Designers konfiguriert und außerhalb des Paketdatenflusses ausgeführt.|Die Skriptkomponente wird auf der Seite Datenfluss des Designers konfiguriert und stellt eine Quelle, Transformation oder ein Ziel im Datenflusstask dar.|  
|Zweck|Ein Skripttask kann fast jede allgemeine Aufgabe ausführen.|Sie müssen festlegen, ob Sie mit der Skriptkomponente eine Quelle, Transformation oder ein Ziel erstellen möchten.|  
|Ausführung|Ein Skripttask führt benutzerdefinierten Code an einem bestimmten Punkt im Paketworkflow aus. Er wird nur einmal ausgeführt, sofern Sie ihn nicht in einem Schleifencontainer oder Ereignishandler platzieren.|Auch eine Skriptkomponente wird einmal ausgeführt. Sie führt aber ihre Verarbeitungsroutine meist für jede Datenzeile im Datenfluss aus.|  
|Editor|Der **Skripttask-Editor** weist drei Seiten auf: **Allgemein**, **Skript** und **Ausdrücke**. Nur die Eigenschaften **ReadOnlyVariables** und **ReadWriteVariables** und **ScriptLanguage** wirken sich direkt auf den Code aus, den Sie schreiben können.|Der **Transformations-Editor für Skripterstellung** verfügt über maximal vier Seiten: **Eingabespalten**, **Eingaben und Ausgaben**, **Skript** sowie **Verbindungs-Manager**. Die Metadaten und Eigenschaften, die Sie auf diesen Seiten konfigurieren, legen die Member der Basisklassen fest, die für Sie bei der Codierung automatisch generiert werden.|  
|Interaktion mit dem Paket|Im Code für einen Skripttask verwenden Sie die **Dts**-Eigenschaft, um auf andere Funktionen des Pakets zuzugreifen. Die **Dts**-Eigenschaft ist ein Mitglied der Klasse **ScriptMain**.|Im Skriptkomponentencode verwenden Sie typisierte Accessoreigenschaften für den Zugriff auf bestimmte Paketfunktionen wie Variablen und Verbindungs-Manager.<br /><br /> Die **PreExecute**-Methode kann nur auf Variablen für den Lesezugriff zugreifen. Die **PostExecute**-Methode kann sowohl auf Variablen für den Lesezugriff als auch auf Variablen für den Lese-/Schreibzugriff zugreifen.<br /><br /> Weitere Informationen zu diesen Methoden finden Sie unter [Coding and Debugging the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md) (Codieren und Debuggen der Skriptkomponente).|  
|Verwenden von Variablen|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>-Eigenschaft des **Dts**-Objekts, um auf Variablen zuzugreifen, die über die Eigenschaften <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> und <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> des Tasks bereitgestellt werden. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Dts.Variables(“MyStringVariable”).Value.ToString`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = Dts.Variables["MyStringVariable"].Value.ToString();`|Die Skriptkomponente verwendet typisierte Accessoreigenschaften der automatisch generierten Basisklasse, die aus den <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A>- und <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A>-Eigenschaften der Komponente erstellt werden. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Me.Variables.MyStringVariable`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = this.Variables.MyStringVariable;`|  
|Verwenden von Verbindungen|Der Skripttask nutzt die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>-Eigenschaft des **Dts**-Objekts, um auf im Paket definierte Verbindungs-Manager zuzugreifen. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim myFlatFileConnection As String` <br /> `myFlatFileConnection = _     DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _     String)`<br /><br /> [C#]<br /><br /> `string myFlatFileConnection;` <br /> `myFlatFileConnection = (Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);`|Die Skriptkomponente verwendet typisierte Accessoreigenschaften der automatisch generierten Basisklasse, die aus der Liste von Verbindungs-Managern erstellt werden, die vom Benutzer auf der Seite Verbindungs-Manager des Editors eingegeben wurden. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim connMgr As IDTSConnectionManager100` <br /> `connMgr = Me.Connections.MyADONETConnection`<br /><br /> [C#]<br /><br /> `IDTSConnectionManager100 connMgr;` <br /> `connMgr = this.Connections.MyADONETConnection;`|  
|Auslösen von Ereignissen|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>-Eigenschaft des **Dts**-Objekts, um Ereignisse auszulösen. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", _     ex.Message & ControlChars.CrLf & ex.StackTrace, _     "", 0)`<br /><br /> [C#]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", ex.Message + "\r" + ex.StackTrace, "", 0);`|Die Skriptkomponente löst Fehler, Warnungen und Informationsmeldungen mithilfe der Methoden der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>-Schnittstelle, die von der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>-Eigenschaft zurückgegeben werden, aus. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim myMetadata as IDTSComponentMetaData100 myMetaData = Me.ComponentMetaData myMetaData.FireError(...)`|  
|Protokollierung|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>-Methode des **Dts**-Objekts, um Informationen bei aktivierten Protokollanbietern zu protokollieren. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte Dts.Log("Test Log Event", _     0, _     bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0];` <br /> `Dts.Log("Test Log Event", 0, bt);`|Die Skriptkomponente verwendet die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>-Methode der automatisch generierten Basisklasse, um Informationen bei aktivierten Protokollanbietern zu protokollieren. Beispiel:<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte`<br /><br /> `Me.Log("Test Log Event", _`<br /><br /> `0, _`<br /><br /> `bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0]; this.Log("Test Log Event", 0, bt);`|  
|Zurückgeben von Ergebnissen|Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>-Eigenschaft sowie die optionale <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>-Eigenschaft des **Dts**-Objekts, um die Runtime über die Ergebnisse zu benachrichtigen.|Die Skriptkomponente wird als Teil des Datenflusstasks ausgeführt und erstellt keine Ergebnisberichte mit einer dieser Eigenschaften.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweitern von Paketen mithilfe des Skripttasks](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Erweitern des Datenflusses mit der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
  
  
