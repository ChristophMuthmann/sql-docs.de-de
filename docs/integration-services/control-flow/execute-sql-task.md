---
title: "Task „SQL ausführen“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executesqltask.f1
- sql13.dts.designer.executesqltask.general.f1
- sql13.dts.designer.executesqltask.parametermapping.f1
- sql13.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
caps.latest.revision: "115"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ae247a65d28b039210dcf8d3243ae19ffde504cc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="execute-sql-task"></a>SQL ausführen (Task)
  Mit dem Task SQL ausführen werden SQL-Anweisungen oder gespeicherte Prozeduren aus einem Paket ausgeführt. Dieser Task kann eine oder mehrere SQL-Anweisungen enthalten, die sequenziell ausgeführt werden. Der Task SQL ausführen kann für folgende Zwecke verwendet werden:  
  
-   Abschneiden einer Tabelle oder Sicht, um das Einfügen von Daten vorzubereiten.  
  
-   Erstellen, Ändern und Löschen von Datenbankobjekten, wie z. B. Tabellen und Sichten.  
  
-   Neuerstellen von Fakten- und Dimensionstabellen vor dem Laden von Daten.  
  
-   Ausführen gespeicherter Prozeduren. Wenn Sie mithilfe einer SQL-Anweisung eine gespeicherte Prozedur aufrufen, die Ergebnisse von einer temporären Tabelle zurückgibt, verwenden Sie die WITH RESULT SETS-Option, um Metadaten für das Resultset zu definieren.  
  
-   Speichern des Rowsets, das von einer Abfrage zurückgegeben wird, in einer Variablen.  
  
 Der Task SQL ausführen kann in Kombination mit dem Foreach-Schleifencontainer und dem For-Schleifencontainer verwendet werden, um mehrere SQL-Anweisungen auszuführen. Diese Container implementieren das Wiederholen von Ablaufsteuerungen in einem Paket und können den Task SQL ausführen wiederholt ausführen. Beispielsweise kann ein Paket mithilfe des Foreach-Schleifencontainers Dateien in einem Ordner aufzählen und einen Task SQL ausführen wiederholt ausführen, um die in jeder Datei gespeicherte SQL-Anweisung auszuführen.  
  
## <a name="connect-to-a-data-source"></a>Herstellen einer Verbindung mit einer Datenquelle  
 Der Task SQL ausführen kann verschiedene Arten von Verbindungs-Managern für die Verbindung mit der Datenquelle verwenden, in der die SQL-Anweisung oder die gespeicherte Prozedur ausgeführt wird. Der Task kann die in der folgenden Tabelle aufgeführten Verbindungstypen verwenden.  
  
