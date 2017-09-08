---
title: OLE DB-Quelle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbsource.f1
- sql13.dts.designer.oledbsourceadapter.connection.f1
- sql13.dts.designer.oledbsourceadapter.columns.f1
- sql13.dts.designer.oledbsourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 995d2688f0e4f8ab9af751c3521e45cb0626451f
ms.contentlocale: de-de
ms.lasthandoff: 08/17/2017

---
# <a name="ole-db-source"></a>OLE DB-Quelle
  Die OLE DB-Quelle extrahiert Daten mithilfe einer Datenbanktabelle, einer Sicht oder eines SQL-Befehls aus einer Reihe von OLE DB-kompatiblen relationalen Datenbanken. Beispielsweise kann die OLE DB-Quelle Daten aus Tabellen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access- oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken extrahieren.  
  
> [!NOTE]  
>  Wenn es sich bei der Datenquelle um [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 handelt, erfordert die Datenquelle einen anderen Verbindungs-Manager als frühere Versionen von Excel. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 Die OLE DB-Quelle stellt vier verschiedene Datenzugriffsmodi zum Extrahieren von Daten bereit:  
  
-   Eine Tabelle oder Sicht.  
  
-   Eine in einer Variablen angegebene Tabelle oder Sicht.  
  
-   Die Ergebnisse einer SQL-Anweisung. Bei der Abfrage kann es sich um eine parametrisierte Abfrage handeln.  
  
-   Die Ergebnisse einer SQL-Anweisung, die in einer Variablen gespeichert werden.  
  
> [!NOTE]  
>  Wenn Sie mithilfe einer SQL-Anweisung eine gespeicherte Prozedur aufrufen, die Ergebnisse von einer temporären Tabelle zurückgibt, verwenden Sie die WITH RESULT SETS-Option, um Metadaten für das Resultset zu definieren.  
  
 Wenn Sie eine parametrisierte Abfrage verwenden, können Sie Parametern Variablen zuordnen, um die Werte einzelner Parameter in SQL-Anweisungen anzugeben.  
  
 Diese Quelle verwendet einen OLE DB-Verbindungs-Manager zum Herstellen einer Verbindung zu einer Datenquelle, und der Verbindungs-Manager gibt den zu verwendenden OLE DB-Anbieter an. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt stellt außerdem das Datenquellenobjekt bereit, von dem Sie einen OLE DB-Verbindungs-Manager erstellen können, um Datenquellen und Datenquellensichten für die OLE DB-Quelle zur Verfügung zu stellen.  
  
 Je nach OLE DB-Anbieter gelten für die OLE DB-Quelle bestimmte Einschränkungen:  
  
-   Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieter für Oracle unterstützt die Oracle-Datentypen BLOB, CLOB, NCLOB, BFILE oder UROWID nicht, und die OLE DB-Quelle kann keine Daten aus Tabellen extrahieren, die Spalten mit diesen Datentypen enthalten.  
  
-   Der IBM OLE DB DB2-Anbieter und der [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2-Anbieter unterstützen keine SQL-Befehle, die eine gespeicherte Prozedur aufrufen. Wenn diese Art von Befehl verwendet wird, kann die OLE DB-Quelle die Spaltenmetadaten nicht erstellen. Für die Datenflusskomponenten, die im Datenfluss auf die OLE DB-Quelle folgen, sind deshalb keine Spaltendaten verfügbar, und beim Ausführen des Datenflusses wird ein Fehler gemeldet.  
  
 Die OLE DB-Quelle weist eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
## <a name="using-parameterized-sql-statements"></a>Verwenden parametrisierter SQL-Anweisungen  
 Die OLE DB-Quelle kann eine SQL-Anweisung zum Extrahieren von Daten verwenden. Die Anweisung kann eine SELECT- oder EXEC-Anweisung sein.  
  
 Die OLE DB-Quelle verwendet einen OLE DB-Verbindungs-Manager zum Herstellen einer Verbindung zur Datenquelle, aus der Daten extrahiert werden. Für die Benennung und Auflistung von Parametern gelten verschiedene Regeln, abhängig vom Anbieter, den der OLE DB-Verbindungs-Manager verwendet, und abhängig vom Managementsystem für relationale Datenbanken (RDBMS), zu dem der Verbindungs-Manager eine Verbindung herstellt. Wenn die Parameternamen vom RDBMS zurückgegeben werden, können Sie Parameternamen verwenden, um die in einer Parameterliste enthaltenen Parameterwerte den Parametern einer SQL-Anweisung zuzuordnen. Andernfalls erfolgt die Zuordnung nach der Ordnungsposition, in der die Parameter in der Parameterliste aufgeführt werden. Die jeweils unterstützten Typen von Parameternamen variieren je nach Anbieter. Beispielsweise erfordern einige Anbieter Variablen- oder Spaltennamen, andere Anbieter erfordern hingegen symbolische Namen, wie z. B. 0 oder Param0. Informationen zu den in SQL-Anweisungen zu verwendenden Parameternamen entnehmen Sie bitte der anbieterspezifischen Dokumentation.  
  
 Bei Verwendung eines OLE DB-Verbindungs-Managers können Sie keine parametrisierten Unterabfragen verwenden, das die OLE DB-Quelle keine Parameterinformationen über den OLE DB-Anbieter ableiten kann. Sie können jedoch einen Ausdruck verwenden, um die Parameterwerte in der Abfrage zu verketten und die SqlCommand-Eigenschaft der Quelle festzulegen. Im Designer von [!INCLUDE[ssIS](../../includes/ssis-md.md)] können Sie eine OLE DB-Quelle im Dialogfeld **Quellen-Editor für OLE DB** konfigurieren und die Parameter Variablen im Dialogfeld **Abfrageparameter festlegen** zuordnen.  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>Angeben von Parametern mithilfe der Ordnungsposition  
 Werden keine Parameternamen zurückgegeben, steuert die Reihenfolge, in der die Parameter in der Liste **Parameter** im Dialogfeld **Abfrageparameter festlegen** aufgelistet werden, welche Parametermarkierungen zur Laufzeit zugeordnet werden. Der erste in der Liste aufgeführte Parameter wird dem ersten ? in der SQL-Anweisung zugeordnet, der zweite Parameter dem zweiten ? usw.  
  
 Die folgende SQL-Anweisung wählt die Zeilen aus der **Product** -Tabelle der [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] -Datenbank aus. Der erste Parameter der **Mappings** -Liste wird dem ersten Parameter der **Color** -Spalte und der zweite Parameter der **Size** -Spalte zugeordnet.  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 Die Parameternamen haben keine Auswirkungen. Wurde z. B. ein Parameter genauso benannt wie die Spalte, für die er gilt, jedoch nicht in der richtigen Ordnungsposition in der **Parameters** -Liste eingereiht, wird in der zur Laufzeit stattfindenden Parameterzuordnung die Ordnungsposition des Parameters verwendet, nicht der Parametername.  
  
 Der EXEC-Befehl erfordert in der Regel die Verwendung der Variablennamen, die in der Prozedur Parameterwerte als Parameternamen bereitstellen.  
  
### <a name="specifying-parameters-by-using-names"></a>Angeben von Parametern mithilfe von Namen  
 Wenn die tatsächlichen Parameternamen vom RDBMS zurückgegeben werden, werden die von einer SELECT- und EXEC-Anweisung verwendeten Parameter den Namen zugeordnet. Die Parameternamen müssen den Namen entsprechen, die die gespeicherte Prozedur, die von der SELECT- oder EXEC-Anweisung ausgeführt wird, erwartet.  
  
 Die folgende SQL-Anweisung führt die in der **-Datenbank verfügbare gespeicherte Prozedur** uspGetWhereUsedProductID [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] aus.  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 Die gespeicherte Prozedur erwartet, dass die `@StartProductID` - und `@CheckDate`-Variablen Parameterwerte bereitstellen. Dabei ist die Reihenfolge, in der die Parameter in der **Mappings** -Liste angezeigt werden, irrelevant. Die einzige Voraussetzung ist, dass die Parameternamen den Variablennamen der gespeicherten Prozedur entsprechen müssen. Hierzu zählt auch das @-Zeichen.  
  
### <a name="mapping-parameters-to-variables"></a>Zuordnen von Parametern zu Variablen  
 Die Parameter werden Variablen zugeordnet, die die Parameterwerte zur Laufzeit bereitstellen. Bei den Variablen handelt es sich in der Regel um benutzerdefinierte Variablen, obwohl Sie auch die in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bereitgestellten Systemvariablen verwenden können. Stellen Sie beim Verwenden von benutzerdefinierten Variablen sicher, dass Sie den Datentyp auf einen Typ festlegen, der mit dem Datentyp der Spalte, auf die der zugeordnete Parameter verweist, kompatibel ist. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="troubleshooting-the-ole-db-source"></a>Problembehandlung der OLE DB-Quelle  
 Sie können die von der OLE DB-Quelle an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Laden von Daten aus externen Datenquellen durch die OLE DB-Quelle behandeln. Aktivieren Sie zum Protokollieren der von der OLE DB-Quelle an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-source"></a>Konfigurieren der OLE DB-Quelle  
 Eigenschaften können Sie programmgesteuert oder mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften für OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Extrahieren von Daten mithilfe der OLE DB-Quelle](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [Zuordnen von Abfrageparametern zu Variablen in einer Datenflusskomponente](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Wiki-Artikel, [SSIS with Oracle Connectors](http://go.microsoft.com/fwlink/?LinkId=220670), auf social.technet.microsoft.com.  
  
## <a name="ole-db-source-editor-connection-manager-page"></a>Quellen-Editor für OLE DB (Seite Verbindungs-Manager)
  Auf der Seite **Verbindungs-Manager** des Dialogfelds **Quellen-Editor für OLE DB** wählen Sie den OLE DB-Verbindungs-Manager für die Quelle aus. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
> [!NOTE]  
>  Verwenden Sie zum Laden von Daten aus einer Datenquelle, für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 verwendet wird, eine OLE DB-Quelle. Sie können eine Excel-Quelle nicht zum Laden von Daten aus einer Excel 2007-Datenquelle verwenden. Weitere Informationen finden Sie unter [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md).  
>   
>  Verwenden Sie zum Laden von Daten aus einer Datenquelle, für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 oder eine frühere Version verwendet wird, eine Excel-Quelle. Weitere Informationen finden Sie unter [Quellen-Editor für Excel &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  Die **CommandTimeout** -Eigenschaft der OLE DB-Quelle ist nicht im **Quellen-Editor für OLE DB**verfügbar, sie kann jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt Excel-Quelle von [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
### <a name="open-the-ole-db-source-editor-connection-manager-page"></a>Öffnen Sie den Editor für OLE DB Source (Seite Verbindungs-Manager)  
  
1.  Fügen Sie die OLE DB-Quelle dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]hinzu.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Quellkomponente, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Klicken Sie auf **Verbindungs-Manager**.  
  
### <a name="static-options"></a>Statische Optionen  
 **OLE DB-Verbindungs-Manager**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** einen neuen Verbindungs-Manager.  
  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Option|Beschreibung|  
|------------|-----------------|  
|Tabelle oder Sicht|Rufen Sie Daten aus einer Tabelle oder Sicht in der OLE DB-Datenquelle ab.|  
|Variable für Tabellenname oder Sichtname|Gibt den Namen der Tabelle oder Sicht in einer Variablen an.<br /><br /> **Verwandte Informationen:** [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL-Befehl|Rufen Sie mit SQL-Abfrage Daten aus der OLE DB-Datenquelle ab.|  
|SQL-Befehl aus Variable|Gibt den SQL-Abfragetext in einer Variablen an.|  
  
 **Vorschau**  
 Zeigt mithilfe des Dialogfelds **Datenansicht** eine Vorschau der Ergebnisse an. In der**Vorschau** können bis zu 200 Zeilen angezeigt werden.  
  
> [!NOTE]  
>  In der Datenvorschau enthalten Spalten mit einem CLR-benutzerdefinierten Typ keine Daten. Stattdessen die Werte \<Wert zu groß zum Anzeigen > oder System.Byte [] angezeigt. Der erste Wert wird angezeigt, wenn mithilfe des SQL-OLE DB-Anbieters auf die Datenquelle zugegriffen wird. Der zweite Wert wird bei Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Anbieters angezeigt.  
  
### <a name="data-access-mode-dynamic-options"></a>Dynamische Optionen (Datenzugriffsmodus)  
  
#### <a name="data-access-mode--table-or-view"></a>Datenzugriffsmodus = Tabelle oder Sicht  
 **Name der Tabelle oder Sicht**  
 Wählen Sie den Namen der Tabelle oder Sicht aus einer Liste der verfügbaren Namen in der Datenquelle aus.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Datenzugriffsmodus = Variable für Tabellenname oder Sichtname  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Namen der Tabelle oder Sicht enthält.  
  
#### <a name="data-access-mode--sql-command"></a>Datenzugriffsmodus = SQL-Befehl  
 **SQL-Befehlstext**  
 Geben Sie den Text einer SQL-Abfrage ein, und erstellen Sie die Abfrage, indem Sie auf **Abfrage erstellen**klicken. Wahlweise können Sie auch nach der Datei suchen, die den Abfragetext enthält, indem Sie auf **Durchsuchen**klicken.  
  
 **Parameter**  
 Wenn Sie eine parametrisierte Abfrage eingeben und im Abfragetext ? als Parameterplatzhalter verwenden, können Sie den Paketvariablen mithilfe des Dialogfelds **Abfrageparameter festlegen** Abfrageeingabeparameter zuordnen.  
  
 **Build query**  
 Mithilfe des Dialogfelds **Abfrage-Generator** können Sie die SQL-Abfrage visuell erstellen.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie nach der Datei suchen, die den Text der SQL-Abfrage enthält.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax des Abfragetexts.  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>Datenzugriffsmodus = SQL-Befehl aus Variable  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Text für die SQL-Abfrage enthält.  
  
## <a name="ole-db-source-editor-columns-page"></a>Quellen-Editor für OLE DB (Seite Spalten)
  Auf der Seite **Spalten** des Dialogfelds **Quellen-Editor für OLE DB** können Sie jeder externen (Quell-)Spalte eine Ausgabespalte zuordnen.  
  
### <a name="options"></a>enthalten  
 **Verfügbare externe Spalten**  
 Zeigt die Liste der in der Datenquelle verfügbaren externen Spalten an. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden.  
  
 **Externe Spalte**  
 Zeigt die externen (Quell-)Spalten in der gleichen Reihenfolge an wie beim Konfigurieren von Komponenten, die Daten aus dieser Quelle verwenden. Sie können die Reihenfolge ändern, indem Sie zunächst die ausgewählten Spalten in der Tabelle löschen. Wählen Sie anschließend die externen Spalten in einer anderen Reihenfolge aus der Liste aus.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen an. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der bereitgestellte Name wird im SSIS-Designer angezeigt.  
  
## <a name="ole-db-source-editor-error-output-page"></a>Quellen-Editor für OLE DB (Seite Fehlerausgabe)
  Mithilfe der Seite **Fehlerausgabe** des Dialogfelds **Quellen-Editor für OLE DB** können Sie Fehlerbehandlungsoptionen auswählen und Eigenschaften für Fehlerausgabespalten festlegen.  
  
### <a name="options"></a>enthalten  
 **Eingabe/Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen (Quell-)Spalten an, die im Dialogfeld **Quellen-Editor für OLE DB** auf der Seite **Verbindungs-Manager**ausgewählt wurden.  
  
 **Fehler**  
 Gibt an, was bei Auftreten eines Fehlers geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Gibt an, was im Falle einer Kürzung geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Description**  
 Zeigt die Beschreibung des Fehlers an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Gibt an, was im Falle eines Fehlers oder einer Kürzung mit den ausgewählten Zellen geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Ziel](../../integration-services/data-flow/ole-db-destination.md)   
 [Integrationsservices &#40; SSIS &#41; Variablen](../../integration-services/integration-services-ssis-variables.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  
