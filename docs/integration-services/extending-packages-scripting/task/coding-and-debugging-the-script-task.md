---
title: Beim Codieren und Debuggen des Skripttasks | Microsoft Docs
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
- Script task [Integration Services], debugging
- SSIS Script task, development environment
- SSIS Script task, debugging
- Script task [Integration Services], development environment
- Script task [Integration Services], coding
- debugging [Integration Services], scripts
- VSTA
- SSIS Script task, coding
ms.assetid: 687c262f-fcab-42e8-92ae-e956f3d92d69
caps.latest.revision: 81
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8c706fc1db3e31130a7754b9e4c3d16f9a13eaf4
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="coding-and-debugging-the-script-task"></a>Codieren und Debuggen des Skripttasks
  Nach dem Konfigurieren des Skripttasks-Task in der **Skripttask-Editor**, Sie Ihren benutzerdefinierten Code schreiben, in der Skripttask-Entwicklungsumgebung.  
  
## <a name="script-task-development-environment"></a>Skripttask-Entwicklungsumgebung  
 Der Skripttask verwendet [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) als Entwicklungsumgebung für das Skript selbst.  
  
 Skriptcode wird in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# geschrieben. Geben Sie die Skriptsprache aus, durch Festlegen der **ScriptLanguage** Eigenschaft in der **Skripttask-Editor**. Falls Sie lieber eine andere Programmiersprache verwenden möchten, können Sie in Ihrer bevorzugten Sprache eine benutzerdefinierte Assembly entwickeln und ihre Funktionen aus dem Code im Skripttask aufrufen.  
  
 Das im Skripttask erstellte Skript wird in der Paketdefinition gespeichert. Es gibt keine separate Skriptdatei. Deshalb hat die Verwendung des Skripttasks keinen Einfluss auf die Paketbereitstellung.  
  
> [!NOTE]  
>  Wenn Sie das Paket entwerfen und das Skript debuggen, wird der Skriptcode vorübergehend in eine Projektdatei geschrieben. Da das Speichern vertraulicher Informationen in einer Datei ein Sicherheitsrisiko darstellt, sollte der Skriptcode keine vertraulichen Daten wie Kennwörter enthalten.  
  
 Standardmäßig **Option Strict** ist in der IDE deaktiviert.  
  
## <a name="script-task-project-structure"></a>Skripttask-Projektstruktur  
 Wenn Sie das in einem Skripttask enthaltene Skript erstellen oder ändern, öffnet VSTA ein neues leeres Projekt oder erneut das vorhandene Projekt. Die Erstellung dieses VSTA-Projekts wirkt sich nicht auf die Paketbereitstellug aus, da das Projekt in der Paketdatei gespeichert wird. Der Skripttask erstellt keine weiteren Dateien.  
  
### <a name="project-items-and-classes-in-the-script-task-project"></a>Projektelemente und -klassen im Skripttaskprojekt  
 Standardmäßig enthält das im VSTA-Projekt-Explorer-Fenster angezeigte skripttaskprojekt ein einzelnes Element **ScriptMain**. Die **ScriptMain** Element enthält wiederum eine einzelne Klasse, die auch als **ScriptMain**. Die Codeelemente in der Klasse variieren abhängig davon, welche Programmiersprache Sie für den Skripttask gewählt haben:  
  
-   Wenn der Skripttask konfiguriert ist, für die [!INCLUDE[vb_orcas_long](../../../includes/vb-orcas-long-md.md)] Programmiersprache, die **ScriptMain** -Klasse verfügt über eine öffentliche Unterroutine namens **Main**. Die **ScriptMain.Main** -Unterroutine ist die Methode, die von der Laufzeit aufgerufen, wenn Sie Ihre Skripttask ausführen.  
  
     Standardmäßig ist der einzige Code in der **Main** -Unterroutine eines neuen Skripts wird die Zeile `Dts.TaskResult = ScriptResults.Success`. Diese Zeile informiert die Laufzeit, dass der Task erfolgreich durchgeführt wurde. Die **Dts.TaskResult** Eigenschaft wird im erläutert [Returning Results from the Script Task](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md).  
  
-   Wenn der Skripttask für die Visual C#-Programmiersprache, konfiguriert ist die **ScriptMain** -Klasse verfügt über eine öffentliche Methode **Main**. Die Methode wird aufgerufen, wenn der Skripttask ausgeführt wird.  
  
     Wird standardmäßig die **Main** Methode enthält die Zeile `Dts.TaskResult = (int)ScriptResults.Success`. Diese Zeile informiert die Laufzeit, dass der Task erfolgreich durchgeführt wurde.  
  
 Die **ScriptMain** Element enthalten Klassen außer der **ScriptMain** Klasse. Klassen stehen nur dem Skripttask, in dem sie sich befinden, zur Verfügung.  
  
 Wird standardmäßig die **ScriptMain** Projektelement enthält die folgenden automatisch generierten Code. Die Codevorlage bietet auch eine Übersicht über den Skripttask, und zusätzliche Informationen über das Abrufen und Bearbeiten von SSIS-Objekten, z. B. Variablen, Ereignisse und Verbindungen.  
  
