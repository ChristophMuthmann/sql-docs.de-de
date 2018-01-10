---
title: Verwenden von Variablen in der Skriptkomponente | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5be7180ca534c697b94655199a7557070e2b319f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="using-variables-in-the-script-component"></a>Verwenden von Variablen in der Skriptkomponente
  Variablen speichern Werte, die von einem Paket und dessen Containern, Tasks und Ereignishandlern zur Laufzeit verwendet werden können. Weitere Informationen finden Sie unter [Integration Services &#40;SSIS&#41; Variables](../../../integration-services/integration-services-ssis-variables.md).  
  
 Sie können vorhandene Variablen für schreibgeschützten oder Lese-/Schreibzugriff mittels eines benutzerdefinierten Skripts zur Verfügung stellen, indem Sie kommagetrennte Listen von Variablen in die Felder **ReadOnlyVariables** und **ReadWriteVariables** auf der Seite **Skript** des **Transformations-Editors für Skripterstellung** eingeben. Beachten Sie, dass bei Variablennamen nach Groß-/Kleinschreibung unterschieden wird. Mithilfe der **Value**-Eigenschaft erhalten Sie Lese- und Schreibzugriff auf einzelne Variablen. Die Skriptkomponente führt erforderliche Sperrungen im Hintergrund aus, da das Skript die Variablen zur Laufzeit verarbeitet.  
  
> [!IMPORTANT]  
>  Die Auflistung von **ReadWriteVariables** ist nur in der **PostExecute**-Methode verfügbar, um das Risiko von Sperrkonflikten zu vermindern und die Leistung zu maximieren. Sie können daher den Wert einer Paketvariablen nicht direkt inkrementieren, während Sie jede Datenzeile verarbeiten. Inkrementieren Sie stattdessen den Wert einer lokalen Variablen, und legen Sie den Wert der Paketvariablen auf den Wert der lokalen Variablen in der **PostExecute**-Methode fest, nachdem alle Daten verarbeitet wurden. Sie können auch die Eigenschaft <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> verwenden, um diese Einschränkung zu umgehen, wie später in diesem Thema beschrieben ist. Wenn Sie jedoch direkt in eine Paketvariable schreiben, während jede Zeile verarbeitet wird, wird die Leistung beeinträchtigt und das Risiko von Sperrkonflikten erhöht.  
  
 Weitere Informationen über die Seite **Skript** im **Transformations-Editor für Skripterstellung** finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) (Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor) und [Script Transformation Editor &#40;Script Page&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md) (Transformations-Editor für Skripterstellung [Seite „Skript“]).  
  
 Die Skriptkomponente erstellt eine **Variables**-Auflistungsklasse im **ComponentWrapper**-Projektelement mit einer Accessoreigenschaft mit starker Typbindung für den Wert jeder vorkonfigurierten Variable, wobei die Eigenschaft denselben Namen wie die Variable selbst hat. Diese Auflistung wird von der **Variables**-Eigenschaft der **ScriptMain**-Klasse verfügbar gemacht. Die Accessoreigenschaft bietet entsprechend Lese- oder Lese-/Schreibberechtigung für den Wert der Variable. Wenn Sie beispielsweise eine Ganzzahlvariable namens `MyIntegerVariable` der Liste **ReadOnlyVariables** hinzugefügt haben, können Sie ihren Wert mit dem folgenden Code in das Skript abrufen:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 Für die Arbeit mit Variablen in der Skriptkomponente können Sie auch die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>-Eigenschaft (Aufruf mit `Me.VariableDispenser`) verwenden. In diesem Fall verwenden Sie nicht die benannten, typisierten Accessoreigenschaften für Variablen, sondern greifen direkt auf die Variablen zu. Bei der Verwendung von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> müssen Sie die Sperrsemantik und die Umwandlung von Datentypen für variable Werte in Ihrem Code berücksichtigen. Wenn Sie mit Variablen arbeiten möchten, die zur Entwurfszeit nicht zur Verfügung stehen, sondern programmgesteuert zur Laufzeit erstellt werden, müssen Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>-Eigenschaft statt der benannten, typisierten Accessoreigenschaften verwenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services-Variablen &#40;SSIS&#41;](../../../integration-services/integration-services-ssis-variables.md)   
 [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
