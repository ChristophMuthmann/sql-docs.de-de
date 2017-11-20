---
title: Integration Services-Transformationen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transformations [Integration Services], listed
- transformations [Integration Services], types
- transformations [Integration Services]
- data flow [Integration Services], transformations
- business intelligence transformations [Integration Services]
- join transformations
- split transformations [Integration Services]
- custom transformations [Integration Services]
- row transformations [Integration Services]
- rowset transformations [Integration Services]
ms.assetid: c70c4f6e-82dd-4948-b923-fd5193f67f7e
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85673091c2531821e62bf7cbeab2bbda6139b384
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-transformations"></a>SQL Server Integration Services-Transformationen
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Transformationen handelt es sich um die Komponenten im Datenfluss eines Pakets, mit denen Daten aggregiert, zusammengeführt, verteilt und geändert werden. Mit Transformationen können auch Suchvorgänge ausgeführt und Stichprobendatasets generiert werden. In diesem Abschnitt werden die Transformationen von [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] beschrieben. Darüber hinaus wird deren Funktionsweise erklärt.  
  
## <a name="business-intelligence-transformations"></a>Business Intelligence-Transformationen  
 Die folgenden Transformationen führen Business Intelligence-Vorgänge aus, wie z. B. das Bereinigen von Daten, Text Mining und das Ausführen von Data Mining-Vorhersageabfragen.  
  
