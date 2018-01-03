---
title: Integration Services-Abfragen (SSIS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
caps.latest.revision: "58"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 86ca875378afdd32cf509767eb3c02dc3ff0154d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="integration-services-ssis-queries"></a>Integration Services-Abfragen (SSIS)
  Der Task SQL ausführen, die OLE DB-Quelle, das OLE DB-Ziel und die Transformation für die Suche können SQL-Abfragen verwenden. In dem Task SQL ausführen können von SQL-Anweisungen Datenbankobjekte und Daten erstellt, aktualisiert und gelöscht sowie gespeicherte Prozeduren und SELECT-Anweisungen ausgeführt werden. In der OLE DB-Quelle und der Nachschlagetransformation sind die SQL-Anweisungen normalerweise SELECT- oder ECEC-Anweisungen. Von den letzteren werden am häufigsten gespeicherte Prozeduren ausgeführt, die Resultsets zurückgeben.  
  
 Eine Abfrage kann analysiert werden, um festzustellen, ob sie gültig ist. Beim Analysieren einer Abfrage, die eine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]verwendet, wird die Abfrage analysiert, ausgeführt, und das Ausführungsergebnis (Erfolg oder Fehlgeschlagen) wird dem Analyseergebnis zugeordnet. Wenn die Abfrage eine Verbindung mit einer Datenquelle verwendet, die nicht zu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]gehört, wird nur die Anweisung analysiert.  
  
Sie können die SQL-Anweisung auf folgende Arten angeben:
1.   Geben Sie sie direkt im Designer ein.
2.   Geben Sie eine Verbindung mit einer Datei an, die die Anweisung enthält.
3.   Geben Sie eine Variable an, die die Anweisung enthält.  
  
## <a name="direct-input-sql"></a>Direkteingabe-SQL  
 Der Query-Generator steht für den Task SQL ausführen, die OLE DB-Quelle, das OLE DB-Ziel und die Transformation für die Suche zur Verfügung. Der Query-Generator bietet die folgenden Vorteile:  
  
-   Visuell oder mit SQL-Befehlen arbeiten.  
  
     Der Abfrage-Generator enthält grafische Bereiche, die eine Abfrage visuell darstellen, und einen Textbereich, der den SQL-Text der jeweiligen Abfrage anzeigt. Sie können entweder in grafischen oder in Textbereichen arbeiten. Der Abfrage-Generator synchronisiert die Sichten, sodass der Abfragetext und die grafische Darstellung immer übereinstimmen.  
  
-   Verknüpfen von verbundenen Tabellen.  
  
     Wenn Sie der Abfrage mehrere Tabellen hinzufügen, bestimmt der Abfrage-Generator automatisch, wie die Tabellen miteinander in Beziehung stehen, und erstellt den geeigneten Joinbefehl.  
  
-   Abfragen oder Aktualisieren von Datenbanken.  
  
     Sie können den Abfrage-Generator verwenden, um mithilfe von SELECT-Anweisungen von Transact-SQL Daten zurückzugeben und um Abfragen zu erstellen, die Datensätze einer Datenbank aktualisieren, einer Datenbank hinzufügen oder aus einer Datenbank löschen.  
  
-   Sofortiges Anzeigen und Bearbeiten der Ergebnisse.  
  
     Sie können die Abfrage ausführen und ein Recordset in einem Raster verwenden, das Ihnen das Durchführen eines Bildlaufs und Bearbeiten der Datensätze in der Datenbank ermöglicht.  
  
 Obwohl der Abfrage-Generator visuell auf das Erstellen von SELECT-Abfragen beschränkt ist, können Sie den SQL-Code für andere Typen von Anweisungen wie z. B. DELETE und UPDATE in den Textbereich eingeben. Der grafische Bereich wird automatisch entsprechend der eingegebenen SQL-Anweisung aktualisiert.  
  
 Die Direkteingabe kann auch durch Eingeben der Abfrage in das Dialogfeld des Tasks oder der Datenflusskomponente oder in das Eigenschaften-Fenster erfolgen.  
  
 Weitere Informationen finden Sie unter [Query Builder](http://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5).  
  
## <a name="sql-in-files"></a>SQL in Dateien  
 Die SQL-Anweisung für den Task "SQL ausführen" kann sich auch in einer getrennten Datei befinden. Sie können z. B. Abfragen mithilfe von Tools wie beispielsweise dem Abfrage-Editor in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]schreiben, die Abfrage in einer Datei speichern und dann die Abfrage aus dieser Datei auslesen, wenn ein Paket ausgeführt wird. Die Datei darf nur die auszuführenden SQL-Anweisungen sowie Kommentare enthalten. Zum Verwenden einer in einer Datei gespeicherten SQL-Anweisung müssen Sie eine Dateiverbindung bereitstellen, die den Dateinamen und den Speicherort der Datei angibt. Weitere Informationen finden Sie unter [File Connection Manager](../integration-services/connection-manager/file-connection-manager.md).  
  