```vb  
' Microsoft SQL Server Integration Services Script Task  
' Write scripts using Microsoft Visual Basic 2008.  
' The ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Runtime.VSTAProxy  
  
<System.AddIn.AddIn("ScriptMain", Version:="1.0", Publisher:="", Description:="")> _  
Partial Class ScriptMain  
  
Private Sub ScriptMain_Startup(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Startup  
  
End Sub  
  
Private Sub ScriptMain_Shutdown(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Shutdown  
Try  
' Unlock variables from the read-only and read-write variable collection properties  
If (Dts.Variables.Count <> 0) Then  
Dts.Variables.Unlock()  
End If  
Catch ex As Exception  
        End Try  
End Sub  
  
Enum ScriptResults  
Success = DTSExecResult.Success  
Failure = DTSExecResult.Failure  
End Enum  
  
' The execution engine calls this method when the task executes.  
' To access the object model, use the Dts property. Connections, variables, events,  
' and logging features are available as members of the Dts property as shown in the following examples.  
'  
' To reference a variable, call Dts.Variables("MyCaseSensitiveVariableName").Value  
' To post a log entry, call Dts.Log("This is my log text", 999, Nothing)  
' To fire an event, call Dts.Events.FireInformation(99, "test", "hit the help message", "", 0, True)  
'  
' To use the connections collection use something like the following:  
' ConnectionManager cm = Dts.Connections.Add("OLEDB")  
' cm.ConnectionString = "Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;"  
'  
' Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.  
'   
' To open Help, press F1.  
  
Public Sub Main()  
'  
' Add your code here  
'  
Dts.TaskResult = ScriptResults.Success  
End Sub  
  
End Class  
```  
  
```csharp  
/*  
   Microsoft SQL Server Integration Services Script Task  
   Write scripts using Microsoft Visual C# 2008.  
   The ScriptMain is the entry point class of the script.  
*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime.VSTAProxy;  
using System.Windows.Forms;  
  
namespace ST_1bcfdbad36d94f8ba9f23a10375abe53.csproj  
{  
    [System.AddIn.AddIn("ScriptMain", Version = "1.0", Publisher = "", Description = "")]  
    public partial class ScriptMain  
    {  
        private void ScriptMain_Startup(object sender, EventArgs e)  
        {  
  
        }  
  
        private void ScriptMain_Shutdown(object sender, EventArgs e)  
        {  
            try  
            {  
                // Unlock variables from the read-only and read-write variable collection properties  
                if (Dts.Variables.Count != 0)  
                {  
                    Dts.Variables.Unlock();  
                }  
            }  
            catch  
            {  
            }  
        }  
  
        #region VSTA generated code  
        private void InternalStartup()  
        {  
            this.Startup += new System.EventHandler(ScriptMain_Startup);  
            this.Shutdown += new System.EventHandler(ScriptMain_Shutdown);  
        }  
        enum ScriptResults  
        {  
            Success = DTSExecResult.Success,  
            Failure = DTSExecResult.Failure  
        };  
  
        #endregion  
  
        /*  
The execution engine calls this method when the task executes.  
To access the object model, use the Dts property. Connections, variables, events,  
and logging features are available as members of the Dts property as shown in the following examples.  
  
To reference a variable, call Dts.Variables["MyCaseSensitiveVariableName"].Value;  
To post a log entry, call Dts.Log("This is my log text", 999, null);  
To fire an event, call Dts.Events.FireInformation(99, "test", "hit the help message", "", 0, true);  
  
To use the connections collection use something like the following:  
ConnectionManager cm = Dts.Connections.Add("OLEDB");  
cm.ConnectionString = "Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;";  
  
Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.  
  
To open Help, press F1.  
*/  
  
        public void Main()  
        {  
            // TODO: Add your code here  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
    }  
```  
  
### <a name="additional-project-items-in-the-script-task-project"></a>Zusätzliche Projektelemente im Skripttaskprojekt  
 Das skripttaskprojekt kann Elemente der Standardnummer enthalten **ScriptMain** Element. Sie können Klassen, Module und Codedateien zum Projekt hinzufügen. Außerdem können Sie Ordner verwenden, um Elementgruppen zu organisieren. Alle Elemente, die Sie hinzufügen, werden im Paket beibehalten.  
  
### <a name="references-in-the-script-task-project"></a>Verweise im Skripttaskprojekt  
 Sie können Verweise auf verwaltete Assemblys hinzufügen, indem Sie mit der rechten Maustaste im skripttaskprojekt **Projektexplorer**, und klicken Sie dann auf **Verweis hinzufügen**. Weitere Informationen finden Sie unter [verweisen auf andere Assemblys in Projektmappen Scripting](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md).  
  
