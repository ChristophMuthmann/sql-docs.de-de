---
title: "Transformation für das Aggregieren | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.aggregatetrans.f1
- sql13.dts.designer.aggregationtransformation.aggregations.f1
- sql13.dts.designer.aggregationtransformation.advanced.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
caps.latest.revision: "59"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1c52546eab7dc5c52fb38e03616df648d3d5d67d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="aggregate-transformation"></a>Transformation für das Aggregieren
  Die Transformation für das Aggregieren wendet Aggregatfunktionen, wie z.B. Average, auf Spaltenwerte an und kopiert die Ergebnisse in die Transformationsausgabe. Neben Aggregatfunktionen stellt diese Transformation die GROUP BY-Klausel bereit, mit der Sie Gruppen für das Aggregieren angeben können.  
  
## <a name="operations"></a>Operationen (Operations)  
 Die Transformation für das Aggregieren unterstützt die folgenden Vorgänge.  
  
|Vorgang|Description|  
|---------------|-----------------|  
|Group By|Unterteilt Datasets in Gruppen. Spalten eines beliebigen Datentyps können für das Gruppieren verwendet werden. Weitere Informationen finden Sie unter [GROUP BY &#40;Transact-SQL&#41;](../../../t-sql/queries/select-group-by-transact-sql.md).|  
|Sum|Summiert die Werte einer Spalte. Summiert werden können nur Spalten mit einem numerischen Datentyp. Weitere Informationen finden Sie unter [SUM &#40;Transact-SQL&#41;](../../../t-sql/functions/sum-transact-sql.md).|  
|Mittelwert|Gibt den Mittelwert der Werte in einer Spalte zurück. Der Mittelwert kann nur für Spalten mit einem numerischen Datentyp ermittelt werden. Weitere Informationen finden Sie unter [AVG &#40;Transact-SQL&#41;](../../../t-sql/functions/avg-transact-sql.md).|  
|Count|Gibt die Anzahl von Elementen in einer Gruppe zurück. Weitere Informationen finden Sie unter [COUNT &#40;Transact-SQL&#41;](../../../t-sql/functions/count-transact-sql.md).|  
|Count distinct|Gibt die Anzahl eindeutiger Werte ungleich null in einer Gruppe zurück.|  
|Minimum|Gibt den kleinsten Wert in einer Gruppe zurück. Weitere Informationen finden Sie unter [MIN &#40;Transact-SQL&#41;](../../../t-sql/functions/min-transact-sql.md). Im Gegensatz zur MIN-Funktion von Transact-SQL kann dieser Vorgang nur mit numerischen, Datums- und Zeitdatentypen verwendet werden.|  
|Maximum|Gibt den größten Wert in einer Gruppe zurück. Weitere Informationen finden Sie unter [MAX &#40;Transact-SQL&#41;](../../../t-sql/functions/max-transact-sql.md). Im Gegensatz zur MAX-Funktion von Transact-SQL kann dieser Vorgang nur mit numerischen, Datums- und Zeitdatentypen verwendet werden.|  
  
 Die Transformation für das Aggregieren behandelt NULL-Werte auf die gleiche Weise wie das relationale Datenbankmodul von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Dieses Verhalten ist im SQL-92-Standard definiert. Dabei gelten die folgenden Regeln:  
  
-   In einer GROUP BY-Klausel werden NULL-Werte wie andere Spaltenwerte behandelt. Enthält die Gruppierungsspalte mehrere NULL-Werte, werden diese in einer Gruppe zusammengefasst.  
  
-   In den Funktionen COUNT (Spaltenname) und COUNT (DISTINCT-Spaltenname) werden NULL-Werte ignoriert. Das Ergebnis schließt Zeilen mit NULL-Werten in der benannten Spalte aus.  
  
-   In der COUNT-Funktion (*) werden alle Zeilen gezählt, auch Zeilen mit NULL-Werten.  
  
## <a name="big-numbers-in-aggregates"></a>Große Zahlen in Aggregaten  
 Eine Spalte kann numerische Werte enthalten, die aufgrund ihres großen Werts oder der Anforderungen an die Genauigkeit speziell berücksichtigt werden müssen. Die Transformation für das Aggregieren beinhaltet die IsBig-Eigenschaft, die Sie für Ausgabespalten festlegen können, um eine spezielle Handhabung großer oder sehr genauer Zahlen aufzurufen. Falls ein Spaltenwert u.U. 4 Milliarden überschreitet oder eine Genauigkeit über den float-Datentyp hinaus erforderlich ist, sollte IsBig auf 1 festgelegt werden.  
  
 Das Festlegen der IsBig-Eigenschaft auf 1 hat folgende Auswirkungen auf die Ausgabe der Transformation für das Aggregieren:  
  
-   Der DT_R8-Datentyp wird anstelle des DT_R4-Datentyps verwendet.  
  
-   Count-Ergebnisse werden als DT_UI8-Datentyp gespeichert.  
  
-   Distinct Count-Ergebnisse werden als DT_UI4-Datentyp gespeichert.  
  
> [!NOTE]  
>  Für Spalten, die für die Vorgänge GROUP BY, Maximum oder Minimum verwendet werden, können Sie IsBig nicht auf 1 festlegen.  
  
## <a name="performance-considerations"></a>Leistungsaspekte  
 Die Transformation für das Aggregieren enthält Eigenschaften, die Sie festlegen können, um die Leistung der Transformation zu optimieren.  
  
-   Wenn Sie einen **GROUP BY** -Vorgang ausführen, legen Sie die Keys-Eigenschaft oder die KeysScale-Eigenschaft für die Komponente und die Komponentenausgaben fest. Mithilfe von Keys können Sie die genaue Anzahl von Schlüsseln festlegen, die von der Transformation behandelt werden sollen. (In diesem Kontext bezeichnet Keys die Anzahl der Gruppen, die als Ergebnis eines **GROUP BY**-Vorgangs erwartet werden.) Mit KeysScale können Sie eine ungefähre Anzahl von Schlüsseln angeben. Wenn Sie einen entsprechenden Wert für Keys oder KeyScale angeben, verbessern Sie damit die Leistung, da von der Transformation den zwischengespeicherten Daten eine ausreichende Menge an Arbeitsspeicher zugewiesen werden kann.  
  
-   Legen Sie beim Durchführen eines **DISTINCT COUNT** -Vorgangs die CountDistinctKeys-Eigenschaft oder die CountDistinctScale-Eigenschaft der Komponente fest. Mithilfe von CountDistinctKeys können Sie die genaue Anzahl von Schlüsseln festlegen, die von der Transformation für einen COUNT DISTINCT-Vorgang behandelt werden sollen. (In diesem Kontext bezeichnet CountDistinctKeys die Anzahl der unterschiedlichen Werte, die als Ergebnis eines **DISTINCT COUNT**-Vorgangs erwartet werden.) Mithilfe von CountDistinctScale können Sie eine ungefähre Anzahl von Schlüsseln für einen COUNT DISTINCT-Vorgang festlegen. Wenn Sie einen entsprechenden Wert für CountDistinctKeys oder CountDistinctScale angeben, verbessern Sie damit die Leistung, da von der Transformation den zwischengespeicherten Daten eine ausreichende Menge an Arbeitsspeicher zugewiesen werden kann.  
  
## <a name="aggregate-transformation-configuration"></a>Konfiguration der Transformation für das Aggregieren  
 Die Transformation für das Aggregieren konfigurieren Sie auf der Transformations-, Ausgabe- und Spaltenebene.  
  
-   Auf der Transformationsebene konfigurieren Sie die Transformation für das Aggregieren auf Leistung, indem Sie die folgenden Werte angeben:  
  
    -   Die Anzahl der Gruppen, die als Ergebnis eines **GROUP BY** -Vorgangs erwartet werden.  
  
    -   Die Anzahl der unterschiedlichen Werte, die als Ergebnis eines **COUNT DISTINCT** -Vorgangs erwartet werden.  
  
    -   Der Prozentsatz, um den der Arbeitsspeicher während der Aggregation erweitert werden kann.  
  
     Für die Transformation für das Aggregieren kann auch konfiguriert werden, dass anstelle eines Fehlers eine Warnung generiert wird, wenn der Wert eines Divisors null ist.  
  
-   Auf der Ausgabeebene können Sie die Transformation für das Aggregieren auf Leistung konfigurieren, indem Sie die Anzahl der Gruppen angeben, die als Ergebnis eines **GROUP BY** -Vorgangs erwartet werden. Die Transformation für das Aggregieren unterstützt mehrere Ausgaben, und jede kann unterschiedlich konfiguriert werden.  
  
-   Auf der Spaltenebene geben Sie die folgenden Werte an:  
  
    -   Die von der Spalte durchgeführte Aggregation.  
  
    -   Die Vergleichsoptionen der Aggregation.  
  
 Sie können die Transformation für das Aggregieren auf Leistung auch konfigurieren, indem Sie diese Werte angeben:  
  
-   Die Anzahl der Gruppen, die als Ergebnis eines **GROUP BY** -Vorgangs für die Spalte erwartet werden.  
  
-   Die Anzahl der unterschiedlichen Werte, die als Ergebnis eines **COUNT DISTINCT** -Vorgangs für die Spalte erwartet werden.  
  
 Sie können Spalten auch als IsBig angeben, wenn eine Spalte große numerische Werte oder numerische Werte mit hoher Genauigkeit enthält.  
  
 Die Transformation für das Aggregieren ist asynchron. Das heißt, sie verwendet und veröffentlicht Daten nicht zeilenweise. Vielmehr verwendet sie das gesamte Rowset, führt Gruppierungen und Aggregationen aus und veröffentlicht dann die Ergebnisse.  
  
 Diese Transformation übergibt keine Spalten, sondern erstellt im Datenfluss für die veröffentlichten Daten neue Spalten. Nur die Eingabespalten, für die Aggregatfunktionen gelten, oder die Eingabespalten, die die Transformation zum Gruppieren verwendet, werden in die Transformationsausgabe kopiert. Angenommen, eine Transformation für das Aggregieren weist drei Spalten auf: **CountryRegion**, **City**und **Population**. Die Transformation gruppiert nach der **CountryRegion** -Spalte und wendet die SUM-Funktion auf die **Population** -Spalte an. Deshalb ist in der Ausgabe die **City** -Spalte nicht enthalten.  
  
 Sie können der Transformation für das Aggregieren auch mehrere Ausgaben hinzufügen und jede Aggregation an eine andere Ausgabe weiterleiten. Wendet beispielsweise die Transformation für das Aggregieren die Funktionen Sum und Average an, kann jede Aggregation an eine andere Ausgabe geleitet werden.  
  
 Auf eine einzelne Eingabespalte können mehrere Aggregationen angewendet werden. Wenn Sie z.B. die Sum- und Average-Werte für eine Eingabespalte mit dem Namen **Sales**haben möchten, können Sie die Transformation so konfigurieren, dass sie die Sum-Funktion und die Average-Funktion auf die **Sales** -Spalte anwendet.  
  
 Die Transformation für das Aggregieren weist je eine Eingabe und mindestens eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Aggregieren von Werten in einem Dataset mithilfe der Transformation für das Aggregieren](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Aggregieren von Werten in einem Dataset mithilfe der Transformation für das Aggregieren](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="aggregate-transformation-editor-aggregations-tab"></a>Transformations-Editor für Aggregieren (Registerkarte Aggregationen)
  Auf der Registerkarte **Aggregationen** des Dialogfelds **Transformations-Editor für Aggregieren** können Sie die Spalten für Aggregationen und Aggregationseigenschaften angeben. Sie können mehrere Aggregationen anwenden. Durch diese Transformation wird keine Fehlerausgabe generiert.  
  
> [!NOTE]  
>  Die Optionen für die Anzahl an Schlüsseln, die Schlüsselskala, die Anzahl unterschiedlicher Schlüssel sowie für unterschiedliche Schlüsselskalen gelten auf der Komponentenebene, wenn sie auf der Registerkarte **Erweitert** angegeben wurden; sie gelten auf der Ausgabeebene, wenn sie in der erweiterten Ansicht der Registerkarte **Aggregationen** angegeben wurden und auf der Spaltenebene, wenn sie in der Spaltenliste im unteren Bereich der Registerkarte **Aggregationen** angegeben wurden.  
>   
>  In der Transformation für das Aggregieren beziehen sich **Schlüssel** und **Schlüsselskala** auf die Anzahl der Gruppen, die als Ergebnis eines **GROUP BY** -Vorgangs erwartet werden. **COUNT DISTINCT-Schlüssel** und **COUNT DISTINCT-Skala** beziehen sich auf die Anzahl der unterschiedlichen Werte, die als Ergebnis eines **DISTINCT COUNT** -Vorgangs erwartet werden.  
  
### <a name="options"></a>enthalten  
 **Erweitert/Standard**  
 Blenden Sie die Optionen ein oder aus, um mehrere Aggregationen für mehrere Ausgaben zu konfigurieren. Die erweiterten Optionen sind standardmäßig ausgeblendet.  
  
 **Aggregationsname**  
 Geben Sie in der erweiterten Anzeige einen Anzeigenamen für die Aggregation ein.  
  
 **Nach Spalten gruppieren**  
 Wählen Sie in der erweiterten Anzeige Spalten für die Gruppierung aus, indem Sie die Liste **Verfügbare Eingabespalten** wie im Folgenden beschrieben verwenden.  
  
 **Schlüsselskala**  
 Geben Sie in der erweiterten Anzeige optional die ungefähre Anzahl der Schlüssel an, die durch die Aggregation geschrieben werden können. Der Standardwert für diese Option ist **Keine Angabe**. Wenn die Eigenschaften **Schlüsselskala** und **Schlüssel** festgelegt sind, wird der Wert von **Schlüssel** vorrangig behandelt.  
  
|Wert|Description|  
|-----------|-----------------|  
|Keine Angabe|Die Eigenschaft Schlüsselskala wird nicht verwendet.|  
|Low|Die Aggregation kann ungefähr 500.000 Schlüssel schreiben.|  
|Medium|Die Aggregation kann ungefähr 5.000.000 Schlüssel schreiben.|  
|High|Die Aggregation kann mehr als 25.000.000 Schlüssel schreiben.|  
  
 **Schlüssel**  
 Geben Sie in der erweiterten Anzeige optional die genaue Anzahl der Schlüssel an, die durch die Aggregation geschrieben werden können. Wenn sowohl **Schlüsselskala** als auch **Schlüssel** angegeben sind, wird **Schlüssel** vorrangig behandelt.  
  
 **Verfügbare Eingabespalten**  
 Wählen Sie aus der Liste der verfügbaren Eingabespalten mithilfe der Kontrollkästchen in dieser Tabelle Spalten aus.  
  
 **Eingabespalte**  
 Wählen Sie Spalten aus der Liste der verfügbaren Eingabespalten aus.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Eingabespalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 **Vorgang**  
 Wählen Sie einen Vorgang aus der Liste der verfügbaren Vorgänge aus, indem Sie die folgende Tabelle zurate ziehen.  
  
|Vorgang|Description|  
|---------------|-----------------|  
|**GroupBy**|Unterteilt Datasets in Gruppen. Zum Gruppieren können Spalten aller Datentypen verwendet werden. Weitere Informationen finden Sie unter GROUP BY.|  
|**Sum**|Summiert die Werte einer Spalte. Summiert werden können nur Spalten mit einem numerischen Datentyp. Weitere Informationen finden Sie unter SUM.|  
|**Mittelwert**|Gibt den Mittelwert der Werte in einer Spalte zurück. Der Mittelwert kann nur für Spalten mit einem numerischen Datentyp ermittelt werden. Weitere Informationen finden Sie unter AVG.|  
|**Count**|Gibt die Anzahl von Elementen in einer Gruppe zurück. Weitere Informationen finden Sie unter COUNT.|  
|**CountDistinct**|Gibt die Anzahl eindeutiger Werte ungleich null in einer Gruppe zurück. Weitere Informationen finden Sie unter COUNT und Distinct.|  
|**Minimum**|Gibt den kleinsten Wert in einer Gruppe zurück. Ist auf numerische Datentypen beschränkt.|  
|**Maximum**|Gibt den größten Wert in einer Gruppe zurück. Ist auf numerische Datentypen beschränkt.|  
  
 **Vergleichsflags**  
 Wenn Sie **Group By**auswählen, steuern Sie mithilfe der Kontrollkästchen, wie der Vergleich durch die Transformation ausgeführt wird. Weitere Informationen zu den Optionen für das Vergleichen von Zeichenfolgen finden Sie unter [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Count Distinct Scale**  
 Gibt optional die ungefähre Anzahl unterschiedlicher Werte an, die durch die Aggregation geschrieben werden können. Der Standardwert für diese Option ist **Keine Angabe**. Wenn sowohl **CountDistinctScale** und **CountDistinctKeys** angegeben werden, wird **CountDistinctKeys** vorrangig behandelt.  
  
|Wert|Description|  
|-----------|-----------------|  
|Keine Angabe|Die **CountDistinctScale** -Eigenschaft wird nicht verwendet.|  
|Low|Die Aggregation kann ungefähr 500.000 unterschiedliche Werte schreiben.|  
|Medium|Die Aggregation kann ungefähr 5.000.000 unterschiedliche Werte schreiben.|  
|High|Die Aggregation kann mehr als 25.000.000 unterschiedliche Werte schreiben.|  
  
 **Count Distinct Keys**  
 Gibt optional die genaue Anzahl unterschiedlicher Werte an, die durch die Aggregation geschrieben werden können. Wenn sowohl **CountDistinctScale** und **CountDistinctKeys** angegeben werden, wird **CountDistinctKeys** vorrangig behandelt.  
  
## <a name="aggregate-transformation-editor-advanced-tab"></a>Transformations-Editor für Aggregieren (Registerkarte Erweitert)
  Mithilfe der Registerkarte **Erweitert** des Dialogfelds **Transformations-Editor für Aggregieren** können Sie Komponenteneigenschaften festlegen, Aggregationen angeben und die Eigenschaften von Eingabe- und Ausgabespalten festlegen.  
  
> [!NOTE]  
>  Die Optionen für die Anzahl an Schlüsseln, die Schlüsselskala, die Anzahl unterschiedlicher Schlüssel sowie für unterschiedliche Schlüsselskalen gelten auf der Komponentenebene, wenn sie auf der Registerkarte **Erweitert** angegeben wurden; sie gelten auf der Ausgabeebene, wenn sie in der erweiterten Ansicht der Registerkarte **Aggregationen** angegeben wurden und auf der Spaltenebene, wenn sie in der Spaltenliste im unteren Bereich der Registerkarte **Aggregationen** angegeben wurden.  
>   
>  In der Transformation für das Aggregieren beziehen sich **Schlüssel** und **Schlüsselskala** auf die Anzahl der Gruppen, die als Ergebnis eines **GROUP BY** -Vorgangs erwartet werden. **COUNT DISTINCT-Schlüssel** und **COUNT DISTINCT-Skala** beziehen sich auf die Anzahl der unterschiedlichen Werte, die als Ergebnis eines **DISTINCT COUNT** -Vorgangs erwartet werden.  
  
### <a name="options"></a>enthalten  
 **Schlüsselskala**  
 Gibt optional die ungefähre Anzahl an Schlüsseln an, die von der Aggregation erwartet werden. Für die Transformation wird diese Information verwendet, um die anfängliche Cachegröße zu optimieren. Der Standardwert für diese Option ist **Keine Angabe**. Wenn sowohl **Schlüsselskala** als auch **Anzahl von Schlüsseln** angegeben wurden, hat **Anzahl von Schlüsseln** Vorrang.  
  
|Wert|Description|  
|-----------|-----------------|  
|Keine Angabe|Die Eigenschaft **Schlüsselskala** wird nicht verwendet.|  
|Low|Die Aggregation kann ungefähr 500.000 Schlüssel schreiben.|  
|Medium|Die Aggregation kann ungefähr 5.000.000 Schlüssel schreiben.|  
|High|Die Aggregation kann mehr als 25.000.000 Schlüssel schreiben.|  
  
 **Anzahl von Schlüsseln**  
 Gibt optional die genaue Anzahl an Schlüsseln an, die von der Aggregation erwartet werden. Für die Transformation wird diese Information verwendet, um die anfängliche Cachegröße zu optimieren. Wenn sowohl **Schlüsselskala** als auch **Anzahl von Schlüsseln** angegeben wurden, hat **Anzahl von Schlüsseln** Vorrang.  
  
 **COUNT DISTINCT-Skala**  
 Gibt optional die ungefähre Anzahl unterschiedlicher Werte an, die durch die Aggregation geschrieben werden können. Der Standardwert für diese Option ist **Keine Angabe**. Wenn sowohl **COUNT DISTINCT-Skala** als auch **COUNT DISTINCT-Schlüssel** angegeben wurden, hat **COUNT DISTINCT-Schlüssel** Vorrang.  
  
|Wert|Description|  
|-----------|-----------------|  
|Keine Angabe|Die CountDistinctScale-Eigenschaft wird nicht verwendet.|  
|Low|Die Aggregation kann ungefähr 500.000 unterschiedliche Werte schreiben.|  
|Medium|Die Aggregation kann ungefähr 5.000.000 unterschiedliche Werte schreiben.|  
|High|Die Aggregation kann mehr als 25.000.000 unterschiedliche Werte schreiben.|  
  
 **COUNT DISTINCT-Schlüssel**  
 Gibt optional die genaue Anzahl unterschiedlicher Werte an, die durch die Aggregation geschrieben werden können. Wenn sowohl **COUNT DISTINCT-Skala** als auch **COUNT DISTINCT-Schlüssel** angegeben wurden, hat **COUNT DISTINCT-Schlüssel** Vorrang.  
  
 **Faktor für automatische Erweiterung**  
 Verwenden Sie einen Wert zwischen 1 und 100, um den Prozentsatz anzugeben, um den der Arbeitsspeicher während der Aggregation erweitert werden kann. Der Standardwert für diese Option ist **25 %**.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