## <a name="sql-in-variables"></a>SQL in Variablen  
 Wenn die Quelle der SQL-Anweisung im Task "SQL ausführen" eine Variable ist, geben Sie den Namen der Variablen an, die die Abfrage enthält. Die „Value“-Eigenschaft der Variablen enthält den Abfragetext. Sie legen die „ValueType“-Eigenschaft der Variablen auf einen Zeichenfolgendatentyp fest. Geben dann die SQL-Anweisung in die „Value“-Eigenschaft ein, oder kopieren Sie sie in die Eigenschaft. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  

## <a name="query-builder-dialog-box"></a>Abfrage-Generator (Dialogfeld)
Verwenden Sie das Dialogfeld **Abfrage-Generator** , um Abfragen zum Verwenden mit dem Task 'SQL ausführen', der OLE DB-Quelle, dem OLE DB-Ziel und der Transformation für die Suche zu erstellen.  
  
 Mit dem Abfrage-Generator können die folgenden Aufgaben ausgeführt werden:  
  
-   **Arbeiten mit einer grafischen Darstellung einer Abfrage oder mit SQL-Befehlen** Der Abfrage-Generator enthält einen Bereich, in dem eine Abfrage grafisch dargestellt wird, und einen Bereich, in dem der SQL-Text der Abfrage angezeigt wird. Sie können entweder im grafischen oder im Textfensterbereich arbeiten. Der Abfrage-Generator synchronisiert die Sichten, damit sie immer aktuell sind.  
  
-   **Verbinden verknüpfter Tabellen** Wenn Sie der Abfrage mehrere Tabellen hinzufügen, bestimmt der Abfrage-Generator automatisch, wie die Tabellen miteinander in Beziehung stehen, und erstellt den geeigneten Joinbefehl.  
  
-   **Abfragen oder Aktualisieren von Datenbanken** Sie können den Abfrage-Generator verwenden, um mithilfe von SELECT-Anweisungen von Transact-SQL Daten zurückzugeben und um Abfragen zu erstellen, die Datensätze einer Datenbank aktualisieren, einer Datenbank hinzufügen oder aus einer Datenbank löschen.  
  
