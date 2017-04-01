---
title: "OLE DB-Quelle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.oledbsource.f1"
helpviewer_keywords: 
  - "Quellen [Integration Services], OLE DB"
  - "OLE DB-Quelle [Integration Services]"
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 69
---
# OLE DB-Quelle
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
  
## Verwenden parametrisierter SQL-Anweisungen  
 Die OLE DB-Quelle kann eine SQL-Anweisung zum Extrahieren von Daten verwenden. Die Anweisung kann eine SELECT- oder EXEC-Anweisung sein.  
  
 Die OLE DB-Quelle verwendet einen OLE DB-Verbindungs-Manager zum Herstellen einer Verbindung zur Datenquelle, aus der Daten extrahiert werden. Für die Benennung und Auflistung von Parametern gelten verschiedene Regeln, abhängig vom Anbieter, den der OLE DB-Verbindungs-Manager verwendet, und abhängig vom Managementsystem für relationale Datenbanken (RDBMS), zu dem der Verbindungs-Manager eine Verbindung herstellt. Wenn die Parameternamen vom RDBMS zurückgegeben werden, können Sie Parameternamen verwenden, um die in einer Parameterliste enthaltenen Parameterwerte den Parametern einer SQL-Anweisung zuzuordnen. Andernfalls erfolgt die Zuordnung nach der Ordnungsposition, in der die Parameter in der Parameterliste aufgeführt werden. Die jeweils unterstützten Typen von Parameternamen variieren je nach Anbieter. Beispielsweise erfordern einige Anbieter Variablen- oder Spaltennamen, andere Anbieter erfordern hingegen symbolische Namen, wie z. B. 0 oder Param0. Informationen zu den in SQL-Anweisungen zu verwendenden Parameternamen entnehmen Sie bitte der anbieterspezifischen Dokumentation.  
  
 Bei Verwendung eines OLE DB-Verbindungs-Managers können Sie keine parametrisierten Unterabfragen verwenden, das die OLE DB-Quelle keine Parameterinformationen über den OLE DB-Anbieter ableiten kann. Sie können jedoch einen Ausdruck verwenden, um die Parameterwerte in der Abfrage zu verketten und die SqlCommand-Eigenschaft der Quelle festzulegen. Im Designer von [!INCLUDE[ssIS](../../includes/ssis-md.md)] können Sie eine OLE DB-Quelle im Dialogfeld **Quellen-Editor für OLE DB** konfigurieren und die Parameter Variablen im Dialogfeld **Abfrageparameter festlegen** zuordnen.  
  
### Angeben von Parametern mithilfe der Ordnungsposition  
 Werden keine Parameternamen zurückgegeben, steuert die Reihenfolge, in der die Parameter in der Liste **Parameter** im Dialogfeld **Abfrageparameter festlegen** aufgelistet werden, welche Parametermarkierungen zur Laufzeit zugeordnet werden. Der erste in der Liste aufgeführte Parameter wird dem ersten ? in der SQL-Anweisung zugeordnet, der zweite Parameter dem zweiten ? usw.  
  
 Die folgende SQL-Anweisung wählt die Zeilen aus der **Product** -Tabelle der [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] -Datenbank aus. Der erste Parameter der **Mappings** -Liste wird dem ersten Parameter der **Color** -Spalte und der zweite Parameter der **Size** -Spalte zugeordnet.  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 Die Parameternamen haben keine Auswirkungen. Wurde z. B. ein Parameter genauso benannt wie die Spalte, für die er gilt, jedoch nicht in der richtigen Ordnungsposition in der **Parameters** -Liste eingereiht, wird in der zur Laufzeit stattfindenden Parameterzuordnung die Ordnungsposition des Parameters verwendet, nicht der Parametername.  
  
 Der EXEC-Befehl erfordert in der Regel die Verwendung der Variablennamen, die in der Prozedur Parameterwerte als Parameternamen bereitstellen.  
  
### Angeben von Parametern mithilfe von Namen  
 Wenn die tatsächlichen Parameternamen vom RDBMS zurückgegeben werden, werden die von einer SELECT- und EXEC-Anweisung verwendeten Parameter den Namen zugeordnet. Die Parameternamen müssen den Namen entsprechen, die die gespeicherte Prozedur, die von der SELECT- oder EXEC-Anweisung ausgeführt wird, erwartet.  
  
 Die folgende SQL-Anweisung führt die in der **-Datenbank verfügbare gespeicherte Prozedur** uspGetWhereUsedProductID [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] aus.  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 Die gespeicherte Prozedur erwartet, dass die `@StartProductID` - und `@CheckDate`-Variablen Parameterwerte bereitstellen. Dabei ist die Reihenfolge, in der die Parameter in der **Mappings** -Liste angezeigt werden, irrelevant. Die einzige Voraussetzung ist, dass die Parameternamen den Variablennamen der gespeicherten Prozedur entsprechen müssen. Hierzu zählt auch das @-Zeichen.  
  
### Zuordnen von Parametern zu Variablen  
 Die Parameter werden Variablen zugeordnet, die die Parameterwerte zur Laufzeit bereitstellen. Bei den Variablen handelt es sich in der Regel um benutzerdefinierte Variablen, obwohl Sie auch die in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bereitgestellten Systemvariablen verwenden können. Stellen Sie beim Verwenden von benutzerdefinierten Variablen sicher, dass Sie den Datentyp auf einen Typ festlegen, der mit dem Datentyp der Spalte, auf die der zugeordnete Parameter verweist, kompatibel ist. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## Problembehandlung der OLE DB-Quelle  
 Sie können die von der OLE DB-Quelle an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Laden von Daten aus externen Datenquellen durch die OLE DB-Quelle behandeln. Aktivieren Sie zum Protokollieren der von der OLE DB-Quelle an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## Konfigurieren der OLE DB-Quelle  
 Eigenschaften können Sie programmgesteuert oder mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Quellen-Editor für OLE DB** festlegen können:  
  
-   [Quellen-Editor für OLE DB &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/ole-db-source-editor-connection-manager-page.md)  
  
-   [Quellen-Editor für OLE DB &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/ole-db-source-editor-columns-page.md)  
  
-   [Quellen-Editor für OLE DB &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/ole-db-source-editor-error-output-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften für OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## Verwandte Aufgaben  
  
-   [Extrahieren von Daten mithilfe der OLE DB-Quelle](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [Zuordnen von Abfrageparametern zu Variablen in einer Datenflusskomponente](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## Verwandte Inhalte  
 Wiki-Artikel, [SSIS with Oracle Connectors](http://go.microsoft.com/fwlink/?LinkId=220670), auf social.technet.microsoft.com.  
  
## Siehe auch  
 [OLE DB-Ziel](../../integration-services/data-flow/ole-db-destination.md)   
 [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  