---
title: "Einschließen einer Datenprofilerstellungs-Task im Paket-Workflow | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling task [Integration Services], using output in workflow
ms.assetid: 39a51586-6977-4c45-b80b-0157a54ad510
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ea3c68e0320216c81ce2a47f426112dd4a25f22f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="incorporate-a-data-profiling-task-in-package-workflow"></a>Einschließen einer Datenprofilerstellungs-Tasks in den Paket-Workflow
  Datenprofilerstellung und Cleanup sind in den Anfangsphasen keine Kandidaten für einen automatisierten Prozess. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]erfordert die Ausgabe des Datenprofilerstellungs-Tasks normalerweise eine visuelle Analyse und menschliches Urteilsvermögen, um zu bestimmen, ob gemeldete Verstöße von Bedeutung sind oder übertrieben. Auch nach Erkennen eines Datenqualitätsproblems ist nach wie vor ein sorgfältig durchdachter Plan erforderlich, der den besten Bereinigungsansatz beinhaltet.  
  
 Nachdem Kriterien für die Datenqualität festgelegt wurden, möchten Sie jedoch möglicherweise eine regelmäßige Analyse und Bereinigung der Datenquelle automatisieren. Betrachten Sie folgende Szenarios:  
  
-   **Überprüfen der Datenqualität vor dem inkrementellen Laden** Berechnen Sie mit dem Datenprofilerstellungs-Task das Profil für das Spalten-NULL-Verhältnis neuer Daten, die für die CustomerName-Spalte in einer Customers-Tabelle bestimmt sind. Wenn der Prozentanteil von NULL-Werten größer als 20 % ist, senden Sie eine E-Mail-Nachricht mit der Profilausgabe an den Operator, und beenden Sie das Paket. Andernfalls setzen Sie das inkrementelle Laden fort.  
  
-   **Automatisieren des Cleanups, wenn die angegebenen Bedingungen erfüllt werden.** Berechnen Sie mit dem Datenprofilerstellungs-Task das Wertinklusionsprofil der State-Spalte anhand einer Suchtabelle für Status und der ZIP Code/Postal Code-Spalte anhand einer Suchtabelle für Postleitzahlen. Wenn die Einschlussstärke der Statuswerte kleiner als 80 % ist, die Einschlussstärke der Postleitzahlwerte hingegen größer als 99 %, weist dies auf zwei Dinge hin. Erstens sind die Statusdaten ungültig. Zweitens sind die Postleitzahldaten gültig. Starten Sie einen Datenflusstask, der die Statusdaten durch eine Suche des richtigen Werts aus dem aktuellen Postleitzahlwert bereinigt.  
  
 Nachdem Sie einen Workflow vorliegen haben, in den Sie den Datenflusstask integrieren können, müssen Sie sich mit den Schritten, die zum Hinzufügen dieses Tasks erforderlich sind, vertraut machen. Im nächsten Abschnitt wird der allgemeine Prozess zur Integration des Datenflusstasks beschrieben. In den beiden letzten Abschnitten wird beschrieben, wie Sie den Datenflusstask entweder direkt mit einer Datenquelle oder mit transformierten Daten aus dem Datenfluss verbinden.  
  
## <a name="defining-a-general-workflow-for-the-data-flow-task"></a>Definieren eines allgemeinen Workflows für den Datenflusstask  
 Das folgende Verfahren erklärt den allgemeinen Ansatz zur Verwendung der Ausgabe des Datenprofilerstellungs-Tasks im Workflow eines Pakets.  
  
#### <a name="to-use-the-output-of-the-data-profiling-task-programmatically-in-a-package"></a>So verwenden Sie die Ausgabe des Datenprofilerstellungs-Tasks programmgesteuert in einem Paket  
  
1.  Fügen Sie den Datenprofilerstellungs-Task zu einem Paket hinzu, und konfigurieren Sie ihn.  
  
2.  Konfigurieren Sie Paketvariablen, um die Werte, die Sie von den Profilergebnissen abrufen möchten, zu speichern.  
  