|Transformation|Description|  
|--------------------|-----------------|  
|[Transformation für langsam veränderliche Dimensionen](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)|Diese Transformation konfiguriert das Aktualisieren einer langsam veränderlichen Dimension.|  
|[Transformation für Fuzzygruppierung](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)|Diese Transformation standardisiert Werte in Spaltendaten.|  
|[Transformation für Fuzzysuche](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)|Diese Transformation sucht Werte in einer Verweistabelle mithilfe einer Fuzzyübereinstimmung.|  
|[Transformation für Ausdrucksextrahierung](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)|Diese Transformation extrahiert Ausdrücke aus dem Text.|  
|[Transformation für Ausdruckssuche](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)|Diese Transformation sucht Ausdrücke in einer Verweistabelle und zählt die aus dem Text extrahierten Ausdrücke.|  
|[Transformation für Data Mining-Abfragen](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|Diese Transformation führt Data Mining-Vorhersageabfragen aus.|  
|[DQS-Bereinigungstransformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)|Diese Transformation korrigiert die Daten einer verbundenen Datenquelle durch Anwenden von Regeln, die für die Datenquelle erstellt wurden.|  
  
## <a name="row-transformations"></a>Zeilentransformationen  
 Mit den folgenden Transformationen werden Spaltenwerte aktualisiert und neue Spalten erstellt. Die Transformation wird auf jede Zeile in der Transformationseingabe angewendet.  
  
|Transformation|Description|  
|--------------------|-----------------|  
|[Transformation zum Zuordnen der Zeichen](../../../integration-services/data-flow/transformations/character-map-transformation.md)|Diese Transformation wendet Zeichenfolgenfunktionen auf Zeichendaten an.|  
|[Transformation für das Kopieren von Spalten](../../../integration-services/data-flow/transformations/copy-column-transformation.md)|Diese Transformation fügt der Transformationsausgabe Kopien von Eingabespalten hinzu.|  
|[Transformation für Datenkonvertierung](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)|Diese Transformation konvertiert den Datentyp einer Spalte in einen anderen Datentyp.|  
|[Transformation für abgeleitete Spalten](../../../integration-services/data-flow/transformations/derived-column-transformation.md)|Diese Transformation füllt Spalten mit den Ergebnissen von Ausdrücken auf.|  
|[Transformation für das Exportieren von Spalten](../../../integration-services/data-flow/transformations/export-column-transformation.md)|Diese Transformation fügt Daten aus einem Datenfluss in eine Datei ein.|  
|[Transformation für das Importieren von Spalten](../../../integration-services/data-flow/transformations/import-column-transformation.md)|Diese Transformation liest Daten aus einer Datei und fügt sie einem Datenfluss hinzu.|  
|[Skriptkomponente](../../../integration-services/data-flow/transformations/script-component.md)|Diese Transformation verwendet ein Skript zum Extrahieren, Transformieren oder Laden von Daten.|  
|[Transformation für OLE DB-Befehl](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)|Diese Transformation führt SQL-Befehle für jede Zeile in einem Datenfluss aus.|  
  
## <a name="rowset-transformations"></a>Rowsettransformationen  
 Mit den folgenden Transformationen werden neue Rowsets erstellt. Rowsets schließen Aggregatwerte und sortierte Werte, Stichprobenrowsets oder pivotierte bzw. nicht pivotierte Rowsets ein.  
  
|Transformation|Description|  
|--------------------|-----------------|  
|[Transformation für das Aggregieren](../../../integration-services/data-flow/transformations/aggregate-transformation.md)|Diese Transformation führt Aggregationen aus, wie z. B. AVERAGE, SUM und COUNT.|  
|[Transformation zum Sortieren](../../../integration-services/data-flow/transformations/sort-transformation.md)|Diese Transformation sortiert Daten.|  
|[Transformation für Prozentwert-Stichproben](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)|Diese Transformation erstellt ein Stichprobendataset mithilfe eines Prozentwerts, um die Stichprobengröße anzugeben.|  
|[Transformation für Zeilenstichproben](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)|Diese Transformation erstellt ein Stichprobendataset, indem die Anzahl von Zeilen in der Stichprobe angegeben wird.|  
|[Transformation für Pivot](../../../integration-services/data-flow/transformations/pivot-transformation.md)|Diese Transformation erstellt eine weniger normalisierte Version einer normalisierten Tabelle.|  
|[Entpivotierungstransformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)|Diese Transformation erstellt eine stärker normalisierte Version einer nicht normalisierten Tabelle.|  
  
## <a name="split-and-join-transformations"></a>Transformationen für Teilen und Verknüpfen  
 Mit den folgenden Transformationen werden Zeilen an verschiedene Ausgaben verteilt, Kopien der Transformationseingaben erstellt, mehrere Eingaben zu einer einzigen Ausgabe verknüpft sowie Suchvorgänge ausgeführt.  
  
|Transformation|Description|  
|--------------------|-----------------|  
|[Transformation für bedingtes Teilen](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)|Diese Transformation routet Datenzeilen an andere Ausgaben.|  
|[Transformation für Multicast](../../../integration-services/data-flow/transformations/multicast-transformation.md)|Diese Transformation verteilt Datasets an mehrere Ausgaben.|  
|[Transformation für UNION ALL](../../../integration-services/data-flow/transformations/union-all-transformation.md)|Diese Transformation führt mehrere Datasets zusammen.|  
|[Transformation für Zusammenführen](../../../integration-services/data-flow/transformations/merge-transformation.md)|Diese Transformation führt zwei sortierte Datasets zusammen.|  
|[Transformation für Zusammenführungsjoin](../../../integration-services/data-flow/transformations/merge-join-transformation.md)|Diese Transformation verknüpft zwei Datasets mithilfe eines FULL-, LEFT- oder INNER-Joins.|  
|[Transformation für Suche](../../../integration-services/data-flow/transformations/lookup-transformation.md)|Diese Transformation sucht Werte in einer Verweistabelle mithilfe einer genauen Übereinstimmung.|  
|[Cachetransformation](../../../integration-services/data-flow/transformations/cache-transform.md)|Die Transformation, die Daten aus einer verbundenen Datenquelle im Datenfluss in einen Cacheverbindungs-Manager schreibt, der die Daten in einer Cachedatei speichert. Die Transformation für Suche führt Suchvorgänge in den Daten der Cachedatei aus.|  
|[Balanced Data Distributor (BDD)-Transformation](../../../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)|Die Transformation verteilt Puffer mit eingehenden Zeilen gleichmäßig auf Ausgaben für separate Threads, um die Leistung von SSIS-Paketen zu verbessern, die auf Mehrkern- und Mehrprozessorservern ausgeführt werden.|  
  
## <a name="auditing-transformations"></a>Überwachen von Transformationen  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] enthält die folgenden Transformationen, um Überwachungsinformationen hinzuzufügen und Zeilen zu zählen.  
  
|Transformation|Description|  
|--------------------|-----------------|  
|[Überwachungstransformation](../../../integration-services/data-flow/transformations/audit-transformation.md)|Diese Transformation stellt dem Datenfluss in einem Paket Informationen zur Umgebung zur Verfügung.|  
|[Transformation für Zeilenanzahl](../../../integration-services/data-flow/transformations/row-count-transformation.md)|Diese Transformation zählt die Zeilen in einem Datenfluss und speichert die endgültige Anzahl in einer Variablen.|  
  
## <a name="custom-transformations"></a>Benutzerdefinierte Transformationen  
 Sie können auch benutzerdefinierte Transformationen erstellen. Weitere Informationen finden Sie unter [Entwickeln einer benutzerdefinierten Transformationskomponente mit synchronen Ausgaben](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) und [Entwickeln einer benutzerdefinierten Transformationskomponente mit asynchronen Ausgaben](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md).  
  
  

