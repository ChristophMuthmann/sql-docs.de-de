---
title: Transformations-Editor (Registerkarte Aggregationen) aggregieren | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.aggregationtransformation.aggregations.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: a01cb124-ec79-4673-b1a1-bf4d60ee1b45
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e7bf78662f021ae3c6ff776635035feea985b12
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="aggregate-transformation-editor-aggregations-tab"></a>Transformations-Editor für Aggregieren (Registerkarte Aggregationen)
  Auf der Registerkarte **Aggregationen** des Dialogfelds **Transformations-Editor für Aggregieren** können Sie die Spalten für Aggregationen und Aggregationseigenschaften angeben. Sie können mehrere Aggregationen anwenden. Durch diese Transformation wird keine Fehlerausgabe generiert.  
  
> [!NOTE]  
>  Die Optionen für die Anzahl an Schlüsseln, die Schlüsselskala, die Anzahl unterschiedlicher Schlüssel sowie für unterschiedliche Schlüsselskalen gelten auf der Komponentenebene, wenn sie auf der Registerkarte **Erweitert** angegeben wurden; sie gelten auf der Ausgabeebene, wenn sie in der erweiterten Ansicht der Registerkarte **Aggregationen** angegeben wurden und auf der Spaltenebene, wenn sie in der Spaltenliste im unteren Bereich der Registerkarte **Aggregationen** angegeben wurden.  
>   
>  In der Transformation für das Aggregieren beziehen sich **Schlüssel** und **Schlüsselskala** auf die Anzahl der Gruppen, die als Ergebnis eines **GROUP BY** -Vorgangs erwartet werden. **COUNT DISTINCT-Schlüssel** und **COUNT DISTINCT-Skala** beziehen sich auf die Anzahl der unterschiedlichen Werte, die als Ergebnis eines **DISTINCT COUNT** -Vorgangs erwartet werden.  
  
 Weitere Informationen zur Transformation für das Aggregieren finden Sie unter [Aggregate Transformation](../../../integration-services/data-flow/transformations/aggregate-transformation.md).  
  
## <a name="options"></a>enthalten  
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
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformations-Editor für aggregieren &#40; Registerkarte "Erweitert" &#41;](../../../integration-services/data-flow/transformations/aggregate-transformation-editor-advanced-tab.md)   
 [Aggregieren von Werten in einem Dataset mithilfe der Transformation für das Aggregieren](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
