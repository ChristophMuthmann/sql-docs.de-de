---
title: "Transformation für Fuzzygruppierung | Microsoft Docs"
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
- sql13.dts.designer.fuzzygroupingtrans.f1
- sql13.dts.designer.fuzzygroupingtransformation.connection.f1
- sql13.dts.designer.fuzzygroupingtransformation.columns.f1
- sql13.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 6fceec90818b05ae23c04f90cff8f68c8c7c3c42
ms.contentlocale: de-de
ms.lasthandoff: 08/19/2017

---
# <a name="fuzzy-grouping-transformation"></a>Transformation für Fuzzygruppierung
  Die Transformation für Fuzzygruppierung führt Datenbereinigungsaufgaben durch, indem Datenzeilen identifiziert werden, die wahrscheinlich Duplikate sind, und eine kanonische Datenzeile ausgewählt wird, die zum Standardisieren der Daten verwendet wird.  
  
> [!NOTE]  
>  Ausführliche Informationen zu den Transformationen für Fuzzygruppierung wie Leistungs- und Speicherbeschränkungen finden Sie im Whitepaper [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604)(Fuzzysuche und Fuzzygruppierungen in SQL Server Integration Services 2005).  
  
 Für die Transformation der Fuzzygruppierung ist eine Verbindung zu einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erforderlich, damit die temporären [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Tabellen erstellt werden können, die der Transformationsalgorithmus zur Durchführung benötigt. Die Verbindung muss für einen Benutzer aufgelöst sein, der die Berechtigung zum Erstellen von Tabellen in der Datenbank besitzt.  
  
 Um die Transformation zu konfigurieren, müssen Sie die Eingabespalten auswählen, die zum Identifizieren von Duplikaten verwendet werden sollen, und Sie müssen für jede Spalte den Typ der Übereinstimmung auswählen – entweder fuzzy oder genau. Mit einer genauen Übereinstimmung wird garantiert, dass nur Zeilen mit identischen Werten in dieser Spalte gruppiert werden. Die genaue Übereinstimmung kann für Spalten aller [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Datentypen verwendet werden, mit Ausnahme von DT_TEXT, DT_NTEXT und DT_IMAGE. Bei der Fuzzyübereinstimmung werden Zeilen gruppiert, die annähernd dieselben Werte aufweisen. Die Methode zur Ermittlung der annähernden Übereinstimmung von Daten basiert auf einem vom Benutzer angegebenen Ähnlichkeitsergebnis. Zur Fuzzyübereinstimmung können nur Spalten mit den Datentypen DT_WSTR und DT_STR verwendet werden. Weitere Informationen finden Sie unter [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Die Transformationsausgabe umfasst alle Eingabespalten, eine oder mehrere Spalten mit standardisierten Daten sowie eine Spalte, die das Ähnlichkeitsergebnis enthält. Das Ergebnis ist ein Dezimalwert zwischen 0 und 1. Die kanonische Zeile weist ein Ergebnis von 1 auf. Andere Zeilen in der Fuzzygruppierung weisen Ergebnisse auf, die angeben, wie stark die Zeile mit der kanonischen Zeile übereinstimmt. Je näher das Ergebnis an 1 liegt, desto genauer stimmt die Zeile mit der kanonischen Zeile überein. Wenn die Fuzzygruppierung Zeilen enthält, die genaue Duplikate der kanonischen Zeile sind, besitzen diese Zeilen ebenfalls das Ergebnis 1. Die Transformation entfernt doppelte Zeilen nicht, sondern gruppiert diese, indem ein Schlüssel erstellt wird, der die kanonische Zeile in Bezug zu ähnlichen Zeilen stellt.  
  
 Die Transformation produziert eine Ausgabezeile für jede Eingabezeile sowie die folgenden zusätzlichen Spalten:  
  
-   **_key_in**, eine Spalte, mit der jede Zeile eindeutig identifiziert wird.  
  
-   **_key_out**, eine Spalte, mit der eine Gruppe von doppelten Zeilen identifiziert wird. Die **_key_out** -Spalte, die den Wert der **_key_in** -Spalte in der kanonischen Datenzeile enthält. Zeilen mit demselben Wert in **_key_out** gehören zur selben Gruppe. Der Wert **_key_out**für eine Gruppe entspricht dem Wert von **_key_in** in der kanonischen Datenzeile.  
  
-   **_score**, ein Wert zwischen 0 und 1, der die Ähnlichkeit der Eingabezeile gegenüber der kanonischen Zeile angibt.  
  
 Dies sind die Standardspaltennamen; Sie können die Transformation für Fuzzygruppierung auch so konfigurieren, dass dabei andere Spaltennamen verwendet werden. Die Ausgabe enthält auch ein Ähnlichkeitsergebnis für jede Spalte, die an einer Fuzzygruppierung beteiligt ist.  
  
 Die Transformation für Fuzzygruppierung enthält zwei Funktionen, mit denen sich die bei der Transformation durchgeführte Gruppierung anpassen lässt: Token-Trennzeichen und den Schwellenwert für Ähnlichkeit. Die Transformation bietet eine Reihe von Standardtrennzeichen für die Tokenisierung der Daten, Sie können jedoch auch neue Trennzeichen hinzufügen, mit denen sich die Tokenisierung Ihrer Daten weiter verbessern lässt.  
  
 Der Schwellenwert für Ähnlichkeit gibt an, wie strikt die Transformation bei der Erkennung von Duplikaten vorgeht. Die Schwellenwerte für Ähnlichkeit können auf der Komponentenebene und auf der Spaltenebene festgelegt werden. Der Schwellenwert für Ähnlichkeit auf der Spaltenebene ist nur für Spalten verfügbar, die eine Fuzzyübereinstimmung durchführen. Der Ähnlichkeitsbereich liegt zwischen 0 und 1. Je näher der Schwellenwert an 1 liegt, desto mehr müssen sich die Zeilen und Spalten ähneln, um als Duplikate gewertet zu werden. Sie geben den Schwellenwert für Ähnlichkeit für Zeilen und Spalten an, indem Sie die MinSimilarity-Eigenschaft auf Komponentenebene und auf Spaltenebene festlegen. Um der auf der Komponentenebene angegebenen Ähnlichkeit gerecht zu werden, müssen alle Zeilen über alle Spalten eine Ähnlichkeit haben, die größer oder gleich dem Schwellenwert für Ähnlichkeit ist, der auf der Komponentenebene angegeben ist.  
  
 Die Transformation für Fuzzygruppierung berechnet interne Measures der Ähnlichkeit, und Zeilen, die weniger ähnlich sind als der Wert, der in MinSimilarity angegeben ist, werden nicht gruppiert.  
  
 Zum Identifizieren eines Schwellenwerts für Ähnlichkeit, der für Ihre Daten geeignet ist, müssen Sie eventuell die Transformation für Fuzzygruppierung mehrfach anwenden und dabei unterschiedliche minimale Schwellenwerte für Ähnlichkeit verwenden. Zur Laufzeit enthalten die Ergebnisspalten in der Transformationsausgabe die Ähnlichkeitsergebnisse für jede Zeile in einer Gruppe. Sie können diese Werte verwenden, um den Schwellenwert der Ähnlichkeit zu identifizieren, der für Ihre Daten geeignet ist. Wenn Sie die Ähnlichkeit erhöhen möchten, müssen Sie MinSimilarity auf einen Wert festlegen, der größer ist als der Wert in den Ergebnisspalten.  
  
 Sie können die von der Transformation durchgeführte Gruppierung anpassen, indem Sie die Eigenschaften der Spalten in der Eingabe der Transformation für Fuzzygruppierung festlegen. So gibt z.B. die FuzzyComparisonFlags-Eigenschaft an, wie die Transformation die Zeichenfolgendaten in einer Spalte vergleicht, und die ExactFuzzy-Eigenschaft gibt an, ob die Transformation eine Fuzzyübereinstimmung oder eine genaue Übereinstimmung verwendet.  
  
 Der von der Transformation für Fuzzygruppierungen verwendete Arbeitsspeicher kann durch Festlegen der benutzerdefinierten Eigenschaft MaxMemoryUsage konfiguriert werden. Sie können die Größe in Megabyte (MB) angeben oder den Wert 0 verwenden, um für die Transformation die Verwendung einer dynamischen Arbeitsspeichermenge auf Basis der Anforderungen und des verfügbaren physischen Speichers zuzulassen. Die benutzerdefinierte MaxMemoryUsage-Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist je eine Eingabe und eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## <a name="row-comparison"></a>Zeilenvergleich  
 Wenn Sie die Transformation für Fuzzygruppierung konfigurieren, können Sie den Vergleichsalgorithmus angeben, den die Transformation zum Vergleichen der Zeilen in der Transformationseingabe verwendet. Wenn Sie die Exhaustive-Eigenschaft auf **TRUE**festlegen, vergleicht die Transformation jede Zeile in der Eingabe mit jeder anderen Zeile in der Eingabe. Dieser Vergleichsalgorithmus kann zwar präzisere Ergebnisse produzieren, führt jedoch wahrscheinlich zu einer Einschränkung der Transformationsleistung, sofern die Anzahl der Zeilen in der Eingabe nicht gering ist. Um Leistungsprobleme zu vermeiden, wird empfohlen, die Exhaustive-Eigenschaft nur während der Paketentwicklung auf **TRUE** festzulegen.  
  
## <a name="temporary-tables-and-indexes"></a>Temporäre Tabellen und Indizes  
 Zur Laufzeit erstellt die Transformation für Fuzzygruppierung temporäre Objekte wie z. B. Tabellen und Indizes mit potenziell erheblicher Größe in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank, zu der die Transformation eine Verbindung herstellt. Die Größe der Tabellen und Indizes ist proportional zur Anzahl der Zeilen in der Transformationseingabe und zur Anzahl der von der Transformation für Fuzzygruppierung erstellten Token.  
  
 Die Transformation fragt auch die temporären Tabellen ab. Deshalb sollten Sie in Erwägung ziehen, die Transformation für Fuzzygruppierung eine Verbindung mit einer Nichtproduktionsinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]herstellen zu lassen, insbesondere wenn auf dem Produktionsserver nur eingeschränkt Speicherplatz verfügbar ist.  
  
 Die Leistung dieser Transformation kann verbessert werden, wenn sich die dabei verwendeten Tabellen und Indizes auf dem lokalen Computer befinden.  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>Konfiguration der Transformation für Fuzzygruppierung  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen der Eigenschaften dieses Tasks anzuzeigen:  
  
-   [Identifizieren ähnlicher Datenzeilen mithilfe der Transformation für Fuzzygruppierung](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>Transformations-Editor für Fuzzygruppierung (Registerkarte Verbindungs-Manager)
  Mithilfe der Registerkarte **Verbindungs-Manager** des Dialogfelds **Transformations-Editor für Fuzzygruppierung** können Sie eine vorhandene Verbindung auswählen oder eine neue erstellen.  
  
> [!NOTE]  
>  Auf dem von der Verbindung angegebenen Server muss [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ausgeführt werden. Die Transformation für Fuzzygruppierung erstellt temporäre Datenobjekte in tempdb, die so groß sein können wie die gesamte Eingabe der Transformation. Während die Transformation ausgeführt wird, werden Abfragen für diese temporären Objekte ausgegeben. Dadurch kann die Gesamtleistung des Servers beeinträchtigt werden.  
  
### <a name="options"></a>enthalten  
 **OLE DB-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen OLE DB-Verbindungs-Manager aus dem Listenfeld aus, oder erstellen Sie mithilfe der Schaltfläche **Neu** eine neue Verbindung.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** eine neue Verbindung.  
  
## <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>Transformations-Editor für Fuzzygruppierung (Registerkarte Spalten)
  Mithilfe der Registerkarte **Spalten** des Dialogfelds **Transformations-Editor für Fuzzygruppierung** können Sie die Spalten angeben, die zum Gruppieren von Zeilen mit doppelten Werten verwendet werden sollen.  
  
### <a name="options"></a>enthalten  
 **Verfügbare Eingabespalten**  
 Wählen Sie aus dieser Liste die Eingabespalten, mit denen Zeilen mit doppelten Werten gruppiert werden sollen.  
  
 **Name**  
 Zeigt die Namen der verfügbaren Eingabespalten an.  
  
 **Pass-Through**  
 Wählen Sie aus, ob die Eingabespalte in der Ausgabe der Transformation eingeschlossen sein soll. Alle für die Gruppierung verwendeten Spalten werden automatisch in die Ausgabe kopiert. Sie können weitere Spalten einschließen, indem Sie diese Spalten auswählen.  
  
 **Eingabespalte**  
 Wählen Sie eine der zu einem früheren Zeitpunkt aus der Liste **Verfügbare Eingabespalten** ausgewählten Eingabespalten aus.  
  
 **Ausgabealias**  
 Geben Sie einen beschreibenden Namen für die entsprechende Ausgabespalte ein. Standardmäßig stimmt der Name der Ausgabespalte mit dem Namen der Eingabespalte überein.  
  
 **Gruppenausgabealias**  
 Geben Sie einen beschreibenden Namen für die Spalte ein, die den kanonischen Wert für die gruppierten Duplikate enthalten soll. Der Standardname dieser Ausgabespalte entspricht dem Namen der Eingabespalte mit dem Anhang _clean.  
  
 **Übereinstimmungstyp**  
 Wählen Sie genaue oder Fuzzyübereinstimmungen aus. Zeilen werden als Duplikate angesehen, wenn Sie über alle Spalten hinweg eine genügend große Ähnlichkeit mit dem Typ einer Fuzzyübereinstimmung haben. Wenn Sie für bestimmte Spalten auch die genaue Übereinstimmung angeben, werden in den Spalten mit den genauen Übereinstimmungen nur Zeilen mit identischen Werten als mögliche Duplikate angesehen. Wenn Sie also wissen, dass eine bestimmte Spalte keine Fehler oder Inkonsistenzen enthält, können Sie für diese Spalte die genaue Übereinstimmung angeben, um die Genauigkeit der Fuzzyübereinstimmungen für andere Spalten zu erhöhen.  
  
 **Minimale Ähnlichkeit**  
 Legen Sie mithilfe des Schiebereglers den Schwellenwert für Ähnlichkeit auf Joinebene fest. Je näher der Wert an 1 liegt, desto stärker muss die Ähnlichkeit zwischen Suchwert und Quellwert sein, um als Übereinstimmung zu gelten. Durch eine Erhöhung des Schwellenwertes kann die Geschwindigkeit beim Abgleich erhöht werden, weil als Kandidaten dann weniger Datensätze berücksichtigt werden müssen.  
  
 **Ähnlichkeitsausgabealias**  
 Geben Sie den Namen für eine Ausgabespalte an, die die Ähnlichkeitsergebnisse für den ausgewählten Join enthält. Wenn Sie diesen Wert nicht angeben, wird die Ausgabespalte nicht erstellt.  
  
 **Zahlen**  
 Gibt die Bedeutung führender und nachfolgender Zahlen beim Vergleichen der Spaltendaten an. Wenn beispielsweise führende Zahlen von Bedeutung sind, wird "123 Main Street" nicht mit "456 Main Street" gruppiert.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Neither**|Weder führende noch nachfolgende Zahlen sind von Bedeutung.|  
|**Leading**|Nur führende Zahlen sind von Bedeutung.|  
|**Trailing**|Nur nachfolgende Zahlen sind von Bedeutung.|  
|**LeadingAndTrailing**|Sowohl führende als auch nachfolgende Zahlen sind von Bedeutung.|  
  
 **Vergleichsflags**  
 Weitere Informationen zu den Optionen für das Vergleichen von Zeichenfolgen finden Sie unter [Vergleichen von Zeichenfolgendaten](../../../integration-services/data-flow/comparing-string-data.md).  
  
## <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>Transformations-Editor für Fuzzygruppierung (Registerkarte Erweitert)
  Geben Sie mithilfe der Registerkarte **Erweitert** von **Transformations-Editor für Fuzzygruppierung** die Ein- und Ausgabespalten an, legen Sie Schwellenwerte für die Ähnlichkeit fest, und definieren Sie Begrenzungszeichen.  
  
> [!NOTE]  
>  Die **Exhaustive** - und **MaxMemoryUsage** -Eigenschaften der Transformation für Fuzzgruppierung sind im **Transformations-Editor für Fuzzygruppierung**nicht verfügbar, können jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Transformation für Fuzzgruppierung von [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
### <a name="options"></a>enthalten  
 **Name der Eingabeschlüsselspalte**  
 Geben Sie den Namen einer Ausgabespalte an, die den eindeutigen Bezeichner für jede Eingabezeile enthält. Die **_key_in** -Spalte enthält einen für jede Zeile eindeutigen Wert.  
  
 **Name der Ausgabeschlüsselspalte**  
 Geben Sie den Namen einer Ausgabespalte an, die den eindeutigen Bezeichner für die kanonische Zeile einer Gruppe doppelter Zeilen enthält. Die **_key_out** -Spalte entspricht dem **_key_in** -Wert der kanonischen Datenzeile.  
  
 **Name der Ähnlichkeitsergebnisspalte**  
 Geben Sie einen Namen für die Spalte an, die das Ähnlichkeitsergebnis enthält. Das Ähnlichkeitsergebnis ist ein Wert zwischen 0 und 1, der die Ähnlichkeit zwischen der Eingabezeile und der kanonischen Zeile anzeigt. Je näher das Ergebnis an 1 liegt, desto genauer stimmt die Zeile mit der kanonischen Zeile überein.  
  
 **Schwellenwert für Ähnlichkeit**  
 Legen Sie den Schwellenwert für die Ähnlichkeit mithilfe des Schiebereglers fest. Je näher der Schwellenwert an 1 kommt, desto mehr müssen die Zeilen einander ähneln, um als Duplikate angesehen zu werden. Durch eine Erhöhung des Schwellenwertes kann die Geschwindigkeit beim Abgleich erhöht werden, weil als Kandidaten dann weniger Datensätze berücksichtigt werden müssen.  
  
 **Tokentrennzeichen**  
 Die Transformation bietet einen Standardsatz von Trennzeichen, um Daten mit Tokens zu versehen. Sie können durch Bearbeiten der Liste aber ggf. Trennzeichen hinzufügen oder entfernen.  
  
## <a name="see-also"></a>Siehe auch  
 [Transformation für Fuzzysuche](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
