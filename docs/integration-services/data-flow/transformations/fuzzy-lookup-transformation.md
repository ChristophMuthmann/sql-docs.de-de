---
title: "Transformation für Fuzzysuche | Microsoft Docs"
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
- sql13.dts.designer.fuzzylookuptrans.f1
- sql13.dts.designer.fuzzylookuptransformation.referencetable.f1
- sql13.dts.designer.fuzzylookuptransformation.columns.f1
- sql13.dts.designer.fuzzylookuptransformation.advanced.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- temporary tables [Integration Services]
- Fuzzy Lookup transformation
- reference tables [Integration Services]
- match similar data [Integration Services]
- replacing missing values
- correcting data [Integration Services]
- cache [Integration Services]
- standardizing data [Integration Services]
- lookups [Integration Services]
- confidence scores [Integration Services]
- fuzzy matches
- missing values replaced [Integration Services]
- similarity thresholds [Integration Services]
ms.assetid: 019db426-3de2-4ca9-8667-79fd9a47a068
caps.latest.revision: 75
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: ff5f003749572b16e750b5940cd0f05b0b879fda
ms.contentlocale: de-de
ms.lasthandoff: 08/19/2017

---
# <a name="fuzzy-lookup-transformation"></a>Transformation für Fuzzysuche
  Die Transformation für Fuzzysuche führt Aufgaben zum Datencleanup durch, wie das Standardisieren von Daten, das Korrigieren von Daten und das Bereitstellen fehlender Werte.  
  
