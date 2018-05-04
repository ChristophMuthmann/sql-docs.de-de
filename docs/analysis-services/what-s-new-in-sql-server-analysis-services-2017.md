---
title: Neuigkeiten in SQL Server 2017 Analysis Services | Microsoft Docs
ms.date: 10/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.custom: ''
ms.technology: ''
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
author: Minewiskan
ms.author: owend
manager: kfile
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 8336d1ce796bb8e83b39d01f0bf6c2b47cb38daa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-in-sql-server-2017-analysis-services"></a>Neuigkeiten in SQL Server 2017 Analysis Services
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

SQL Server 2017 Analysis Services finden Sie einige der wichtigsten Verbesserungen seit SQL Server 2012. Auf den Erfolg des tabellarischen Modus (eingeführt in SQL Server 2012 Analysis Services), diese Version erstellen, können tabellarische Modelle leistungsfähiger als je zuvor.

Im mehrdimensionalen Modus und PowerPivot für SharePoint-Modus sind eine Klammer bei vielen Analysis Services-Bereitstellungen. In der Analysis Services-Produktlebenszyklus sind diese Modi ausgereifte. Es sind keine neuen Funktionen für einen der folgenden Modi in dieser Version. Fehlerbehebungen und leistungsverbesserungen werden jedoch berücksichtigt.

Die hier beschriebenen Funktionen sind in SQL Server 2017 Analysis Services enthalten. Aber um von ihnen nutzen können, müssen Sie auch die neuesten Versionen der verwenden [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) (SSDT) und [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) (SSMS). SSDT und SSMS werden monatlich mit neuen und verbesserten Features aktualisiert, die in der Regel mit neuen Funktionen in SQL Server.  

Während es wichtig, den neuen Funktionen vertraut ist, ist es auch wichtig zu wissen, was wird als veraltet markiert und in dieser Version und zukünftigen Versionen nicht mehr unterstützt. Achten Sie darauf, dass Sie Auschecken [Abwärtskompatibilität (SQL Server 2017 Analysis Services)](analysis-services-backward-compatibility-sql2017.md).

Werfen wir einen Blick auf einige der wichtigsten neuen Funktionen in dieser Version.

## <a name="1400-compatibility-level-for-tabular-models"></a>1400 Kompatibilitätsgrad für Tabellenmodelle
  Viele neue Funktionen und Funktionalität beschrieben hier nutzen möchten, müssen neue oder vorhandene Tabellenmodelle festgelegt oder auf den Kompatibilitätsgrad 1400 aktualisiert werden. Modelle mit dem Kompatibilitätsgrad 1400 können nicht für SQL Server 2016 SP1 oder früher bereitgestellt oder auf niedrigere Kompatibilitätsgrade herabgestuft werden. Weitere Informationen finden Sie unter [Kompatibilitätsgrad für tabellarische Modelle von Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).
  
In SSDT können Sie den neuen Kompatibilitätsgrad 1400 auswählen, wenn Sie neue Tabellenmodellprojekte erstellen. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)


