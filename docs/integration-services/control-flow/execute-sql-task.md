---
title: "SQL ausf&#252;hren (Task) | Microsoft Docs"
ms.custom: 
  - "ssisdev020617"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executesqltask.f1"
  - "sql13.dts.designer.executesqltask.general.f1"
  - "sql13.dts.designer.executesqltask.parametermapping.f1"
  - "sql13.dts.designer.executesqltask.resultset.f1"
helpviewer_keywords: 
  - "Transact-SQL-Anweisungen, SSIS"
  - "Anweisungen [Integration Services]"
  - "Batches [Integration Services]"
  - "SQL ausführen (Task) [Integration Services]"
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
caps.latest.revision: 115
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 113
---
# SQL ausf&#252;hren (Task)
  Mit dem Task SQL ausführen werden SQL-Anweisungen oder gespeicherte Prozeduren aus einem Paket ausgeführt. Dieser Task kann eine oder mehrere SQL-Anweisungen enthalten, die sequenziell ausgeführt werden. Der Task SQL ausführen kann für folgende Zwecke verwendet werden:  
  
-   Abschneiden einer Tabelle oder Sicht, um das Einfügen von Daten vorzubereiten.  
  
-   Erstellen, Ändern und Löschen von Datenbankobjekten, wie z. B. Tabellen und Sichten.  
  
-   Neuerstellen von Fakten- und Dimensionstabellen vor dem Laden von Daten.  
  
-   Ausführen gespeicherter Prozeduren. Wenn Sie mithilfe einer SQL-Anweisung eine gespeicherte Prozedur aufrufen, die Ergebnisse von einer temporären Tabelle zurückgibt, verwenden Sie die WITH RESULT SETS-Option, um Metadaten für das Resultset zu definieren.  
  
-   Speichern des Rowsets, das von einer Abfrage zurückgegeben wird, in einer Variablen.  
  
 Der Task SQL ausführen kann in Kombination mit dem Foreach-Schleifencontainer und dem For-Schleifencontainer verwendet werden, um mehrere SQL-Anweisungen auszuführen. Diese Container implementieren das Wiederholen von Ablaufsteuerungen in einem Paket und können den Task SQL ausführen wiederholt ausführen. Beispielsweise kann ein Paket mithilfe des Foreach-Schleifencontainers Dateien in einem Ordner aufzählen und einen Task SQL ausführen wiederholt ausführen, um die in jeder Datei gespeicherte SQL-Anweisung auszuführen.  
  
## Herstellen einer Verbindung mit einer Datenquelle  
 Der Task SQL ausführen kann verschiedene Arten von Verbindungs-Managern für die Verbindung mit der Datenquelle verwenden, in der die SQL-Anweisung oder die gespeicherte Prozedur ausgeführt wird. Der Task kann die in der folgenden Tabelle aufgeführten Verbindungstypen verwenden.  
  