> [!NOTE]  
>  Ausführliche Informationen über die Transformationen für Fuzzysuche wie Leistungs- und Speicherbeschränkungen finden Sie im Whitepaper [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604)(Fuzzysuche und Fuzzygruppierung in SQL Server Integration Services 2005).  
  
 Die Transformation für Fuzzysuche weicht in ihrer Verwendung der Fuzzyübereinstimmung von der Transformation für Suche ab. Die Transformation für Suche verwendet einen Gleichheitsjoin zum Suchen von übereinstimmenden Datensätzen in der Verweistabelle. Sie gibt Datensätze mit mindestens einem übereinstimmendem Datensatz Datensätze ohne übereinstimmende Datensätze zurück. Im Gegensatz dazu verwendet die Transformation für Fuzzysuche die Fuzzyübereinstimmung, um mindestens eine nahe Übereinstimmung in der Verweistabelle zurückzugeben.  
  
 Eine Transformation für Fuzzysuche folgt häufig einer Transformation für Suche in einem Paketdatenfluss. Zunächst versucht die Transformation für Suche, eine genaue Übereinstimmung zu finden. Falls dies fehlschlägt, bietet die Transformation für Fuzzysuche nahe Übereinstimmungen aus der Verweistabelle.  
  
 Die Transformation benötigt Zugriff auf eine Verweisdatenquelle, die die Werte enthält, die zum Bereinigen und Erweitern der Eingabedaten verwendet werden. Bei der Verweisdatenquelle muss es sich um eine Tabelle in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank handeln. Bei der Übereinstimmung zwischen dem Wert in einer Eingabespalte und dem Wert in der Verweistabelle kann es sich um eine genaue Übereinstimmung oder eine Fuzzyübereinstimmung handeln. Für die Transformation ist jedoch mindestens eine Spaltenübereinstimmung erforderlich, die für die Fuzzyübereinstimmung konfiguriert wird. Wenn Sie nur eine genaue Übereinstimmung verwenden möchten, verwenden Sie stattdessen die Transformation für Suche.  
  
 Diese Transformation weist je eine Eingabe und eine Ausgabe auf.  
  
 Für die Fuzzyübereinstimmung können nur Spalten mit den Datentypen **DT_WSTR** und **DT_STR** verwendet werden. Die genaue Übereinstimmung kann Spalten aller DTS-Datentypen verwendet, mit Ausnahme von **DT_TEXT**, **DT_NTEXT**und **DT_IMAGE**. Weitere Informationen finden Sie unter [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md). Spalten, die einen Join zwischen der Eingabe- und der Verweistabelle aufweisen, müssen kompatible Datentypen enthalten. So ist beispielsweise das Verknüpfen einer Spalte mit dem DTS-Datentyp **DT_WSTR** mit einer Spalte mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **nvarchar** gültig, das Verknüpfen einer Spalte mit dem **DT_WSTR** mit einer Spalte mit dem **int** -Datentyp ist jedoch ungültig.  
  
 Sie können diese Transformation anpassen, indem Sie den maximalen Umfang des Arbeitsspeichers, den Zeilenvergleichsalgorithmus sowie den Zwischenspeicher für Indizes und Verweistabellen, die von der Transformation verwendet werden, angeben.  
  
 Der von der Transformation für Fuzzysuche verwendete Arbeitsspeicher kann durch Festlegen der benutzerdefinierten Eigenschaft MaxMemoryUsage konfiguriert werden. Sie können die Größe in Megabyte (MB) angeben oder den Wert 0 verwenden, um bei der Transformation eine dynamische Arbeitsspeichermenge auf Basis der Anforderungen und des verfügbaren physischen Speichers zu verwenden. Die benutzerdefinierte Eigenschaft MaxMemoryUsage kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## <a name="controlling-fuzzy-matching-behavior"></a>Steuern des Verhaltens der Fuzzyübereinstimmung  
 Die Transformation für Fuzzysuche umfasst drei Funktionen zum Anpassen der durchgeführten Suche: maximale Suche nach Übereinstimmungen, die pro Eingabezeile zurückgegeben werden, Token-Trennzeichen und Schwellenwerte für Ähnlichkeit.  
  
 Die Transformation gibt null oder mehr Übereinstimmungen bis zur angegebenen Anzahl an Übereinstimmungen zurück. Die Angabe einer maximalen Anzahl an Übereinstimmungen stellt nicht sicher, dass die Transformation die maximale Anzahl an Übereinstimmungen zurückgibt. Es wird lediglich sichergestellt, dass die Transformation maximal diese Anzahl an Überseinstimmungen zurückgibt. Wenn Sie die maximale Anzahl an Übereinstimmungen auf einen Wert größer als 1 festlegen, kann die Ausgabe der Transformation eventuell mehr als eine Zeile pro Suche enthalten, und bei einigen Zeilen kann es sich um Duplikate handeln.  
  
 Die Transformation bietet eine Reihe von Standardtrennzeichen zur Zerlegung der Daten in Token. Sie können jedoch auch Token-Trennzeichen hinzufügen, mit denen sich die Zerlegung Ihrer Daten in Token weiter verbessern lässt. Die Delimiters-Eigenschaft enthält die Standardtrennzeichen. Die Tokenisierung ist wichtig, da die Einheiten innerhalb der Daten definiert werden, die miteinander verglichen werden.  
  
 Die Schwellenwerte für Ähnlichkeit können auf der Komponenten- und Joinebene festgelegt werden. Der Schwellenwert für Ähnlichkeit auf Joinebene steht nur zur Verfügung, wenn die Transformation eine Fuzzyübereinstimmung zwischen den Spalten in der Eingabe- und der Verweistabelle durchführt. Der Ähnlichkeitsbereich liegt zwischen 0 und 1. Je näher der Schwellenwert an 1 liegt, desto mehr müssen sich die Zeilen und Spalten ähneln, um als Duplikate gewertet zu werden. Sie geben den Schwellenwert für Ähnlichkeit an, indem Sie die MinSimilarity-Eigenschaft auf den Komponenten- und Joinebenen festlegen. Um der auf der Komponentenebene angegebenen Ähnlichkeit gerecht zu werden, müssen alle Zeilen über alle Übereinstimmungen hinweg eine Ähnlichkeit haben, die größer oder gleich dem Schwellenwert für Ähnlichkeit ist, der auf der Komponentenebene angegeben ist. Sie können also auf der Komponentenebene keine sehr nahe Übereinstimmung angeben, es sei denn, die Übereinstimmungen auf der Zeilen- oder Joinebene sind gleich nah.  
  
 Jede Übereinstimmung umfasst ein Ähnlichkeits- und ein Vertrauensergebnis. Das Ähnlichkeitsergebnis ist ein mathematisches Maß der strukturellen Ähnlichkeit zwischen dem Eingabedatensatz und dem Datensatz, der von der Transformation für Fuzzysuche aus der Verweistabelle zurückgegeben wird. Das Vertrauensergebnis ist ein Maß der Wahrscheinlichkeit, mit der ein bestimmter Wert die beste Übereinstimmung zwischen den in der Verweistabelle gefundenen Übereinstimmungen darstellt. Das einem Datensatz zugewiesene Vertrauensergebnis richtet sich nach den anderen zurückgegebenen übereinstimmenden Datensätzen. So gibt z. B. *St.* und *Saint* unabhängig von anderen Übereinstimmungen ein niedriges Ähnlichkeitsergebnis zurück. Wenn es sich bei *Saint* um die einzige zurückgegebene Übereinstimmung handelt, ist das Vertrauensergebnis hoch. Wenn sowohl *Saint* als auch *St.* in der Verweistabelle enthalten sind, ist das Vertrauen in *St.* hoch und das Vertrauen in *Saint* niedrig. Hohe Ähnlichkeit bedeutet aber nicht notwendigerweise hohes Vertrauen. Wenn Sie z. B. den Wert *Chapter 4*suchen, haben die zurückgegebenen Ergebnisse *Chapter 1*, *Chapter 2*und *Chapter 3* ein hohes Ähnlichkeitsergebnis, aber ein niedriges Vertrauensergebnis, da es unklar ist, welches der Ergebnisse die beste Übereinstimmung ist.  
  
 Das Ähnlichkeitsergebnis wird anhand eines Dezimalwerts zwischen 0 und 1 dargestellt, wobei ein Ähnlichkeitsergebnis von 1 eine genaue Übereinstimmung zwischen dem Wert in der Eingabespalte und dem Wert in der Verweistabelle bedeutet. Das Vertrauensergebnis, auch ein Dezimalwert zwischen 0 und 1, gibt das Vertrauen der Übereinstimmung an. Wenn keine verwendbare Übereinstimmung gefunden wird, werden der Zeile Ähnlichkeits- und Vertrauensergebnisse von 0 zugewiesen, und die aus der Verweistabelle kopierten Ausgabespalten enthalten Nullwerte.  
  
 Manchmal findet die Fuzzysuche eventuell keine entsprechenden Übereinstimmungen in der Verweistabelle. Dies kann vorkommen, wenn es sich bei dem für eine Suche verwendeten Eingabewert um ein einzelnes, kurzes Wort handelt. Beispielsweise wird in einer Verweistabelle *helo* nicht dem Wert *hello* zugewiesen, wenn keine anderen Token in dieser Spalte oder einer anderen Spalte in der Zeile vorhanden sind.  
  
 Die Transformationsausgabespalten enthalten die Eingabespalten, die als Pass-Through-Spalten markiert sind, die ausgewählten Spalten in der Suchtabelle und die folgenden zusätzlichen Spalten:  
  
