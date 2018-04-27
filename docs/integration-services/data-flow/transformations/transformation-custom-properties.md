---
title: Benutzerdefinierte Eigenschaften von Transformationen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Slowly Changing Dimension transformation
- Import Column transformation [Integration Services]
- Sort transformation
- Unpivot transformation
- Merge Join transformation
- Data Mining Query transformation
- Fuzzy Grouping transformation
- Data Conversion transformation
- Fuzzy Lookup transformation
- Term Extraction transformation
- Row Count transformation custom properties [Integration Services]
- transformations [Integration Services], properties
- Pivot transformation
- Lookup transformation
- Percentage Sampling transformation
- Export Column transformation [Integration Services]
- Row Sampling transformation
- Conditional Split transformation custom properties [Integration Services]
- custom properties [Integration Services]
- Audit transformation
- Term Lookup transformation
- Script Component transformation custom properties [Integration Services]
- Derived Column transformation
- OLE DB Command transformation
- Copy Column transformation custom properties [Integration Services]
- Character Map transformation custom properties [Integration Services]
ms.assetid: 56f5df6a-56f6-43df-bca9-08476a3bd931
caps.latest.revision: 72
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 649d1253bad67ae846b2aaa8e9c26bb8ffebfb3e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="transformation-custom-properties"></a>Transformation Custom Properties
  Neben den Eigenschaften, die die meisten Datenflussobjekte im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Objektmodell aufweisen, verfügen zahlreiche Datenflussobjekte über benutzerdefinierte objektspezifische Eigenschaften. Diese benutzerdefinierten Eigenschaften sind nur zur Laufzeit verfügbar und sind nicht in der [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Managed Programming Referenz-Dokumentation dokumentiert.  
  
 In diesem Thema werden die benutzerdefinierten Eigenschaften der verschiedenen Datenflusstransformationen aufgelistet und beschrieben. Informationen über die gemeinsamen Eigenschaften der meisten Datenflussobjekte finden Sie unter [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 Einige Eigenschaften von Transformationen können mit Eigenschaftsausdrücken festgelegt werden. Weitere Informationen finden Sie unter [Data Flow-Eigenschaften, die mithilfe von Ausdrücken festgelegt werden können](http://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8).  
  
## <a name="transformations-with-custom-properties"></a>Transformationen mit benutzerdefinierten Eigenschaften  
  
||||  
|-|-|-|  
|[Aggregat](#aggregate)|[Exportieren von Spalten](#extract)|[Zeilenanzahl](#rowcount)|  
|[Überwachung](#audit)|[Fuzzygruppierung](#fgroup)|[Zeilenstichprobe](#rowsamp)|  
|[Cachetransformation](#cachetransform)|[Fuzzysuche](#flookup)|[Skriptkomponente](#script)|  
|[Zeichenzuordnung](#charmap)|[Importieren von Spalten](#insert)|[Langsam veränderliche Dimensionen](#scd)|  
|[Bedingtes Teilen](#condsplit)|[Suche](#lookup)|[Sort](#sort)|  
|[Kopieren von Spalten](#copymap)|[Merge Join](#mjoin)|[Ausdrucksextrahierung](#textract)|  
|[Datenkonvertierung](#dataconv)|[OLE DB-Befehl](#oledbcmd)|[Ausdruckssuche](#tlookup)|  
|[Data Mining-Abfrage](#dmquery)|[Prozentwert-Stichprobe](#percent)|[Entpivotieren](#unpivot)|  
|[Abgeleitete Spalte](#derived)|[Pivotieren](#pivot)||  
  
### <a name="transformations-without-custom-properties"></a>Transformationen ohne benutzerdefinierte Eigenschaften  
 Die folgenden Transformationen verfügen nicht über benutzerdefinierte Eigenschaften auf Komponenten-, Eingabe- oder Ausgabeebene: [Merge Transformation](../../../integration-services/data-flow/transformations/merge-transformation.md), [Multicast Transformation](../../../integration-services/data-flow/transformations/multicast-transformation.md)und [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md). Sie verwenden nur die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
##  <a name="aggregate"></a> Benutzerdefinierte Eigenschaften der Transformation für das Aggregieren  
 Die Transformation für das Aggregieren verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für das Aggregieren. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|AutoExtendFactor|Integer|Ein Wert zwischen 1 und 100, der den Prozentsatz angibt, um den der Arbeitsspeicher während der Aggregation erweitert werden kann. Der Standardwert dieser Eigenschaft ist **25**.|  
|CountDistinctKeys|Integer|Ein Wert, der die genaue Anzahl unterschiedlicher Werte angibt, die durch die Aggregation geschrieben werden können. Wenn ein CountDistinctScale-Wert angegeben wird, hat der Wert in CountDistinctKeys Vorrang.|  
|CountDistinctScale|Ganze Zahl (Enumeration)|Ein Wert, der die ungefähre Anzahl unterschiedlicher Werte in einer Spalte beschreibt, die von der Aggregation gezählt werden können. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **Niedrig** (1) – bis zu 500.000 Schlüsselwerte.<br /><br /> **Mittel** (2) – bis zu 5 Millionen Schlüsselwerte.<br /><br /> **Hoch** (3) – mehr als 25 Millionen Schlüsselwerte.<br /><br /> **Keine Angabe** (0) – es wird kein CountDistinctScale-Wert verwendet. Die Verwendung der Option „ **Keine Angabe** (0)“ beeinträchtigt bei großen Datasets möglicherweise die Leistung.|  
|Schlüssel|Integer|Ein Wert, der die genaue Anzahl der GROUP BY-Schlüssel angibt, die durch die Aggregation geschrieben werden. Wenn ein KeyScale-Wert angegeben wird, hat der Wert in „Keys“ Vorrang.|  
|KeyScale|Ganze Zahl (Enumeration)|Ein Wert, der beschreibt, wie viele GROUP BY-Schlüsselwerte ungefähr von der Aggregation geschrieben werden können. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **Niedrig** (1) – bis zu 500.000 Schlüsselwerte.<br /><br /> **Mittel** (2) – bis zu 5 Millionen Schlüsselwerte.<br /><br /> **Hoch** (3) – mehr als 25 Millionen Schlüsselwerte.<br /><br /> **Keine Angabe** (0) – es wird kein KeyScale-Wert verwendet.|  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften der Ausgabe der Transformation für das Aggregieren beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|Schlüssel|Integer|Ein Wert, der die genaue Anzahl der GROUP BY-Schlüssel angibt, die durch die Aggregation geschrieben werden können. Wenn ein KeyScale-Wert angegeben wird, hat der Wert in „Keys“ Vorrang.|  
|KeyScale|Ganze Zahl (Enumeration)|Ein Wert, der beschreibt, wie viele GROUP BY-Schlüsselwerte ungefähr von der Aggregation geschrieben werden können. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **Niedrig** (1) – bis zu 500.000 Schlüsselwerte.<br /><br /> **Mittel** (2) – bis zu 5 Millionen Schlüsselwerte.<br /><br /> **Hoch** (3) – mehr als 25 Millionen Schlüsselwerte.<br /><br /> **Keine Angabe** (0) – es wird kein KeyScale-Wert verwendet.|  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für das Aggregieren beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|AggregationColumnId|Integer|Die **LineageID** einer Spalte, die an der GROUP BY-Funktion oder der Aggregatfunktion teilnimmt.|  
|AggregationComparisonFlags|Integer|Ein Wert, der angibt, wie die Transformation für das Aggregieren Zeichenfolgendaten in einer Spalte vergleicht. Weitere Informationen finden Sie unter [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|AggregationType|Ganze Zahl (Enumeration)|Ein Wert, der den Aggregationsvorgang angibt, der für die Spalte ausgeführt werden soll. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **Gruppieren nach** (0)<br /><br /> **Anzahl** (1)<br /><br /> **Alle zählen** (2)<br /><br /> **CountDistinct** (3)<br /><br /> **Summe** (4)<br /><br /> **Durchschnitt** (5)<br /><br /> **Maximum** (7)<br /><br /> **Minimum** (6)|  
|CountDistinctKeys|Integer|Wenn der Aggregationstyp **COUNT DISTINCT**ist, ein Wert, der die genaue Anzahl von Schlüsseln angibt, die von der Aggregation geschrieben werden können. Wenn ein CountDistinctScale-Wert angegeben wird, hat der Wert in CountDistinctKeys Vorrang.|  
|CountDistinctScale|Ganze Zahl (Enumeration)|Wenn der Aggregationstyp **COUNT DISTINCT**ist, ein Wert, der beschreibt, wie viele Schlüsselwerte ungefähr von der Aggregation geschrieben werden können. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **Niedrig** (1) – bis zu 500.000 Schlüsselwerte.<br /><br /> **Mittel** (2) – bis zu 5 Millionen Schlüsselwerte.<br /><br /> **Hoch** (3) – mehr als 25 Millionen Schlüsselwerte.<br /><br /> **Keine Angabe** (0) – es wird kein CountDistinctScale-Wert verwendet.|  
|IsBig|Boolean|Ein Wert, der angibt, ob die Spalte einen Wert größer als 4 Milliarden oder einen Wert mit einer höheren Genauigkeit als ein Gleitkommawert mit doppelter Genauigkeit enthält. Der Wert kann 0 oder 1 sein. 0 gibt an, dass IsBig **False** ist und dass die Spalte keinen großen oder genauen Wert enthält. Der Standardwert dieser Eigenschaft ist „1“.|  
  
 Die Eingabe und die Eingabespalten der Transformation für das Aggregieren verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Aggregate Transformation](../../../integration-services/data-flow/transformations/aggregate-transformation.md).  
  
##  <a name="audit"></a> Benutzerdefinierte Eigenschaften der Überwachungstransformation  
 Die Überwachungstransformation verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Überwachungstransformation. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|LineageItemSelected|Ganze Zahl (Enumeration)|Das für die Ausgabe ausgewählte Überwachungsobjekt. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **GUID der Ausführungsinstanz** (0)<br /><br /> **Startzeit der Ausführung** (4)<br /><br /> **Computername** (5)<br /><br /> **Paket-ID** (1)<br /><br /> **Paketname** (2)<br /><br /> **Task-ID** (8)<br /><br /> **Taskname** (7)<br /><br /> **Benutzername** (6)<br /><br /> **Versions-ID** (3)|  
  
 Die Eingabe, die Eingabespalten und die Ausgabe der Überwachungstransformation verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Audit Transformation](../../../integration-services/data-flow/transformations/audit-transformation.md).  
  
##  <a name="cachetransform"></a> Benutzerdefinierte Eigenschaften der Transformation für Cachetransformation  
 Die Transformation für Cachetransformation verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die Eigenschaften der Transformation für Cachetransformation. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ConnectionManager|Zeichenfolge|Gibt den Namen des Verbindungs-Managers an.|  
|ValidateExternalMetadata|Boolean|Gibt an, ob die Cachetransformation zur Entwurfszeit mit externen Datenquellen überprüft wird. Wenn die Eigenschaft auf **False**festgelegt wird, erfolgt zur Laufzeit eine Überprüfung anhand externer Datenquellen.<br /><br /> Der Standardwert lautet **True**.|  
|AvailableInputColumns|Zeichenfolge|Eine Liste der verfügbaren Eingabespalten.|  
|InputColumns|Zeichenfolge|Eine Liste der ausgewählten Eingabespalten.|  
|CacheColumnName|Zeichenfolge|Gibt den Namen der Spalte an, die einer ausgewählten Eingabespalte zugeordnet wird.<br /><br /> Der Name der Spalte in der CacheColumnName-Eigenschaft muss mit dem Namen der entsprechenden Spalte übereinstimmen, die auf der Seite **Spalten** des **Editors für den Cacheverbindungs-Manager**aufgelistet ist.<br /><br /> Weitere Informationen finden Sie unter [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md).|  
  
##  <a name="charmap"></a> Benutzerdefinierte Eigenschaften der Transformation zum Zuordnen der Zeichen  
 Die Transformation zum Zuordnen der Zeichen verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation zum Zuordnen der Zeichen. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|Ein Wert, der die **LineageID** der Eingabespalte angibt, die die Quelle der Ausgabespalte ist.|  
|MapFlags|Ganze Zahl (Enumeration)|Ein Wert, der die Zeichenfolgenvorgänge angibt, die die Transformation zum Zuordnen der Zeichen für die Spalte ausführt. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **Byteumkehrung** (2)<br /><br /> **Normale Breite** (6)<br /><br /> **Halbe Breite** (5)<br /><br /> **Hiragana** (3)<br /><br /> **Katakana** (4)<br /><br /> **Linguistische Schreibweise** (7)<br /><br /> **Kleinbuchstaben** (0)<br /><br /> **Chinesisch (vereinfacht)** (8)<br /><br /> **Chinesisch (traditionell)**(9)<br /><br /> **Großbuchstaben** (1)|  
  
 Die Eingabe, die Eingabespalten und die Ausgabe der Transformation zum Zuordnen der Zeichen verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md).  
  
##  <a name="condsplit"></a> Benutzerdefinierte Eigenschaften der Transformation für bedingtes Teilen  
 Die Transformation für bedingtes Teilen verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabe der Transformation für bedingtes Teilen. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|EvaluationOrder|Integer|Ein Wert, der die Position einer Bedingung, die einer Ausgabe zugeordnet ist, in der Liste der Bedingungen angibt, die die Transformation für bedingtes Teilen auswertet. Die Bedingungen werden vom niedrigsten bis zum höchsten Wert ausgewertet.|  
|expression|Zeichenfolge|Ein Ausdruck, der die Bedingung darstellt, die die Transformation für bedingtes Teilen auswertet. Spalten werden durch Herkunftsbezeichner dargestellt.|  
|FriendlyExpression|Zeichenfolge|Ein Ausdruck, der die Bedingung darstellt, die die Transformation für bedingtes Teilen auswertet. Spalten werden durch ihre Namen dargestellt.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
|IsDefaultOut|Boolean|Ein Wert, der angibt, ob die Ausgabe die Standardausgabe ist.|  
  
 Die Eingabe, die Eingabespalten und die Ausgabespalten der Transformation für bedingtes Teilen verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
##  <a name="copymap"></a> Benutzerdefinierte Eigenschaften der Transformation für das Kopieren von Spalten  
 Die Transformation für das Kopieren von Spalten verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für das Kopieren von Spalten. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|copyColumnId|Integer|Die **LineageID** der Eingabespalte, aus der die Ausgabespalte kopiert wird.|  
  
 Die Eingabe, die Eingabespalten und die Ausgabe der Transformation für das Kopieren von Spalten verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Copy Column Transformation](../../../integration-services/data-flow/transformations/copy-column-transformation.md).  
  
##  <a name="dataconv"></a> Benutzerdefinierte Eigenschaften der Transformation für Datenkonvertierung  
 Die Transformation für Datenkonvertierung verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für Datenkonvertierung. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|FastParse|Boolean|Ein Wert, der angibt, ob die Spalte die schnelleren gebietsschemaneutralen Analyseroutinen von [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] oder die gebietsschemabezogenen Standardanalyseroutinen verwendet. Der Standardwert dieser Eigenschaft ist **False**. Weitere Informationen finden Sie unter [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) und [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013). zugreifen.<br /><br /> Hinweis: Diese Eigenschaft ist im **Transformations-Editor für Datenkonvertierung**nicht verfügbar, kann aber mit dem **Erweiterten Editor**festgelegt werden.|  
|SourceInputColumnLineageId|Integer|Die **LineageID** der Eingabespalte, die die Quelle der Ausgabespalte ist.|  
  
 Die Eingabe, die Eingabespalten und die Ausgabe der Transformation für Datenkonvertierung verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
##  <a name="dmquery"></a> Benutzerdefinierte Eigenschaften der Transformation für Data Mining-Abfragen  
 Die Transformation für Data Mining-Abfragen verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Data Mining-Abfragen. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ASConnectionId|Zeichenfolge|Der eindeutige Bezeichner des Verbindungsobjekts.|  
|ASConnectionString|Zeichenfolge|Die Verbindungszeichenfolge zu einem [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Projekt oder einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Datenbank.|  
|CatalogName|Zeichenfolge|Der Name einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Datenbank.|  
|ModelName|Zeichenfolge|Der Name des Data Mining-Modells.|  
|ModelStructureName|Zeichenfolge|Der Name der Miningstruktur.|  
|ObjectRef|Zeichenfolge|Ein XML-Tag, das die Data Mining-Struktur identifiziert, die von der Transformation verwendet wird.|  
|QueryText|Zeichenfolge|Die Vorhersageabfrageanweisung, die die Transformation verwendet.|  
  
 Die Eingabe, die Eingabespalten, die Ausgabe und die Ausgabespalten der Transformation für Data Mining-Abfragen verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Data Mining Query Transformation](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md).  
  
##  <a name="derived"></a> Benutzerdefinierte Eigenschaften der Transformation für abgeleitete Spalten  
 Die Transformation für abgeleitete Spalten verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten und Ausgabespalten der Transformation für abgeleitete Spalten. Wenn Sie die abgeleitete Spalte als neue Spalte hinzufügen, gelten diese benutzerdefinierten Eigenschaften für die neue Ausgabespalte. Wenn Sie den Inhalt einer vorhandenen Eingabespalte durch die abgeleiteten Ergebnisse ersetzen, gelten diese benutzerdefinierten Eigenschaften für die vorhandene Eingabespalte. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|expression|Zeichenfolge|Ein Ausdruck, der die Bedingung darstellt, die die Transformation für bedingtes Teilen auswertet. Spalten werden durch die **LineageID** -Eigenschaft für die Spalte dargestellt.|  
|FriendlyExpression|Zeichenfolge|Ein Ausdruck, der die Bedingung darstellt, die die Transformation für bedingtes Teilen auswertet. Spalten werden durch ihre Namen dargestellt.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
  
 Die Eingabe und die Ausgabe der Transformation für abgeleitete Spalten verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Derived Column Transformation](../../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
##  <a name="extract"></a> Benutzerdefinierte Eigenschaften der Transformation für das Exportieren von Spalten  
 Die Transformation für das Exportieren von Spalten verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation für das Exportieren von Spalten. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|AllowAppend|Boolean|Ein Wert, der angibt, ob die Transformation Daten an eine vorhandene Datei anhängt. Der Standardwert dieser Eigenschaft ist **False**.|  
|ForceTruncate|Boolean|Ein Wert, der angibt, ob die Transformation eine vorhandene Datei vor dem Schreiben der Daten abschneidet. Der Standardwert dieser Eigenschaft ist **False**.|  
|FileDataColumnID|Integer|Ein Wert, der die Spalte identifiziert, die die Daten enthält, die von der Transformation in eine Datei eingefügt werden. In **Spalte extrahieren**hat diese Eigenschaft den Wert 0; in der Dateipfadspalte enthält diese Eigenschaft die **LineageID** von Spalte extrahieren.|  
|WriteBOM|Boolean|Ein Wert, der angibt, ob eine Bytereihenfolge-Marke (Byte-Order Mark, BOM) in die Datei geschrieben wird.|  
  
 Die Eingabe, die Ausgabe und die Ausgabespalten der Transformation für das Exportieren von Spalten verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md).  
  
##  <a name="insert"></a> Benutzerdefinierte Eigenschaften der Transformation für das Importieren von Spalten  
 Die Transformation für das Importieren von Spalten verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation für das Importieren von Spalten. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ExpectBOM|Boolean|Ein Wert, der angibt, ob die Transformation zum Importieren von Spalten eine Bytereihenfolge-Marke (BOM) erwartet. Eine BOM wird nur bei Daten vom DT_NTEXT-Datentyp erwartet.|  
|FileDataColumnID|Integer|Ein Wert, der die Spalte identifiziert, die die Daten enthält, die von der Transformation in den Datenfluss eingefügt werden. In der Spalte mit den einzufügenden Daten hat diese Eigenschaft den Wert 0; in der Spalte mit den Quelldateipfaden enthält diese Eigenschaft die **LineageID** der Spalte mit den einzufügenden Daten.|  
  
 Die Eingabe, die Ausgabe und die Ausgabespalten der Transformation für das Importieren von Spalten verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Import Column Transformation](../../../integration-services/data-flow/transformations/import-column-transformation.md).  
  
##  <a name="fgroup"></a> Benutzerdefinierte Eigenschaften der Transformation für Fuzzygruppierung  
 Die Transformation für Fuzzygruppierung verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Fuzzygruppierung. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|Trennzeichen|Zeichenfolge|Die von der Transformation verwendeten Tokentrennzeichen. Zu den Standardtrennzeichen zählen folgende Zeichen: Leerzeichen ( ), Komma (,), Punkt (.), Semikolon (;), Doppelpunkt (:), Bindestrich (-), doppeltes gerades Anführungszeichen ("), einfaches gerades Anführungszeichen ('), kaufmännisches Und-Zeichen (&), Schrägstrich (/), umgekehrter Schrägstrich (\\), at-Zeichen (@), Ausrufezeichen (!), Fragezeichen (?), öffnende Klammer ((), schließende Klammer ()), kleiner als (\<), größer als (>), öffnende eckige Klammer ([), schließende eckige Klammer (]), öffnende geschweifte Klammer ({), schließende geschweifte Klammer (}), senkrechter Strich (&#124;), Nummernzeichen (#), Sternchen (*), Caretzeichen (^) und Prozentzeichen (%).|  
|Exhaustive|Boolean|Ein Wert, der angibt, ob jeder Eingabedatensatz mit jedem anderen Eingabedatensatz verglichen wird. Der Wert von **True** wird meistens zu Debugzwecken verwendet. Der Standardwert dieser Eigenschaft ist **False**.<br /><br /> Hinweis: Diese Eigenschaft ist im **Transformations-Editor für Fuzzygruppierung**nicht verfügbar, kann aber mit dem **Erweiterten Editor**festgelegt werden.|  
|MaxMemoryUsage|Integer|Die Höchstmenge an Arbeitsspeicher zur Verwendung durch die Transformation. Der Standardwert dieser Eigenschaft ist **0**, wodurch die dynamische Speicherauslastung aktiviert wird.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.<br /><br /> Hinweis: Diese Eigenschaft ist im **Transformations-Editor für Fuzzygruppierung**nicht verfügbar, kann aber mit dem **Erweiterten Editor**festgelegt werden.|  
|MinSimilarity|Double|Der Schwellenwert für die Ähnlichkeit, mit dem die Transformation Duplikate ermittelt, der als ein Wert zwischen 0 und 1 ausgedrückt wird.  Der Standardwert dieser Eigenschaft ist 0.8.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation für Fuzzygruppierung. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ExactFuzzy|Ganze Zahl (Enumeration)|Ein Wert, der angibt, ob die Transformation eine Fuzzyübereinstimmung oder eine genaue Übereinstimmung ausführt. Die gültigen Werte sind **Genau** und **Fuzzy**. Der Standardwert für diese Eigenschaft ist **Fuzzy**.|  
|FuzzyComparisonFlags|Ganze Zahl (Enumeration)|Ein Wert, der angibt, wie die Transformation die Zeichenfolgendaten in einer Spalte vergleicht. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **FullySensitive**<br /><br /> **IgnoreCase**<br /><br /> **IgnoreKanaType**<br /><br /> **IgnoreNonSpace**<br /><br /> **IgnoreSymbols**<br /><br /> **IgnoreWidth**<br /><br /> <br /><br /> Weitere Informationen finden Sie unter [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|LeadingTrailingNumeralsSignificant|Ganze Zahl (Enumeration)|Ein Wert, der die Bedeutung von Zahlen angibt. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **NumeralsNotSpecial** (0) – wird verwendet, wenn Zahlen nicht von Bedeutung sind.<br /><br /> **LeadingNumeralsSignificant** (1) – wird verwendet, wenn führende Zahlen von Bedeutung sind.<br /><br /> **TrailingNumeralsSignificant** (2) – wird verwendet, wenn nachfolgende Zahlen von Bedeutung sind.<br /><br /> **LeadingAndTrailingNumeralsSignificant** (3) – wird verwendet, wenn sowohl führende als auch nachfolgende Zahlen von Bedeutung sind.|  
|MinSimilarity|Double|Der Schwellenwert für die Ähnlichkeit, der für den Join in der Spalte verwendet und als ein Wert zwischen 0 und 1 angegeben wird. Nur Zeilen, die größer sind als der Schwellenwert, gelten als Übereinstimmung.|  
|ToBeCleaned|Boolean|Ein Wert, der angibt, ob die Spalte zum Ermitteln von Duplikaten verwendet wird, d. h., ob dies eine Spalte ist, für die Sie eine Gruppierung vornehmen. Der Standardwert dieser Eigenschaft ist **False**.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für Fuzzygruppierung. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|ColumnType|Ganze Zahl (Enumeration)|Ein Wert, der den Typ der Ausgabespalte identifiziert. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **Nicht definiert** (0)<br /><br /> **KeyIn** (1)<br /><br /> **KeyOut** (2)<br /><br /> **Ähnlichkeit** (3)<br /><br /> **ColumnSimilarity** (4)<br /><br /> **PassThru** (5)<br /><br /> **Kanonisch**(6)|  
|InputID|Integer|Die **LineageID** der entsprechenden Eingabespalte.|  
  
 Die Eingabe und die Ausgabe der Transformation für Fuzzygruppierung verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
##  <a name="flookup"></a> Benutzerdefinierte Eigenschaften der Transformation für Fuzzysuche  
 Die Transformation für Fuzzysuche verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Fuzzysuche. Alle Eigenschaften außer **ReferenceMetadataXML** haben Lese-/Schreibzugriff.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|CopyReferenceTable|Boolean|Gibt an, ob eine Kopie der Verweistabelle für die Indexerstellung der Fuzzysuche und nachfolgende Suchen erstellt werden soll. Der Standardwert dieser Eigenschaft ist **True**.|  
|Trennzeichen|Zeichenfolge|Die Trennzeichen, die von der Transformation verwendet werden, um Spaltenwerte mit Token zu versehen. Zu den Standardtrennzeichen zählen folgende Zeichen: Leerzeichen ( ), Komma (,), Punkt (.), Semikolon (;), Doppelpunkt (:), Bindestrich (-), doppeltes gerades Anführungszeichen ("), einfaches gerades Anführungszeichen ('), kaufmännisches Und-Zeichen (&), Schrägstrich (/), umgekehrter Schrägstrich (\\), at-Zeichen (@), Ausrufezeichen (!), Fragezeichen (?), öffnende Klammer ((), schließende Klammer ()), kleiner als (\<), größer als (>), öffnende eckige Klammer ([), schließende eckige Klammer (]), öffnende geschweifte Klammer ({), schließende geschweifte Klammer (}), senkrechter Strich (&#124;). Nummernzeichen (#), Sternchen (*), Caretzeichen (^) und Prozentzeichen (%).|  
|DropExistingMatchIndex|Boolean|Ein Wert, der angibt, ob der in MatchIndexName angegebene Übereinstimmungsindex gelöscht wird, wenn MatchIndexOptions nicht auf ReuseExistingIndex festgelegt ist. Der Standardwert dieser Eigenschaft ist **True**.|  
|Exhaustive|Boolean|Ein Wert, der angibt, ob jeder Eingabedatensatz mit jedem anderen Eingabedatensatz verglichen wird. Der Wert von **True** wird meistens zu Debugzwecken verwendet. Der Standardwert dieser Eigenschaft ist **False**.<br /><br /> Hinweis: Diese Eigenschaft ist im **Transformations-Editor für Fuzzysuche**nicht verfügbar, kann aber mit dem **Erweiterten Editor**festgelegt werden.|  
|MatchIndexName|Zeichenfolge|Der Name des Übereinstimmungsindexes. Der Übereinstimmungsindex ist die Tabelle, in der die Transformation den von ihr verwendeten Index erstellt und speichert. Wenn der Übereinstimmungsindex wiederverwendet wird, gibt MatchIndexName den wiederzuverwendenden Index an. MatchIndexName muss ein gültiger [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Bezeichnername sein. Wenn der Name z. B. Leerzeichen enthält, muss der Name in Klammern eingeschlossen werden.|  
|MatchIndexOptions|Ganze Zahl (Enumeration)|Ein Wert, der angibt, wie die Transformation den Übereinstimmungsindex verwaltet. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **ReuseExistingIndex** (0)<br /><br /> **GenerateNewIndex** (1)<br /><br /> **GenerateAndPersistNewIndex** (2)<br /><br /> **GenerateAndMaintainNewIndex** (3)|  
|MaxMemoryUsage|Integer|Die maximale Cachegröße für die Suchtabelle. Der Standardwert dieser Eigenschaft ist **0**. Das bedeutet, dass es kein Limit für die Cachegröße gibt.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.<br /><br /> Hinweis: Diese Eigenschaft ist im **Transformations-Editor für Fuzzysuche**nicht verfügbar, kann aber mit dem **Erweiterten Editor**festgelegt werden.|  
|MaxOutputMatchesPerInput|Integer|Die maximale Anzahl der Übereinstimmungen, die pro Eingabezeile von der Transformation zurückgegeben werden können. Der Standardwert dieser Eigenschaft ist **1**.<br /><br /> Hinweis: Werte größer als 100 können nur mit dem **Erweiterten Editor**angegeben werden.|  
|MinSimilarity|Integer|Der Schwellenwert für die Ähnlichkeit, den die Transformation auf der Komponentenebene verwendet und der als ein Wert zwischen 0 und 1 angegeben wird. Nur Zeilen, die größer sind als der Schwellenwert, gelten als Übereinstimmung.|  
|ReferenceMetadataXML|Zeichenfolge|[!INCLUDE[ssInternalOnly](../../../includes/ssinternalonly-md.md)]|  
|ReferenceTableName|Zeichenfolge|Der Name der Suchtabelle. Der Name muss ein gültiger [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Bezeichnername sein. Wenn der Name z. B. Leerzeichen enthält, muss der Name in Klammern eingeschlossen werden.|  
|WarmCaches|Boolean|Wenn der Wert "true" ist, lädt die Suche den Index und die Verweistabelle in den Arbeitsspeicher, bevor die Ausführung beginnt. Dadurch kann die Leistung optimiert werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation für Fuzzysuche. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|FuzzyComparisonFlags|Integer|Ein Wert, der angibt, wie die Transformation die Zeichenfolgendaten in einer Spalte vergleicht. Weitere Informationen finden Sie unter [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|FuzzyComparisonFlagsEx|Ganze Zahl (Enumeration)|Ein Wert, der angibt, welche erweiterten Vergleichsflags die Transformation verwendet. Die Werte können **MapExpandLigatures, MapFoldCZone**, **MapFoldDigits**, **MapPrecomposed**, und **NoMapping**umfassen. **NoMapping** kann nicht mit anderen Flags verwendet werden.|  
|JoinToReferenceColumn|Zeichenfolge|Ein Wert, der den Namen der Spalte in der Verweistabelle angibt, mit der die Spalte verknüpft wird.|  
|JoinType|Integer|Ein Wert, der angibt, ob die Transformation eine Fuzzyübereinstimmung oder eine genaue Übereinstimmung ausführt. Der Standardwert für diese Eigenschaft ist **Fuzzy**. Der ganzzahlige Wert für den genauen Jointyp ist **1** , und der Wert für den Fuzzyjointyp ist **2**.|  
|MinSimilarity|Double|Der Schwellenwert für die Ähnlichkeit, den die Transformation auf der Spaltenebene verwendet und der als ein Wert zwischen 0 und 1 angegeben wird. Nur Zeilen, die größer sind als der Schwellenwert, gelten als Übereinstimmung.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für Fuzzysuche. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
> [!NOTE]  
>  Für Ausgabespalten, die Pass-Through-Werte aus den entsprechenden Eingabespalten enthalten, ist CopyFromReferenceColumn leer, und SourceInputColumnLineageID enthält die **LineageID** der entsprechenden Eingabespalte. Für Ausgabespalten, die Suchergebnisse enthalten, enthält CopyFromReferenceColumn den Namen der Suchspalte, und SourceInputColumnLineageID ist leer.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ColumnType|Ganze Zahl (Enumeration)|Ein Wert, der den Typ der Ausgabespalte für Spalten ermittelt, die die Transformation der Ausgabe hinzufügt. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **Nicht definiert** (0)<br /><br /> **Ähnlichkeit** (1)<br /><br /> **Vertrauen** (2)<br /><br /> **ColumnSimilarity** (3)|  
|CopyFromReferenceColumn|Zeichenfolge|Ein Wert, der den Namen der Spalte in der Verweistabelle angibt, die den Wert in einer Ausgabetabelle bereitstellt.|  
|SourceInputColumnLineageId|Integer|Ein Wert, der die Eingabespalte identifiziert, die Werte für diese Ausgabespalte bereitstellt.|  
  
 Die Eingabe und die Ausgabe der Transformation für Fuzzysuche verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
##  <a name="lookup"></a> Benutzerdefinierte Eigenschaften der Transformation für Suche  
 Die Transformation für Suche verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Suche. Alle Eigenschaften außer **ReferenceMetadataXML** haben Lese-/Schreibzugriff.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|CacheType|Ganze Zahl (Enumeration)|Der Cachetyp für die Suchtabelle. Die Werte sind **Vollständig** (0), **Teilweise** (1) und **Keine** (2). Der Standardwert dieser Eigenschaft ist **Full**.|  
|DefaultCodePage|Integer|Die zu verwendende Standardcodepage, wenn keine Codepageinformationen aus der Datenquelle verfügbar sind.|  
|MaxMemoryUsage|Integer|Die maximale Cachegröße für die Suchtabelle. Der Standardwert dieser Eigenschaft ist **25**. Das bedeutet, dass es kein Limit für die Cachegröße gibt.|  
|MaxMemoryUsage64|Integer|Die maximale Cachegröße für die Suchtabelle auf einem 64-Bit-Computer.|  
|NoMatchBehavior|Ganze Zahl (Enumeration)|Ein Wert, der angibt, ob Zeilen ohne übereinstimmende Einträge im Verweisdataset als Fehler behandelt werden.<br /><br /> Wenn die Eigenschaft auf „ **Zeilen ohne übereinstimmende Einträge als Fehler behandeln** (0)“ festgelegt wird, werden die Zeilen, die keine übereinstimmenden Einträge aufweisen, als Fehler behandelt. Mit der Seite **Fehlerausgabe** im Dialogfeld **Transformations-Editor für Suche** können Sie angeben, welche Aktionen ausgeführt werden sollen, wenn diese Art von Fehler auftritt. Weitere Informationen finden Sie unter [Transformations-Editor für Suche &#40;Seite Fehlerausgabe&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).<br /><br /> Wenn die Eigenschaft auf „**Zeilen ohne übereinstimmende Einträge an die Ausgabe nicht übereinstimmender Einträge senden** (1)“ festgelegt ist, werden die Zeilen nicht als Fehler behandelt.<br /><br /> Der Standardwert ist „ **Zeilen ohne übereinstimmende Einträge als Fehler behandeln** (0)“.|  
|ParameterMap|Zeichenfolge|Eine durch Semikolons getrennte Liste von Herkunfts-IDs, die den in der **SqlCommand** -Anweisung verwendeten Parametern zugeordnet werden.|  
|ReferenceMetadataXML|Zeichenfolge|Metadaten für die Spalten in der Suchtabelle, die die Transformation in ihre Ausgabe kopiert.|  
|SqlCommand|Zeichenfolge|Die SELECT-Anweisung, die Daten in die Suchtabelle lädt.|  
|SqlCommandParam|Zeichenfolge|Die parametrisierte SQL-Anweisung, die Daten in die Suchtabelle lädt.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation für Suche. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|CopyFromReferenceColumn|Zeichenfolge|Der Name der Spalte in der Verweistabelle, aus der eine Spalte kopiert wird.|  
|JoinToReferenceColumns|Zeichenfolge|Der Name der Spalte in der Verweistabelle, mit der eine Quellspalte verknüpft wird.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für Suche. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|CopyFromReferenceColumn|Zeichenfolge|Der Name der Spalte in der Verweistabelle, aus der eine Spalte kopiert wird.|  
  
 Die Eingabe und die Ausgabe der Transformation für Suche verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
##  <a name="mjoin"></a> Benutzerdefinierte Eigenschaften der Transformation für Zusammenführungsjoin  
 Die Transformation für Zusammenführungsjoin verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Zusammenführungsjoin.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|JoinType|Ganze Zahl (Enumeration)|Gibt an, ob es sich bei dem Join um einen inneren (2), linken äußeren (1) oder vollständigen Join (0) handelt.|  
|MaxBuffersPerInput|Integer|Der Wert der **MaxBuffersPerInput** -Eigenschaft muss nicht mehr konfiguriert werden, da Microsoft Änderungen vorgenommen hat, die das Risiko einer übermäßigen Arbeitsspeicherbelegung bei der Transformation für Zusammenführungsjoins reduzieren. Dieses Problem trat in einigen Fällen auf, wenn durch die Eingaben des Zusammenführungsjoins unregelmäßige Daten erzeugt wurden.|  
|NumKeyColumns|Integer|Die Anzahl von Spalten, die im Join verwendet werden.|  
|TreatNullsAsEqual|Boolean|Ein Wert, der angibt, ob die Transformation NULL-Werte als identische Werte behandelt. Der Standardwert dieser Eigenschaft ist **True**. Wenn der Eigenschaftenwert **False**ist, behandelt die Transformation NULL-Werte wie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für Zusammenführungsjoin. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|InputColumnID|Integer|Die **LineageID** der Eingabespalte, aus der Daten in diese Ausgabespalte kopiert werden.|  
  
 Die Eingabe, die Eingabespalten und die Ausgabe der Transformation für Zusammenführungsjoin verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Merge Join Transformation](../../../integration-services/data-flow/transformations/merge-join-transformation.md).  
  
##  <a name="oledbcmd"></a> Benutzerdefinierte Eigenschaften der Transformation für OLE DB-Befehl  
 Die Transformation für OLE DB-Befehl verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für OLE DB-Befehl.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|CommandTimeout|Integer|Die maximale Ausführungsdauer in Sekunden, bevor ein Timeout für den SQL-Befehl eintritt. Der Wert **0** gibt einen unbegrenzten Zeitraum an. Der Standardwert dieser Eigenschaft ist **0**.|  
|DefaultCodePage|Integer|Die zu verwendende Codepage, wenn keine Codepageinformationen aus der Datenquelle verfügbar sind.|  
|SqlCommand|Zeichenfolge|Die Transact-SQL-Anweisung, die von der Transformation für jede Zeile im Datenfluss ausgeführt wird.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der externen Spalten der Transformation für OLE DB-Befehl. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|DBParamInfoFlag|Ganze Zahl (Bitmaske)|Eine Gruppe von Flags, die Parametereigenschaften beschreiben. Weitere Informationen finden Sie unter DBPARAMFLAGSENUM in der OLE DB-Dokumentation in der MSDN Library.|  
  
 Die Eingabe, die Eingabespalten, die Ausgabe und die Ausgabespalten der Transformation für OLE DB-Befehl verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [OLE DB Command Transformation](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
##  <a name="percent"></a> Benutzerdefinierte Eigenschaften der Transformation für Prozentwert-Stichproben  
 Die Transformation für Prozentwert-Stichproben verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Prozentwert-Stichproben.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|Der vom Zufallszahlen-Generator verwendete Ausgangswert. Der Standardwert dieser Eigenschaft ist **0**und gibt an, dass die Transformation eine Taktanzahl verwendet.|  
|SamplingValue|Integer|Die Größe der Stichprobe als Prozentwert der Quelle.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgaben der Transformation für Prozentwert-Stichproben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|Ausgewählt|Boolean|Legt die Ausgabe fest, an die die als Stichprobe entnommenen Zeilen weitergeleitet werden. In der ausgewählten Ausgabe ist „Ausgewählt“ auf **True**festgelegt, in der nicht ausgewählten Ausgabe auf **False**.|  
  
 Die Eingabe, die Eingabespalten und die Ausgabespalten der Transformation für Prozentwert-Stichproben verfügen nicht über benutzerdefinierten Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
##  <a name="pivot"></a> Benutzerdefinierte Eigenschaften der Transformation für Pivot  
 Die folgende Tabelle beschreibt die benutzerdefinierten Komponenteneigenschaften der Pivottransformation.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|**PassThroughUnmatchedPivotKeyts**|Boolean|Legen Sie den Wert auf **True** fest, um die Pivottransformation zu konfigurieren, um Zeilen zu ignorieren, die nicht erkannte Werte in der Spalte "Pivotschlüssel" enthalten, und alle Pivotschlüsselwerte zu einer Protokollmeldung auszugeben, wenn das Paket ausgeführt wird.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation für Pivot. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|PivotUsage|Ganze Zahl (Enumeration)|Ein Wert, der die Rolle einer Spalte angibt, wenn das Dataset pivotiert wird.<br /><br /> **0**:<br />                      Die Spalte ist nicht pivotiert, und die Spaltenwerte werden über die Transformationsausgabe übergeben.<br /><br /> **1**:<br />                      Die Spalte ist Teil des festgelegten Schlüssels, der mindestens eine Zeile als Teil eines Datasets identifiziert. Alle Eingabezeilen mit demselben festgelegten Schlüssel werden zu einer einzigen Ausgabezeile zusammengefasst.<br /><br /> **2**:<br />                      Die Spalte ist eine Pivotspalte. Mindestens eine Spalte wird von jedem Spaltenwert erstellt.<br /><br /> **3**:<br />                      Die Werte aus dieser Spalte werden in Spalten platziert, die als Ergebnis des Pivotvorgangs erstellt werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für Pivot. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|PivotKeyValue|Zeichenfolge|Einer der möglichen Werte aus der Spalte, der durch den Wert seiner PivotUsage-Eigenschaft als Pivotschlüssel markiert wird.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
|SourceColumn|Integer|Die **LineageID** einer Eingabespalte, die einen pivotierten Wert oder -1 enthält. Der Wert -1 gibt an, dass die Spalte nicht in einem Pivotvorgang verwendet wird.|  
  
 Weitere Informationen finden Sie unter [Pivot Transformation](../../../integration-services/data-flow/transformations/pivot-transformation.md).  
  
##  <a name="rowcount"></a> Benutzerdefinierte Eigenschaften der Transformation für Zeilenanzahl  
 Die Transformation für Zeilenanzahl verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Zeilenanzahl. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|VariableName|Zeichenfolge|Der Name der Variablen, die die Zeilenanzahl enthält.|  
  
 Die Eingabe, die Eingabespalten, die Ausgabe und die Ausgabespalten der Transformation für Zeilenanzahl verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md).  
  
##  <a name="rowsamp"></a> Benutzerdefinierte Eigenschaften der Transformation für Zeilenstichproben  
 Die Transformation für Zeilenstichproben verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Zeilenstichproben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|Der vom Zufallszahlen-Generator verwendete Ausgangswert. Der Standardwert dieser Eigenschaft ist **0**und gibt an, dass die Transformation eine Taktanzahl verwendet.|  
|SamplingValue|Integer|Die Zeilenanzahl der Stichprobe.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgaben der Transformation für Zeilenstichproben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|Ausgewählt|Boolean|Legt die Ausgabe fest, an die die als Stichprobe entnommenen Zeilen weitergeleitet werden. In der ausgewählten Ausgabe ist „Ausgewählt“ auf **True**festgelegt, in der nicht ausgewählten Ausgabe auf **False**.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für Zeilenstichproben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|Ein Wert, der die **LineageID** der Eingabespalte angibt, die die Quelle der Ausgabespalte ist.|  
  
 Die Eingabe und die Eingabespalten der Transformation für Zeilenstichproben verfügen nicht über benutzerdefinierten Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md).  
  
##  <a name="script"></a> Benutzerdefinierte Eigenschaften der Skriptkomponente  
 Die Skriptkomponente verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind. Unabhängig davon, ob die Skriptkomponente als Quelle, Transformation oder Ziel fungiert, sind die gleichen benutzerdefinierten Eigenschaften verfügbar.  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften der Skriptkomponente beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|ReadOnlyVariables|Zeichenfolge|Eine durch Trennzeichen getrennte Liste von Variablen für den schreibgeschützten Zugriff durch die Skriptkomponente.|  
|ReadWriteVariables|Zeichenfolge|Eine durch Trennzeichen getrennte Liste von Variablen für den Lese-/Schreibzugriff durch die Skriptkomponente.|  
  
 Die Eingabe, die Eingabespalten, die Ausgabe und die Ausgabespalten der Skriptkomponente verfügen nicht über benutzerdefinierte Eigenschaften, sofern der Skriptentwickler keine benutzerdefinierten Eigenschaften erstellt.  
  
 Weitere Informationen finden Sie unter [Script Component](../../../integration-services/data-flow/transformations/script-component.md).  
  
##  <a name="scd"></a> Benutzerdefinierte Eigenschaften der Transformation für langsam veränderliche Dimensionen  
 Die Transformation für langsam veränderliche Dimensionen verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für langsam veränderliche Eigenschaften. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|CurrentRowWhere|Zeichenfolge|Die WHERE-Klausel in der SELECT-Anweisung, die die aktuelle Zeile aus Zeilen mit demselben Geschäftsschlüssel auswählt.|  
|EnableInferredMember|Boolean|Ein Wert, der angibt, ob Updates abgeleiteter Elemente erkannt werden. Der Standardwert dieser Eigenschaft ist **True**.|  
|FailOnFixedAttributeChange|Boolean|Ein Wert, der angibt, ob die Transformation fehlschlägt, wenn Zeilen oder Spalten mit festen Attributen Änderungen enthalten oder die Suche in der Dimensionstabelle fehlschlägt. Wenn Sie davon ausgehen, dass eingehende Zeilen neue Datensätze enthalten, legen Sie diesen Wert auf **True** fest, damit die Transformation fortgesetzt wird, wenn die Suche fehlgeschlagen ist, da die Transformation den Ausfall verwendet, um neue Datensätze zu ermitteln. Der Standardwert dieser Eigenschaft ist **False**.|  
|FailOnLookupFailure|Boolean|Ein Wert, der angibt, ob die Transformation fehlschlägt, wenn eine Suche nach einem vorhandenen Datensatz fehlschlägt. Der Standardwert dieser Eigenschaft ist **False**.|  
|IncomingRowChangeType|Integer|Ein Wert, der angibt, ob alle eingehenden Zeilen neue Zeilen sind oder ob die Transformation die Art der Änderung erkennen sollte.|  
|InferredMemberIndicator|Zeichenfolge|Der Spaltenname für das abgeleitete Element.|  
|SqlCommand|Zeichenfolge|Die SQL-Anweisung, die zum Erstellen eines Schemarowsets verwendet wird.|  
|UpdateChangingAttributeHistory|Boolean|Ein Wert, der angibt, ob Updates historischer Attribute an die Transformationsausgabe für veränderliche Attributupdates weitergeleitet werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation für langsam veränderliche Dimensionen. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ColumnType|Ganze Zahl (Enumeration)|Der Updatetyp der Spalte. Die Werte sind: **Veränderliches Attribut** (2), **Festes Attribut** (4), **Verlaufsattribut** (3) **Schlüssel** (1) und **Andere** (0).|  
  
 Die Eingabe, die Ausgaben und die Ausgabespalten der Transformation für langsam veränderliche Dimensionen verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
##  <a name="sort"></a> Benutzerdefinierte Eigenschaften der Transformation zum Sortieren  
 Die Transformation zum Sortieren verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation zum Sortieren. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|EliminateDuplicates|Boolean|Gibt an, ob die Transformation doppelte Zeilen aus der Transformationsausgabe entfernt. Der Standardwert dieser Eigenschaft ist **False**.|  
|MaximumThreads|Integer|Enthält die maximale Anzahl an Threads, die die Transformation zum Sortieren verwenden kann. Der Wert **0** gibt eine unendliche Anzahl an Threads an. Der Standardwert dieser Eigenschaft ist **0**.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation zum Sortieren. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|NewComparisonFlags|Ganze Zahl (Bitmaske)|Ein Wert, der angibt, wie die Transformation die Zeichenfolgendaten in einer Spalte vergleicht. Weitere Informationen finden Sie unter [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|NewSortKeyPosition|Integer|Ein Wert, der die Sortierreihenfolge der Spalte angibt. Der Wert 0 gibt an, dass die Daten in dieser Spalte nicht sortiert werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation zum Sortieren. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|SortColumnID|Integer|Die **LineageID** einer Sortierspalte.|  
  
 Die Eingabe und die Ausgabe der Transformation zum Sortieren verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Sort Transformation](../../../integration-services/data-flow/transformations/sort-transformation.md).  
  
##  <a name="textract"></a> Benutzerdefinierte Eigenschaften der Transformation für Ausdrucksextrahierung  
 Die Transformation für Ausdrucksextrahierung verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Ausdrucksextrahierung. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|--------------|-----------------|  
|FrequencyThreshold|Integer|Ein numerischer Wert, der angibt, wie oft ein Ausdruck auftreten muss, bevor er extrahiert wird. Der Standardwert dieser Eigenschaft ist **2**.|  
|IsCaseSensitive|Boolean|Ein Wert, der angibt, ob beim Extrahieren von Nomen und nominalen Ausdrücken die Groß-/Kleinschreibung berücksichtigt wird. Der Standardwert dieser Eigenschaft ist **False**.|  
|MaxLengthOfTerm|Integer|Ein numerischer Wert, der die maximale Länge eines Ausdrucks angibt. Diese Eigenschaft bezieht sich nur auf Ausdrücke. Der Standardwert dieser Eigenschaft ist **12**.|  
|NeedRefenceData|Boolean|Ein Wert, der angibt, ob die Transformation eine in einer Verweistabelle gespeicherte Liste mit Ausschlussausdrücken verwendet. Der Standardwert dieser Eigenschaft ist **False**.|  
|OutTermColumn|Zeichenfolge|Der Name der Spalte, die die Ausschlussausdrücke enthält.|  
|OutTermTable|Zeichenfolge|Der Name der Tabelle, die die Spalte mit Ausschlussausdrücken enthält.|  
|ScoreType|Integer|Ein Wert, der den Ergebnistyp angibt, der dem Ausdruck zugeordnet werden soll. Gültige Werte sind 0 für Häufigkeit und 1 für ein TFIDF-Ergebnis. Das TFIDF-Ergebnis ist das Produkt von Ausdruckshäufigkeit und umgekehrter Dokumenthäufigkeit, definiert als: TFIDF des Ausdrucks T = (Häufigkeit von T) \* log( (Anz. Zeilen in der Eingabe) / (Anz. Zeilen mit T) ). Der Standardwert dieser Eigenschaft ist **0**.|  
|WordOrPhrase|Integer|Ein Wert, der den Ausdruckstyp angibt. Die gültigen Werte sind 0 zur Angabe von Wörtern, 1 zur Angabe von nominalen Ausdrücken und 2 zur Angabe von Wörtern und nominalen Ausdrücken. Der Standardwert dieser Eigenschaft ist **0**.|  
  
 Die Eingabe, die Eingabespalten, die Ausgabe und die Ausgabespalten der Transformation für Ausdrucksextrahierung verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md).  
  
##  <a name="tlookup"></a> Benutzerdefinierte Eigenschaften der Transformation für Ausdruckssuche  
 Die Transformation für Ausdruckssuche verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Transformation für Ausdruckssuche. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|IsCaseSensitive|Boolean|Ein Wert, der angibt, ob ein Vergleich mit Beachtung der Groß-/Kleinschreibung auf die Übereinstimmung des Texts in der Eingabespalte und den Suchbegriff angewendet wird. Der Standardwert dieser Eigenschaft ist **False**.|  
|RefTermColumn|Zeichenfolge|Der Name der Spalte, die die Suchausdrücke enthält.|  
|RefTermTable|Zeichenfolge|Der Name der Tabelle, die die Spalte mit Suchausdrücken enthält.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Transformation für Ausdruckssuche. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|InputColumnType|Integer|Ein Wert, der die Verwendung der Spalte angibt. Gültige Werte sind 0 für eine Pass-Through-Spalte, 1 für eine Suchspalte und 2 für eine Spalte, die sowohl eine Pass-Through-Spalte als auch eine Suchspalte ist.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Transformation für Ausdruckssuche. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|CustomLineageID|Integer|Die **LineageID** der entsprechenden Eingabespalte, wenn der **InputColumnType** dieser Spalte 0 oder 2 ist.|  
  
 Die Eingabe und die Ausgabe der Transformation für Ausdruckssuche verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
##  <a name="unpivot"></a> Benutzerdefinierte Eigenschaften der Entpivotierungstransformation  
 Die Entpivotierungstransformation verfügt lediglich über die Eigenschaften, die allen Datenflusskomponenten auf Komponentenebene gemeinsam sind.  
  
> [!NOTE]  
>  In diesem Abschnitt wird die Verwendung der hier beschriebenen Optionen auf der Grundlage des in [Entpivotierungstransformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md) beschriebenen Entpivotierungsszenarios veranschaulicht.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Eingabespalten der Entpivotierungstransformation. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|DestinationColumn|Integer|Die **LineageID** der Ausgabespalte, der die Eingabespalte zugeordnet wird. Ein Wert von -1 gibt an, dass die Eingabespalte keiner Ausgabespalte zugeordnet wird.|  
|PivotKeyValue|Zeichenfolge|Ein Wert, der in eine Transformationsausgabespalte kopiert wird.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.<br /><br /> In dem in [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)beschriebenen Entpivotierungsszenario sind die Pivotwerte die Textwerte Ham, Coke, Milk, Beer und Chips. Diese werden in der neuen Produktspalte, die durch die **Name der Pivotschlüsselwert-Spalte** -Option festgelegt wird, als Textwerte angezeigt.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabespalten der Entpivotierungstransformation. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|PivotKey|Boolean|Gibt an, ob die Werte in der **PivotKeyValue** -Eigenschaft von Eingabespalten in diese Ausgabespalte geschrieben werden.<br /><br /> In dem in [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)beschriebenen Entpivotierungsszenario lautete der Name der Pivotwertspalte **Product** und bezieht sich auf die neue **Product** -Spalte, in der die Pivotierung der Spalten Ham, Coke, Milk, Beer und Chips aufgehoben wird.|  
  
 Die Eingabe und die Ausgabe der Entpivotierungstransformation verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)   
 [Pfadeigenschaften](http://msdn.microsoft.com/library/89b1e347-9579-4f6b-af74-c6519ea08eea)   
 [Data Flow-Eigenschaften, die mithilfe von Ausdrücken festgelegt werden können](http://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)  
  
  
