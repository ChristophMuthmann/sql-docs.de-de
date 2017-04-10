---
title: "Skripttask-Editor (Seite Skript) | Microsoft Docs"
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
  - "sql13.dts.designer.scripttask.script.f1"
helpviewer_keywords: 
  - "Skripttask-Editor"
ms.assetid: 93da0e0d-83f5-406d-b144-4cce216571cb
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Skripttask-Editor (Seite Skript)
  Mithilfe der Seite **Skript** des Dialogfelds **Skripttask-Editor** können Sie Skripteigenschaften festlegen und Variablen angeben, auf die dieses Skript zugreifen kann.  
  
> [!NOTE]  
>  In [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] und höheren Versionen werden alle Skripts vorkompiliert. In früheren Versionen wurde eine **PrecompileScriptIntoBinaryCode** -Eigenschaft festgelegt, um anzugeben, dass das Skript vorkompiliert wurde.  
  
 Weitere Informationen zum Skripttask finden Sie unter [Script Task](../../integration-services/control-flow/script-task.md) und [Configuring the Script Task in the Script Task Editor](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md). Informationen zum Programmieren des Skripttasks finden Sie unter [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md).  
  
## enthalten  
 **ScriptLanguage**  
 Wählen Sie die Skriptsprache für den Task aus, entweder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Nachdem Sie ein Skript für den Task erstellt haben, können Sie den Wert der **ScriptLanguage** -Eigenschaft nicht mehr ändern.  
  
 Um die Standardskriptsprache für den Skripttask festzulegen, verwenden Sie im Dialogfeld **Optionen** auf der Seite **Allgemein** die Option **Skriptsprache** . Weitere Informationen finden Sie unter [General Page](../Topic/General%20Page.md).  
  
 **EntryPoint**  
 Geben Sie die Methode an, die die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Laufzeit als Einstiegspunkt in den Code des Skripttasks aufruft. Die angegebene Methode muss in der ScriptMain-Klasse des Projekts der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]-Tools für Anwendungen (VSTA) angegeben werden. ScriptMain ist die Standardklasse, die von den Skriptvorlagen generiert wird.  
  
 Wenn Sie den Namen der Methode im VSTA-Projekt geändert haben, müssen Sie den Wert der **EntryPoint** -Eigenschaft ändern.  
  
 **ReadOnlyVariables**  
 Geben Sie eine durch Trennzeichen getrennte Liste von schreibgeschützten Variablen ein, die für das Skript verfügbar sind, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten (**…**), und wählen Sie die Variablen im Dialogfeld **Variablen auswählen** aus.  
  
> [!NOTE]  
>  Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.  
  
 **ReadWriteVariables**  
 Geben Sie eine durch Trennzeichen getrennte Liste von Lese-/Schreibvariablen ein, die für das Skript verfügbar sind, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten (**…**), und wählen Sie die Variablen im Dialogfeld **Variablen auswählen** aus.  
  
> [!NOTE]  
>  Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.  
  
 **Skript bearbeiten**  
 Öffnet die VSTA IDE, in der Sie das Skript erstellen oder ändern können.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Seite Allgemein](../Topic/General%20Page.md)   
 [Skripttask-Editor &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/script-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [Skripttask-Beispiele](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)   
 [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Hinzufügen, Löschen, Ändern des Bereichs von benutzerdefinierten Variablen in einem Paket](../Topic/Add,%20Delete,%20Change%20Scope%20of%20User-Defined%20Variable%20in%20a%20Package.md)  
  
  