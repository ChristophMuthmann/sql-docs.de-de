---
title: Beim Codieren und Debuggen der Skriptkomponente | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
caps.latest.revision: 66
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ff6c9814547a83439717f8a88d3bd52be80c4ca5
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="coding-and-debugging-the-script-component"></a>Codieren und Debuggen der Skriptkomponente
  Im [!INCLUDE[ssIS](../../../includes/ssis-md.md)]-Designer weist die Skriptkomponente zwei Modi auf: Metadatenentwurfsmodus und Codeentwurfsmodus. Beim Öffnen der **Skript Transformations-Editor**, die Komponente wird im metadatenentwurfsmodus, in dem Metadaten konfiguriert und Komponenteneigenschaften festlegen. Nachdem Sie die Eigenschaften der Skriptkomponente festgelegt und die Eingaben und Ausgaben im Metadatenentwurfsmodus konfiguriert haben, können Sie zum Schreiben des benutzerdefinierten Skripts in den Codeentwurfsmodus wechseln. Weitere Informationen zum metadatenentwurfsmodus und codeentwurfsmodus finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
## <a name="writing-the-script-in-code-design-mode"></a>Schreiben des Skripts im Codeentwurfsmodus  
  
### <a name="script-component-development-environment"></a>Skriptkomponenten-Entwicklungsumgebung  
 Zum Schreiben des Skripts klicken Sie auf **Bearbeitungsskript** auf die **Skript** auf der Seite der **Skript Transformations-Editor** So öffnen die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE. Die VSTA IDE enthält alle Standardfunktionen der [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET-Umgebung wie den [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]-Editor mit Farbcodierung, IntelliSense und den Objektkatalog.  
  
 Skriptcode wird in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# geschrieben. Geben Sie die Skriptsprache aus, durch Festlegen der **ScriptLanguage** Eigenschaft in der **Skript Transformations-Editor**. Falls Sie lieber eine andere Programmiersprache verwenden möchten, können Sie in Ihrer bevorzugten Sprache eine benutzerdefinierte Assembly entwickeln und ihre Funktionen aus dem Code in der Skriptkomponente aufrufen.  
  
 Das in der Skriptkomponente erstellte Skript wird in der Paketdefinition gespeichert. Es gibt keine separate Skriptdatei. Deshalb hat die Verwendung der Skriptkomponente keinen Einfluss auf die Paketbereitstellung.  
  
> [!NOTE]  
>  Beim Entwurf des Pakets wird der Skriptcode vorübergehend in eine Projektdatei geschrieben. Da das Speichern vertraulicher Informationen in einer Datei ein potenzielles Sicherheitsrisiko ist, wird empfohlen, dass Sie vertraulichen Informationen wie Kennwörter nicht in den Skriptcode enthalten.  
  
 Standardmäßig **Option Strict** ist in der IDE deaktiviert.  
  
### <a name="script-component-project-structure"></a>Skriptkomponenten-Projektstruktur  
 Die Leistungsfähigkeit der Skriptkomponente rührt daher, dass Infrastrukturcode erstellt werden kann, mit dem der erforderliche Codeumfang reduziert werden kann. Für diese Funktion ist es erforderlich, dass Eingaben und Ausgaben mit den zugehörigen Spalten und Eigenschaften festgelegt und im Voraus bekannt sind. Aus diesem Grund können nachträgliche Änderungen an den Metadaten der Komponente dazu führen, dass der von Ihnen geschriebene Code ungültig wird. Dies verursacht während der Ausführung des Pakets Kompilierungsfehler.  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>Projektelemente und -klassen im Skriptkomponentenprojekt  
 Wenn Sie zum codeentwurfsmodus wechseln, wird die VSTA IDE wird geöffnet und zeigt die **ScriptMain** -Projektelement. Die **ScriptMain** Projektelement enthält die bearbeitbare **ScriptMain** Klasse dient als Eintrag für das Skript verwenden und die, in dem Sie Code schreiben. Die Codeelemente in der Klasse variieren abhängig davon, welche Programmiersprache Sie für den Skripttask gewählt haben.  
  
 Das Skriptprojekt enthält zwei zusätzliche, automatisch generierte und schreibgeschützte Projektelemente:  
  
-   Die **ComponentWrapper** -Projektelement enthält drei Klassen:  
  
    -   Die **UserComponent** -Klasse, die erbt <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> und enthält die Methoden und Eigenschaften, die Sie zum Verarbeiten von Daten und für die Interaktion mit dem Paket verwenden. Die **ScriptMain** Klasse erbt von der **UserComponent** Klasse.  
  
    -   Ein **Verbindungen** -Auflistungsklasse mit Verweisen auf die Verbindungen, die auf der Seite Verbindungs-Manager den Skript-Transformations-Editor ausgewählt.  
  
    -   Ein **Variablen** -Auflistungsklasse mit Verweisen zu den Variablen, die eingegeben werden, der **ReadOnlyVariable** und **ReadWriteVariables** Eigenschaften auf der **Skript** auf der Seite der **Skript Transformations-Editor**.  
  
-   Die **BufferWrapper** Projektelement enthält eine Klasse, die von erben <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> für jede konfigurierte Eingabe und Ausgabe auf die **Eingaben und Ausgaben** auf der Seite der **Skript Transformations-Editor**. Jede dieser Klassen enthält typisierte Accessoreigenschaften, die mit den konfigurierten Eingabe- und Ausgabespalten übereinstimmen, sowie die Datenflusspuffer, in denen sich diese Spalten befinden.  
  
 Informationen zur Verwendung dieser Objekte, Methoden und Eigenschaften finden Sie unter [Grundlegendes zu den Script Component Object Model](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md). Informationen dazu, wie die Methoden und Eigenschaften dieser Klassen in einem bestimmten Typ von Skriptkomponente verwenden, finden Sie im Abschnitt [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Die Beispielthemen enthalten auch vollständige Codebeispiele.  
  
 Beim Konfigurieren der Skriptkomponente als Transformation, die **ScriptMain** Projektelement enthält die folgenden automatisch generierten Code. Die Codevorlage bietet auch eine Übersicht über die Skriptkomponente und zusätzliche Informationen über das Abrufen und Bearbeiten von SSIS-Objekten, z. B. Variablen, Ereignisse und Verbindungen.  
  
```vb  
' Microsoft SQL Server Integration Services Script Component  
' Write scripts using Microsoft Visual Basic 2008.  
' ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _  
<CLSCompliant(False)> _  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub PreExecute()  
        MyBase.PreExecute()  
        '  
        ' Add your code here for preprocessing or remove if not needed  
        '  
    End Sub  
  
    Public Overrides Sub PostExecute()  
        MyBase.PostExecute()  
        '  
        ' Add your code here for postprocessing or remove if not needed  
        ' You can set read/write variables here, for example:  
        ' Me.Variables.MyIntVar = 100  
        '  
    End Sub  
  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
        '  
        ' Add your code here  
        '  
    End Sub  
  
End Class  
```  
  
```csharp  
/* Microsoft SQL Server Integration Services user script component  
*  Write scripts using Microsoft Visual C# 2008.  
*  ScriptMain is the entry point class of the script.*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]  
public class ScriptMain : UserComponent  
{  
  
    public override void PreExecute()  
    {  
        base.PreExecute();  
        /*  
          Add your code here for preprocessing or remove if not needed  
        */  
    }  
  
    public override void PostExecute()  
    {  
        base.PostExecute();  
        /*  
          Add your code here for postprocessing or remove if not needed  
          You can set read/write variables here, for example:  
          Variables.MyIntVar = 100  
        */  
    }  
  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
        /*  
          Add your code here  
        */  
    }  
  
}  
```  
  
#### <a name="additional-project-items-in-the-script-component-project"></a>Zusätzliche Projektelemente im Skriptkomponentenprojekt  
 Das skriptkomponentenprojekt kann Elemente der Standardnummer enthalten **ScriptMain** Element. Sie können dem Projekt Klassen, Module, Codedateien und Ordner hinzufügen und die Ordner zum Organisieren von Elementgruppen verwenden.  
  
 Alle Elemente, die Sie hinzufügen, werden im Paket beibehalten.  
  
#### <a name="references-in-the-script-component-project"></a>Verweise im Skriptkomponentenprojekt  
 Sie können Verweise auf verwaltete Assemblys hinzufügen, indem Sie mit der rechten Maustaste im skripttaskprojekt **Projektexplorer**, und klicken Sie dann auf **Verweis hinzufügen**. Weitere Informationen finden Sie unter [verweisen auf andere Assemblys in Projektmappen Scripting](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md).  
  
> [!NOTE]  
>  Sie können Projektverweise anzeigen, in die VSTA IDE in **Klassenansicht** oder im **Projektexplorer**. Öffnen Sie diese Fenster über das **Ansicht** Menü. Sie können über einen neuen Verweis hinzufügen der **Projekt** im Menü aus **Projektexplorer**, oder aus **Klassenansicht**.  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>Interagieren mit Paketen in der Skriptkomponente  
 Das benutzerdefinierte Skript, das in der Skriptkomponente geschrieben wird, kann mithilfe von stark typisierten  Accessoren in automatisch generierten Basisklassen auf Variablen und Verbindungs-Manager aus dem entsprechenden Paket zugreifen und diese verwenden. Die Variablen und Verbindungs-Manager müssen vor dem Wechseln in den Codeentwurfsmodus konfiguriert werden, wenn sie für das Skript zur Verfügung stehen sollen. Sie können auch Ereignisse auslösen und die Protokollierung von Ihrem Skriptkomponentencode ausführen.  
  
 Die automatisch generierten Projektelemente im Skriptkomponentenprojekt stellen die folgenden Objekte, Methoden und Eigenschaften zum Interagieren mit dem Paket bereit.  
  
|Funktion des Pakets|Zugriffsmethode|  
|---------------------|-------------------|  
|Variablen|Verwenden Sie die benannten, typisierten Accessoreigenschaften in der **Variablen** -Auflistungsklasse im die **ComponentWrapper** Projektelement, verfügbar gemacht werden, über die **Variablen** Eigenschaft von der **ScriptMain** Klasse.<br /><br /> Die **PreExecute** Methode kann nur für schreibgeschützte Variablen zugreifen. Die **"PostExecute"** Methode kann Zugriff auf beide schreibgeschützten und Lese-/schreibvariablen.|  
|Verbindungen|Verwenden Sie die benannten, typisierten Accessoreigenschaften in der **Verbindungen** -Auflistungsklasse im die **ComponentWrapper** Projektelement, verfügbar gemacht werden, über die **Verbindungen** Eigenschaft von der **ScriptMain** Klasse.|  
|Ereignisse|Lösen Ereignisse mit der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> Eigenschaft von der **ScriptMain** Klasse und die **auslösen\<X >** Methoden der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> Schnittstelle.|  
|Protokollierung|Protokollierungen werden mit der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> Methode der **ScriptMain** Klasse.|  
  
## <a name="debugging-the-script-component"></a>Debuggen der Skriptkomponente  
 Legen Sie zum Debuggen des Codes in der Skriptkomponente mindestens einen Breakpoint fest, und schließen Sie dann die VSTA IDE, um das Paket in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] auszuführen. Wenn die Ausführung der Skriptkomponente beginnt, wird die VSTA IDE erneut geöffnet und der Code schreibgeschützt angezeigt. Nachdem die Ausführung den Breakpoint erreicht hat, können Sie die Variablenwerte untersuchen und den übrigen Code schrittweise durchgehen.  
  
> [!NOTE]  
>  Sie können eine Skriptkomponente nicht debuggen, wenn sie als Teil eines untergeordneten Pakets in einem Task Paket ausführen ausgeführt wird. Breakpoints, die Sie in der Skriptkomponente im untergeordneten Paket festlegen, werden unter diesen Umständen ignoriert. Sie können das untergeordnete Paket normalerweise debuggen, indem Sie es getrennt ausführen.  
  
> [!NOTE]  
>  Wenn Sie ein Paket debuggen, das mehrere Skriptkomponenten enthält, debuggt der Debugger eine Skriptkomponente. Das System kann eine andere Skriptkomponente debuggen, wenn der Debugger wie im Fall eines Foreach- oder For-Schleifencontainers abgeschlossen wird.  
  
 Sie können die Ausführung der Skriptkomponente auch mit den folgenden Methoden überwachen:  
  
-   Unterbrechen Sie die Ausführung und eine modale Meldung angezeigt, mit der **MessageBox.Show** Methode in der **"System.Windows.Forms"** Namespace. (Entfernen Sie diesen Code, nachdem der Debugprozess abgeschlossen wurde.)  
  
-   Lösen Sie Ereignisse für Informationsmeldungen, Warnungen und Fehler aus. Die Methoden FireInformation FireWarning und FireError zeigen die Ereignisbeschreibung in Visual Studio **Ausgabe** Fenster. Allerdings FireProgress-Methode, die Console.Write-Methode und Console.WriteLine Methode zeigen keine Informationen in den **Ausgabe** Fenster. Nachrichten aus dem FireProgress-Ereignis angezeigt wird, auf die **Status** Registerkarte [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Weitere Informationen finden Sie unter [Auslösen von Ereignissen in der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md).  
  
-   Protokollieren Sie Ereignisse oder benutzerdefinierte Meldungen an aktivierte Protokollanbieter. Weitere Informationen finden Sie unter [Logging in the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md).  
  
 Wenn Sie nur die Ausgabe einer Skriptkomponente als Quelle oder Transformation, ohne Speichern der Daten an ein Ziel konfiguriert untersuchen möchten kann, beenden Sie den Datenfluss mit einer [Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md) , und fügen Sie einen Daten-Viewer an die Ausgabe der Skriptkomponente. Informationen zu den Daten-Viewer finden Sie unter [Debugging Data Flow](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 Weitere Informationen zum Codieren der Skriptkomponente finden Sie in den folgenden Themen in diesem Abschnitt.  
  
 [Grundlegendes zu den Script Component Object Model](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 Erklärt, wie die von der Skriptkomponente bereitgestellten Objekte, Methoden und Eigenschaften verwendet werden.  
  
 [Verweisen auf andere Assemblys in Skriptlösungen](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 Erklärt, wie auf Objekte von der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Klassenbibliothek in der Skriptkomponente verwiesen wird.  
  
 [Simulieren einer Fehlerausgabe für die Skriptkomponente](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 Erklärt, wie eine Fehlerausgabe für die Zeilen simuliert wird, die während der Verarbeitung durch die Skriptkomponente Fehler auslösen.  
  
## <a name="external-resources"></a>Externe Ressourcen  
  
-   Blogeintrag, [VSTA Setup und Konfiguration Troubles für SSIS 2008 and R2 Installationen](http://go.microsoft.com/fwlink/?LinkId=215661), auf blogs.msdn.com.  
  
## <a name="see-also"></a>Siehe auch  
 [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
  
  

