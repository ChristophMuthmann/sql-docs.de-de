---
title: "Zusammenhängende Projekte für Datamining-Lösungen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dc26489a-4c27-4b89-8215-6d245427c350
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 290142e362b4e41148ab2042c8c76738f3e7b54c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="related-projects-for-data-mining-solutions"></a>Verwandte Projekte für Data Mining-Lösungen
  Eine Data Mining-Projektmappe erfordert mindestens das Data Mining-Projekt, in dem Datenquellen, Datenquellenansichten, Miningstrukturen und Miningmodelle definiert werden. Wenn Data Mining-Modelle jedoch für die tägliche Entscheidungsfindung eingesetzt werden, ist es wichtig, Data Mining in andere Teile der vorhersagenden Analytiklösung zu integrieren, die die folgenden Prozesse und Komponenten enthalten kann:  
  
-   Vorbereitung und Auswahl der Daten und Variablen. Schließt Datenbereinigung, Metadatenverwaltung, Integration mehrerer Datenquellen, Konvertierung, Zusammenführung und das Hochladen von Daten in ein Data Warehouse ein.  
  
-   Das Berichten über die Analyse, Präsentation von Vorhersagen und die Überwachung/Nachverfolgung von Data Mining-Aktivitäten.  
  
-   Mehrdimensionale Modelle oder tabellarische Modelle, um den Treffer zu untersuchen.  
  