So aktualisieren Sie ein vorhandenes tabellarisches Modell in SSDT im Projektmappen-Explorer mit der rechten Maustaste **Model.bim**, und klicken Sie dann im **Eigenschaften**legen die **Kompatibilitätsgrad** Eigenschaft  **SQL Server-2017 (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

Es ist wichtig zu bedenken, sobald Sie ein vorhandenes Modell 1400 aktualisieren, können nicht herabstufen. Achten Sie darauf, dass Sie eine Sicherung Ihrer 1200-Modell-Datenbank beibehalten.

## <a name="modern-get-data-experience"></a>Moderne Get Data-Funktion
Wenn es sich um das Importieren von Daten aus Datenquellen in tabellarischen Modellen geht, führt SQL Server Data Tools (SSDT) die moderne **Daten abrufen** für Modelle mit Kompatibilitätsgrad 1400 auftreten. Diese neue Funktion basiert auf einer ähnlichen Funktion in Power BI Desktop und Microsoft Excel 2016. Moderne Get Data-Erfahrung bietet enorme Datentransformation und die Fähigkeit zum Kombinieren von Daten mit dem Get Data-Abfrage-Generator und M-Ausdrücke.

Die moderne Daten abrufen Erfahrung bietet Unterstützung für eine Vielzahl von Datenquellen. In Zukunft wird werden Updates Unterstützung für noch länger enthalten.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

 Eine leistungsstarke und intuitive Benutzeroberfläche macht auswählen, Ihre Daten und Data Transformation/Mashup-Funktionen ist einfacher als je zuvor.

![Erweiterte kombinieren](../analysis-services/media/as-get-data-advanced.png)


Auftreten, die moderne Daten abrufen und M-Mashup-Funktionen gelten nicht für vorhandene Upraded für tabellarische Modelle aus dem Kompatibilitätsgrad 1200 1400. Die neue Umgebung gilt nur für neue Modelle mit Kompatibilitätsgrad 1400 erstellt.

## <a name="encoding-hints"></a>Codierung Hinweise
Diese Version führt Codierung Hinweise, eine erweiterte Funktion, die zur Optimierung der Verarbeitung (Refresh Data) des großen tabellarischen in-Memory-Modellen verwendet. Zum besseren Verständnis Codierung finden Sie unter [Leistung optimieren von tabellarischen Modellen in SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx) in diesem Whitepaper Codierung besser zu verstehen.

* Wertcodierung bietet eine bessere abfrageleistung für Spalten, die in der Regel nur für Aggregationen verwendet werden.

* Hashcodierung wird bevorzugt für Group by-Spalten (häufig Dimensionstabelle Werte) und Fremdschlüssel. Zeichenfolgenspalten sind immer Hash codiert.

Numerische Spalten können mit dieser Codierung Methoden verwenden. Wenn Analysis Services ist entweder die Tabelle leer ist (mit oder ohne Partitionen) startet die Verarbeitung einer Tabelle oder ein vollständigen Tabelle Verarbeitungsvorgang durchgeführt werden, werden Beispiele Werte für jede numerische Spalte zu bestimmen, ob die anzuwendende Wert oder hashcodierung übernommen. . Wertcodierung wird standardmäßig ausgewählt, wenn das Beispiel von unterschiedlichen Werten in der Spalte ist groß genug – hashcodierung andernfalls in der Regel eine bessere Komprimierung bietet. Es ist möglich, dass Analysis Services Codierungsmethode ändern, nachdem die Spalte basierend auf Weitere Informationen über die datenverteilung teilweise verarbeitet wird, und Starten des Codierungsvorgangs; Diese können jedoch erhöhen die Verarbeitungszeit und ist ineffizient. Im Whitepaper zur Optimierung der Leistung wird die Codierung erneut im Detail erläutert und beschrieben, wie mit SQL Server Profiler erkannt.

Codierung Hinweise können der Modellierer eine Einstellung dafür Codierungsmethode erhält Vorkenntnisse von datenprofilerstellungs und/oder als Antwort auf die erneute Verschlüsselung Ablaufverfolgungsereignisse an. Da Aggregation über Spalten Hash-codierte langsamer ist als über Spalten Wert-codierte wertcodierung als Hinweis für solche Spalten angegeben werden kann. Es ist nicht sichergestellt, dass die Einstellung angewendet wird. Es ist ein Hinweis im Gegensatz zu einer Einstellung. Um eine codierungshinweis anzugeben, legen Sie die EncodingHint-Eigenschaft für die Spalte ein. Mögliche Werte sind "Default", "Value" und "Hash". Der folgende Codeausschnitt von JSON-basierte Metadaten aus der Datei Model.bim gibt die Codierung für die Spalte Sales Amount Wert an.

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

## <a name="ragged-hierarchies"></a>Unregelmäßige Hierarchien
In Tabellenmodellen können Sie über- und untergeordnete Hierarchien modellieren. Hierarchien mit einer unterschiedlichen Anzahl von Ebenen werden häufig als unregelmäßige Hierarchien bezeichnet. Standardmäßig werden unregelmäßige Hierarchien mit Leerzeichen für Ebenen unterhalb der untersten untergeordneten Ebene angezeigt. Nachfolgend sehen Sie ein Beispiel für eine unregelmäßige Hierarchie in einem Organigramm:

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

In dieser Version wird die Eigenschaft **Member ausblenden** eingeführt. Sie können für die Eigenschaft **Member ausblenden** einer Hierarchie die Option **Leere Member ausblenden**festlegen.

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > Leere Member im Modell werden durch einen leeren DAX-Wert und nicht durch eine leere Zeichenfolge dargestellt.

Wenn **Leere Member ausblenden**ausgewählt und das Modell bereitgestellt wird, wird in Clients für die Fehlerberichterstattung wie Excel eine besser lesbare Version der Hierarchie angezeigt.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)


