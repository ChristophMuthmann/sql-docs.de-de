---
title: "Überwachen von Leistungsindikatoren with the Script Task | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- performance counters [Integration Services]
- SSIS Script task, performance counters
- custom performance counters [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], performance counters
- counters [Integration Services]
ms.assetid: 86609bf1-cae6-435e-a58d-41bdfc521e94
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: fd733f7d2fdf9c5d1181df6e7856d729e9a58026
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="monitoring-performance-counters-with-the-script-task"></a>Überwachen von Leistungsindikatoren mit dem Skripttask
  Administratoren müssen möglicherweise die Leistung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen überwachen, die komplexe Transformationen mit großen Datenmengen durchführen. Die **System.Diagnostics** Namespace, der die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] stellt Klassen bereit, für die Verwendung von vorhandenen Leistungsindikatoren und zum Erstellen eigener Leistungsindikatoren.  
  
 Leistungsindikatoren speichern Leistungsdaten von Anwendungen, anhand derer Sie die Leistung von Software über einen bestimmten Zeitraum analysieren können. Leistungsindikatoren können überwacht werden lokal oder Remote mithilfe der **Systemmonitor** Tool. Für die spätere Verzweigung der Ablaufsteuerung im Paket können Sie die Werte der Leistungsindikatoren in Variablen speichern.  
  
 Als Alternative zum Verwenden von Leistungsindikatoren können Sie heraufstufen können die <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> Ereignis mit der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> Eigenschaft von der **Dts** Objekt. Das <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A>-Ereignis gibt sowohl inkrementelle Status- als auch abgeschlossene Prozentsatzinformationen an die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Laufzeit zurück.  
  
> [!NOTE]  
>  Wenn Sie einen Task erstellen möchten, den Sie einfacher in mehreren Paketen wiederverwenden können, empfiehlt es sich, den Code in diesem Skripttaskbeispiel als Ausgangspunkt für einen benutzerdefinierten Task zu verwenden. Weitere Informationen finden Sie unter [Entwickeln eines benutzerdefinierten Tasks](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Description  
 Im folgenden Beispiel wird ein benutzerdefinierter Leistungsindikator erstellt und anschließend inkrementiert. Zuerst wird ermittelt, ob der Leistungsindikator bereits vorhanden ist. Wenn der Leistungsindikator noch nicht erstellt wurde, ruft das Skript die **erstellen** Methode der **PerformanceCounterCategory** Objekt zu erstellen. Anschließend inkrementiert das Skript den Leistungsindikator. Im Beispiel folgt schließlich die bewährte Methode des Aufrufs der **schließen** -Methode für den Leistungsindikator, wenn er nicht mehr benötigt wird.  
  
> [!NOTE]  
>  Zum Erstellen einer neuen Leistungsindikatorkategorie und eines Leistungsindikators sind Administratorrechte erforderlich. Außerdem bleiben die neue Kategorie und der Leistungsindikator nach der Erstellung auf dem Computer erhalten.  
  
#### <a name="to-configure-this-script-task-example"></a>So konfigurieren Sie dieses Skripttaskbeispiel  
  
-   Verwenden einer **Importe** -Anweisung im Code zum Importieren der **System.Diagnostics** Namespace.  
  
### <a name="example-code"></a>Beispielcode  
  
```vb  
Public Sub Main()  
  
    Dim myCounter As PerformanceCounter  
  
    Try  
        'Create the performance counter if it does not already exist.  
        If Not _  
        PerformanceCounterCategory.Exists("TaskExample") Then  
            PerformanceCounterCategory.Create("TaskExample", _  
                "Task Performance Counter Example", "Iterations", _  
                "Number of times this task has been called.")  
        End If  
  
        'Initialize the performance counter.  
        myCounter = New PerformanceCounter("TaskExample", _  
            "Iterations", String.Empty, False)  
  
        'Increment the performance counter.  
        myCounter.Increment()  
  
         myCounter.Close()  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Task Performance Counter Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
  
public class ScriptMain  
{  
  
public void Main()  
        {  
  
            PerformanceCounter myCounter;  
  
            try  
            {  
                //Create the performance counter if it does not already exist.  
                if (!PerformanceCounterCategory.Exists("TaskExample"))  
                {  
                    PerformanceCounterCategory.Create("TaskExample", "Task Performance Counter Example", "Iterations", "Number of times this task has been called.");  
                }  
  
                //Initialize the performance counter.  
                myCounter = new PerformanceCounter("TaskExample", "Iterations", String.Empty, false);  
  
                //Increment the performance counter.  
                myCounter.Increment();  
  
                myCounter.Close();  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Task Performance Counter Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
```  

