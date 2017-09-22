---
title: Was &#39; s neu in SQL Server 2017 Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: eb98483d6237f2db2fdb0cb9aa444dd938a431f0
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="what39s-new-in-sql-server-2017-analysis-services"></a>Was &#39; s neu in SQL Server 2017 Analysis Services
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]


## <a name="sql-server-2017-analysis-services-rc2"></a>SQL Server 2017 Analysis Services RC2
Diese Version enthält keine neuen Funktionen. Verbesserungen in dieser Version enthalten Programmfehlerbehebungen und Leistung.

## <a name="sql-server-2017-analysis-services-rc1"></a>SQL Server 2017 Analysis Services RC1
Es sind keine neuen Funktionen in dieser Version, aber diese Version enthält zusätzliche Verbesserungen an [dynamische Verwaltungssichten](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMVS) für tabellarische Modelle mit Kompatibilitätsgrad 1200 und 1400.

Funktioniert nun DISCOVER_CALC_DEPENDENCY mit tabellarischen 1200 und 1400-Modellen. Tabellenmodelle 1400 anzeigen Abhängigkeiten zwischen M Partitionen, M-Ausdrücke und strukturierte Datenquellen Weitere Informationen finden Sie unter der [Analysis Services-Blog](https://blogs.msdn.microsoft.com/analysisservices/).

MDSCHEMA_MEASUREGROUP_DIMENSIONS-Verbesserungen sind für diese DMV, die von verschiedenen Clienttools verwendet wird, um Measure Dimensionalität anzuzeigen. Beispielsweise kann die Durchsuchen-Funktion in Excel-Pivot-Tabellen der Benutzer Cross-Drilldown zu Dimensionen im Bezug auf die ausgewählten Measures. Diese Version korrigiert die Kardinalität-Spalten, in denen zuvor falsche Werte angezeigt wurden.

## <a name="sql-server-analysis-services-ctp-21"></a>SQL Server Analysis Services der CTP-Version 2.1
Diese Version enthält keine neuen Funktionen. Verbesserungen in dieser Version enthalten, Fehlerkorrekturen und Leistung sowie Verbesserungen [dynamische Verwaltungssichten](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV). DMVs werden Abfragen in SQL Server Profiler, die Informationen zu lokalen Servervorgängen und Serverzustand zurückgeben. Weitere Informationen finden Sie unter der [Analysis Services-Blog](https://blogs.msdn.microsoft.com/analysisservices/).

## <a name="sql-server-analysis-services-ctp-20"></a>SQL Server Analysis Services CTP 2.0
Diese Version enthält zahlreiche neue Verbesserungen für tabellarische Modelle, einschließlich:

* Sicherheit der Objektebene zum Sichern der Metadaten von tabellarischen Modellen.
* Transaktionsleistung Verbesserungen Reaktionsgeschwindigkeit Entwickler zu vereinfachen.
* Verbesserungen des dynamischen Ansicht "Verwaltung" auf 1200 und 1400 Modelle Abhängigkeitsanalyse aktivieren und Berichte.
* Verbesserungen an der Entwicklungs-Erfahrung für Zeilen Detailausdrücken.
* Hierarchie und Spalte wiederverwenden, um in aussagekräftigere Speicherorte in der Liste der Power BI-Feld angefügt werden sollen.
* Datum Beziehungen problemlos Beziehungen zu Datumsdimensionen auf Grundlage von Datumsfeldern zu erstellen.
* Die Standardinstallationsoption für Analysis Services ist jetzt für den Tabellenmodus.
* Neue Daten abrufen (Power Qery) Datenquellen.
* DAX-Editor für SSDT.
* Vorhandene DirectQuery-Datenquellen für M Abfragen unterstützen.
* SSMS-Verbesserungen, z. B. anzeigen, bearbeiten und die Unterstützung der Skripterstellung für strukturierte Datenquellen.

Um weitere Details zu dieser Version CTP 2.0 zu erhalten, finden Sie unter der [Analysis Services-Blog](https://blogs.msdn.microsoft.com/analysisservices/).

## <a name="sql-server-analysis-services-on-windows-ctp-14"></a>SQL Server Analysis Services unter Windows CTP 1.4
[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate) und [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms-release-candidate) Preview-Versionen in der Regel mit SQL Server-2017 Preview-Versionen. Achten Sie darauf, dass Sie das neueste zu verwenden, um neue Funktionen zu erhalten. Weitere Informationen finden Sie unter der [Analysis Services-Blog](https://blogs.msdn.microsoft.com/analysisservices/).



## <a name="sql-server-analysis-services-on-windows-ctp-13"></a>SQL Server Analysis Services unter Windows CTP-Version 1.3

### <a name="encoding-hints"></a>Codierung Hinweise

Diese Version führt Codierung Hinweise, eine erweiterte Funktion, die zur Optimierung der Verarbeitung (Refresh Data) des großen tabellarischen in-Memory-Modellen verwendet. Zum besseren Verständnis Codierung finden Sie unter [Leistung optimieren von tabellarischen Modellen in SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx) in diesem Whitepaper Codierung besser zu verstehen. Die hier beschriebenen Codierungsvorgangs gilt in der CTP-Version 1.3.

* Wertcodierung bietet eine bessere abfrageleistung für Spalten, die in der Regel nur für Aggregationen verwendet werden.

* Hashcodierung wird bevorzugt für Group by-Spalten (häufig Dimensionstabelle Werte) und Fremdschlüssel. Zeichenfolgenspalten sind immer Hash codiert.

Numerische Spalten können mit dieser Codierung Methoden verwenden. Wenn Analysis Services ist entweder die Tabelle leer ist (mit oder ohne Partitionen) startet die Verarbeitung einer Tabelle oder ein vollständigen Tabelle Verarbeitungsvorgang durchgeführt werden, werden Beispiele Werte für jede numerische Spalte zu bestimmen, ob die anzuwendende Wert oder hashcodierung übernommen. . Wertcodierung wird standardmäßig ausgewählt, wenn das Beispiel von unterschiedlichen Werten in der Spalte ist groß genug – andernfalls hashcodierung wird in der Regel bieten eine bessere Komprimierung. Es ist möglich, dass Analysis Services Codierungsmethode ändern, nachdem die Spalte basierend auf Weitere Informationen über die datenverteilung teilweise verarbeitet wird, und starten Sie den Prozess der codieren. Dies natürlich erhöhen die Verarbeitungszeit und ist ineffizient. Im Whitepaper zur Optimierung der Leistung wird die Codierung erneut im Detail erläutert und beschrieben, wie mit SQL Server Profiler erkannt.

Codierung Hinweise in der CTP-Version 1.3 zulassen der Modellierer an eine Einstellung für die angegebene Vorkenntnisse von datenprofilerstellungs und/oder als Antwort auf die erneute Verschlüsselung Ablaufverfolgungsereignisse Codierungsmethode Da Aggregation über Spalten Hash-codierte langsamer ist als über Spalten Wert-codierte wertcodierung als Hinweis für solche Spalten angegeben werden kann. Es ist nicht sichergestellt, dass die Einstellung angewendet werden; Daher ist es ein Hinweis im Gegensatz zu einer Einstellung an. Um eine codierungshinweis anzugeben, legen Sie die EncodingHint-Eigenschaft für die Spalte ein. Mögliche Werte sind "Default", "Value" und "Hash". Zum Zeitpunkt der Verfassung wird die Eigenschaft nicht noch in SSDT, daher muss mit der JSON-basierte Metadaten, Tabular Model Scripting Language (TMSL) oder tabellarisches Objekt Model (TOM) festgelegt werden verfügbar gemacht. Der folgende Codeausschnitt von JSON-basierte Metadaten aus der Datei Model.bim gibt die Codierung für die Spalte Sales Amount Wert an.

```
{
    "name": "Sales Amount",
    "dataType": "decimal",
    "sourceColumn": "SalesAmount",
    "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",
    "sourceProviderType": "Currency",
    "encodingHint": "Value"
}
```

### <a name="extended-events-not-working-in-ctp-13"></a>Erweiterte Ereignisse, die in der CTP-Version 1.3 nicht funktionsfähig.
Erweiterte Ereignisse SSAS funktionieren nicht in der CTP-Version 1.3. Ein Update ist in der nächsten CTP-Version geplant.

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>SQL Server Analysis Services unter Windows CTP 1.2

Diese Version enthält keine neuen Funktionen. Verbesserungen schließen Fehlerbehebungen und Leistung ein.

Die aktuelle Vorschauversion von SQL Server Data Tools (SSDT), zusammenfällt mit der SQL Server 2017 CTP-Version 1.2, verbessert die neue moderne Get Data-Erfahrung mit neues Abfrage-Editor-Menü und schnellen Zugriff-Funktionalität in der CTP-Version 1.1 eingeführt. 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>SQL Server Analysis Services unter Windows CTP 1.1 

Mit dieser Version werden Erweiterungen für Tabellenmodelle eingeführt. 

### <a name="1400-compatibility-level-for-tabular-models"></a>1400 Kompatibilitätsgrad für Tabellenmodelle
  Um die in diesem Artikel beschriebenen Features und Funktionen zu nutzen, müssen neue und vorhandene Tabellenmodelle auf den Kompatibilitätsgrad 1400 gesetzt werden. Modelle mit dem Kompatibilitätsgrad 1400 können nicht für SQL Server 2016 SP1 oder früher bereitgestellt oder auf niedrigere Kompatibilitätsgrade herabgestuft werden.
  
  Um neue Tabellenmodellprojekte zu erstellen oder vorhandene Projekte auf den Kompatibilitätsgrad 1400 zu aktualisieren, müssen Sie eine **Preview-Version** von [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939)herunterladen und installieren. 
  
In SSDT können Sie den neuen Kompatibilitätsgrad 1400 auswählen, wenn Sie neue Tabellenmodellprojekte erstellen. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE]
> Der integrierte Arbeitsbereich in der Dezember-Version von SQL Server Data Tools (SSDT) unterstützt den Kompatibilitätsgrad 1400. Wenn Sie neue Tabellenmodellprojekte auf einer Arbeitsbereichserverinstanz erstellen, muss es sich bei dieser Instanz bzw. bei allen bereitgestellten Instanzen um [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1 handeln. 

So aktualisieren Sie ein vorhandenes tabellarisches Modell in SSDT im Projektmappen-Explorer mit der rechten Maustaste **Model.bim**, und klicken Sie dann im **Eigenschaften**legen die **Kompatibilitätsgrad** Eigenschaft ** SQL Server-2017 (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>Moderne Get Data-Funktion
In der neuesten Preview-Version von SQL Server Data Tools (SSDT), die zeitlich mit der Version [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1 zusammenfällt, wird eine moderne **Get Data** -Funktion für Tabellenmodelle mit dem Kompatibilitätsgrad 1400 eingeführt. Diese neue Funktion basiert auf einer ähnlichen Funktion in Power BI Desktop und Microsoft Excel 2016.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE]
> In dieser Version wird eine begrenzte Anzahl von Datenquellen unterstützt. Zukünftige Updates werden weitere Datenquellen und Funktionen unterstützen.

Weitere Informationen über die moderne Get Data-Funktion finden Sie im [Analysis Services-Teamblog](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/).

## <a name="ragged-hierarchies"></a>Unregelmäßige Hierarchien
In Tabellenmodellen können Sie über- und untergeordnete Hierarchien modellieren. Hierarchien mit einer unterschiedlichen Anzahl von Ebenen werden häufig als unregelmäßige Hierarchien bezeichnet. Standardmäßig werden unregelmäßige Hierarchien mit Leerzeichen für Ebenen unterhalb der untersten untergeordneten Ebene angezeigt. Nachfolgend sehen Sie ein Beispiel für eine unregelmäßige Hierarchie in einem Organigramm:

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

In dieser Version wird die Eigenschaft **Member ausblenden** eingeführt. Sie können für die Eigenschaft **Member ausblenden** einer Hierarchie die Option **Leere Member ausblenden**festlegen.

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > Leere Member im Modell werden durch einen leeren DAX-Wert und nicht durch eine leere Zeichenfolge dargestellt.

Wenn **Leere Member ausblenden**ausgewählt und das Modell bereitgestellt wird, wird in Clients für die Fehlerberichterstattung wie Excel eine besser lesbare Version der Hierarchie angezeigt.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>Detailzeilen
Sie können jetzt einen benutzerdefinierten Zeilensatz definieren, der zu einem Measurewert beiträgt. Detailzeilen ähneln der Standard-Drillthroughaktion in mehrdimensionalen Modellen. Auf diese Weise können Endbenutzer Informationen noch ausführlicher anzeigen als auf der aggregierten Ebene. 

Die folgende PivotTable zeigt ein Beispieltabellenmodell von Adventure Works mit einem Internetumsatz nach Jahren. Sie können mit der rechten Maustaste auf eine Zelle mit einem aggregierten Wert des Measure klicken und anschließend auf **Details anzeigen** klicken, um die Detailzeilen anzuzeigen.

![AS_Show_Details](../analysis-services/media/as-show-details.png)

Standardmäßig werden die zugehörigen Daten in der Tabelle „Internetumsatz“ angezeigt. Dieses eingeschränkte Verhalten ist häufig für den Benutzer wenig sinnvoll, da die Tabelle möglicherweise nicht über die erforderlichen Spalten verfügt, um nützliche Informationen wie den Kundennamen oder Auftragsdaten anzuzeigen. Mit Detailzeilen können Sie eine Eigenschaft **Detailzeilenausdruck** für Measures angeben.

#### <a name="detail-rows-expression-property-for-measures"></a>Eigenschaft „Detailzeilenausdruck“ für Measures
Mit der Eigenschaft **Detailzeilenausdruck** für Measures können Modellautoren die Spalten und Zeilen anpassen, die an die Endbenutzer zurückgegeben werden.

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

Die DAX-Funktion [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) wird häufig in einem Detailzeilenausdruck verwendet. Mit dem folgenden Beispiel werden die Spalten definiert, die für Zeilen in der Tabelle „Internetumsatz“ im Beispieltabellenmodell von Adventure Works zurückgegeben werden:

```
SELECTCOLUMNS(
    'Internet Sales',
    "Customer First Name", RELATED( Customer[Last Name]),
    "Customer Last Name", RELATED( Customer[First Name]),
    "Order Date", 'Internet Sales'[Order Date],
    "Internet Total Sales", [Internet Total Sales]
)
```

Wenn die Eigenschaft definiert und das Modell bereitgestellt wurde, wird ein benutzerdefinierter Zeilensatz zurückgegeben, wenn der Benutzer **Details anzeigen**auswählt. Der Filterkontext der ausgewählten Zelle wird automatisch berücksichtigt. In diesem Beispiel werden nur die Zeilen für den Wert 2010 angezeigt:

![AS_Detail_Rows](../analysis-services/media/as-detail-rows.png)

#### <a name="default-detail-rows-expression-property-for-tables"></a>Eigenschaft „Standard-Detailzeilenausdruck“ für Tabellen
Neben Measures verfügen Tabellen auch über eine Eigenschaft, um einen Detailzeilenausdruck zu definieren. Die Eigenschaft **Standard-Detailzeilenausdruck** fungiert als Standard für alle Measures innerhalb der Tabelle. Measures, für die kein eigener Ausdruck definiert wurde, erben den Ausdruck der Tabelle und zeigen den für die Tabelle definierten Zeilensatz an. Dies ermöglicht die Wiederverwendung von Ausdrücken, und neue Measures, die später zur Tabelle hinzugefügt werden, erben automatisch den Ausdruck.

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>DAX-Funktion DETAILROWS
Diese Version enthält eine neue `DETAILROWS` DAX-Funktion, die den Zeilensatz zurückgibt, der durch den Detailzeilenausdruck definiert wurde. Dies funktioniert ähnlich wie die `DRILLTHROUGH` -Anweisung in MDX, die ebenfalls mit Detailzeilenausdrücken kompatibel ist, die in Tabellenmodellen definiert werden.

Die folgende DAX-Abfrage gibt den Zeilensatz zurück, der durch den Detailzeilenausdruck für das Measure oder seine Tabelle definiert ist. Wenn kein Ausdruck definiert ist, werden die Daten für die Tabelle „Internetverkäufe“ zurückgegeben, da dies die Tabelle mit dem Measure ist.

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="dax-enhancements"></a>DAX-Verbesserungen
Diese Version enthält einen `IN` -Operator für DAX-Ausdrücke. Dies ist vergleichbar mit dem [`TSQL IN`](/sql-docs/docs/t-sql/language-elements/in-transact-sql)-Operator, der üblicherweise verwendet wird, um mehrere Werte in einer `WHERE`-Klausel anzugeben.

Früher war es üblich, mithilfe des logischen `OR` -Operators Filter für mehrere Werte anzugeben, wie beispielsweise im folgenden Measureausdruck:

```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
                 'Product'[Color] = "Red"
            || 'Product'[Color] = "Blue"
            || 'Product'[Color] = "Black"
    )
```

Dies wird durch Verwendung des `IN` -Operators vereinfacht:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], 'Product'[Color] IN { "Red", "Blue", "Black" }
    )
```

In diesem Fall bezieht sich der `IN` -Operator auf eine einspaltige Tabelle mit drei Zeilen, eine Zeile für jede der angegebenen Farben. Beachten Sie, dass die Tabellenkonstruktorsyntax geschweifte Klammern verwendet.

Der `IN` -Operator ist hinsichtlich seiner Funktion gleichwertig zur `CONTAINSROW` -Funktion:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], CONTAINSROW({ "Red", "Blue", "Black" }, 'Product'[Color])
    )
```

Der `IN` -Operator kann auch effizient mit Tabellenkonstruktoren verwendet werden. Das folgende Measure filtert beispielsweise nach Kombinationen aus Produktfarbe und Kategorie:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
              ( 'Product'[Color] = "Red"   && Product[Product Category Name] = "Accessories" )
         || ( 'Product'[Color] = "Blue"  && Product[Product Category Name] = "Bikes" )
         || ( 'Product'[Color] = "Black" && Product[Product Category Name] = "Clothing" )
        )
    )
```

Bei Verwendung des neuen `IN` -Operators entspricht der obige Measureausdruck nun dem Ausdruck unten:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
            ('Product'[Color], Product[Product Category Name]) IN
            { ( "Red", "Accessories" ), ( "Blue", "Bikes" ), ( "Black", "Clothing" ) }
        )
    )
```


## <a name="table-level-security"></a>Sicherheit auf Tabellenebene
Mit dieser Version wird Sicherheit auf Tabellenebene eingeführt. Es kann nicht nur der Zugriff auf Tabellendaten eingeschränkt werden, sondern vertrauliche Tabellennamen können ebenfalls gesichert werden. Dadurch wird verhindert, dass ein böswilliger Benutzer entdeckt, dass eine solche Tabelle vorhanden ist.

Die Sicherheit auf Tabellenebene muss mit den JSON-basierten Metadaten, der Tabular Model Scripting Language (TMSL) oder dem Tabular Object Model (TOM) festgelegt werden. 

Der folgende Code schützt beispielsweise die Produkttabelle im Beispieltabellenmodell von Adventure Works, indem die **MetadataPermission** -Eigenschaft der **TablePermission** -Klasse auf **Keine**gesetzt wird.

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```


