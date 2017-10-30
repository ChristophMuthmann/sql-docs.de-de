---
title: Verwenden von Variablen im Skripttask | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- Foreach Loop containers
- Script task [Integration Services], variables
- scripts [Integration Services], variables
- Variables property
- Variable object
- SSIS Script task, variables
- variables [Integration Services], Script task
ms.assetid: 593b5961-4bfa-4ce1-9531-a251c34e89d3
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ccfd7ce8e8f53d12dac3b021d5f62bd03947413d
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-task"></a>Verwenden von Variablen im Skripttask
  Variablen ermöglichen es dem Skripttask, Daten mit anderen Objekten im Paket auszutauschen. Weitere Informationen finden Sie unter [Integration Services &#40;SSIS&#41; Variables](../../../integration-services/integration-services-ssis-variables.md).  
  
 Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> Eigenschaft von der **Dts** Objekt, das über Lese- und Schreibberechtigungen für <xref:Microsoft.SqlServer.Dts.Runtime.Variable> Objekte im Paket.  
  
> [!NOTE]  
>  Die <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> Eigenschaft von der <xref:Microsoft.SqlServer.Dts.Runtime.Variable> -Klasse ist vom Typ **Objekt**. Da der Skripttask **Option Strict** aktiviert ist, müssen Sie eine Umwandlung der <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> Eigenschaft in den entsprechenden Typ, bevor Sie ihn verwenden können.  
  
 Sie vorhandene Variablen hinzufügen, die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> und <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> in Listen der **Skripttask-Editor** , die sie für das benutzerdefinierte Skript verfügbar zu machen. Beachten Sie, dass bei Variablennamen nach Groß-/Kleinschreibung unterschieden wird. Innerhalb des Skripts greifen Sie auf Variablen beider Typen über die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> Eigenschaft von der **Dts** Objekt. Verwenden der **Wert** Eigenschaft Lese-und Schreibzugriff auf einzelne Variablen. Der Skripttask verwaltet Sperren transparent, während das Skript die Werte von Variablen liest und ändert.  
  
 Mithilfe der <xref:Microsoft.SqlServer.Dts.Runtime.Variables.Contains%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Runtime.Variables>-Auflistung, die von der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>-Eigenschaft zurückgegeben wird, können Sie das Vorhandensein von Variablen vor ihrer Verwendung im Code überprüfen.  
  
 Sie können auch die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> Eigenschaft (Dts.VariableDispenser), um die Arbeit mit Variablen im Skripttask. Bei der Verwendung von <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> müssen Sie die Sperrsemantik und die Umwandlung von Datentypen für variable Werte in Ihrem Code berücksichtigen. Wenn Sie mit Variablen arbeiten möchten, die zur Entwurfszeit nicht zur Verfügung stehen, sondern programmgesteuert zur Laufzeit erstellt werden, müssen Sie möglicherweise auf die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>-Eigenschaft anstelle der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>-Eigenschaft zurückgreifen.  
  
## <a name="using-the-script-task-within-a-foreach-loop-container"></a>Verwenden des Skripttasks in einem Foreach-Schleifencontainer  
 Wenn ein Skripttask wiederholt innerhalb eines Foreach-Schleifencontainers ausgeführt wird, muss das Skript normalerweise auf den Inhalt des aktuellen Elements im Enumerator zugreifen. Bei der Verwendung eines Foreach-Dateienumerators muss das Skript beispielsweise über den aktuellen Dateinamen verfügen und bei der Verwendung eines Foreach-ADO-Enumerators über den Inhalt der Spalten in der aktuellen Datenzeile.  
  
 Variablen ermöglichen diese Kommunikation zwischen dem Foreach-Schleifencontainer und dem Skripttask. Auf der **Variablenzuordnungen** auf der Seite der **foreach-Schleifen-Editor**, weisen Sie die Variablen auf jedes Element der Daten, die von einem Enumerationselement zurückgegeben werden. Ein Foreach-Dateienumerator gibt z. B. nur am Index 0 einen Dateinamen zurück und erfordert daher nur eine Variablenzuordnung. Bei einem Enumerator, der in jeder Zeile mehrere Datenspalten zurückgibt, müssen Sie hingegen für jede Spalte, die Sie im Skripttask verwenden möchten, eine andere Variable zuordnen.  
  
 Nachdem Sie die Enumerationselemente Variablen zugeordnet haben, Sie hinzufügen die zugeordneten Variablen der **ReadOnlyVariables** Eigenschaft auf die **Skript** auf der Seite der **Skripttask-Editor** um für das Skript verfügbar zu machen. Ein Beispiel eines Skripttasks innerhalb einer ForEach-Schleifencontainer, der die Bilddateien in einem Ordner verarbeitet, finden Sie unter [arbeiten mit Bildern mithilfe des Skripttasks](../../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md).  
  
## <a name="variables-example"></a>Variablenbeispiel  
 Das folgende Beispiel veranschaulicht den Zugriff auf und die Verwendung von Variablen in einem Skripttask zur Ermittlung des Pfads eines Paket-Workflows. Im Beispiel wird davon ausgegangen, dass Sie ganzzahlige Variablen mit dem Namen erstellt haben `CustomerCount` und `MaxRecordCount` hinzugefügt wurden, und die **ReadOnlyVariables** Sammlung in der **Skripttask-Editor**. Die `CustomerCount`-Variable enthält die Anzahl an Kundendatensätzen, die importiert werden sollen. Falls der Wert höher als der Wert von `MaxRecordCount` ist, gibt der Skripttask eine Fehlermeldung aus. Falls der Fehler auftritt, weil der `MaxRecordCount`-Schwellenwert überschritten wurde, kann der Fehlerpfad des Workflows alle erforderlichen Cleanup-Schritte implementieren.  
  
 Um das Beispiel erfolgreich zu kompilieren, müssen Sie einen Verweis auf die Microsoft.SqlServer.ScriptTask-Assembly hinzufügen.  
  
```vb  
Public Sub Main()  
  
    Dim customerCount As Integer  
    Dim maxRecordCount As Integer  
  
    If Dts.Variables.Contains("CustomerCount") = True AndAlso _  
        Dts.Variables.Contains("MaxRecordCount") = True Then  
  
        customerCount = _  
            CType(Dts.Variables("CustomerCount").Value, Integer)  
        maxRecordCount = _  
            CType(Dts.Variables("MaxRecordCount").Value, Integer)  
  
    End If  
  
    If customerCount > maxRecordCount Then  
            Dts.TaskResult = ScriptResults.Failure  
    Else  
            Dts.TaskResult = ScriptResults.Success  
    End If  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
    {  
        int customerCount;  
        int maxRecordCount;  
  
        if (Dts.Variables.Contains("CustomerCount")==true&&Dts.Variables.Contains("MaxRecordCount")==true)  
  
        {  
            customerCount = (int) Dts.Variables["CustomerCount"].Value;  
            maxRecordCount = (int) Dts.Variables["MaxRecordCount"].Value;  
  
        }  
  
        if (customerCount>maxRecordCount)  
        {  
            Dts.TaskResult = (int)ScriptResults.Failure;  
        }  
        else  
        {  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Variablen](../../../integration-services/integration-services-ssis-variables.md)   
 [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