|Verbindungstyp|Verbindungs-Manager|  
|---------------------|------------------------|  
|EXCEL|[Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC-Verbindungs-Manager](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[ADO-Verbindungs-Manager](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition-Verbindungs-Manager](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## Erstellen von SQL-Anweisungen  
 Die Quelle für die SQL-Anweisungen, die von diesem Task verwendet werden, kann eine Taskeigenschaft mit einer Anweisung, eine Verbindung mit einer Datei mit mindestens einer Anweisung oder der Name einer Variablen sein, die eine Anweisung enthält. Die SQL-Anweisungen müssen in dem Dialekt des Quelldatenbank-Managementsystems (DBMS, Database Management System) erstellt werden. Weitere Informationen finden Sie unter [Integration Services-Abfragen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-queries.md).  
  
 Wenn die SQL-Anweisungen in einer Datei gespeichert sind, stellt der Task mithilfe eines Verbindungs-Managers eine Verbindung mit der Datei her. Weitere Informationen finden Sie unter [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 Im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer können Sie zum Eingeben von SQL-Anweisungen das Dialogfeld **Editor für den Task SQL ausführen** oder den **Abfrage-Generator**verwenden. Dabei handelt es sich um eine grafische Benutzeroberfläche zum Erstellen von SQL-Abfragen. Weitere Informationen finden Sie unter [Editor für den Task „SQL ausführen“ &#40;Seite „Allgemein“&#41;](../Topic/Execute%20SQL%20Task%20Editor%20\(General%20Page\).md) und [Abfrage-Generator](../Topic/Query%20Builder.md).  
  
> [!NOTE]  
>  Gültige SQL-Anweisungen, die außerhalb des Tasks "SQL ausführen" erstellt wurden, werden vom Task "SQL ausführen" möglicherweise nicht erfolgreich analysiert.  
  
> [!NOTE]  
>  Der Task "SQL ausführen" verwendet den **RecognizeAll** ParseMode-Enumerationswert. Weitere Informationen finden Sie unter [ManagedBatchParser-Namespace](http://go.microsoft.com/fwlink/?LinkId=223617).  
  
## Senden mehrerer Anweisungen in einem Batch  
 Wenn Sie für den Task "SQL ausführen" mehrere Anweisungen einschließen, können Sie diese gruppieren und als Batch ausführen. Verwenden Sie den GO-Befehl, um das Ende eines Batches zu signalisieren. Alle SQL-Anweisungen zwischen zwei GO-Befehlen werden als Batch an den OLE DB-Anbieter zum Ausführen gesendet. Der SQL-Befehl kann mehrere durch GO-Befehle getrennte Batches einschließen.  
  
 Bezüglich der SQL-Anweisungen, die als Batch gruppiert werden können, sind Einschränkungen vorhanden. Weitere Informationen finden Sie unter [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md).  
  
 Falls der Task SQL ausführen einen Batch mit SQL-Anweisungen ausführt, gelten für den Batch die folgenden Regeln:  
  
-   Nur eine Anweisung kann ein Resultset zurückgeben. Sie muss außerdem die erste Anweisung im Batch sein.  
  
-   Falls das Resultset Ergebnisbindungen verwendet, müssen die Abfragen die gleiche Anzahl von Spalten zurückgeben. Falls die Abfragen eine andere Anzahl von Spalten zurückgeben, wird für den Task ein Fehler gemeldet. Bei einem Fehler des Tasks werden jedoch die von dem Task ausgeführten Abfragen, wie z. B. DELETE- oder INSERT-Abfragen, möglicherweise erfolgreich ausgeführt.  
  
-   Falls für die Ergebnisbindungen Spaltennamen verwendet werden, muss die Abfrage Spalten zurückgeben, die die gleichen Namen wie die vom Task verwendeten Resultsetnamen besitzen. Wenn die Spalten fehlen, wird für den Task ein Fehler gemeldet.  
  
-   Falls für den Task die Parameterbindung verwendet wird, müssen alle Abfragen im Batch die gleiche Anzahl und Art von Parametern aufweisen.  
  
## Ausführen parametrisierter SQL-Befehle  
 SQL-Anweisungen und gespeicherte Prozeduren verwenden häufig Eingabeparameter, Ausgabeparameter und Rückgabecodes. Der Task SQL ausführen unterstützt die **Input**-, **Output**- und **ReturnValue** -Parametertypen. Sie können den **Input** -Typ für Eingabeparameter, den **Output** -Typ für Ausgabeparameter und den **ReturnValue** -Typ für Rückgabecodes verwenden.  
  
> [!NOTE]  
>  Parameter können in einem Task SQL ausführen nur verwendet werden, wenn dies vom Datenanbieter unterstützt wird.  
  
 Informationen über die Verwendung von Parametern und Rückgabecodes im Task „SQL ausführen“ finden Sie unter [Parameter und Rückgabecodes im Task „SQL ausführen“](../Topic/Parameters%20and%20Return%20Codes%20in%20the%20Execute%20SQL%20Task.md).  
  
## Angeben eines Resultsettyps  
 Der Typ des SQL-Befehls bestimmt, ob für den Task SQL ausführen ein Resultset zurückgegeben wird. Beispielsweise gibt eine SELECT-Anweisung in der Regel ein Resultset zurück, eine INSERT-Anweisung jedoch nicht. Das Resultset einer SELECT-Anweisung kann keine Zeilen, eine Zeile oder viele Zeilen enthalten. Gespeicherte Prozeduren können außerdem einen ganzzahligen Wert, der als Rückgabecode bezeichnet wird, zurückgeben, um den Ausführungsstatus der Prozedur anzuzeigen. In diesem Fall besteht das Resultset aus einer einzelnen Zeile.  
  
 Informationen über das Abrufen von Resultsets aus SQL-Befehlen im Task „SQL ausführen“ finden Sie unter [Resultsets im Task „SQL ausführen“](../Topic/Result%20Sets%20in%20the%20Execute%20SQL%20Task.md).  
  
## Problembehandlung des Tasks SQL ausführen  
 Sie können die vom Task SQL ausführen an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktionen können Sie Probleme bei SQL-Befehlen behandeln, die vom Task SQL ausführen ausgeführt werden. Aktivieren Sie zum Protokollieren der vom Task SQL ausführen an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandlung von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Gelegentlich gibt ein SQL-Befehl oder eine gespeicherte Prozedur mehrere Resultsets zurück. Zu diesen Resultsets gehören nicht nur Rowsets, die das Ergebnis von **SELECT** -Abfragen sind, sondern auch einzelne Werte als Ergebnis von Fehlern in der **RAISERROR** -Anweisung oder **PRINT** -Anweisung. Ob der Task Fehler in Resultsets nach dem ersten Resultset ignoriert, hängt vom verwendeten Typ des Verbindungs-Managers ab:  
  
-   Wenn Sie OLE DB- und ADO-Verbindungs-Manager verwenden, ignoriert der Task die Resultsets, die nach dem ersten Resultset auftreten. Das bedeutet, dass der Task bei diesen Verbindungs-Managern einen von einem SQL-Befehl oder einer gespeicherten Prozedur zurückgegebenen Fehler ignoriert, wenn der Fehler nicht Teil des ersten Resultsets ist.  
  
-   Wenn Sie ODBC- und ADO.NET-Verbindungs-Manager verwenden, werden die Resultsets, die nach dem ersten Resultset auftreten, vom Task nicht ignoriert. Bei diesen Verbindungs-Managern erzeugt der Task einen Fehler, wenn ein anderes Resultset als das erste Resultset einen Fehler aufweist.  
  
### Benutzerdefinierte Protokolleinträge  
 In der folgenden Tabelle wird der benutzerdefinierte Protokolleintrag für den Task <legacyBold>SQL ausführen</legacyBold> beschrieben. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) und [Benutzerdefinierte Meldungen für die Protokollierung](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|Enthält Informationen zu den Ausführungsphasen der SQL-Anweisung. Protokolleinträge werden geschrieben, wenn der Task eine Verbindung mit der Datenbank erhält, wenn der Task beginnt, die SQL-Anweisung vorzubereiten, und nachdem die Ausführung der SQL-Anweisung abgeschlossen wurde. Der Protokolleintrag für die Vorbereitungsphase schließt die vom Task verwendete SQL-Anweisung ein.|  
  
## Konfigurieren des Tasks SQL ausführen  
 Es gibt folgende Möglichkeiten, um den Task SQL ausführen zu konfigurieren:  
  
-   Geben Sie den Verbindungs-Manager an, der zum Verbinden mit einer Datenbank verwendet werden soll.  
  
-   Geben Sie den Resultsettyp an, der von der SQL-Anweisung zurückgegeben wird.  
  
-   Geben Sie ein Timeout für die SQL-Anweisungen an.  
  
-   Geben Sie die Quelle der SQL-Anweisung an.  
  
-   Geben Sie an, ob der Task die Vorbereitungsphase für die SQL-Anweisung auslässt.  
  
-   Wenn Sie den ADO-Verbindungstyp verwenden, müssen Sie angeben, ob es sich bei der SQL-Anweisung um eine gespeicherte Prozedur handelt. Für andere Verbindungstypen ist diese Eigenschaft schreibgeschützt und weist immer den Wert **false** auf.  
  
 Eigenschaften können Sie programmgesteuert oder mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „SQL ausführen“ &#40;Seite „Allgemein“&#41;](../Topic/Execute%20SQL%20Task%20Editor%20\(General%20Page\).md)  
  
-   [Editor für den Task „SQL ausführen“ &#40;Seite „Parameterzuordnung“&#41;](../Topic/Execute%20SQL%20Task%20Editor%20\(Parameter%20Mapping%20Page\).md)  
  
-   [Editor für den Task „SQL ausführen“ &#40;Seite „Resultset“&#41;](../Topic/Execute%20SQL%20Task%20Editor%20\(Result%20Set%20Page\).md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Programmgesteuertes Konfigurieren des Tasks SQL ausführen  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask>  
  
## Verwandte Aufgaben  
  
-   [Zuordnen von Abfrageparametern zu Variablen in einem Task SQL ausführen](../Topic/Map%20Query%20Parameters%20to%20Variables%20in%20an%20Execute%20SQL%20Task.md)  
  
-   [Zuordnen von Resultsets zu Variablen in einem Task 'SQL ausführen'](../Topic/Map%20Result%20Sets%20to%20Variables%20in%20an%20Execute%20SQL%20Task.md)  
  
## Verwandte Inhalte  
  
-   [Parameter und Rückgabecodes im Task 'SQL ausführen'](../Topic/Parameters%20and%20Return%20Codes%20in%20the%20Execute%20SQL%20Task.md)  
  
-   [Resultsets im Task 'SQL ausführen'](../Topic/Result%20Sets%20in%20the%20Execute%20SQL%20Task.md)  
  
-   [Transact-SQL-Referenz &#40;Datenbankmodul&#41;](../../t-sql/transact-sql-reference-database-engine.md)  
  
-   Blogeintrag [Neue Datums- und Uhrzeitfunktionen in SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=239783)auf mssqltips.com.  
  
  