-   **_Similarity**, eine Spalte, die die Ähnlichkeit zwischen den Werten in den Eingabe- und Verweisspalten beschreibt.  
  
-   **_Confidence**, eine Spalte, die die Qualität der Übereinstimmung beschreibt.  
  
 Die Transformation verwendet die Verbindung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank, um die temporären Tabellen zu erstellen, die vom Fuzzyübereinstimmungsalgorithmus verwendet werden.  
  
## <a name="running-the-fuzzy-lookup-transformation"></a>Ausführen der Transformation für Fuzzysuche  
 Wenn das Paket die Transformation zum ersten Mal ausführt, wird die Verweistabelle kopiert, ein Schlüssel mit einem ganzzahligen Datentyp der neuen Tabelle hinzugefügt und ein Index für die Schlüsselspalte erstellt. Im nächsten Schritt der Transformation wird ein Index, ein so genannter Übereinstimmungsindex, für die Kopie der Verweistabelle generiert. Im Übereinstimmungsindex werden die Ergebnisse der Tokenzerlegung in den Transformationseingabespalten gespeichert, und die Transformation verwendet dann die Token für den Suchvorgang. Der Übereinstimmungsindex ist eine Tabelle in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank.  
  
 Wenn das Paket erneut ausgeführt wird, kann von der Transformation entweder ein bereits vorhandener Übereinstimmungsindex verwendet werden oder ein neuer Index erstellt werden. Bei einer statischen Verweistabelle kann der möglicherweise kostspielige Vorgang der erneuten Indexgenerierung für wiederholte Datencleanupsitzungen vermieden werden. Wenn Sie einen bereits vorhandenen Index verwenden möchten, wird der Index bei der ersten Paketausführung erstellt. Wenn mehrere Transformationen für Fuzzysuche dieselbe Verweistabelle verwenden, können alle denselben Index verwenden. Um den Index erneut zu verwenden, müssen die Suchvorgänge identisch sein; die Suche muss dieselben Spalten verwenden. Sie können den Index benennen und die Verbindung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank auswählen, in der der Index gespeichert ist.  
  
 Wenn bei der Transformation der Übereinstimmungsindex gespeichert wird, kann dieser automatisch verwaltet werden. Dies bedeutet, dass bei jedem Update eines Datensatzes in der Verweistabelle auch der Übereinstimmungsindex aktualisiert wird. Die Verwaltung des Übereinstimmungsindexes kann Verarbeitungszeit sparen, da der Index bei Paketausführung nicht neu erstellt werden muss. Sie können angeben, wie der Übereinstimmungsindex von der Transformation verwaltet wird.  
  
 In der folgenden Tabelle werden die Optionen für den Übereinstimmungsindex beschrieben.  
  