|Verbindungstyp|Verbindungs-Manager|  
|---------------------|------------------------|  
|EXCEL|[Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC-Verbindungs-Manager](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[ADO-Verbindungs-Manager](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition-Verbindungs-Manager](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="create-sql-statements"></a>Erstellen von SQL-Anweisungen  
 Die Quelle für die SQL-Anweisungen, die von diesem Task verwendet werden, kann eine Taskeigenschaft mit einer Anweisung, eine Verbindung mit einer Datei mit mindestens einer Anweisung oder der Name einer Variablen sein, die eine Anweisung enthält. Die SQL-Anweisungen müssen in dem Dialekt des Quelldatenbank-Managementsystems (DBMS, Database Management System) erstellt werden. Weitere Informationen finden Sie unter [Integration Services-Abfragen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-queries.md).  
  
 Wenn die SQL-Anweisungen in einer Datei gespeichert sind, stellt der Task mithilfe eines Verbindungs-Managers eine Verbindung mit der Datei her. Weitere Informationen finden Sie unter [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 Im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer können Sie zum Eingeben von SQL-Anweisungen das Dialogfeld **Editor für den Task SQL ausführen** oder den **Abfrage-Generator**verwenden. Dabei handelt es sich um eine grafische Benutzeroberfläche zum Erstellen von SQL-Abfragen. 
  
> [!NOTE]  
>  Gültige SQL-Anweisungen, die außerhalb des Tasks "SQL ausführen" erstellt wurden, werden vom Task "SQL ausführen" möglicherweise nicht erfolgreich analysiert.  
  
> [!NOTE]  
>  Der Task "SQL ausführen" verwendet den **RecognizeAll** ParseMode-Enumerationswert. Weitere Informationen finden Sie unter [ManagedBatchParser-Namespace](http://go.microsoft.com/fwlink/?LinkId=223617).  
  
## <a name="send-multiple-statements-in-a-batch"></a>Senden mehrerer Anweisungen in einem Batch  
 Wenn Sie für den Task "SQL ausführen" mehrere Anweisungen einschließen, können Sie diese gruppieren und als Batch ausführen. Verwenden Sie den GO-Befehl, um das Ende eines Batches zu signalisieren. Alle SQL-Anweisungen zwischen zwei GO-Befehlen werden als Batch an den OLE DB-Anbieter zum Ausführen gesendet. Der SQL-Befehl kann mehrere durch GO-Befehle getrennte Batches einschließen.  
  
 Bezüglich der SQL-Anweisungen, die als Batch gruppiert werden können, sind Einschränkungen vorhanden. Weitere Informationen finden Sie unter [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md).  
  
 Falls der Task SQL ausführen einen Batch mit SQL-Anweisungen ausführt, gelten für den Batch die folgenden Regeln:  
  
-   Nur eine Anweisung kann ein Resultset zurückgeben. Sie muss außerdem die erste Anweisung im Batch sein.  
  
-   Falls das Resultset Ergebnisbindungen verwendet, müssen die Abfragen die gleiche Anzahl von Spalten zurückgeben. Falls die Abfragen eine andere Anzahl von Spalten zurückgeben, wird für den Task ein Fehler gemeldet. Bei einem Fehler des Tasks werden jedoch die von dem Task ausgeführten Abfragen, wie z. B. DELETE- oder INSERT-Abfragen, möglicherweise erfolgreich ausgeführt.  
  
-   Falls für die Ergebnisbindungen Spaltennamen verwendet werden, muss die Abfrage Spalten zurückgeben, die die gleichen Namen wie die vom Task verwendeten Resultsetnamen besitzen. Wenn die Spalten fehlen, wird für den Task ein Fehler gemeldet.  
  
-   Falls für den Task die Parameterbindung verwendet wird, müssen alle Abfragen im Batch die gleiche Anzahl und Art von Parametern aufweisen.  
  
## <a name="run-parameterized-sql-commands"></a>Ausführen parametrisierter SQL-Befehle  
 SQL-Anweisungen und gespeicherte Prozeduren verwenden häufig Eingabeparameter, Ausgabeparameter und Rückgabecodes. Der Task SQL ausführen unterstützt die **Input**-, **Output**- und **ReturnValue** -Parametertypen. Sie können den **Input** -Typ für Eingabeparameter, den **Output** -Typ für Ausgabeparameter und den **ReturnValue** -Typ für Rückgabecodes verwenden.  
  
> [!NOTE]  
>  Parameter können in einem Task SQL ausführen nur verwendet werden, wenn dies vom Datenanbieter unterstützt wird.  
  
## <a name="specify-a-result-set-type"></a>Angeben eines Resultsettyps  
 Der Typ des SQL-Befehls bestimmt, ob für den Task SQL ausführen ein Resultset zurückgegeben wird. Beispielsweise gibt eine SELECT-Anweisung in der Regel ein Resultset zurück, eine INSERT-Anweisung jedoch nicht. Das Resultset einer SELECT-Anweisung kann keine Zeilen, eine Zeile oder viele Zeilen enthalten. Gespeicherte Prozeduren können außerdem einen ganzzahligen Wert, der als Rückgabecode bezeichnet wird, zurückgeben, um den Ausführungsstatus der Prozedur anzuzeigen. In diesem Fall besteht das Resultset aus einer einzelnen Zeile.  
  
## <a name="configure-the-execute-sql-task"></a>Konfigurieren des Tasks „SQL ausführen“  
 Es gibt folgende Möglichkeiten, um den Task SQL ausführen zu konfigurieren:  
  
-   Geben Sie den Verbindungs-Manager an, der zum Verbinden mit einer Datenbank verwendet werden soll.  
  
-   Geben Sie den Resultsettyp an, der von der SQL-Anweisung zurückgegeben wird.  
  
-   Geben Sie ein Timeout für die SQL-Anweisungen an.  
  
-   Geben Sie die Quelle der SQL-Anweisung an.  
  
-   Geben Sie an, ob der Task die Vorbereitungsphase für die SQL-Anweisung auslässt.  
  
-   Wenn Sie den ADO-Verbindungstyp verwenden, müssen Sie angeben, ob es sich bei der SQL-Anweisung um eine gespeicherte Prozedur handelt. Für andere Verbindungstypen ist diese Eigenschaft schreibgeschützt und weist immer den Wert **false**auf.  
  
 Eigenschaften können Sie programmgesteuert oder mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen.  

## <a name="general-page---execute-sql-task-editor"></a>Seite „Allgemein“ – Editor für den Task „SQL ausführen“
 Mithilfe der Seite **Allgemein** im Dialogfeld **Editor für den Task „SQL ausführen“** können Sie den Task „SQL ausführen“ konfigurieren und die SQL-Anweisung bereitstellen, die vom Task ausgeführt wird.  

Weitere Informationen zur Transact-SQL-Abfragesprache finden Sie unter [Transact-SQL-Referenz &#40;Datenbankmodul&#41;](../../t-sql/transact-sql-reference-database-engine.md).  
  
### <a name="static-options"></a>Statische Optionen  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Task 'SQL ausführen' im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie den Task 'SQL ausführen'. Es wird hierbei empfohlen, das Paket zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und einfacher zu verwalten sind.  
  
 **TimeOut**  
 Gibt die maximale Ausführungsdauer in Sekunden an, bevor ein Timeout für den Task eintritt. Der Wert 0 steht für eine unbegrenzte Dauer. Die Standardeinstellung ist 0.  
  
> [!NOTE]  
>  Bei gespeicherten Prozeduren tritt kein Timeout ein, wenn sie diese die Funktionalität des Ruhezustands dadurch emulieren, dass sie mehr Zeit für das Herstellen von Verbindungen und das Abschließen von Transaktionen bereitstellen, als durch den Wert für **TimeOut**angegeben wird. Gespeicherte Prozeduren, die Abfragen ausführen, unterliegen jedoch immer den durch den Wert für **TimeOut**angegebenen Zeitbeschränkungen.  
  
 **CodePage**  
 Geben Sie die Codepage an, die beim Übersetzen von Unicode-Werten in Variablen verwendet werden soll. Der Standardwert ist die Codepage des lokalen Computers.  
  
> [!NOTE]  
>  Wenn der Task „SQL ausführen“ einen ADO- oder ODBC-Verbindungs-Manager verwendet, ist die **CodePage** -Eigenschaft nicht verfügbar. Wenn Ihre Projektmappe eine Codepage erfordert, verwenden Sie einen OLE DB- oder einen ADO.NET-Verbindungs-Manager mit dem Task "SQL ausführen".  
  
 **TypeConversionMode**  
 Wenn Sie diese Eigenschaft auf **Allowed**festlegen, versucht der Task „SQL ausführen“, Ausgabeparameter sowie Abfrageergebnisse in den Datentyp der Variablen zu konvertieren, der die Ergebnisse zugewiesen sind. Dies gilt für den Resultsettyp **Einzelne Zeile** .  
  
 **ResultSet**  
 Geben Sie den von der auszuführenden SQL-Anweisung erwarteten Ergebnistyp an. Wählen Sie zwischen **Einzelne Zeile**, **Vollständiges Resultset**, **XML**und **Keine**aus.  
  
 **ConnectionType**  
 Wählen Sie den Typ des Verbindungs-Managers aus, der zum Herstellen der Verbindung mit der Datenquelle verwendet werden soll. Zu den verfügbaren Verbindungstypen zählen: **OLE DB**, **ODBC**, **ADO**, **ADO.NET** und **SQLMOBILE**.  
  
 **Verwandte Themen:** [OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md), [ODBC-Verbindungs-Manager](../../integration-services/connection-manager/odbc-connection-manager.md), [ADO-Verbindungs-Manager-](../../integration-services/connection-manager/ado-connection-manager.md), [ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md), [SQL Server Compact Edition-Verbindungs-Manager](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **Verbindung**  
 Wählen Sie die Verbindung aus einer Liste definierter Verbindungs-Manager aus. Klicken Sie zum Erstellen einer neuen Verbindung auf \<**Neue Verbindung...**>.  
  
 **SQLSourceType**  
 Wählen Sie den Quelltyp der SQL-Anweisung aus, die von dem Task ausgeführt wird.  
  
 Je nachdem, welchen Verbindungs-Manager-Typ der Task SQL ausführen verwendet, müssen Sie bestimmte Parametermarkierungen in parametrisierten SQL-Anweisungen verwenden.    
  
 Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Direct input**|Legen Sie als Quelle eine Transact-SQL-Anweisung fest. Bei Auswahl dieses Wertes wird die dynamische Option **SQLStatement**angezeigt.|  
|**File connection**|Wählen Sie eine Datei aus, die eine Transact-SQL-Anweisung enthält. Durch Festlegen dieser Option wird die dynamische Option **FileConnection**angezeigt.|  
|**Variable**|Legen Sie als Quelle eine Variable fest, die die Transact-SQL-Anweisung definiert. Bei Auswahl dieses Wertes wird die dynamische Option **SourceVariable**angezeigt.|  
  
 **QueryIsStoredProcedure**  
 Zeigt an, ob die angegebene auszuführende SQL-Anweisung eine gespeicherte Prozedur ist. Diese Eigenschaft weist nur dann den Lese-/Schreibmodus auf, wenn der Task den ADO-Verbindungs-Manager verwendet. Andernfalls ist die Eigenschaft schreibgeschützt, und ihr Wert ist auf **FALSE**festgelegt.  
  
 **BypassPrepare**  
 Geben Sie an, ob die SQL-Anweisung vorbereitet ist.  **TRUE** überspringt die Vorbereitung. Mit **FALSE** wird die SQL-Anweisung vor dem Ausführen vorbereitet. Diese Option ist nur für OLE DB-Verbindungen verfügbar, die die Vorbereitung unterstützen.  
  
 **Verwandte Themen:**  [Vorbereitete Ausführung](../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **Durchsuchen**  
 Suchen Sie mithilfe des Dialogfelds **Öffnen** eine Datei, die eine SQL-Anweisung enthält. Wählen Sie eine Datei aus, um den Dateiinhalt als SQL-Anweisung in die **SQLStatement** -Eigenschaft zu kopieren.  
  
 **Abfrage erstellen**  
 Erstellen Sie mithilfe des Dialogfelds **Abfrage-Generator** , einem grafischen Tool zum Erstellen von Abfragen, eine SQL-Anweisung. Diese Option ist verfügbar, wenn die Option **SQLSourceType** auf **Direct input**festgelegt ist.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax der SQL-Anweisung.  
  
### <a name="sqlsourcetype-dynamic-options"></a>SQLSourceType (dynamische Optionen)  
  
#### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = Direct input  
 **SQLStatement**  
 Geben Sie die auszuführende SQL-Anweisung in das Optionsfeld ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen (…), um die SQL-Anweisung in das Dialogfeld **SQL-Abfrage eingeben** einzugeben. Sie können auch auf **Abfrage erstellen** klicken, um die Anweisung mithilfe des Dialogfelds **Abfrage-Generator** zusammenzustellen.  
  
 **Verwandte Themen:** [Abfrage-Generator](http://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5)  
  
#### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = File connection  
 **FileConnection**  
 Wählen Sie einen vorhandenen Dateiverbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="sqlsourcetype--variable"></a>SQLSourceType = Variable  
 **SourceVariable**  
 Wählen Sie eine vorhandene Variable aus, oder klicken Sie auf \<**Neue Variable...**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
 
## <a name="parameter-mapping-page---execute-sql-task-editor"></a>Seite „Parameterzuordnung“ – Editor für den Task „SQL ausführen“
Mithilfe der Seite **Parameterzuordnung** des Dialogfelds **Editor für den Task 'SQL ausführen'** können Sie Parametern in der SQL-Anweisung Variablen zuordnen.  
  
### <a name="options"></a>enthalten  
 **Variablenname**  
 Nachdem Sie auf **Hinzufügen** geklickt und damit eine neue Parameterzuordnung hinzugefügt haben, wählen Sie in der Liste eine Systemvariable oder eine benutzerdefinierte Variable aus, oder klicken Sie auf \<**Neue Variable...**>, um mithilfe des Dialogfelds **Variable hinzufügen** eine neue Variable hinzuzufügen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 **Richtung**  
 Wählen Sie die Richtung des Parameters aus. Ordnen Sie jede Variable einem Eingabeparameter, einem Ausgabeparameter oder einem Rückgabecode zu.  
  
 **Datentyp**  
 Wählen Sie den Datentyp des Parameters aus. Die Liste der verfügbaren Datentypen hängt von dem Anbieter ab, den Sie in dem vom Task verwendeten Verbindungs-Manager ausgewählt haben.  
  
 **Parametername**  
 Geben Sie einen Parameternamen an.  
  
 Je nachdem, welchen Verbindungs-Manager-Typ der Task verwendet, müssen Sie Zahlen oder Parameternamen verwenden. Bei einigen Verbindungs-Manager-Typen wird vorausgesetzt, dass Parameternamen mit dem @-Zeichen beginnen oder bestimmte Namen (z.B. @Param1) oder Spaltennamen als Parameternamen verwendet werden.  
  
 **Parametergröße**  
 Geben Sie die Größe von Parametern mit variabler Länge an, z. B. Zeichenfolgen und binäre Felder.  
  
 Durch diese Einstellung wird sichergestellt, dass der Anbieter genügend Speicherplatz für Parameterwerte variabler Länge zuordnet.  
  
 **Hinzufügen**  
 Klicken Sie auf diese Option, um eine Parameterzuordnung hinzuzufügen.  
  
 **Entfernen**  
 Wählen Sie in der Liste eine Parameterzuordnung aus, und klicken Sie anschließend auf **Entfernen**.  
 
## <a name="result-set-page---execute-sql-task-editor"></a>Seite „Resultset“ – Editor für den Task „SQL ausführen“
Mithilfe der Seite **Resultset** des Dialogfelds **Editor für den Task 'SQL ausführen'** können Sie das Ergebnis der SQL-Anweisung neuen oder vorhandenen Variablen zuordnen. Die Optionen in diesem Dialogfeld sind deaktiviert, wenn auf der Seite Allgemein für **ResultSet** der Wert **Keine**festgelegt ist.  
  
### <a name="options"></a>enthalten  
 **Ergebnisname**  
 Nachdem Sie durch Klicken auf **Hinzufügen**eine Resultsetzuordnung hinzugefügt haben, geben Sie einen Namen für das Ergebnis an. Je nach Resultsettyp müssen Sie bestimmte Ergebnisnamen verwenden.  
  
 Für den Resultsettyp **Einzelne Zeile**können Sie entweder den Namen einer von der Abfrage zurückgegebenen Spalte verwenden oder die Zahl, die die Position einer Spalte in der von der Abfrage zurückgegebenen Spaltenliste angibt.  
  
 Für den Resultsettyp **Vollständiges Resultset** oder **XML**müssen Sie 0 als Resultsetnamen verwenden.  
 
  
 **Variablenname**  
 Ordnen Sie das Resultset einer Variablen zu, indem Sie eine Variable auswählen, oder klicken Sie auf \<**Neue Variable...**>, um mithilfe des Dialogfelds **Variable hinzufügen** eine neue Variable hinzuzufügen.  
  
 **Hinzufügen**  
 Klicken Sie auf diese Option, um eine Resultsetzuordnung hinzuzufügen.  
  
 **Entfernen**  
 Wählen Sie eine Resultsetzuordnung aus der Liste aus, und klicken Sie anschließend auf **Entfernen**.  
 
## <a name="parameters-in-the-execute-sql-task"></a>Parameter im Task „SQL ausführen“
SQL-Anweisungen und gespeicherte Prozeduren verwenden häufig **input** -Parameter, **output** -Parameter und Rückgabecodes. In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt der Task „SQL ausführen“ die **Input**-, **Output**- und **ReturnValue**-Parametertypen. Sie können den **Input** -Typ für Eingabeparameter, den **Output** -Typ für Ausgabeparameter und den **ReturnValue** -Typ für Rückgabecodes verwenden.  
  
> [!NOTE]  
>  Parameter können in einem Task SQL ausführen nur verwendet werden, wenn dies vom Datenanbieter unterstützt wird.  
  
 Parameter in SQL-Befehlen, einschließlich Abfragen und gespeicherte Prozeduren, werden benutzerdefinierten Variablen zugeordnet, die im Bereich des Tasks "SQL ausführen", eines übergeordneten Containers oder im Bereich des Pakets erstellt werden. Die Werte für Variablen können zur Entwurfszeit festgelegt oder zur Laufzeit dynamisch aufgefüllt werden. Sie können Parameter auch Systemvariablen zuordnen. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Systemvariablen](../../integration-services/system-variables.md).  
  
 Das Arbeiten mit Parametern und Rückgabecodes in einem Task „SQL ausführen“ bedeutet jedoch mehr, als nur zu wissen, welche Parametertypen der Task unterstützt und wie diese Parameter zugeordnet werden. Es müssen weitere Benutzungsanforderungen und Richtlinien beachtet werden, um Parameter und Rückgabecodes erfolgreich in einem Task „SQL ausführen“ zu verwenden. Diese Benutzungsanforderungen und Richtlinien werden am Ende dieses Themas behandelt:  
  
-   [Verwenden von Parametern, Namen und Markern](#Parameter_names_and_markers)  
  
-   [Verwenden von Parametern mit Datums- und Zeitdatentypen](#Date_and_time_data_types)  
  
-   [Verwenden von Parametern in WHERE-Klauseln](#WHERE_clauses)  
  
-   [Verwenden von Parametern mit gespeicherten Prozeduren](#Stored_procedures)  
  
-   [Abrufen von Rückgabecodewerten](#Return_codes)    
  
###  <a name="Parameter_names_and_markers"></a> Parameternamen und Marker  
 Die Syntax des SQL-Befehls verwendet verschiedene Parametermarkierungen, je nach verwendetem Verbindungstyp im Task SQL ausführen. Beispielsweise erfordert der [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager-Typ, dass der SQL-Befehl eine Parametermarkierung im Format **@varParameter** verwendet, während für den OLEDB-Verbindungstyp das Fragezeichen („?“) als Parametermarkierung erforderlich ist.  
  
 Die Namen, die in den Zuordnungen zwischen Variablen und Parametern als Parameternamen verwendet werden können, variieren ebenfalls je nach Managertyp. Beispielsweise verwendet der [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Managertyp einen benutzerdefinierten Namen mit einem @-Präfix, während der OLE DB-Verbindungs-Managertyp die Verwendung des numerischen Wertes einer 0-basierten Ordnungszahl als Parameternamen erfordert.  
  
 In der folgenden Tabelle finden Sie eine Auflistung der Anforderungen für SQL-Befehle für Verbindungs-Managertypen, die der Task SQL ausführen verwenden kann.  
  
|Verbindungstyp|Parametermarkierung|Parametername|Beispiel SQL-Befehl|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|@\<Parametername>|@\<Parametername>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = @parmContactID|  
|ODBC|?|1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL und OLE DB|?|0, 1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
#### <a name="use-parameters-with-adonet-and-ado-connection-managers"></a>Verwenden von Parametern mit ADO.NET- und ADO-Verbindungs-Managern  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)]- und ADO-Verbindungs-Manager besitzen besondere Anforderungen für SQL-Befehle, die Parameter verwenden:  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager erfordern die Verwendung von Parameternamen als Parametermarker in SQL-Befehlen. Das bedeutet, dass Variablen Parametern direkt zugeordnet werden können. Beispielsweise wird die `@varName` -Variable dem Parameter mit der Bezeichnung `@parName` zugeordnet. Auf diese Weise wird dem `@parName`-Parameter ein Wert bereitgestellt.  
  
-   ADO-Verbindungs-Manager erfordern die Verwendung von Fragezeichen ("?") als Parametermarker in SQL-Befehlen. Sie können jedoch einen beliebigen benutzerdefinierten Namen, mit Ausnahme von ganzzahligen Werten, als Parameternamen verwenden.  
  
 Variablen werden Parameternamen zugeordnet, um Parametern Werte bereitzustellen. Anschließend verwendet der Task „SQL ausführen“ den Ordinalwert des Parameternamens in der Parameterliste, um die Variablenwerte in Parametern zu laden.  
  
#### <a name="use-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>Verwenden von Parametern mit EXCEL-, ODBC- und OLEDB-Verbindungs-Managern  
 EXCEL-, ODBC- und OLE DB-Verbindungs-Manager erfordern die Verwendung von Fragezeichen ("?") als Parametermarkierungen in SQL-Befehlen sowie die Verwendung 0-basierter bzw. 1-basierter numerischer Werte als Parameternamen. Wenn der Task „SQL ausführen“ den ODBC-Verbindungs-Manager verwendet, wird der Parametername, der dem ersten Parameter in der Abfrage zugeordnet wird, mit 1 bezeichnet, andernfalls wird er mit 0 bezeichnet. Für nachfolgende Parameter gibt der numerische Wert des Parameternamens den Parameter in dem SQL-Befehl an, dem der Parametername zugeordnet wird. Beispielsweise wird der Parametername mit der Bezeichnung "3" dem dritten Parameter zugeordnet, der im SQL-Befehl durch das dritte Fragezeichen ("?") dargestellt wird.  
  
 Um Werte für Parameter bereitzustellen, werden den Parameternamen Variablen zugeordnet. Der Task SQL ausführen verwendet dann den Ordinalwert des Parameternamens, um die Variablenwerte in Parametern zu laden.  
  
 Einige OLE DB-Datentypen werden, abhängig vom Anbieter, den der Verbindungs-Manager verwendet, nicht unterstützt. Beispielsweise erkennt der Excel-Treiber nur einen begrenzten Satz von Datentypen. Weitere Informationen zum Verhalten des Jet-Anbieters mit dem Excel-Treiber finden Sie unter [Excel Source](../../integration-services/data-flow/excel-source.md).  
  
#### <a name="use-parameters-with-ole-db-connection-managers"></a>Verwenden von Parametern mit OLEDB-Verbindungs-Managern  
 Wenn der Task „SQL ausführen“ den OLE DB-Verbindungs-Manager verwendet, ist die BypassPrepare-Eigenschaft des Tasks verfügbar. Sie sollten für diese Eigenschaft **true** festlegen, wenn der Task „SQL ausführen“ SQL-Anweisungen mit Parametern verwendet.  
  
 Bei Verwendung eines OLE DB-Verbindungs-Managers können Sie keine parametrisierten Unterabfragen verwenden, da der Task „SQL ausführen“ keine Parameterinformationen über den OLE DB-Anbieter ableiten kann. Sie können jedoch einen Ausdruck verwenden, um die Parameterwerte in der Abfragezeichenfolge zu verketten und die SqlStatementSource-Eigenschaft des Tasks festzulegen.  
  
###  <a name="Date_and_time_data_types"></a> Verwenden von Parametern mit Datums- und Zeitdatentypen  
  
#### <a name="use-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>Verwenden von Datums- und Zeitparametern mit ADO.NET- und ADO-Verbindungs-Managern  
 Beim Lesen von Daten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Typen **time** und **datetimeoffset** gelten für einen Task „SQL ausführen“, der einen [!INCLUDE[vstecado](../../includes/vstecado-md.md)]- oder ADO-Verbindungs-Manager verwendet, folgende zusätzliche Anforderungen:  
  
-   Bei **time**-Daten wird vom [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager gefordert, dass diese Daten in einem Parameter gespeichert werden, dessen Parametertyp **Input** oder **Output** und dessen Datentyp **string** lautet.  
  
-   Für **datetimeoffset**-Daten verlangt ein [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager, dass diese Daten in einem der folgenden Parameter gespeichert werden:  
  
    -   Ein Parameter mit dem Parametertyp **Input** und dem Datentyp **string**.  
  
    -   Ein Parameter mit dem Parametertyp **Output** oder **ReturnValue**und dem Datentyp **datetimeoffset**, **string**oder **datetime2**. Wenn Sie einen Parameter auswählen, dessen Datentyp **string** oder **datetime2** ist, werden die Daten von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in den Datentyp „string“ bzw. „datetime2“ konvertiert.  
  
-   Für einen ADO-Verbindungs-Manager ist es erforderlich, dass **time** -Daten oder **datetimeoffset** -Daten in einem Parameter mit dem Parametertyp **Input** oder **Output**und dem Datentyp **adVarWchar**gespeichert werden.  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen sowie deren Zuordnung zu [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Datentypen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) und [SQL Server Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
#### <a name="use-date-and-time-parameters-with-ole-db-connection-managers"></a>Verwenden von Datums- und Zeitparametern mit OLEDB-Verbindungs-Managern  
 Bei der Verwendung eines OLE DB-Verbindungs-Managers besitzt ein Task „SQL ausführen“ bestimmte Speicheranforderungen für Daten mit den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen **date**, **time**, **datetime**, **datetime2** und **datetimeoffset**. Sie müssen diese Daten in einem der folgenden Parametertypen speichern:  
  
-   In einem Eingabeparameter mit dem Datentyp NVARCHAR  
  
-   In einem Ausgabeparameter mit dem entsprechenden Datentyp, wie in der folgenden Tabelle aufgeführt  
  
    |Parametertyp**Output** |Date-Datumstyp|  
    |-------------------------------|--------------------|  
    |DBDATE|**Datum**|  
    |DBTIME2|**Uhrzeit**|  
    |DBTIMESTAMP|**datetime**, **datetime2**|  
    |DBTIMESTAMPOFFSET|**datetimeoffset**|  
  
 Wenn die Daten nicht im entsprechenden Eingabe- oder Ausgabeparameter gespeichert werden, erzeugt das Paket einen Fehler.  
  
#### <a name="use-date-and-time-parameters-with-odbc-connection-managers"></a>Verwenden von Datums- und Zeitparametern mit ODBC-Verbindungs-Managern  
 Bei der Verwendung eines ODBC-Verbindungs-Managers besitzt ein Task „SQL ausführen“ bestimmte Speicheranforderungen für Daten mit einem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen **date**, **time**, **datetime**, **datetime2** oder **datetimeoffset**. Sie müssen diese Daten in einem der folgenden Parametertypen speichern:  
  
-   In einem **Eingabeparameter** mit dem Datentyp SQL_WVARCHAR  
  
-   Ein **output** -Parameter mit dem entsprechenden Datentyp, wie in der folgenden Tabelle aufgeführt  
  
    |Parametertyp**Output** |Date-Datumstyp|  
    |-------------------------------|--------------------|  
    |SQL_DATE|**Datum**|  
    |SQL_SS_TIME2|**Uhrzeit**|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -oder-<br /><br /> SQL_TIMESTAMP|**datetime**, **datetime2**|  
    |SQL_SS_TIMESTAMPOFFSET|**datetimeoffset**|  
  
 Wenn die Daten nicht im entsprechenden Eingabe- oder Ausgabeparameter gespeichert werden, erzeugt das Paket einen Fehler.  
  
###  <a name="WHERE_clauses"></a> Verwenden von Parametern in WHERE-Klauseln  
 In SELECT-, INSERT-, UPDATE- und DELETE-Befehlen sind häufig WHERE-Klauseln enthalten, um Filter anzugeben, die die Bedingungen definieren, die die Zeilen in den Quelltabellen für einen SQL-Befehl erfüllen müssen. Parameter stellen die Filterwerte in den WHERE-Klauseln bereit.  
  
 Sie können Parametermarkierungen verwenden, um Parameterwerte dynamisch bereitzustellen. Die Regeln für die in der SQL-Anweisung zu verwendenden Parametermarkierungen und Parameternamen hängen vom Typ des Verbindungs-Managers ab, den der Task SQL ausführen verwendet.  
  
 In der folgenden Tabelle finden Sie eine Auflistung von Beispielen des SELECT-Befehls nach verschiedenen Verbindungs-Managertypen. Die INSERT-, UPDATE- und DELETE-Anweisungen ähneln sich. In den Beispielen wird die SELECT-Anweisung verwendet, um Produkte aus der **Product** -Tabelle in [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] zurückzugeben, die eine **ProductID** aufweisen, die größer oder kleiner als die angegebenen Werte von zwei Parametern ist.  
  
|Verbindungstyp|SELECT-Syntax|  
|---------------------|-------------------|  
|EXCEL, ODBC und OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 In den Beispielen werden Parameter mit den folgenden Namen benötigt:  
  
-   Die EXCEL- und OLED DB-Verbindungs-Manager verwenden die Parameternamen 0 und 1. Der ODBC-Verbindungstyp verwendet die Namen 1 und 2.  
  
-   Der ADO-Verbindungstyp kann zwei beliebige Parameternamen verwenden, wie z. B. Param1 und Param2, deren Zuordnung muss aber nach ihrer Ordnungsposition in der Parameterliste erfolgen.  
  
-   Der [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungstyp verwendet die Parameternamen @parmMinProductID und @parmMaxProductID.  
  
###  <a name="Stored_procedures"></a> Verwenden von Parametern mit gespeicherten Prozeduren  
 Für SQL-Befehle, die gespeicherte Prozeduren ausführen, kann die Parameterzuordnung ebenfalls verwendet werden. Die Regeln für die zu verwendenden Parametermarkierungen und Parameternamen hängen, wie die Regeln für parametrisierte Abfragen, vom Typ des Verbindungs-Managers ab, den der Task SQL ausführen verwendet.  
  
 In der folgenden Tabelle finden Sie eine Auflistung von Beispielen des EXEC-Befehls nach verschiedenen Verbindungs-Managertypen. Die Beispiele führen die gespeicherte Prozedur **uspGetBillOfMaterials** in [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]aus. Die gespeicherte Prozedur verwendet die `@StartProductID` - und `@CheckDate` **input** .  
  
|Verbindungstyp|EXEC-Syntax|  
|---------------------|-----------------|  
|EXCEL und OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> Weitere Informationen über die ODBC-Aufrufsyntax finden Sie im Thema [Prozedurparameter](http://go.microsoft.com/fwlink/?LinkId=89462)in der ODBC Programmer's Reference in der MSDN Library.|  
|ADO|Wenn IsQueryStoredProcedure auf **FALSE** festgelegt ist, `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> Wenn IsQueryStoredProcedure auf **TRUE** festgelegt ist, `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Wenn IsQueryStoredProcedure auf **FALSE** festgelegt ist, `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> Wenn IsQueryStoredProcedure auf **TRUE** festgelegt ist, `uspGetBillOfMaterials`|  
  
 Um Ausgabeparameter verwenden zu können, erfordert die Syntax die Verwendung des OUTPUT-Schlüsselworts am Ende jeder Parametermarkierung. Zum Beispiel ist die folgende Ausgabeparametersyntax richtig: `EXEC myStoredProcedure ? OUTPUT`.  
  
 Weitere Informationen zum Verwenden von Eingabe- und Ausgabeparametern mit gespeicherten Prozeduren von Transact-SQL finden Sie unter [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
 
### <a name="map-query-parameters-to-variables"></a>Zuordnen von Abfrageparametern zu Variablen
In diesem Abschnitt wird beschrieben, wie Sie eine parametrisierte SQL-Anweisung im Task „SQL ausführen“ verwenden und Zuordnungen zwischen Variablen und den Parametern der SQL-Anweisung erstellen.  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das gewünschte [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Wenn das Paket noch keinen Task SQL ausführen enthält, fügen Sie der Ablaufsteuerung des Pakets einen solchen Task hinzu. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen eines Tasks oder Containers in einer Ablaufsteuerung](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
5.  Doppelklicken Sie auf den Task SQL ausführen.  
  
6.  Stellen Sie auf eine der folgenden Arten einen parametrisierten SQL-Befehl bereit:  
  
    -   Verwenden Sie die direkte Eingabe, und geben Sie den SQL-Befehl für die SQLStatement-Eigenschaft ein.  
  
    -   Verwenden Sie die direkte Eingabe, klicken Sie auf **Abfrage erstellen**, und erstellen Sie einen SQL-Befehl mithilfe der grafischen Tools des Abfrage-Generators.  
  
    -   Verwenden Sie eine Dateiverbindung, und verweisen Sie auf die Datei, die den SQL-Befehl enthält.  
  
    -   Verwenden Sie eine Variable, und verweisen Sie auf die Variable, die den SQL-Befehl enthält.  
  
     Die in parametrisierten SQL-Anweisungen verwendeten Parametermarkierungen hängen vom Verbindungstyp ab, den der Task SQL ausführen verwendet.  
  
    |Verbindungstyp|Parametermarkierung|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET und SQLMOBILE|@\<Parametername>|  
    |ODBC|?|  
    |EXCEL und OLE DB|?|  
  
     In der folgenden Tabelle finden Sie eine Auflistung von Beispielen des SELECT-Befehls nach verschiedenen Verbindungs-Managertypen. Parameter stellen die Filterwerte in den WHERE-Klauseln bereit. In den Beispielen wird die SELECT-Anweisung verwendet, um Produkte aus der **Product** -Tabelle in [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] zurückzugeben, die eine **ProductID** aufweisen, die größer oder kleiner als die angegebenen Werte von zwei Parametern ist.  
  
    |Verbindungstyp|SELECT-Syntax|  
    |---------------------|-------------------|  
    |EXCEL, ODBC und OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
   
7.  Klicken Sie auf **Parameterzuordnung**.  
  
8.  Klicken Sie auf **Hinzufügen**, um eine Parameterzuordnung hinzuzufügen.  
  
9. Stellen Sie im Feld **Parametername** einen Namen bereit.  
  
     Die verwendeten Parameternamen hängen vom Verbindungstyp ab, den der Task 'SQL ausführen' verwendet.  
  
    |Verbindungstyp|Parametername|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, …|  
    |ADO.NET und SQLMOBILE|@\<Parametername>|  
    |ODBC|1, 2, 3, …|  
    |EXCEL und OLE DB|0, 1, 2, 3, …|  
  
10. Wählen Sie in der Liste **Variablenname** eine Variable aus. Weitere Informationen finden Sie unter [Hinzufügen, Löschen, Ändern des Bereichs von benutzerdefinierten Variablen in einem Paket](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e).  
  
11. Geben Sie in der Liste **Richtung** an, ob der Parameter eine Eingabe, eine Ausgabe oder ein Rückgabewert ist.  
  
12. Legen Sie in der Liste **Datentyp** den Datentyp des Parameters fest.  
  
    > [!IMPORTANT]  
    >  Der Datentyp des Parameters muss mit dem Datentyp der Variablen kompatibel sein.  
  
13. Wiederholen Sie die Schritte 8 bis 11 für jeden Parameter in der SQL-Anweisung.  
  
    > [!IMPORTANT]  
    >  Die Reihenfolge von Parameterzuordnungen muss mit der Reihenfolge identisch sein, in der Parameter in der SQL-Anweisung aufgeführt sind.  
  
14. Klicken Sie auf **OK**.  

##  <a name="Return_codes"></a> Abrufen von Rückgabecodewerten  
 Eine gespeicherte Prozedur kann einen ganzzahligen Wert zurückgeben, der als Rückgabecode bezeichnet wird, um den Ausführungsstatus einer Prozedur anzuzeigen. Verwenden Sie Parameter des **ReturnValue** -Typs, um Rückgabecodes im Task SQL ausführen zu implementieren.  
  
 In der folgenden Tabelle finden Sie eine Auflistung einiger Beispiele des EXEC-Befehls nach verschiedenen Verbindungstypen, die Rückgabecodes implementieren. In alle Beispiele wird ein **input** -Parameter verwendet. Die Regeln für die Verwendung von Parametermarkierungen und Parameternamen sind für alle Parametertypen,**Input**, **Output**und **ReturnValue**, gleich.  
  
 Ein Teil der Syntax unterstützt keine Parameterliterale. In diesem Fall müssen Sie die Parameterwerte mithilfe einer Variablen bereitstellen.  
  
|Verbindungstyp|EXEC-Syntax|  
|---------------------|-----------------|  
|EXCEL und OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> Weitere Informationen über die ODBC-Aufrufsyntax finden Sie im Thema [Prozedurparameter](http://go.microsoft.com/fwlink/?LinkId=89462)in der ODBC Programmer's Reference in der MSDN Library.|  
|ADO|Wenn IsQueryStoreProcedure auf **FALSE** festgelegt ist, `EXEC ? = myStoredProcedure 1`<br /><br /> Wenn IsQueryStoreProcedure auf **TRUE** festgelegt ist, `myStoredProcedure`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Legen Sie IsQueryStoreProcedure auf **TRUE**fest.<br /><br /> `myStoredProcedure`|  
  
 In der in der obigen Tabelle gezeigten Syntax verwendet der Task "SQL ausführen" zum Ausführen der gespeicherten Prozedur den Quelltyp **Direkteingabe** . Der Task "SQL ausführen" kann auch den Quelltyp **Dateiverbindung** verwenden, um eine gespeicherte Prozedur auszuführen. Unabhängig davon, ob der Task "SQL ausführen" den Quelltyp **Direkteingabe** oder **Dateiverbindung** verwendet, implementieren Sie den Rückgabecode mit einem Parameter des Typs **ReturnValue** .
  
 Weitere Informationen zum Verwenden von Rückgabecodes mit gespeicherten Prozeduren von Transact-SQL finden Sie unter [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md).  
  
## <a name="result-sets-in-the-execute-sql-task"></a>Resultsets im Task „SQL ausführen“
 In einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket ist es vom Typ des von dem Task verwendeten SQL-Befehls abhängig, ob an den Task „SQL ausführen“ ein Resultset zurückgegeben wird. Beispielsweise gibt eine SELECT-Anweisung in der Regel ein Resultset zurück, eine INSERT-Anweisung jedoch nicht.  
  
 Auch der Inhalt des Resultsets ist von dem SQL-Befehl abhängig. Das Resultset einer SELECT-Anweisung kann beispielsweise keine Zeilen, eine Zeile oder viele Zeilen enthalten. Das Resultset einer SELECT-Anweisung, die eine Anzahl oder eine Summe zurückgibt, enthält jedoch nur eine einzige Zeile.  
  
 Das Arbeiten mit Resultsets in einem Task „SQL ausführen“ bedeutet mehr, als nur zu wissen, ob ein SQL-Befehl ein Resultset zurückgibt und was dieses Resultset enthält. Es müssen weitere Benutzungsanforderungen und Richtlinien beachtet werden, um Resultsets erfolgreich in einem Task „SQL ausführen“ zu verwenden. Diese Benutzungsanforderungen und Richtlinien werden am Ende dieses Themas behandelt:  
  
-   [Angeben eines Resultsettyps](#Result_set_type)  
  
-   [Auffüllen einer Variablen mit einem Resultset](#Populate_variable_with_result_set)  
  
###  <a name="Result_set_type"></a> Angeben eines Resultsettyps  
 Der Task SQL ausführen unterstützt die folgenden Resultsettypen:  
  
-   Das Resultset **Keine** wird verwendet, wenn die Abfrage keine Ergebnisse zurückgibt. Beispielsweise wird dieses Resultset für Abfragen verwendet, die Datensätze in einer Tabelle hinzufügen, ändern und löschen.  
  
-   Das Resultset **Einzelne Zeile** wird verwendet, wenn die Abfrage nur eine Zeile zurückgibt. Beispielsweise wird dieses Resultset für eine SELECT-Anweisung verwendet, die eine Anzahl oder eine Summe zurückgibt.  
  
-   Das Resultset **Vollständiges Resultset** wird verwendet, wenn die Abfrage mehrere Zeilen zurückgibt. Beispielsweise wird dieses Resultset für eine SELECT-Anweisung verwendet, die alle Zeilen in einer Tabelle abruft.  
  
-   Das Resultset **XML** wird verwendet, wenn die Abfrage ein Resultset in einem XML-Format zurückgibt. Beispielsweise wird dieses Resultset für eine SELECT-Anweisung verwendet, die eine FOR XML-Klausel einschließt.  
  
 Wenn der Task SQL ausführen das Resultset **Vollständiges Resultset** verwendet und die Abfrage mehrere Rowsets zurückgibt, gibt der Task nur das erste Rowset zurück. Generiert dieses Rowset einen Fehler, wird der Fehler vom Task gemeldet. Von anderen Rowsets generierte Fehler werden vom Task nicht gemeldet.  
  
###  <a name="Populate_variable_with_result_set"></a> Auffüllen einer Variablen mit einem Resultset  
 Sie können das von einer Abfrage zurückgegebene Resultset an eine benutzerdefinierte Variable binden, falls der Resultsettyp eine einzelne Zeile, ein Rowset oder XML ist.  
  
 Ist der Resultsettyp **Einzelne Zeile**, können Sie eine Spalte im Rückgabeergebnis an eine Variable binden, indem Sie den Spaltennamen als Resultsetnamen verwenden. Sie können auch die Ordnungsposition der Spalte in der Spaltenliste als Resultsetnamen verwenden. Der Resultsetnamen für die Abfrage `SELECT Color FROM Production.Product WHERE ProductID = ?` könnte beispielsweise **Color** oder **0**sein. Gibt die Abfrage mehrere Spalten zurück, und Sie möchten auf die Werte in allen Spalten zugreifen, müssen Sie jede Spalte an eine andere Variable binden. Wenn Sie Spalten mithilfe von Zahlen als Resultsetnamen zu Variablen zuordnen, geben die Zahlen die Reihenfolge wieder, in der die Spalten in der Spaltenliste der Abfrage erscheinen. In der Abfrage `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`verwenden Sie beispielsweise 0 für die Spalte **Color** und 1 für die Spalte **ListPrice** . Ob ein Spaltenname als Namen eines Resultsets verwendet werden kann, hängt davon ab, für welchen Anbieter der Task konfiguriert ist. Nicht alle Anbieter machen Spaltennamen verfügbar.  
  
 Bei einigen Abfragen, die einen einzelnen Wert zurückgeben, kann es sein, dass keine Spaltennamen enthalten sind. Beispielsweise gibt die `SELECT COUNT (*) FROM Production.Product` -Anweisung keinen Spaltennamen zurück. Sie können auf das Rückgabeergebnis zugreifen, indem Sie die Ordnungsposition 0 als Ergebnisnamen verwenden. Für den Zugriff auf das Rückgabeergebnis über den Spaltennamen muss in der Abfrage eine AS <Aliasname\<-Klausel enthalten sein, damit ein Spaltenname bereitgestellt werden kann. Die `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`-Anweisung stellt die **CountOfProduct** -Spalte bereit. Sie können dann auf die Rückgabeergebnisspalte zugreifen, indem Sie den **CountOfProduct** -Spaltennamen bzw. die Ordnungsposition 0 verwenden.  
  
 Für den Resultsettyp **Vollständiges Resultset** oder **XML**müssen Sie 0 als Resultsetnamen verwenden.  
  
 Wenn Sie eine Variable einem Resultset mit dem Resultsettyp **Einzelne Zeile** zuordnen, muss die Variable einen Datentyp haben, der mit dem Datentyp der Spalte im Resultset kompatibel ist. So kann beispielsweise ein Resultset, das eine Spalte mit einem **String** -Datentyp enthält, keiner Variable mit einem numerischen Datentyp zugeordnet werden. Wenn Sie die Eigenschaft **TypeConversionMode** auf **Allowed**festlegen, wird anhand des Tasks "SQL ausführen" versucht, Ausgabeparameter sowie Abfrageergebnisse in den Datentyp der Variablen zu konvertieren, der die Ergebnisse zugewiesen sind.  
  
 Ein XML-Resultset kann nur einer Variable mit dem Datentyp **String** oder **Object** zugeordnet werden. Hat die Variable den **String** -Datentyp, gibt der Task SQL ausführen eine Zeichenfolge zurück, und die XML-Quelle kann die XML-Daten verwenden. Hat die Variable den **Object** -Datentyp, gibt der Task „SQL ausführen“ ein DOM-Objekt (Document Object Model) zurück.  
  
 Ein Resultset vom Typ **Vollständiges Resultset** muss einer Variablen vom Datentyp **Object** zugeordnet werden. Als Ergebnis wird ein Rowsetobjekt zurückgegeben. Sie können einen Foreach-Schleifen-Container verwenden, um die Tabellenzeilenwerte, die in der Objektvariable gespeichert sind, in Paketvariablen zu extrahieren. Verwenden Sie dann ein Skripttask, um die Daten, die in Paketvariablen gespeichert sind, in eine Datei zu schreiben. Eine Demonstration zur Durchführung dieses Vorgangs unter Verwendung eines Foreach-Schleifen-Containers und eines Skripttasks finden Sie im CodePlex-Beispiel [Execute SQL Parameters and Result Sets](http://go.microsoft.com/fwlink/?LinkId=157863)(Ausführen von SQL-Parametern und Resultsets, in englischer Sprache), auf msftisprodsamples.codeplex.com.  
  
 In der folgenden Tabelle werden die Datentypen von Variablen zusammengefasst, die Resultsets zugeordnet werden können.  
  
|Typ des Resultsets|Datentyp der Variablen|Typ des Objekts|  
|---------------------|---------------------------|--------------------|  
|Einzelne Zeile|Jeder mit der Typspalte im Resultset kompatible Typ|Nicht verfügbar|  
|Vollständiges Resultset|**Objekt**|Wenn der Task einen systemeigenen Verbindungs-Manager, wie z. B. einen ADO-, OLE DB-, Excel- oder ODBC-Verbindungs-Manager, verwendet, wird als Objekt ein ADO- **Recordset**zurückgegeben.<br /><br /> Wenn der Task einen verwalteten Verbindungs-Manager, wie z.B. den [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager, verwendet, wird als Objekt ein **System.Data.DataSet** zurückgegeben.<br /><br /> Sie können mithilfe eines Skripttasks auf das **System.Data.DataSet** -Objekt zugreifen, wie im folgenden Beispiel veranschaulicht.<br /><br /> `Dim dt As Data.DataTable`<br /><br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet) dt = ds.Tables(0)`|  
|XML|**String**|**String**|  
|XML|**Objekt**|Wenn der Task einen systemeigenen Verbindungs-Manager, wie z. B. einen ADO-, OLE DB-, Excel- oder ODBC-Verbindungs-Manager, verwendet, wird als Objekt ein **MSXML6.IXMLDOMDocument**zurückgegeben.<br /><br /> Wenn der Task einen verwalteten Verbindungs-Manager, wie z.B. den [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager, verwendet, wird als Objekt ein **System.Xml.XmlDocument** zurückgegeben.|  
  
 Die Variable kann im Bereich des Tasks SQL ausführen oder des Pakets definiert werden. Falls die Variable einen Paketbereich aufweist, ist das Resultset für andere Tasks und Container innerhalb des Pakets verfügbar sowie für alle Pakete, die von den Tasks "Paket ausführen" oder "DTS 2000-Paket ausführen" ausgeführt werden.  
  
 Wenn Sie einem **Single row** -Resultset eine Variable zuordnen, könnten von der SQL-Anweisung zurückgegebene Werte, die noch keine Zeichenfolgen sind, in Zeichenfolgen konvertiert werden. Dazu müssen die folgenden Bedingungen erfüllt sein:  
  
-   Die Eigenschaft **TypeConversionMode** ist auf "True" festgelegt. Sie haben den Eigenschaftswert im Eigenschaftenfenster oder mit dem **Editor für den Task "SQL ausführen"**festgelegt.  
  
-   Die Konvertierung führt nicht zu einem Abschneiden von Daten.  
  
## <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>Zuordnen von Resultsets zu Variablen in einem Task 'SQL ausführen'
In diesem Abschnitt wird das Erstellen einer Zuordnung zwischen einem Resultset und einer Variablen in einem Task „SQL ausführen“ beschrieben. Indem Sie ein Resultset zu einer Variablen zuordnen, wird das Resultset für andere Elemente des Pakets zur Verfügung gestellt. Beispielsweise kann ein Skript eines Skripttasks die Variable lesen und dann die Werte des Resultsets verwenden, oder eine XML-Quelle kann das in einer Variable gespeicherte Resultset verwenden. Wenn das Resultset durch ein übergeordnetes Paket generiert wird, kann das Resultset für ein untergeordnetes Paket, das von einem Task Paket ausführen aufgerufen wird, zur Verfügung gestellt werden. Hierzu wird das Resultset im übergeordneten Paket einer Variablen zugeordnet. Anschließend wird im untergeordneten Paket eine übergeordnete Variablenkonfiguration erstellt, um den übergeordneten Variablenwert zu speichern.  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im **Projektmappen-Explorer**auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Wenn das Paket noch keinen Task SQL ausführen enthält, fügen Sie der Ablaufsteuerung des Pakets einen solchen Task hinzu. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen eines Tasks oder Containers in einer Ablaufsteuerung](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
5.  Doppelklicken Sie auf den Task SQL ausführen.  
  
6.  Wählen Sie im Dialogfeld **Editor für den Task 'SQL ausführen'** auf der Seite **Allgemein** den Resultsettyp **Einzelne Zeile**, **Vollständiges Resultset**oder **XML** aus.  

7.  Klicken Sie auf **Resultset**.  
  
8.  Klicken Sie auf **Hinzufügen**, um eine Resultsetzuordnung hinzuzufügen.  
  
9. Wählen Sie in der Liste **Variablenname** eine Variable aus, oder erstellen Sie eine neue Variable. Weitere Informationen finden Sie unter [Hinzufügen, Löschen, Ändern des Bereichs von benutzerdefinierten Variablen in einem Paket](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e).  
  
10. Ändern Sie in der Liste **Ergebnisname** optional den Namen des Resultsets.  
  
     Im Allgemeinen können Sie den Spaltennamen als Resultsetnamen verwenden, oder Sie können die Ordnungsposition der Spalte in der Spaltenliste als Resultset verwenden. Ob ein Spaltenname als Resultsetname verwendet werden kann, hängt davon ab, für welchen Anbieter der Task konfiguriert ist. Nicht alle Anbieter machen Spaltennamen verfügbar.  
  
11. Klicken Sie auf **OK**.  

## <a name="troubleshoot-the-execute-sql-task"></a>Problembehandlung des Tasks „SQL ausführen“  
 Sie können die vom Task SQL ausführen an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktionen können Sie Probleme bei SQL-Befehlen behandeln, die vom Task SQL ausführen ausgeführt werden. Aktivieren Sie zum Protokollieren der vom Task SQL ausführen an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandlung von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Gelegentlich gibt ein SQL-Befehl oder eine gespeicherte Prozedur mehrere Resultsets zurück. Zu diesen Resultsets gehören nicht nur Rowsets, die das Ergebnis von **SELECT** -Abfragen sind, sondern auch einzelne Werte als Ergebnis von Fehlern in der **RAISERROR** -Anweisung oder **PRINT** -Anweisung. Ob der Task Fehler in Resultsets nach dem ersten Resultset ignoriert, hängt vom verwendeten Typ des Verbindungs-Managers ab:  
  
-   Wenn Sie OLE DB- und ADO-Verbindungs-Manager verwenden, ignoriert der Task die Resultsets, die nach dem ersten Resultset auftreten. Das bedeutet, dass der Task bei diesen Verbindungs-Managern einen von einem SQL-Befehl oder einer gespeicherten Prozedur zurückgegebenen Fehler ignoriert, wenn der Fehler nicht Teil des ersten Resultsets ist.  
  
-   Wenn Sie ODBC- und ADO.NET-Verbindungs-Manager verwenden, werden die Resultsets, die nach dem ersten Resultset auftreten, vom Task nicht ignoriert. Bei diesen Verbindungs-Managern erzeugt der Task einen Fehler, wenn ein anderes Resultset als das erste Resultset einen Fehler aufweist.  
  
### <a name="custom-log-entries"></a>Benutzerdefinierte Protokolleinträge  
 In der folgenden Tabelle wird der benutzerdefinierte Protokolleintrag für den Task <legacyBold>SQL ausführen</legacyBold> beschrieben. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|Enthält Informationen zu den Ausführungsphasen der SQL-Anweisung. Protokolleinträge werden geschrieben, wenn der Task eine Verbindung mit der Datenbank erhält, wenn der Task beginnt, die SQL-Anweisung vorzubereiten, und nachdem die Ausführung der SQL-Anweisung abgeschlossen wurde. Der Protokolleintrag für die Vorbereitungsphase schließt die vom Task verwendete SQL-Anweisung ein.|  