> [!NOTE]  
>  Sie können Projektverweise anzeigen, in die VSTA IDE in **Klassenansicht** oder im **Projektexplorer**. Öffnen Sie diese Fenster über das **Ansicht** Menü. Sie können über einen neuen Verweis hinzufügen der **Projekt** im Menü aus **Projektexplorer**, oder aus **Klassenansicht**.  
  
## <a name="interacting-with-the-package-in-the-script-task"></a>Interagieren mit Paketen im Skripttask  
 Der Skripttask verwendet die globale **Dts** -Objekt, das eine Instanz von der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> Klasse und ihre Member für die Interaktion mit dem entsprechenden Paket und die [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Common Language Runtime.  
  
 Die folgende Tabelle enthält die wichtigsten öffentlichen Elemente von der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> -Klasse, die Code des Skripttasks über das globale verfügbar gemacht wird **Dts** Objekt. In den Themen in diesem Abschnitt wird die Verwendung dieser Elemente detaillierter erläutert.  
  
|Member|Zweck|  
|------------|-------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>|Bietet Zugriff auf im Paket definierte Verbindungs-Manager.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>|Liefert eine Ereignisschnittstelle, damit der Skripttask Fehler, Warnungen und Informationsmeldungen auslösen kann.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>|Bietet eine einfache Möglichkeit, ein einzelnes Objekt an die Laufzeit auszugeben (zusätzlich zu den **TaskResult**), auch für die workflowverzweigung verwendet werden kann.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>|Protokolliert Informationen wie den Taskstatus und die Ergebnisse bei aktivierten Protokollanbietern.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>|Meldet den Erfolg oder Misserfolg des Tasks.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Transaction%2A>|Stellt ggf. die Transaktion bereit, innerhalb derer der Taskcontainer ausgeführt wird.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>|Ermöglicht den Zugriff auf die Variablen in der **ReadOnlyVariables** und **ReadWriteVariables** Taskeigenschaften für die Verwendung innerhalb des Skripts.|  
  
 Die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel>-Klasse enthält auch einige öffentliche Elemente, die Sie wahrscheinlich nicht verwenden.  
  
|Member|Description|  
|------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>|Die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>-Eigenschaft ermöglicht einen einfacheren Zugriff auf Variablen. Sie können zwar <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> verwenden, müssen jedoch explizit Methoden aufrufen, um Variablen für das Lesen und Schreiben zu sperren und die Sperre wieder aufzuheben. Der Skripttask erledigt die Sperrsemantik für Sie, wenn Sie die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>-Eigenschaft verwenden.|  
  
## <a name="debugging-the-script-task"></a>Debuggen des Skripttasks  
 Legen Sie zum Debuggen des Codes im Skripttask mindestens einen Breakpoint fest, und schließen Sie dann die VSTA IDE, um das Paket in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] auszuführen. Wenn die Ausführung des Skripttasks beginnt, wird die VSTA IDE erneut geöffnet und der Code schreibgeschützt angezeigt. Nachdem die Ausführung den Breakpoint erreicht hat, können Sie die Variablenwerte untersuchen und den übrigen Code schrittweise durchgehen.  
  
> [!WARNING]  
>  Sie können den Skripttask debuggen, wenn Sie das Paket im 64-Bit-Modus ausführen.  
  
> [!NOTE]  
>  Sie müssen das Paket ausführen, um den Skripttask zu debuggen. Wenn Sie nur den einzelnen Task ausführen, werden Breakpoints im Skripttaskcode ignoriert.  
  
> [!NOTE]  
>  Sie können einen Skripttask nicht debuggen, wenn Sie ihn als Teil eines untergeordneten Pakets aus dem Task Paket ausführen ausführen. Breakpoints, die Sie im Skripttask in dem untergeordneten Paket festlegen, werden unter diesen Umständen ignoriert. Sie können das untergeordnete Paket normalerweise debuggen, indem Sie es getrennt ausführen.  
  
> [!NOTE]  
>  Wenn Sie ein Paket debuggen, das mehrere Skripttasks enthält, debuggt der Debugger einen Skripttask. Das System kann einen anderen Skripttask debuggen, wenn der Debugger wie im Fall eines Foreach- oder For-Schleifencontainers abgeschlossen wird.  
  
## <a name="external-resources"></a>Externe Ressourcen  
  
-   Blogeintrag, [VSTA Setup und Konfiguration Troubles für SSIS 2008 and R2 Installationen](http://go.microsoft.com/fwlink/?LinkId=215661), auf blogs.msdn.com.  
  
## <a name="see-also"></a>Siehe auch  
 [Verweisen auf andere Assemblys in Skriptlösungen](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)   
 [Konfigurieren des Skripttasks in der Skripttask-Editor](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
  
  