|Option|Description|  
|------------|-----------------|  
|**GenerateAndMaintainNewIndex**|Zum Erstellen, Speichern und Verwalten eines neuen Indexes. Bei der Transformation werden Trigger für die Verweistabelle installiert, damit Verweis- und Indextabelle synchronisiert bleiben.|  
|**GenerateAndPersistNewIndex**|Zum Erstellen und Speichern eines Indexes, aber nicht zum Verwalten.|  
|**GenerateNewIndex**|Zum Erstellen eines neuen Indexes, aber nicht zum Speichern.|  
|**ReuseExistingIndex**|Zur erneuten Verwendung eines bereits vorhandenen Indexes.|  
  
### <a name="maintenance-of-the-match-index-table"></a>Verwaltung der Übereinstimmungsindextabelle  
 Mit der Option **GenerateAndMaintainNewIndex** werden Trigger für die Verweistabelle installiert, damit die Übereinstimmungsindextabelle und die Verweistabelle synchronisiert bleiben. Wenn Sie den installierten Trigger entfernen müssen, müssen Sie die gespeicherte **sp_FuzzyLookupTableMaintenanceUnInstall** -Prozedur ausführen und den in der MatchIndexName-Eigenschaft als Eingabeparameterwert festgelegten Namen angeben.  
  
 Sie sollten die verwaltete Übereinstimmungsindextabelle nicht löschen, bevor Sie die gespeicherte **sp_FuzzyLookupTableMaintenanceUnInstall** -Prozedur ausgeführt haben. Falls die Übereinstimmungsindextabelle gelöscht wird, werden die Trigger für die Verweistabelle nicht ordnungsgemäß ausgeführt. Sämtliche nachfolgenden Updates der Verweistabelle schlagen fehl, bis Sie die Trigger für die Verweistabelle manuell löschen.  
  
 Der SQL TRUNCATE TABLE-Befehl ruft keine DELETE-Trigger auf. Wenn für die Verweistabelle der TRUNCATE TABLE-Befehl verwendet wird, werden die Verweistabelle und der Übereinstimmungsindex nicht mehr synchronisiert, und die Transformation für Fuzzysuche schlägt fehl. Während die Trigger, mit denen die Übereinstimmungsindextabelle für die Verweistabelle verwaltet wird, installiert werden, sollten Sie den SQL DELETE- statt des TRUNCATE TABLE-Befehls verwenden.  
  
> [!NOTE]  
>  Wenn Sie **Gespeicherten Index beibehalten** auf der Registerkarte **Verweistabelle** des Dialogfelds **Transformations-Editor für Fuzzysuche**wählen, verwendet die Transformation verwaltete gespeicherte Prozeduren zum Verwalten des Index. Diese verwalteten gespeicherten Prozeduren verwenden die Common Language Runtime-Integrationsfunktion (CLR) in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Standardmäßig ist die CLR-Integration in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht aktiviert. Um die Funktion **Gespeicherten Index beibehalten** zu verwenden, müssen Sie die CLR-Integration aktivieren. Weitere Informationen finden Sie unter [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Da die Option **Gespeicherten Index beibehalten** die CLR-Integration erfordert, kann diese Funktion nur verwendet werden, wenn Sie in einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] eine Verweistabelle auswählen, für die die CLR-Integration aktiviert ist.  
  
