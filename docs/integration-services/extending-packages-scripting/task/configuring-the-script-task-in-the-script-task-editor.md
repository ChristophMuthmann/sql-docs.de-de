---
title: Konfigurieren des Skripttasks in the Script Task Editor | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 182a7b8f04c2339a8f3d3b986c978a7998c8a9c3
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>Konfigurieren des Skripttasks im Skripttask-Editor
  Bevor Sie benutzerdefinierten Code im Skripttask schreiben, konfigurieren Sie seine prinzipaleigenschaften in den drei Seiten der **Skripttask-Editor**. Mithilfe des Eigenschaftsfensters können Sie zusätzliche Taskeigenschaften, die nicht nur für den Skripttask vorhanden sind, konfigurieren.  
  
> [!NOTE]  
>  Anders als in früheren Versionen, in denen Sie angeben konnten, ob die Skripts vorkompiliert sind, werden ab [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] alle Skripts vorkompiliert.  
  
## <a name="general-page-of-the-script-task-editor"></a>Seite 'Allgemein' des Skripttask-Editors  
 Auf der **allgemeine** auf der Seite der **Skripttask-Editor**, Sie weisen Sie einen eindeutigen Namen und eine Beschreibung für den Skripttask.  
  
## <a name="script-page-of-the-script-task-editor"></a>Seite 'Skript' des Skripttask-Editors  
 Die **Skript** auf der Seite der **Skripttask-Editor** werden die benutzerdefinierten Eigenschaften des Skripttasks angezeigt.  
  
### <a name="scriptlanguage-property"></a>ScriptLanguage-Eigenschaft  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) unterstützt die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#-Programmiersprachen zu vergleichen. Nach der Erstellung eines Skripts im Skripttask können Sie den Wert des ändern die **ScriptLanguage** Eigenschaft.  
  
 Um die Standardskriptsprache für Skripttasks und Skriptkomponenten festzulegen, verwenden die **ScriptLanguage** Eigenschaft auf die **allgemeine** auf der Seite der **Optionen** (Dialogfeld). Weitere Informationen finden Sie unter [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
### <a name="entrypoint-property"></a>EntryPoint-Eigenschaft  
 Die **EntryPoint** Eigenschaft gibt die Methode für die **ScriptMain** -Klasse im VSTA-Projekt aus, die die [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Laufzeit als Einstiegspunkt in den Code des Skripttasks aufruft. Die **ScriptMain** Klasse ist die Standardklasse, die von den Skriptvorlagen generiert.  
  
 Wenn Sie den Namen der Methode im VSTA-Projekt geändert haben, müssen Sie den Wert der **EntryPoint** -Eigenschaft ändern.  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>Eigenschaften 'ReadOnlyVariables' und 'ReadWriteVariables'  
 Sie können kommagetrennte Listen von vorhandenen Variablen als Werte dieser Eigenschaften eingeben, um die Variablen für schreibgeschützten oder Lese-/Schreibzugriff im Code des Skripttasks verfügbar zu machen. Variablen beider Typen erfolgt im Code über die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> Eigenschaft von der **Dts** Objekt. Weitere Informationen finden Sie unter [Using Variables in the Script Task](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  
  
> [!NOTE]  
>  Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.  
  
 Um die Variablen auszuwählen, klicken Sie auf die Auslassungspunkte (**...** ) neben dem Eigenschaftenfeld. Weitere Informationen finden Sie unter [Seite "Variablen" Wählen Sie](../../../integration-services/control-flow/select-variables-page.md).  
  
### <a name="edit-script-button"></a>Schaltfläche 'Skript bearbeiten'  
 Die **Bearbeitungsskript** Schaltfläche öffnet die VSTA-Entwicklungsumgebung, in dem Sie das benutzerdefinierte Skript schreiben. Weitere Informationen finden Sie unter [codieren und Debuggen des Skripttasks](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md).  
  
## <a name="expressions-page-of-the-script-task-editor"></a>Seite 'Ausdrücke' des Skripttask-Editors  
 Auf der **Ausdrücke** auf der Seite der **Skripttask-Editor**, Sie können Ausdrücke verwenden, um Werte für die Eigenschaften des oben aufgeführten Skripttasks und viele weitere Taskeigenschaften bereitzustellen. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Beim Codieren und Debuggen des Skripttasks](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