3.  Fügen Sie einen Skripttask hinzu, und konfigurieren Sie ihn. Verbinden Sie den Skripttask mit dem Datenprofilerstellungs-Task. Schreiben Sie Code in den Skripttask, der die gewünschten Werte aus der Ausgabedatei des Datenprofilerstellungs-Tasks liest und die Paketvariablen auffüllt.  
  
4.  Verwenden Sie in den Rangfolgeneinschränkungen, mit denen der Skripttask mit Downstream-Verzweigungen verbunden wird, Ausdrücke, die den Workflow anhand der Werte der Variablen steuern.  
  
 Beim Integrieren des Datenprofilerstellungs-Tasks in den Workflow eines Pakets berücksichtigen Sie die beiden folgenden Taskfunktionen:  
  
-   **Taskausgabe**. Der Datenprofilerstellungs-Task schreibt die Ausgabe in eine Datei oder eine Paketvariable im XML-Format, das dem Schema DataProfile.xsd entsprechend strukturiert ist. Daher müssen Sie die XML-Ausgabe abfragen, wenn Sie die Profilergebnisse im bedingten Workflow eines Pakets verwenden möchten. Zur Abfrage dieser XML-Ausgabe verwenden Sie am besten die Xpath-Abfragesprache. Um sich die Struktur dieser XML-Ausgabe anzusehen, können Sie eine Beispielausgabedatei oder das Schema selbst öffnen. Zum Öffnen der Ausgabedatei oder des Schemas können Sie [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], einen anderen XML-Editor oder einen Texteditor wie Notepad verwenden.  
  
    > [!NOTE]  
    >  Einige der im Datenprofil-Viewer angezeigten Profilergebnisse sind berechnete Werte, die nicht direkt in der Ausgabe zu finden sind. Die Ausgabe des Profils für das Spalten-NULL-Verhältnis enthält beispielsweise die Gesamtzahl der Zeilen und die Anzahl der Zeilen mit NULL-Werten. Zur Berechnung des Spalten-NULL-Verhältnisses müssen Sie diese beiden Werte abfragen und anschließend den Prozentanteil der Zeilen mit NULL-Werten berechnen.  
  
-   **Taskeingabe**. Der Datenprofilerstellungs-Task liest seine Eingabe aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen. Daher müssen Sie die im Speicher befindlichen Daten in Stagingtabellen speichern, wenn Sie ein Profil für Daten erstellen möchten, die bereits geladen und in den Datenfluss transformiert wurden.  
  
 In den folgenden Abschnitten wird beschrieben, wie dieser allgemeine Workflow auf Profildaten angewendet wird, die direkt aus einer externen Datenquelle oder transformiert aus dem Datenflusstask stammen. In diesen Abschnitten wird außerdem erklärt, wie die Eingabe- und Ausgabeanforderungen des Datenflusstasks behandelt werden.  
  
## <a name="connecting-the-data-profiling-task-directly-to-an-external-data-source"></a>Direktes Verbinden des Datenprofilerstellungs-Tasks mit einer externen Datenquelle  
 Der Datenprofilerstellungs-Task erstellt Profile für Daten, die direkt aus einer Datenquelle stammen.  Zur Veranschaulichung dieser Funktion wird im folgenden Beispiel anhand des Datenprofilerstellungs-Tasks ein Profil für ein Spalten-NULL-Verhältnis für die Spalten der Person.Address-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank berechnet. Anschließend werden die Ergebnisse mithilfe eines Skripttasks aus der Ausgabedatei abgerufen, und Paketvariablen, die zur Steuerung des Workflows dienen können, werden aufgefüllt.  
  
> [!NOTE]  
>  Für dieses einfache Beispiel wurde die AddressLine2-Spalte ausgewählt, da diese Spalte einen hohen Anteil an NULL-Werten enthält.  
  
 Dieses Beispiel umfasst die folgenden Schritte:  
  
-   Konfigurieren der Verbindungs-Manager, die die Verbindung zur externen Datenquelle und zur Ausgabedatei mit den Profilergebnissen herstellen.  
  
-   Konfigurieren der Paketvariablen, die die vom Datenprofilerstellungs-Task benötigten Werte enthalten.  
  