## <a name="row-comparison"></a>Zeilenvergleich  
 Wenn Sie die Transformation für Fuzzysuche konfigurieren, können Sie den Vergleichsalgorithmus angeben, den die Transformation für die Suche von übereinstimmenden Datensätzen in der Verweistabelle verwendet. Wenn Sie die Exhaustive-Eigenschaft auf **TRUE**festlegen, vergleicht die Transformation jede Zeile in der Eingabe mit jeder anderen Zeile in der Verweistabelle. Dieser Vergleichsalgorithmus kann zwar präzisere Ergebnisse produzieren, führt jedoch wahrscheinlich zu einer Einschränkung der Transformationsleistung, sofern die Anzahl der Zeilen in der Verweistabelle nicht gering ist. Wenn die Exhaustive-Eigenschaft auf **TRUE**festgelegt ist, wird die gesamte Verweistabelle in den Arbeitsspeicher geladen. Um Leistungsprobleme zu vermeiden, wird empfohlen, die Exhaustive-Eigenschaft nur während der Paketentwicklung auf **TRUE** festzulegen.  
  
 Wenn die Exhaustive-Eigenschaft auf **FALSE**festgelegt ist, gibt die Transformation für die Fuzzysuche nur übereinstimmende Werte zurück, bei denen mindestens ein indiziertes Token bzw. eine Teilzeichenfolge (die Teilzeichenfolge wird *q-gram*genannt) mit dem Eingabedatensatz übereinstimmt. Zum Maximieren der Sucheffizienz wird in jeder Zeile der Tabelle nur eine Teilmenge der Token in der invertierten Indexstruktur indiziert, die die Transformation für Fuzzysuche zum Suchen von übereinstimmenden Werten verwendet. Wenn das Eingabedataset klein ist, können Sie die Exhaustive-Eigenschaft auf **TRUE** festlegen, um fehlende Übereinstimmungen, für die keine allgemeinen Token in der Indextabelle vorhanden sind, zu vermeiden.  
  
## <a name="caching-of-indexes-and-reference-tables"></a>Zwischenspeichern von Indizes und Verweistabellen  
 Bei der Konfiguration der Transformation für Fuzzysuche können Sie angeben, ob die Transformation den Index und die Verweistabelle teilweise im Arbeitsspeicher zwischenspeichern soll, bevor die Transformation mit der Verarbeitung beginnt. Wenn Sie die WarmCaches-Eigenschaft auf **TRUE**festlegen, werden der Index und die Verweistabelle in den Arbeitsspeicher geladen. Wenn die Eingabe aus vielen Zeilen besteht, kann durch das Festlegen der WarmCaches-Eigenschaft auf **TRUE** die Transformationsleistung verbessert werden. Wenn die Anzahl der Eingabezeilen gering ist, kann durch das Festlegen der WarmCaches-Eigenschaft auf **FALSE** die Wiederverwendung eines großen Indexes schneller sein.  
  
## <a name="temporary-tables-and-indexes"></a>Temporäre Tabellen und Indizes  
 Zur Laufzeit erstellt die Transformation für Fuzzysuche temporäre Objekte, z. B. Tabellen und Indizes, in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank, mit der die Transformation eine Verbindung herstellt. Die Größe dieser temporären Tabellen und Indizes ist proportional zur Anzahl der Zeilen und Token in der Verweistabelle und zur Anzahl der Token, die von der Transformation für Fuzzysuche erstellt werden; deshalb können sie möglicherweise einen großen Teil des Speicherplatzes belegen. Die Transformation fragt auch diese temporären Tabellen ab. Deshalb sollten Sie in Erwägung ziehen, die Transformation für Fuzzysuche eine Verbindung mit einer Nichtproduktionsinstanz einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank herstellen zu lassen, insbesondere wenn auf dem Produktionsserver nur eingeschränkt Speicherplatz verfügbar ist.  
  
 Die Leistung dieser Transformation kann verbessert werden, wenn sich die dabei verwendeten Tabellen und Indizes auf dem lokalen Computer befinden. Wenn sich die Verweistabelle, die von der Transformation für Fuzzysuche verwendet wird, auf dem Produktionsserver befindet, sollten Sie die Tabelle auf einen Nichtproduktionsserver kopieren und die Transformation für Fuzzysuche für den Zugriff auf die Kopie konfigurieren. So können Sie verhindern, dass die Suchabfragen Ressourcen auf dem Produktionsserver verbrauchen. Wenn die Transformation für Fuzzysuche den Übereinstimmungsindex verwaltet, d.h., wenn MatchIndexOption auf **GenerateAndMaintainNewIndex**festgelegt ist, sperrt die Transformation eventuell überdies die Verweistabelle für die Dauer des Datencleanupvorgangs und verhindert, dass andere Benutzer und Anwendungen auf die Tabelle zugreifen.  
  
