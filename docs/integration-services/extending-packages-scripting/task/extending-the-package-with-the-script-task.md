---
title: Extending the Package with the Script Task | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- scripts [Integration Services]
- SSIS Script task
- tasks [Integration Services], scripts
- Script task [Integration Services], about Script task
- scripts [Integration Services], about Script task with packages
- SSIS Script task, about Script task
ms.assetid: 911e6d26-a6fd-4fc3-a111-bf5f048e9bff
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2e0b0a933568f8313cefd2f1d6dbdd02f5d3cbc
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="extending-the-package-with-the-script-task"></a>Erweitern von Paketen mithilfe des Skripttasks
  Der Skripttask erweitert die Laufzeitfunktionen von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Paketen durch benutzerdefinierten Code geschrieben [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual c#, der kompiliert und zur Laufzeit des Pakets ausgeführt wird. Der Skripttask vereinfacht die Entwicklung eines benutzerdefinierten Laufzeittasks, falls die in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] enthaltenen Tasks Ihre Anforderungen nicht voll erfüllen. Der Skripttask schreibt den nötigen Infrastrukturcode für Sie, damit Sie sich vollständig auf den Code konzentrieren können, der für die benutzerdefinierte Verarbeitung erforderlich ist.  
  
 Ein Skripttask interagiert mit dem entsprechenden Paket über das globale **Dts** -Objekt, das eine Instanz der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> -Klasse, die in der skriptumgebung verfügbar gemacht wird. In einem Skripttask können Sie Code schreiben, der die in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]-Variablen gespeicherten Werte ändert. Anschließend kann das Paket anhand dieser aktualisierten Werte den Workflowpfad ermitteln. Der Skripttask kann außerdem den [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]-Namespace und die [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Klassenbibliothek sowie benutzerdefinierte Assemblys zum Implementieren individueller Funktionen verwenden.  
  
 Der Skripttask und der Infrastrukturcode, den er generiert, erleichtern die Entwicklung von benutzerdefinierten Tasks deutlich. Allerdings zum Verständnis der Funktionsweise des Skripttasks sicherlich nützlich, um den Abschnitt lesen [Entwickeln eines benutzerdefinierten Tasks](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md) werden die Schritte erläutert, die bei der Entwicklung eines benutzerdefinierten Tasks beteiligt sind.  
  
 Wenn Sie einen Task erstellen, den Sie in mehreren Paketen wiederverwenden möchten, sollten Sie nicht den Skripttask verwenden, sondern einen benutzerdefinierte Task entwickeln. Weitere Informationen finden Sie unter [Scripting Solutions vergleichen und benutzerdefinierten Objekten](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 Die folgenden Themen enthalten weitere Informationen zum Skripttask.  
  
 [Konfigurieren des Skripttasks in der Skripttask-Editor](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 Erläutert, wie die Eigenschaften, die Sie in Konfigurieren der **Skripttask-Editor** wirken sich auf die Funktionen und die Leistung des Codes im Skripttask.  
  
 [Beim Codieren und Debuggen des Skripttasks](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 Erklärt, wie [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) zum Entwickeln von den Skripts, die im Skripttask enthalten sind.  
  
 [Verwenden von Variablen im Skripttask](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 Erklärt, wie Variablen mithilfe der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>-Eigenschaft verwendet werden.  
  
 [Connecting to Data Sources in the Script Task](../../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 Erklärt, wie Verbindungen mithilfe der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>-Eigenschaft verwendet werden.  
  
 [Auslösen von Ereignissen im Skripttask](../../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 Erklärt, wie mithilfe der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>-Eigenschaft Ereignisse ausgelöst werden.  
  
 [Protokollieren im Skripttask](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 Erklärt, wie Informationen über die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>-Methode protokolliert werden.  
  
 [Zurückgeben von Ergebnissen aus dem Skripttask](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)  
 Erklärt, wie Ergebnisse über die Eigenschaften <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> und <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> zurückgegeben werden.  
  
 [Skripttask-Beispiele](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 Stellt einfache Beispiele bereit, in denen mehrere mögliche Verwendungen für einen Skripttask veranschaulicht werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Skripttask](../../../integration-services/control-flow/script-task.md)   
 [Vergleichen den Skripttask und Skriptkomponente](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  