-   Konfigurieren des Datenprofilerstellungs-Tasks, um das Profil für das Spalten-NULL-Verhältnis zu berechnen.  
  
-   Konfigurieren des Skripttasks, um die XML-Ausgabe vom Datenprofilerstellungs-Task zu verarbeiten.  
  
-   Konfigurieren der Rangfolgeneinschränkungen, mit denen gesteuert wird, welche Downstream-Verzweigungen im Workflow basierend auf den Ergebnissen des Datenprofilerstellungs-Tasks ausgeführt werden.  
  
### <a name="configure-the-connection-managers"></a>Konfigurieren der Verbindungs-Manager  
 Dieses Beispiel umfasst zwei Verbindungs-Manager:  
  
-   Einen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager, der eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank herstellt.  
  
-   Einen Dateiverbindungs-Manager, der die Ausgabedatei erstellt, in der die Ergebnisse des Datenprofilerstellungs-Tasks gespeichert werden.  
  
##### <a name="to-configure-the-connection-managers"></a>So konfigurieren Sie die Verbindungs-Manager  
  
1.  Erstellen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ein neues [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket.  
  
2.  Fügen Sie den [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager zum Paket hinzu. Konfigurieren Sie diesen Verbindungs-Manager für die Verwendung des .NET-Datenanbieters für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) und für die Verbindung mit einer verfügbaren Instanz der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank.  
  
     Der Verbindungs-Manager hat standardmäßig die folgenden Namen: \<Servername >. "AdventureWorks1".  
  
3.  Fügen Sie einen Dateiverbindungs-Manager zum Paket hinzu. Konfigurieren Sie diesen Verbindungs-Manager für das Erstellen der Ausgabedatei für den Datenprofilerstellungs-Task.  
  
     In diesem Beispiel wird der Dateiname "DataProfile1.xml" verwendet. Standardmäßig ist der Name des Verbindungs-Managers mit dem Dateinamen identisch.  
  
### <a name="configure-the-package-variables"></a>Konfigurieren der Paketvariablen  
 In diesem Beispiel werden zwei Paketvariablen verwendet:  
  
-   Die ProfileConnectionName-Variable übergibt den Namen des Dateiverbindungs-Managers an den Skripttask.  
  
-   Die AddressLine2NullRatio-Variable übergibt das berechnete NULL-Verhältnis für diese Spalte vom Skripttask an das Paket.  
  
##### <a name="to-configure-the-package-variables-that-will-hold-profile-results"></a>So konfigurieren Sie die Paketvariablen, die Profilergebnisse speichern  
  
-   Fügen Sie im Fenster **Variablen** die beiden folgenden Paketvariablen hinzu, und konfigurieren Sie sie:  
  
    -   Geben Sie den Namen **ProfileConnectionName**für eine der Variablen ein, und legen Sie den Typ dieser Variablen auf **String**fest.  
  
    -   Geben Sie den Namen **AddressLine2NullRatio**für die andere Variable ein, und legen Sie den Typ dieser Variablen auf **Double**fest.  
  
### <a name="configure-the-data-profiling-task"></a>Konfigurieren des Datenprofilerstellungs-Tasks  
 Der Datenprofilerstellungs-Task muss wie folgt konfiguriert werden:  
  
-   Um die Daten zu verwenden, die der [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager als Eingabe angibt.  
  
-   Um ein Profil für ein Spalten-NULL-Verhältnis für die Eingabedaten zu erstellen.  
  
-   Um die Profilergebnisse in der Datei zu speichern, die dem Dateiverbindungs-Manager zugeordnet ist.  
  
##### <a name="to-configure-the-data-profiling-task"></a>So konfigurieren Sie den Datenprofilerstellungs-Task  
  
1.  Fügen Sie der Ablaufsteuerung einen Datenprofilerstellungs-Task hinzu.  
  
2.  Öffnen Sie den **Editor für den Datenprofilerstellungs-Task** , um den Task zu konfigurieren.  
  
3.  Wählen Sie auf der Seite **Allgemein** für **Ziel**den Namen des Dateiverbindungs-Managers aus, den Sie zuvor konfiguriert haben.  
  
4.  Erstellen Sie auf der Seite **Profilanforderungen** des Editors ein neues Profil für ein Spalten-NULL-Verhältnis.  
  
5.  Wählen Sie im Bereich **Anforderungseigenschaften** für **ConnectionManager**den [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager aus, den Sie zuvor konfiguriert haben. Wählen Sie dann für **TableOrView**Person.Address aus.  
  
6.  Schließen Sie den Editor für den Datenprofilerstellungs-Task.  
  
### <a name="configure-the-script-task"></a>Konfigurieren des Skripttasks  
 Der Skripttask muss so konfiguriert werden, dass die Ergebnisse aus der Ausgabedatei abgerufen und die zuvor konfigurierten Paketvariablen aufgefüllt werden.  
  
##### <a name="to-configure-the-script-task"></a>So konfigurieren Sie den Skripttask  
  
1.  Fügen Sie der Ablaufsteuerung einen Skripttask hinzu.  
  
2.  Verbinden Sie den Skripttask mit dem Datenprofilerstellungs-Task.  
  
3.  Öffnen Sie den **Skripttask-Editor** , um den Task zu konfigurieren.  
  
4.  Wählen Sie auf der Seite **Skript** die bevorzugte Programmiersprache aus. Machen Sie die beiden Paketvariablen anschließend für das Skript verfügbar:  
  
    1.  Für **ReadOnlyVariables**wählen Sie **ProfileConnectionName**aus.  
  
    2.  Für **ReadWriteVariables**wählen Sie **AddressLine2NullRatio**aus.  
  
5.  Wählen Sie **Skript bearbeiten** aus, um die Skriptentwicklungsumgebung zu öffnen.  
  
6.  Fügen Sie einen Verweis zum System.Xml-Namespace hinzu.  
  
7.  Geben Sie den Beispielcode ein, der der Programmiersprache entspricht:  
  
    ```vb  
    Imports System  
    Imports Microsoft.SqlServer.Dts.Runtime  
    Imports System.Xml  
  
    Public Class ScriptMain  
  
      Private FILENAME As String = "C:\ TEMP\DataProfile1.xml"  
      Private PROFILE_NAMESPACE_URI As String = "http://schemas.microsoft.com/DataDebugger/"  
      Private NULLCOUNT_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()"  
      Private TABLE_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table"  
  
      Public Sub Main()  
  
        Dim profileConnectionName As String  
        Dim profilePath As String  
        Dim profileOutput As New XmlDocument  
        Dim profileNSM As XmlNamespaceManager  
        Dim nullCountNode As XmlNode  
        Dim nullCount As Integer  
        Dim tableNode As XmlNode  
        Dim rowCount As Integer  
        Dim nullRatio As Double  
  
        ' Open output file.  
        profileConnectionName = Dts.Variables("ProfileConnectionName").Value.ToString()  
        profilePath = Dts.Connections(profileConnectionName).ConnectionString  
        profileOutput.Load(profilePath)  
        profileNSM = New XmlNamespaceManager(profileOutput.NameTable)  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI)  
  
        ' Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM)  
        nullCount = CType(nullCountNode.Value, Integer)  
  
        ' Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM)  
        rowCount = CType(tableNode.Attributes("RowCount").Value, Integer)  
  
        ' Compute and return null ratio.  
        nullRatio = nullCount / rowCount  
        Dts.Variables("AddressLine2NullRatio").Value = nullRatio  
  
        Dts.TaskResult = Dts.Results.Success  
  
      End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using Microsoft.SqlServer.Dts.Runtime;  
    using System.Xml;  
  
    public class ScriptMain  
    {  
  
      private string FILENAME = "C:\\ TEMP\\DataProfile1.xml";  
      private string PROFILE_NAMESPACE_URI = "http://schemas.microsoft.com/DataDebugger/";  
      private string NULLCOUNT_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()";  
      private string TABLE_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table";  
  
      public void Main()  
      {  
  
        string profileConnectionName;  
        string profilePath;  
        XmlDocument profileOutput = new XmlDocument();  
        XmlNamespaceManager profileNSM;  
        XmlNode nullCountNode;  
        int nullCount;  
        XmlNode tableNode;  
        int rowCount;  
        double nullRatio;  
  
        // Open output file.  
        profileConnectionName = Dts.Variables["ProfileConnectionName"].Value.ToString();  
        profilePath = Dts.Connections[profileConnectionName].ConnectionString;  
        profileOutput.Load(profilePath);  
        profileNSM = new XmlNamespaceManager(profileOutput.NameTable);  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI);  
  
        // Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM);  
        nullCount = (int)nullCountNode.Value;  
  
        // Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM);  
        rowCount = (int)tableNode.Attributes["RowCount"].Value;  
  
        // Compute and return null ratio.  
        nullRatio = nullCount / rowCount;  
        Dts.Variables["AddressLine2NullRatio"].Value = nullRatio;  
  
        Dts.TaskResult = Dts.Results.Success;  
  
      }  
  
    }  
    ```  
  
    > [!NOTE]  
    >  Der in diesem Verfahren angezeigte Beispielcode veranschaulicht, wie die Ausgabe des Datenprofilerstellungs-Tasks aus einer Datei geladen wird. Um die Ausgabe des Datenprofilerstellungs-Tasks stattdessen aus einer Paketvariablen zu laden, verwenden Sie den alternativen Beispielcode, der im Anschluss an dieses Verfahren dargestellt wird.  
  
8.  Schließen Sie die Skriptentwicklungsumgebung, und schließen Sie dann den Skripttask-Editor.  
  
#### <a name="alternative-codereading-the-profile-output-from-a-variable"></a>Alternativer Code – Lesen der Profilausgabe aus einer Variablen  
 Das vorherige Verfahren zeigt, wie die Ausgabe des Datenprofilerstellungs-Tasks aus einer Datei geladen wird. Eine alternative Methode wäre allerdings, diese Ausgabe aus einer Paketvariablen zu laden. Um die Ausgabe aus einer Variablen zu laden, müssen Sie den Beispielcode wie folgt ändern:  
  
-   Rufen Sie die **LoadXml** -Methode der **XmlDocument** -Klasse statt der **Load** -Methode auf.  
  
-   Fügen Sie im Skripttask-Editor den Namen der Paketvariablen, die die Profilausgabe enthält, zur **ReadOnlyVariables** -Liste des Tasks hinzu.  
  
-   Übergeben Sie der **LoadXML** -Methode den string-Wert der Variablen, wie im folgenden Codebeispiel dargestellt. (In diesem Beispiel wird "ProfileOutput" als Name der Paketvariable verwendet, die die Profilausgabe enthält.)  
  
    ```vb  
    Dim outputString As String  
    outputString = Dts.Variables("ProfileOutput").Value.ToString()  
    ...  
    profileOutput.LoadXml(outputString)  
    ```  
  
    ```csharp  
    string outputString;  
    outputString = Dts.Variables["ProfileOutput"].Value.ToString();  
    ...  
    profileOutput.LoadXml(outputString);  
    ```  
  
### <a name="configure-the-precedence-constraints"></a>Konfigurieren der Rangfolgeneinschränkungen  
 Die Rangfolgeneinschränkungen müssen so konfiguriert werden, dass gesteuert wird, welche Downstream-Verzweigungen im Workflow basierend auf den Ergebnissen des Datenprofilerstellungs-Tasks ausgeführt werden.  
  
##### <a name="to-configure-the-precedence-constraints"></a>So konfigurieren Sie die Rangfolgeneinschränkungen  
  
-   Verwenden Sie in den Rangfolgeneinschränkungen, mit denen der Skripttask mit Downstream-Verzweigungen verbunden wird, Ausdrücke, die den Workflow anhand der Werte der Variablen steuern.  
  
     Sie können beispielsweise den **Auswertungsvorgang** der Rangfolgeneinschränkung auf **Ausdruck und Einschränkung**festlegen. Dann können Sie `@AddressLine2NullRatio < .90` als Wert des Ausdrucks verwenden. Dadurch folgt der Workflow dem ausgewählten Pfad, wenn die vorherigen Tasks erfolgreich sind und wenn der Anteil der NULL-Werte in der ausgewählten Spalte unter 90 % beträgt.  
  
## <a name="connecting-the-data-profiling-task-to-transformed-data-from-the-data-flow"></a>Verbinden des Datenprofilerstellungs-Tasks mit transformierten Daten aus dem Datenfluss  
 Statt direkt ein Profil der Daten aus einer Datenquelle zu erstellen, können Sie ein Profil für Daten erstellen, die bereits geladen und im Datenfluss transformiert wurden. Der Datenprofilerstellungs-Task funktioniert jedoch nur mit persistenten Daten, nicht mit Daten im Arbeitsspeicher. Aus diesem Grund müssen Sie zuerst eine Zielkomponente verwenden, um die transformierten Daten in einer Stagingtabelle zu speichern.  
  
> [!NOTE]  
>  Wenn Sie den Datenprofilerstellungs-Task konfigurieren, müssen Sie vorhandene Tabellen und Spalten auswählen. Daher müssen Sie die Stagingtabelle zur Entwurfszeit erstellen, bevor Sie den Task konfigurieren können. Mit anderen Worten, dieses Szenario erlaubt keine Verwendung einer temporären Tabelle, die zur Laufzeit erstellt wird.  
  
 Nachdem Sie die Daten in einer Stagingtabelle gespeichert haben, können Sie die folgenden Aktionen ausführen:  
  
-   Erstellen Sie mit dem Datenprofilerstellungs-Task ein Profil der Daten.  
  
-   Lesen Sie mit einem Skripttask die Ergebnisse, wie weiter oben in diesem Thema beschrieben.  
  
-   Verwenden Sie diese Ergebnisse, um den nachfolgenden Workflow des Pakets zu steuern.  
  
 Das folgende Verfahren bietet den allgemeinen Ansatz zur Verwendung des Datenprofilerstellungs-Tasks, um ein Profil der vom Datenfluss transformierten Daten zu erstellen. Viele dieser Schritte sind identisch mit den bereits für die Erstellung eines Profils für Daten, die direkt aus einer externen Datenquelle stammen, beschriebenen. Schauen Sie sich diese bereits beschriebenen Schritte an, um weitere Informationen zum Konfigurieren der verschiedenen Komponenten zu erhalten.  
  
#### <a name="to-use-the-data-profiling-task-in-the-data-flow"></a>So verwenden Sie den Datenprofilerstellungs-Task im Datenfluss  
  
1.  Erstellen Sie ein Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Fügen Sie im Datenfluss die entsprechenden Quellen und die Transformationen hinzu, konfigurieren und verbinden Sie sie.  
  
3.  Fügen Sie im Datenfluss eine Zielkomponente, die die transformierten Daten in einer Stagingtabelle speichert, hinzu, konfigurieren und verbinden Sie sie.  
  
4.  Fügen Sie in der Ablaufsteuerung einen Datenprofilerstellungs-Task, der die gewünschten Profile anhand der transformierten Daten in der Stagingtabelle berechnet, hinzu, konfigurieren und verbinden Sie ihn. Verbinden Sie den Datenprofilerstellungs-Task mit dem Datenflusstask.  
  
5.  Konfigurieren Sie Paketvariablen, um die Werte, die Sie von den Profilergebnissen abrufen möchten, zu speichern.  
  
6.  Fügen Sie einen Skripttask hinzu, und konfigurieren Sie ihn. Verbinden Sie den Skripttask mit dem Datenprofilerstellungs-Task. Schreiben Sie Code in den Skripttask, der die gewünschten Werte aus der Ausgabedatei des Datenprofilerstellungs-Tasks liest und die Paketvariablen auffüllt.  
  
7.  Verwenden Sie in den Rangfolgeneinschränkungen, mit denen der Skripttask mit Downstream-Verzweigungen verbunden wird, Ausdrücke, die den Workflow anhand der Werte der Variablen steuern.  
  
## <a name="see-also"></a>Siehe auch  
 [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)   
 [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md)  
  
  