## <a name="detail-rows"></a>Detailzeilen
Sie können jetzt einen benutzerdefinierten Zeilensatz definieren, der zu einem Measurewert beiträgt. Detailzeilen ähneln der Standard-Drillthroughaktion in mehrdimensionalen Modellen. Auf diese Weise können Endbenutzer Informationen noch ausführlicher anzeigen als auf der aggregierten Ebene. 

Die folgende PivotTable zeigt ein Beispieltabellenmodell von Adventure Works mit einem Internetumsatz nach Jahren. Sie können mit der rechten Maustaste auf eine Zelle mit einem aggregierten Wert des Measure klicken und anschließend auf **Details anzeigen** klicken, um die Detailzeilen anzuzeigen.

![AS_Show_Details](../analysis-services/media/as-show-details.png)

Standardmäßig werden die zugehörigen Daten in der Tabelle „Internetumsatz“ angezeigt. Dieses eingeschränkte Verhalten ist häufig für den Benutzer wenig sinnvoll, da die Tabelle möglicherweise nicht über die erforderlichen Spalten verfügt, um nützliche Informationen wie den Kundennamen oder Auftragsdaten anzuzeigen. Mit Detailzeilen können Sie eine Eigenschaft **Detailzeilenausdruck** für Measures angeben.

#### <a name="detail-rows-expression-property-for-measures"></a>Eigenschaft „Detailzeilenausdruck“ für Measures
Mit der Eigenschaft **Detailzeilenausdruck** für Measures können Modellautoren die Spalten und Zeilen anpassen, die an die Endbenutzer zurückgegeben werden.

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

Die [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) DAX-Funktion wird häufig in einem Ausdruck verwendet Detail Zeilen verwendet. Mit dem folgenden Beispiel werden die Spalten definiert, die für Zeilen in der Tabelle „Internetumsatz“ im Beispieltabellenmodell von Adventure Works zurückgegeben werden:

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
Neben Measures verfügen Tabellen auch über eine Eigenschaft, um einen Detailzeilenausdruck zu definieren. Die Eigenschaft **Standard-Detailzeilenausdruck** fungiert als Standard für alle Measures innerhalb der Tabelle. Measures, die keine eigene definierter Ausdruck erbt den Ausdruck aus der Tabelle und das Rowset für die Tabelle definierten anzeigen. Dies ermöglicht die Wiederverwendung von Ausdrücken und neue Measures, die automatisch an die Tabelle später erbt den Ausdruck.

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>DAX-Funktion DETAILROWS
Diese Version enthält eine neue `DETAILROWS` DAX-Funktion, die den Zeilensatz zurückgibt, der durch den Detailzeilenausdruck definiert wurde. Dies funktioniert ähnlich wie die `DRILLTHROUGH` -Anweisung in MDX, die ebenfalls mit Detailzeilenausdrücken kompatibel ist, die in Tabellenmodellen definiert werden.