-   **Sofortiges Anzeigen und Bearbeiten der Ergebnisse** Sie können die Abfrage ausführen und ein Recordset in einem Raster verwenden, das Ihnen das Durchführen eines Bildlaufs und Bearbeiten der Datensätze in der Datenbank ermöglicht.  
  
 Mit den grafischen Tools im Dialogfeld **Abfrage-Generator** können Sie Abfragen mithilfe von Drag &amp; Drop konstruieren. Standardmäßig erstellt der Abfrage-Generator SELECT-Abfragen. Sie können jedoch auch INSERT-, UPDATE- oder DELETE-Abfragen erstellen. Alle Typen von SQL-Anweisungen können im Dialogfeld **Abfrage-Generator** analysiert und ausgeführt werden. Weitere Informationen zu SQL-Anweisungen in Paketen finden Sie unter [Integration Services-Abfragen &#40;SSIS&#41;](../integration-services/integration-services-ssis-queries.md).  
  
 Weitere Informationen zur Transact-SQL-Sprache und -Syntax finden Sie unter [Transact-SQL-Referenz &#40;Datenbankmodul&#41;](../t-sql/transact-sql-reference-database-engine.md).  
  
 Sie können Variablen auch in einer Abfrage verwenden, um Werte für einen Eingabeparameter bereitzustellen, um Werte von Ausgabeparametern aufzuzeichnen und um Rückgabecodes zu speichern. Weitere Informationen zum Verwenden von Variablen in Abfragen, die in Paketen verwendet werden, finden Sie unter [SQL ausführen (Task)](../integration-services/control-flow/execute-sql-task.md), [OLE DB-Quelle](../integration-services/data-flow/ole-db-source.md)und [Integration Services &#40;SSIS&#41; Queries](../integration-services/integration-services-ssis-queries.md). Weitere Informationen zum Verwenden von Variablen im Task „SQL ausführen“ finden Sie unter [Parameter und Rückgabecodes im Task „SQL ausführen“](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663) und [Resultsets im Task „SQL ausführen“](http://msdn.microsoft.com/library/62605b63-d43b-49e8-a863-e154011e6109).  
  
 Die Transformationen für Suche und Fuzzysuche können ebenfalls Variablen mit Parametern und Rückgabecodes verwenden. Die Informationen zur OLE DB-Quelle gelten auch für diese beiden Transformationen.  
  
### <a name="options"></a>Tastatur  
 **Symbolleiste**  
 Mithilfe der Symbolleiste können Sie Datasets verwalten, Bereiche zur Anzeige auswählen und Abfragefunktionen steuern.  
  
|value|Description|  
|-----------|-----------------|  
|**Diagrammbereich ein-/ausblenden**|Blendet den Bereich **Diagramm** ein oder aus.|  
|**Rasterbereich ein-/ausblenden**|Blendet den Bereich **Raster** ein oder aus.|  
|**SQL-Bereich ein-/ausblenden**|Blendet den Bereich **SQL** ein oder aus.|  
|**Ergebnisbereich ein-/ausblenden**|Blendet den Bereich **Ergebnisse** ein oder aus.|  
|**Ausführen**|Führt die Abfrage aus. Ergebnisse werden im Ergebnisbereich angezeigt.|  
|**SQL überprüfen**|Überprüft, ob das SQL-Konto gültig ist.|  
|**Aufsteigend sortieren**|Sortiert die Ausgabezeilen der ausgewählten Spalte des Rasterbereichs in aufsteigender Reihenfolge.|  
|**Absteigend sortieren**|Sortiert die Ausgabezeilen der ausgewählten Spalte des Rasterbereichs in absteigender Reihenfolge.|  
|**Filter entfernen**|Wählen Sie einen Spaltennamen im Rasterbereich aus, und klicken Sie auf **Filter entfernen** , um die Sortierungskriterien aus der Spalte zu entfernen.|  
|**GROUP BY verwenden**|Fügt der Abfrage die GROUP BY-Funktionalität hinzu.|  
|**Tabelle hinzufügen**|Fügt der Abfrage eine neue Tabelle hinzu.|  
  
 **Abfragedefinition**  
 Die Abfragedefinition stellt eine Symbolleiste und Bereiche bereit, mit deren Hilfe die Abfrage definiert und getestet werden kann.  
  
|Bereich|Description|  
|----------|-----------------|  
|Bereich**Diagramm** |Zeigt die Abfrage in einem Diagramm an. Das Diagramm zeigt die in der Abfrage enthaltenen Tabellen sowie die Art, wie diese miteinander verknüpft sind. Aktivieren oder deaktivieren Sie das Kontrollkästchen neben einer Spalte in einer Tabelle, um die entsprechende Spalte der Abfrageausgabe hinzuzufügen bzw. sie daraus zu entfernen.<br /><br /> Wenn Sie der Abfrage Tabellen hinzufügen, erstellt der Abfrage-Generator auf der Grundlage der Tabellen Joins zwischen Tabellen, abhängig von den Schlüsseln in der Tabelle. Um einen Join hinzuzufügen, ziehen Sie ein Feld aus einer Tabelle auf ein Feld in einer anderen Tabelle. Sie können den Join verwalten, indem Sie mit der rechten Maustaste auf den Join klicken und Optionen aus einem Menü wählen.<br /><br /> Klicken Sie mit der rechten Maustaste auf den Bereich **Diagramm** , um Tabellen hinzuzufügen oder zu entfernen, alle Tabellen auszuwählen oder Bereiche ein- oder auszublenden.|  
|Bereich**Raster** |Zeigt die Abfrage in einem Raster an. Sie können diesen Bereich verwenden, um der Abfrage Spalten hinzuzufügen bzw. Spalten daraus zu entfernen, sowie um die Einstellungen der einzelnen Spalten zu ändern.|  
|Bereich**SQL** |Zeigt die Abfrage als SQL-Text an. Änderungen, die in den Bereichen **Diagramm** und **Raster** vorgenommen worden sind, werden hier angezeigt, genauso wie hier vorgenommene Änderungen in den Bereichen **Diagramm** und **Raster** angezeigt werden.|  
|Bereich**Ergebnisse** |Zeigt die Ergebnisse der Abfrage an, wenn Sie auf die Schaltfläche **Ausführen** auf der Symbolleiste klicken.| 

  