-   Eingrenzung der Data Mining-Projektmappe für die Unterstützung neuer Daten oder Änderungen in der Unterstützungsinfrastruktur, die von der aktuellen Analyse verwendet wird.  
  
 In diesem Thema werden die anderen Funktionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] beschrieben, die oftmals Teil einer vorhersagenden Analytiklösung sind, um entweder die Prozesse der Datenvorbereitung und Data Mining zu unterstützen oder um Benutzer beim Bereitstellen von Tools für Analysen und Aktionen zu unterstützen.  
  
 [Integration Services](#bkmk_SSIS)  
  
 [Reporting Services](#bkmk_SSRS)  
  
 [Data Quality Services](#bkmk_DQSetc)  
  
 [Volltextsuche](#bkmk_FTSetc)  
  
 [Semantische Indizierung](#bkmk_SemSearch)  
  
##  <a name="bkmk_SSIS"></a> SQL Server Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt Komponenten und Funktionen bereit, die für die Datenvorbereitung und die Trainingsphasen eines Data Mining-Projekts erforderlich sind. Obwohl Sie mit anderen Tools viele Datenbereinigungs- oder Vorbereitungsaufgaben ausführen können (beispielsweise Skripte), bietet [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zahlreiche Vorteile für Data Mining.  
  
-   Stellt Aufgaben als Teil eines Workflows dar, die wiederholt, automatisiert, verzweigt und erweitert werden können.  
  
-   Bietet eine ausführliche Unterstützung für die Überwachung und mehrere Wege, Fehler zu erfassen und Ereignisse zu protokollieren.  
  
     Zusätzlich zum Erfassen der Datenherkunft können Änderungen an den Daten mithilfe der Data Transformation Pipeline überwacht werden.  
  
     Sie können auch Ihre SSIS-Workflows in die Funktionen integrieren, die die Change Data Capture-Funktionalität in SQL Server unterstützen.  
  
-   Data Mining kann in den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Workflow integriert werden, um eingehende Daten in mehrere Tabellen intelligent zu trennen. Beispielsweise könnten Sie eine Vorhersageabfrage verwenden, um neue Kunden in unterschiedliche Gruppen für eine E-Mail-Kampagne aufzuteilen.  
  
 Die folgenden Listen stellen Links für die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten bereit, die am häufigsten in Bezug auf die Unterstützung von Data Mining verwendet werden.  
  
 **Ablaufsteuerungskomponenten**  
  
-   [DDL ausführen (Analysis Services-Task)](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services-Verarbeitungstask](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [CDC-Steuerungstask](../../integration-services/control-flow/cdc-control-task.md)  
  
-   [Datenbereinigung](../../data-quality-services/data-cleansing.md)  
  
-   [Data Mining-Abfragetask](../../integration-services/control-flow/data-mining-query-task.md)  
  
-   [Datenprofilerstellungs-Task](../../integration-services/control-flow/data-profiling-task.md)  
  
 **Datenflusskomponenten**  
  
-   [CDC-Flusskomponenten](../../integration-services/data-flow/cdc-flow-components.md)  
  
-   [Transformation für bedingtes Teilen](../../integration-services/data-flow/transformations/conditional-split-transformation.md)  
  
-   [Transformation für Datenkonvertierung](../../integration-services/data-flow/transformations/data-conversion-transformation.md)  
  
-   [Ziel des Data Mining-Modelltrainings](../../integration-services/data-flow/data-mining-model-training-destination.md)  
  
-   [Transformation für Data Mining-Abfragen](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)  
  
-   [Transformation für abgeleitete Spalten](../../integration-services/data-flow/transformations/derived-column-transformation.md)  
  
-   [Transformation für Prozentwert-Stichproben](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
-   [Transformation für Ausdrucksextrahierung](../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
-   [Transformation für Ausdruckssuche](../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
##  <a name="bkmk_SSRS"></a> SQL Server Reporting Services  
 Obwohl [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] normalerweise nicht als wichtige Komponente von Data Mining-Projektmappen gesehen wird, stellt es die folgenden Funktionen bereit, die für Präsentation von Data Mining-Projektmappen nützlich sind.  
  
-   Integration der Daten von mehreren Quellen in komplexen Berichten. Erstellen von Abfragen des Modellinhalts für Analytiker und von Berichten, die Endbenutzern Vorhersagen und Trends anzeigen.  
  
-   Fähigkeit, einen Bericht zu erstellen, mit dem Benutzer direkt Abfragen gegen ein vorhandenes Miningmodell ausführen können.  
  
-   Integration in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]für die Unterstützung von Drillthrough und das Durchsuchen der Data Mining-Dimensionen und Data Mining-Cubes, die aus OLAP-Modellen erstellt wurden.  
  
-   Parametrisierung und Formatierungsfunktionen die in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]verfügbar sind.  
  
 Weitere Informationen zum Verwenden von Reporting Services mit DMX-Abfragen als Datenquelle sind diesen Links zu entnehmen:  
  
 [Abrufen von Daten aus einem Data Mining-Modell &#40;DMX&#41; &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)  
  
 [Benutzeroberfläche des DMX-Abfrage-Designers für Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
 [Analysis Services-Verbindungstyp für DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
 Es ist jedoch nicht notwendig, DMX als Datenquelle zu verwenden. Die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten für Data Mining unterstützen auch das Speichern der Ergebnisse einer Vorhersageabfrage in einer relationalen Datenbank. Wenn Sie zum Aktualisieren von Modellen mithilfe von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]einen bewährten Workflow erstellt haben, können Sie mit beibehaltenen Vorhersagen und anderen Data Mining-Abfrageergebnissen für SQL Server [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] und andere Tools für die Berichterstellung verwenden, die nicht mit DMX verbunden sind.  
  
 Weitere Informationen über die Verwendung von Reporting Services als Darstellungsschicht für Datenquellen finden Sie unter [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md).  
  
##  <a name="bkmk_DQSetc"></a> Data Quality Services  
 Data Quality Services (DQS) ist ein neuer Dienst in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Da Datenprobleme Data Mining unmöglich machen können, erachten Data Mining-Benutzer, die wiederholte Analysen ausführen oder in großen Organisationen mit komplexen Datenquellen arbeiten, ein gut geplantes Datenprojekt unter Verwendung von DQS als verlässlichere Lösung für die Unterstützung von Data Mining als Ad-hoc-Bereinigungen von Daten unter Verwendung von [!INCLUDE[tsql](../../includes/tsql-md.md)] oder anderen Skripten.  
  
 Die folgenden Funktionen von DQS sollten für Datenvorbereitung und Datenintegrität in einer Data Mining-Projektmappe in Betracht gezogen werden.  
  
 **Ein computerunterstützter Datenbereinigungsprozess, der Quelldaten analysiert und Änderungen vorschlägt.**  
 DQS kann Quelldaten mit Cloud-basierten Verweisdaten vergleichen, die von Datenqualitätsanbietern gewartet und garantiert werden.  
  
 DQS kann auch unformatierte Quelldaten analysieren und eine Wissensdatenbank aus Benutzerdaten erstellen. Die verarbeiteten Daten werden kategorisiert und werden dem Benutzer dann zur weiteren Verarbeitung angezeigt. Der Bereinigungsprozess ist interaktiv. Der Data Steward kann demzufolge die vom computerunterstützten Datenbereinigungsprozess vorgeschlagenen Daten genehmigen, ablehnen oder ändern.  
  
 Das Ergebnis des Prozesses ist eine Wissensdatenbank, die Sie kontinuierlich verbessern können, oder in mehreren Datenerweiterungsphasen erneut verwenden können.  
  
 Weitere Informationen finden Sie unter [Data Cleansing](../../data-quality-services/data-cleansing.md).  
  
 **Ein computerunterstützter Abgleichungsprozess, der Quelldaten analysiert und Änderungen vorschlägt.**  
 Zum Verhindern von Datenverdoppelung können Sie eine zusätzliche Bereinigung der Datenquelle ausführen, um genaue und ungefähre Übereinstimmungen zu identifizieren. Mit diesen Komponenten können Sie die Abgleichsregeln bestimmen sowie die Schwellenwerte, ab wann sie angewendet werden sollen.  
  
 Indem Sie Datenübereinstimmungen suchen, können Sie Duplikate entfernen, die ein Problem für Data Mining sein können. Die Datendeduplizierung erfolgt nicht automatisch. Sowohl der Data Steward als auch der IT-Spezialist müssen die Informationen in der Wissensdatenbank und die vorzunehmenden Änderungen an den Daten überprüfen.  
  
 Nachdem Sie das ursprüngliche DQS-Projekt erstellt haben, können Sie viele der Aufgaben mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten automatisieren.  
  
 Weitere Informationen finden Sie unter [Data Matching](../../data-quality-services/data-matching.md).  
  
 Beim Ausführen der Bereinigungs- und Abgleichsaktivitäten in einem Data Quality-Projekt können Sie Statistiken und Informationen über die von DQS verarbeiteten Daten in Echtzeit abrufen. Mithilfe der Datenprofilerstellung können Sie das Ausmaß bewerten, inwiefern die Datenbereinigung oder der -abgleich dabei behilflich waren, die Datenqualität zu verbessern und um die vorgenommenen Änderungen zu verstehen. Weitere Informationen zur Datenprofilerstellung und zu Benachrichtigungen finden Sie unter [Data Profiling and Notifications in DQS](../../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
 **Eine Wissensdatenbank, die drei Typen an Informationen darstellt: Standardinformationen, vom DQS-Server generierte Informationen und vom Benutzer generierte Informationen.**  
 Wenn Sie eine Wissensdatenbank erstellt haben, können Sie sie iterativ für die Bereinigung und Überprüfung anderer Daten verwenden.  
  
 Sie können neue Daten in die Wissensdatenbankdaten von mehreren Quellen importieren, und zwar entweder in Form bekannter bereinigter Daten von Verweisanbietern oder in Form von Rohdaten, die in der Wissensdatenbank mit vorhandenen Daten abgeglichen werden.  
  
 Ausführliche Informationen zur Bereinigungsaktivität in einem Datenqualitätsprojekt finden Sie unter „Datenbereinigung (DQS)“.  
  
 Sie können die Informationen in der Wissensdatenbank auch auf andere Quellen anwenden, um eine Datenbereinigung innerhalb anderer Prozesse auszuführen. Solche Datenbereinigungen können dabei helfen, Eingabefehler, Übertragungsfehler bzw. Beschädigungen beim Speichern oder von nicht übereinstimmenden Definitionen in Datenwörterbüchern zu identifizieren.  
  
 Weitere Informationen finden Sie unter [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
##  <a name="bkmk_FTSetc"></a> Volltextsuche  
 Mit der Volltextsuche in SQL Server können von Anwendungen und Benutzern Volltextabfragen für zeichenbasierte Daten in SQL Server-Tabellen ausgeführt werden. Wenn die Volltextsuche aktiviert ist, können Sie Suchvorgänge für Textdaten ausführen, die durch sprachspezifische Regeln über mehrere Formen eines Worts oder Ausdrucks erweitert werden. Sie können auch Suchbedingungen konfigurieren, beispielsweise die Abweichung zwischen mehreren Begriffen, und Funktionen verwenden, um die Ergebnisse einzuschränken, die in Reihenfolge der Wahrscheinlichkeit zurückgegeben werden.  
  
 Da Volltextabfragen eine vom SQL Server-Modul bereitgestellte Funktion sind, können Sie parametrisierte Abfragen erstellen, benutzerdefinierte Datasets generieren oder Vektoren benennen, indem Sie Funktionen für die Volltextsuche für eine Textdatenquelle und diese Quellen in Data Mining verwenden.  
  
 Weitere Informationen über die Interaktion von Volltextabfragen mit dem Volltextindex finden Sie unter [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md).  
  
 Ein Vorteil, die Funktionen für die Volltextsuche von SQL Server zu verwenden, besteht darin, dass Sie von der linguistischen Intelligenz profitieren können, die in den Wörtertrennungen und Wortstammerkennungen für alle SQL Server-Sprachen enthalten sind. Mit den angegebenen Wörtertrennungen und den Wortstammerkennungen können Sie sicherstellen, dass Wörter mit den für jede Sprache angemessenen Zeichen getrennt werden und dass Synonyme, die auf diakritischen Zeichen oder orthografischen Variationen (wie die Vielzahl an Zahlenformaten auf Japanisch) basieren, nicht übersehen werden.  
  
 Zusätzlich zur linguistischen Intelligenz, die die Wortgrenzen regelt, können die Wortstammerkennungen für jede Sprache Varianten eines Worts auf einen einzelnen Begriff reduzieren, und zwar anhand der Regeln für Konjugation und orthografische Variation in dieser Sprache. Die Regeln für die linguistische Analyse unterscheiden sich für jede Sprache und werden auf Grundlage umfangreicher Forschung auf wirklichen Korpera entwickelt.  
  
 Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
 Die Version eines Worts, das nach der Volltextindizierung gespeichert wird, ist ein Token in komprimierter Form. Nachfolgende Abfragen für den Volltextindex generieren mehrere flektierte Formen eines bestimmten Worts, und zwar anhand der Regeln dieser Sprache, um sicherzustellen, dass alle wahrscheinlichen Abgleiche vorgenommen wurden. Obwohl das gespeicherte Token beispielsweise „lesen“ sein kann, sucht das Abfragemodul auch nach den Begriffen „gelesen“, „las“ und „Leser“, da es sich bei diesen um die regulär abgeleitete morphologische Abweichung des Wortstamms „run“ handelt.  
  
 Sie können auch einen Benutzerthesaurus erstellen, um Synonyme zu speichern und um bessere Suchergebnisse oder eine bessere Kategorisierung der Begriffe zu ermöglichen Indem Sie einen Thesaurus entwickeln, der genau auf Ihre Volltextdaten abgestimmt ist, können Sie den Bereich der Volltextabfragen für diese Daten effektiv erweitern. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
 Anforderungen zum Verwenden der Volltextsuche schließen Folgendes ein:  
  
-   Der Datenbankadministrator muss für die Tabelle einen Volltextindex erstellen.  
  
-   Nur ein Volltextindex pro Tabelle ist zulässig.  
  
-   Jede von Ihnen indizierte Spalte muss über einen eindeutigen Schlüssel verfügen.  
  
-   Die Volltextindizierung wird nur für Spalten mit den folgenden Datentypen unterstützt: „char“, „varchar“, „nchar“, „nvarchar“, „text“, „ntext“, „image“, „xml“, „varbinary“ und „varbinary(max)“. Wenn die Spalte „varbinary“, „varbinary(max)“, „image“ oder „xml“ ist, müssen Sie die Dateierweiterung des indizierbaren Dokuments (DOC-, PDF-, XLS-Datei usw.) in einer separaten Typspalte angeben.  
  
##  <a name="bkmk_SemSearch"></a> Semantische Indizierung  
 Die semantische Suche basiert auf der vorhandenen Volltextsuchfunktion in SQL Server, verwendet aber zusätzliche Funktionalitäten und Statistiken, um Szenarien wie die automatische Schlüsselwortextraktion und die Ermittlung verwandter Dokumente zu ermöglichen. Sie könnten beispielsweise mithilfe der semantischen Suche eine Basistaxonomie für eine Organisation erstellen oder einen Dokumentenkorpus klassifizieren. Sie könnten die Kombination von extrahierten Begriffen und Dokumentähnlichkeitsergebnissen alternativ in Cluster- oder Entscheidungsstrukturmodellen verwenden.  
  
 Nachdem Sie die semantische Suche erfolgreich aktiviert und Ihre Datenspalten indiziert haben, können Sie die nativ bereitgestellten Funktionen mit der semantischen Indizierung verwenden, um wie folgt vorzugehen:  
  
-   Rückgabe von aus einem Wort bestehenden Schlüsselausdrücken mit ihrem Ergebnis.  
  
-   Rückgabe von Dokumenten, die einen spezifischen Schlüsselausdruck enthalten.  
  
-   Rückgabe von Ähnlichkeitsergebnissen und den Begriffen, die zum Ergebnis beitragen.  
  
 Weitere Informationen finden Sie unter [Suchen von Schlüsselausdrücken in Dokumenten mit der semantischen Suche](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) und [Suchen von ähnlichen und verwandten Dokumenten mit semantischer Suche](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
 Weitere Informationen zu den Datenbankobjekten, die semantische Indizierung unterstützen, finden Sie unter [Aktivieren der semantischen Suche in Tabellen und Spalten](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md).  
  
 Für die Verwendung der semantischen Suche ist Folgendes zu beachten:  
  
-   Die Volltextsuche wird auch aktiviert.  
  
-   Bei der Installation der Komponenten der semantischen Suche wird zudem eine spezielle Systemdatenbank erstellt, die nicht umbenannt, geändert oder ersetzt werden kann.  
  
-   Mithilfe des Diensts indizierte Dokumente müssen in SQL Server gespeichert werden, und zwar in sämtlichen Datenbankobjekten, die für die Volltextindizierung unterstützt werden, einschließlich Tabellen und indizierte Ansichten.  
  
-   Nicht alle Volltextsprachen unterstützen die semantische Indizierung. Eine Liste mit unterstützten Sprachen finden Sie unter [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionale Modelllösungen &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [Tabellenmodelllösungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)  
  
  