Die folgende DAX-Abfrage gibt den Zeilensatz zurück, der durch den Detailzeilenausdruck für das Measure oder seine Tabelle definiert ist. Wenn kein Ausdruck definiert ist, werden die Daten für die Tabelle „Internetverkäufe“ zurückgegeben, da dies die Tabelle mit dem Measure ist.

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="object-level-security"></a>Sicherheit auf Nachrichtenebene-Objekt
Ab dieser Version steht [Sicherheit auf Nachrichtenebene Objekt](../analysis-services/tabular-models/object-level-security.md) für Tabellen und Spalten. Zusätzlich zum Einschränken des Zugriffs auf Tabellen-und Spaltendaten, können sensible Tabellen- und Spaltennamen gesichert werden. Dadurch wird verhindert, dass ein böswilliger Benutzer entdeckt, dass eine solche Tabelle vorhanden ist.

Sicherheit auf Nachrichtenebene Objekt muss mit der JSON-basierte Metadaten, Tabular Model Scripting Language (TMSL) oder tabellarisches Objekt Model (TOM) festgelegt werden. 

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

## <a name="dynamic-management-views-dmvs"></a>Dynamische Verwaltungssichten (DMVs)
[DMVs](../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md) sind Abfragen in SQL Server Profiler, Informationen zu lokalen Servervorgängen und Serverzustand zurückgeben.
Diese Version bietet Verbesserungen an [dynamische Verwaltungssichten](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMVS) für tabellarische Modelle mit Kompatibilitätsgrad 1200 und 1400.

[DISCOVER_CALC_DEPENDENCY](../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md) arbeitet jetzt mit 1200 und 1400 Tabellenmodelle. Tabellenmodelle 1400 anzeigen Abhängigkeiten zwischen M Partitionen, M-Ausdrücke und strukturierte Datenquellen Weitere Informationen finden Sie unter der [Analysis Services-Blog](https://blogs.msdn.microsoft.com/analysisservices/2017/07/17/whats-new-in-sql-server-2017-rc1-for-analysis-services/).

[MDSCHEMA_MEASUREGROUP_DIMENSIONS](../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md) Verbesserungen sind für diese DMV, die von verschiedenen Clienttools verwendet wird, um Measure Dimensionalität anzuzeigen. Beispielsweise kann die Durchsuchen-Funktion in Excel-Pivot-Tabellen der Benutzer Cross-Drilldown zu Dimensionen im Bezug auf die ausgewählten Measures. Diese Version korrigiert die Kardinalität-Spalten, in denen zuvor falsche Werte angezeigt wurden.

## <a name="dax-enhancements"></a>DAX-Verbesserungen
Diese Version enthält Unterstützung für neue DAX-Funktionen und Funktionalität. Damit nutzen können, müssen Sie die neueste Version von SSDT verwenden. Weitere Informationen finden Sie unter [neue DAX-Funktionen](https://msdn.microsoft.com/library/mt704075.aspx).

Einer der wichtigsten Teile der neuen DAX-Funktionen ist die neue [IN-Operator / CONTAINSROW Funktion](https://msdn.microsoft.com/library/mt842621.aspx) für DAX-Ausdrücke. Dies ist vergleichbar mit dem [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) -Operator, der üblicherweise verwendet wird, um mehrere Werte in einer `WHERE` -Klausel anzugeben.

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

## <a name="additional-improvements"></a>Weitere Verbesserungen
Zusätzlich zu den neuen Features gehören Analysis Services, SSDT und SSMS, die folgenden Verbesserungen:

* Hierarchie und Spalte Wiederverwendung eingeblendet, in aussagekräftigere Speicherorte in der Liste der Power BI-Feld.
* Datum Beziehungen problemlos Beziehungen zu Datumsdimensionen auf Grundlage von Datumsfeldern zu erstellen.
* Die Standardinstallationsoption für Analysis Services ist jetzt für den Tabellenmodus.
* Neue Datenquellen "Daten abrufen" (Power Abfrage).
* DAX-Editor für SSDT.
* Vorhandene DirectQuery-Datenquellen für M Abfragen unterstützen.
* SSMS-Verbesserungen, z. B. anzeigen, bearbeiten und die Unterstützung der Skripterstellung für strukturierte Datenquellen.



## <a name="see-also"></a>Siehe auch
[Versionsanmerkungen zu SQLServer 2017](../sql-server/sql-server-2017-release-notes.md)   
[Neues in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)