## <a name="configuring-the-fuzzy-lookup-transformation"></a>Konfigurieren der Transformation für Fuzzysuche  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Weitere Informationen zum Festlegen der Eigenschaften einer Datenflusskomponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>Transformations-Editor für Fuzzysuche (Registerkarte Verweistabelle)
  Auf der Registerkarte **Verweistabelle** des Dialogfelds **Transformations-Editor für Fuzzysuche** können Sie die Quelltabelle und den Index für die Suche angeben. Bei der Verweisdatenquelle muss es sich um eine Tabelle in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank handeln.  
  
> [!NOTE]  
>  Durch die Transformation für die Fuzzysuche wird eine Arbeitskopie der Verweistabelle erstellt. Die nachfolgend beschriebenen Indizes werden für diese Arbeitstabelle mithilfe einer Spezialtabelle erstellt, und nicht mit einem normalen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Index. Durch die Transformation werden die vorhandenen Quelltabellen nicht verändert, sofern Sie nicht **Gespeicherten Index beibehalten**auswählen. In diesem Fall wird ein Trigger für die Verweistabelle erstellt, der die Arbeitstabelle und die Suchindextabelle auf der Grundlage von Änderungen an der Verweistabelle aktualisiert.  
  
> [!NOTE]  
>  Die **Exhaustive** - und **MaxMemoryUsage** -Eigenschaften der Transformation für Fuzzysuche sind im **Transformations-Editor für Fuzzysuche**nicht verfügbar, können jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Darüber hinaus kann ein Wert größer als 100 für **MaxOutputMatchesPerInput** nur im Dialogfeld **Erweiterter Editor**festgelegt werden. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Transformation für Fuzzysuche von [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
### <a name="options"></a>enthalten  
 **OLE DB-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen OLE DB-Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** eine neue Verbindung.  
  
 **Neuen Index generieren**  
 Geben Sie an, dass die Transformation einen neuen Index erstellen soll, der für die Suche verwendet wird.  
  
 **Name der Verweistabelle**  
 Wählen Sie die vorhandene Tabelle aus, die als Verweis-(Such-)Tabelle verwendet werden soll.  
  
 **Neuen Index speichern**  
 Wählen Sie diese Option aus, wenn Sie den neuen Suchindex speichern möchten.  
  
 **Name des neuen Indexes**  
 Wenn Sie den neuen Suchindex speichern möchten, geben Sie einen beschreibenden Namen für den Index ein.  
  
 **Gespeicherten Index beibehalten**  
 Wenn Sie den neuen Suchindex speichern möchten, geben Sie an, ob der Index auch in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] beibehalten werden soll.  
  
> [!NOTE]  
>  Wenn Sie **Gespeicherten Index beibehalten** auf der Registerkarte **Verweistabelle** des Dialogfelds **Transformations-Editor für Fuzzysuche**wählen, verwendet die Transformation verwaltete gespeicherte Prozeduren zum Verwalten des Index. Diese verwalteten gespeicherten Prozeduren verwenden die Common Language Runtime-Integrationsfunktion (CLR) in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Standardmäßig ist die CLR-Integration in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht aktiviert. Um die Funktion **Gespeicherten Index beibehalten** zu verwenden, müssen Sie die CLR-Integration aktivieren. Weitere Informationen finden Sie unter [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Da die Option **Gespeicherten Index beibehalten** die CLR-Integration erfordert, kann diese Funktion nur verwendet werden, wenn Sie in einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] eine Verweistabelle auswählen, für die die CLR-Integration aktiviert ist.  
  
 **Vorhandenen Index verwenden**  
 Gibt an, dass bei der Transformation ein vorhandener Index für die Suche verwendet werden soll.  
  
 **Name eines vorhandenen Indexes**  
 Wählen Sie einen zu einem früheren Zeitpunkt erstellten Index aus der Liste aus.  
  
