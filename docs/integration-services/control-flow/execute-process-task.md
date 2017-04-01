---
title: "Prozess ausf&#252;hren (Task) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executeprocesstask.f1"
helpviewer_keywords: 
  - "Prozess ausführen (Task) [Integration Services]"
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
caps.latest.revision: 65
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 65
---
# Prozess ausf&#252;hren (Task)
  Der Task Prozess ausführen führt eine Anwendung oder eine Batchdatei als Teil eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets aus. Mit der Task 'Prozess ausführen' können alle Standardanwendungen wie z. B. [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] oder [!INCLUDE[ofprword](../../includes/ofprword-md.md)]geöffnet werden, normalerweise wird er jedoch zum Ausführen von Geschäftsanwendungen oder Batchdateien für eine Datenquelle verwendet. Beispielsweise können Sie mit dem Task 'Prozess ausführen' eine komprimierte Textdatei expandieren. Anschließend kann das Paket die Textdatei als Datenquelle für den Datenfluss im Paket verwenden. Sie können mit dem Task 'Prozess ausführen' auch eine benutzerdefinierte [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Anwendung ausführen, die einen täglichen Umsatzbericht erstellt. Anschließend können Sie den Bericht an einen "Mail senden"'-Task anfügen und an eine Verteilerliste weiterleiten.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] schließt weitere Tasks ein, die Workflowvorgänge ausführen, wie z. B. das Ausführen von Paketen. Weitere Informationen finden Sie unter [Execute Package Task](../../integration-services/control-flow/execute-package-task.md).  
  
## Verfügbare benutzerdefinierte Protokolleinträge für den Task 'Prozess ausführen'  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task Prozess ausführen aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) und [Benutzerdefinierte Meldungen für die Protokollierung](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|Enthält Informationen zu dem Prozess, für dessen Ausführung der Task konfiguriert ist.<br /><br /> Es werden zwei Protokolleinträge geschrieben. Der eine Protokolleintrag enthält Informationen über den Namen und Speicherort der vom Task ausgeführten ausführbaren Datei, im anderen Eintrag wird das Beenden der ausführbaren Datei erfasst.|  
|**ExecuteProcessVariableRouting**|Enthält Informationen darüber, welche Variablen an die Eingabe und an die Ausgaben der ausführbaren Datei geleitet werden. Es werden Protokolleinträge für stdin (für die Eingabe), für stdout (für die Ausgabe) und für stderr (für die Fehlerausgabe) geschrieben.|  
  
## Konfiguration des Tasks "Prozess ausführen"  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „Prozess ausführen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/execute-process-task-editor-general-page.md)  
  
-   [Editor für den Task „Prozess ausführen“ &#40;Seite „Verarbeiten“&#41;](../../integration-services/control-flow/execute-process-task-editor-process-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
### Eigenschafteneinstellungen  
 Wenn der Task "Prozess ausführen" eine benutzerdefinierte Anwendung ausführt, stellt der Task mithilfe einer der beiden folgenden Methoden eine Eingabe für die Anwendung bereit:  
  
-   Eine Variable, die Sie in der Eigenschaftseinstellung **StandardInputVariable** angeben. Weitere Informationen zu Variablen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md).  
  
-   Ein Argument, das Sie in der Eigenschaftseinstellung **Argumente** angeben. (Wenn der Task beispielsweise ein Dokument in Word öffnet, kann mit dem Argument die DOC-Datei angegeben werden.)  
  
 Um mehrere Argumente an eine benutzerdefinierte Anwendung in einem einzigen 'Prozess ausführen'-Task zu übergeben, verwenden Sie Leerzeichen, um die Argumente voneinander zu trennen. Ein Argument darf kein Leerzeichen enthalten; sonst wird der Task nicht ausgeführt. Sie können einen Ausdruck verwenden, um einen Variablenwert als Argument zu übergeben. Im folgenden Beispiel übergibt der Ausdruck zwei Variablenwerte als Argumente und verwendet ein Leerzeichen, um die Argumente voneinander zu trennen:  
  
 `@variable1 + " " + @variable2`  
  
 Sie können einen Ausdruck verwenden, um verschiedene Eigenschaften des Tasks 'Prozess ausführen' festzulegen.  
  
 Wenn Sie zum Konfigurieren des Tasks Prozess ausführen für Eingaben die Eigenschaft **StandardInputVariable** verwenden, rufen Sie zum Lesen der Eingabe die **Console.ReadLine** -Methode der Anwendung auf. Weitere Informationen finden Sie in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Klassenbibliothek im Thema [Console.ReadLine-Methode](http://go.microsoft.com/fwlink/?LinkId=129201).  
  
 Wenn Sie zum Konfigurieren des Tasks Prozess ausführen für Eingaben die Eigenschaft **Argumente** verwenden, führen Sie zum Abrufen der Argumente einen der folgenden Schritte aus:  
  
-   Wenn Sie Microsoft Visual Basic verwenden, um die Anwendung zu schreiben, legen Sie die **My.Application.CommandLineArgs** -Eigenschaft fest. Im folgenden Beispiel ruft die **My.Application.CommandLineArgs** -Eigenschaft zwei Argumente ab:  
  
    ```  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     Weitere Informationen finden Sie in der [-Referenz unter](http://go.microsoft.com/fwlink/?LinkId=129200)My.Application.CommandLineArgs Property [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .  
  
-   Wenn Sie Microsoft Visual C# verwenden, um die Anwendung zu schreiben, verwenden Sie die **Main**-Methode.  
  
     Weitere Informationen finden Sie im C#-Programmierhandbuch unter [Befehlszeilenargumente (C#-Programmierhandbuch)](http://go.microsoft.com/fwlink/?LinkId=129406).  
  
 Der Task 'Prozess ausführen' enthält außerdem die Eigenschaften **StandardOutputVariable** und **StandardErrorVariable** zum Angeben der Variablen, die jeweils die Standardausgabe und die Fehlerausgabe der Anwendung in Anspruch nehmen.  
  
 Darüber hinaus können Sie für den Task 'Prozess ausführen' ein Arbeitsverzeichnis, einen Timeoutzeitraum oder einen Wert zum Anzeigen der erfolgreichen Ausführung der ausführbaren Datei konfigurieren. Für den Task kann außerdem konfiguriert werden, dass ein Fehler gemeldet wird, falls der Rückgabecode der ausführbaren Datei nicht mit dem Wert übereinstimmt, der für die erfolgreiche Ausführung steht, oder falls die ausführbare Datei im angegebenen Speicherort nicht gefunden wird.  
  
## Programmgesteuerte Konfiguration des Tasks "Prozess ausführen"  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  