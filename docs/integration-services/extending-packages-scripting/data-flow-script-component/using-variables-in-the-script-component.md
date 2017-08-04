---
title: Verwenden von Variablen in der Skriptkomponente | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bac1e6d96e872be0355282c3e12fc81054ca41cd
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-component"></a>Verwenden von Variablen in der Skriptkomponente
  Variablen speichern Werte, die von einem Paket und dessen Containern, Tasks und Ereignishandlern zur Laufzeit verwendet werden können. Weitere Informationen finden Sie unter [Integration Services &#40;SSIS&#41; Variables](../../../integration-services/integration-services-ssis-variables.md).  
  
 Sie können vorhandene Variablen verfügbar machen für schreibgeschützten oder Lese-/Schreibzugriff mittels eines benutzerdefinierten Skripts durch Eingabe von durch Trennzeichen getrennte Listen von Variablen in der **ReadOnlyVariables** und **ReadWriteVariables** Felder auf der **Skript** auf der Seite der **Skript Transformations-Editor**. Beachten Sie, dass bei Variablennamen nach Groß-/Kleinschreibung unterschieden wird. Verwenden der **Wert** Eigenschaft Lese-und Schreibzugriff auf einzelne Variablen. Die Skriptkomponente führt erforderliche Sperrungen im Hintergrund aus, da das Skript die Variablen zur Laufzeit verarbeitet.  
  
> [!IMPORTANT]  
>  Die Auflistung der **ReadWriteVariables** steht nur in der **"PostExecute"** Methode, um die Leistung zu maximieren und das Risiko von Sperrkonflikten minimieren. Sie können daher den Wert einer Paketvariablen nicht direkt inkrementieren, während Sie jede Datenzeile verarbeiten. Inkrementieren Sie stattdessen den Wert einer lokalen Variablen, und legen Sie den Wert der Paketvariablen auf den Wert der lokalen Variablen in der **"PostExecute"** Methode auf, nachdem alle Daten wurden verarbeitet. Sie können auch die Eigenschaft <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> verwenden, um diese Einschränkung zu umgehen, wie später in diesem Thema beschrieben ist. Wenn Sie jedoch direkt in eine Paketvariable schreiben, während jede Zeile verarbeitet wird, wird die Leistung beeinträchtigt und das Risiko von Sperrkonflikten erhöht.  
  
 Weitere Informationen zu den **Skript** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) und [Skript Transformations-Editor &#40; Seite "Skript" &#41; ](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 Die Skriptkomponente erstellt eine **Variablen** Auflistungsklasse in der **ComponentWrapper** Projektelement mit stark typisierten Accessoreigenschaft für den Wert jeder vorkonfigurierten Variable, in dem die Eigenschaft den gleichen Namen wie die Variable selbst hat. Diese Auflistung abgelesen der **Variablen** Eigenschaft von der **ScriptMain** Klasse. Die Accessoreigenschaft bietet entsprechend Lese- oder Lese-/Schreibberechtigung für den Wert der Variable. Angenommen, wenn Sie eine ganzzahlige Variable mit dem Namen hinzugefügt haben `MyIntegerVariable` auf die **ReadOnlyVariables** Liste können Sie dessen Wert abrufen in Ihrem Skript mithilfe des folgenden Codes:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 Für die Arbeit mit Variablen in der Skriptkomponente können Sie auch die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>-Eigenschaft (Aufruf mit `Me.VariableDispenser`) verwenden. In diesem Fall verwenden Sie nicht die benannten, typisierten Accessoreigenschaften für Variablen, sondern greifen direkt auf die Variablen zu. Bei der Verwendung von <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> müssen Sie die Sperrsemantik und die Umwandlung von Datentypen für variable Werte in Ihrem Code berücksichtigen. Wenn Sie mit Variablen arbeiten möchten, die zur Entwurfszeit nicht zur Verfügung stehen, sondern programmgesteuert zur Laufzeit erstellt werden, müssen Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>-Eigenschaft statt der benannten, typisierten Accessoreigenschaften verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Variablen](../../../integration-services/integration-services-ssis-variables.md)   
 [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