## <a name="fuzzy-lookup-transformation-editor-columns-tab"></a>Transformations-Editor für Fuzzysuche (Registerkarte Spalten)
  Auf der Registerkarte **Spalten** des Dialogfelds **Transformations-Editor für Fuzzysuche** können Sie die Eigenschaften für die Eingabe- und Ausgabespalten festlegen.  
  
### <a name="options"></a>enthalten  
 **Verfügbare Eingabespalten**  
 Um Eingabespalten mit verfügbaren Suchspalten zu verbinden, ziehen Sie diese auf die Suchspalten. Diese Spalten müssen übereinstimmende, unterstützte Datentypen aufweisen. Wählen Sie eine Zuordnungszeile aus, und klicken Sie mit der rechten Maustaste darauf, um die Zuordnungen im Dialogfeld [Beziehungen erstellen](../../../integration-services/data-flow/transformations/create-relationships.md) zu bearbeiten.  
  
 **Name**  
 Zeigen Sie die Namen der verfügbaren Eingabespalten an.  
  
 **Pass-Through**  
 Geben Sie an, ob die Eingabespalten in der Ausgabe der Transformation eingeschlossen sein sollen.  
  
 **Verfügbare Suchspalten**  
 Wählen Sie mithilfe der Kontrollkästchen die Spalten aus, für die die Fuzzysuchvorgänge ausgeführt werden sollen.  
  
 **Suchspalte**  
 Wählen Sie Suchspalten aus der Liste der verfügbaren Spalten der Verweistabelle aus. Ihre Auswahl wird entsprechend in der Auswahl der Kontrollkästchen in der **Verfügbare Suchspalten** -Tabelle deutlich. Durch das Auswählen einer Spalte in der **Verfügbare Suchspalten** -Tabelle wird eine Ausgabespalte erstellt, die den Spaltenwert der Verweistabelle für jede übereinstimmende Zeile enthält, die zurückgegeben wird.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für die Ausgabe der einzelnen Suchspalten ein. Standardmäßig wird der Name der Suchspalte mit einem angefügten numerischen Indexwert verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
## <a name="fuzzy-lookup-transformation-editor-advanced-tab"></a>Transformations-Editor für Fuzzysuche (Registerkarte Erweitert)
  Auf der Registerkarte **Erweitert** des Dialogfelds **Transformations-Editor für Fuzzysuche** können Sie die Parameter für die Fuzzysuche festlegen.  
  
### <a name="options"></a>enthalten  
 **Maximale Anzahl von Übereinstimmungen, die pro Suche ausgegeben werden**  
 Geben Sie die maximale Anzahl der Übereinstimmungen an, die pro Eingabezeile von der Transformation zurückgegeben werden können. Der Standardwert lautet **1**.  
  
 **Schwellenwert für Ähnlichkeit**  
 Legen Sie mithilfe des Schiebereglers den Schwellenwert für Ähnlichkeit auf Komponentenebene fest. Je näher der Wert an 1 liegt, desto stärker muss die Ähnlichkeit zwischen Suchwert und Quellwert sein, um als Übereinstimmung zu gelten. Durch eine Erhöhung des Schwellenwertes kann die Geschwindigkeit beim Abgleich erhöht werden, weil als Kandidaten dann weniger Datensätze berücksichtigt werden müssen.  
  
 **Tokentrennzeichen**  
 Geben Sie die Trennzeichen an, die von der Transformation verwendet werden, um Spaltenwerte mit Token zu versehen.  
  
## <a name="see-also"></a>Siehe auch  
 [Transformation für Suche](../../../integration-services/data-flow/transformations/lookup-transformation.md)   
 [Transformation für Fuzzygruppierung](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

