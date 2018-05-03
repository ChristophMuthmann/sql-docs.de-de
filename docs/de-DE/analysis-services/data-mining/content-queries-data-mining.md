---
title: Inhaltsabfragen (Datamining) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 057134e35d748c49a535fb32070484d7d228c5d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="content-queries-data-mining"></a>Inhaltsabfragen (Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Eine Inhaltsabfrage stellt eine Möglichkeit dar, Informationen über interne Statistiken und die Struktur des Miningmodells zu extrahieren. Mitunter enthält eine Inhaltsabfrage Details, die im Viewer nicht unmittelbar verfügbar sind. Sie können auch die Ergebnisse einer Inhaltsabfrage verwenden, um Informationen programmgesteuert zu anderen Verwendungszwecken zu extrahieren.  
  
 Dieser Abschnitt enthält allgemeine Informationen über die Art der Informationen, die Sie mit einer Inhaltsabfrage abrufen können, sowie die allgemeine DMX-Syntax für Inhaltsabfragen.  
  
 [Grundlegende Inhaltsabfragen](#bkmk_ContentQuery)  
  
-   [Abfragen für Struktur- und Falldaten](#bkmk_Structure)  
  
-   [Abfragen für Modellmuster](#bkmk_Patterns)  
  
 [Beispiele](#bkmk_Examples)  
  
-   [Inhaltsabfrage für ein Zuordnungsmodell](#bkmk_Assoc)  
  
-   [Inhaltsabfrage für ein Entscheidungsstrukturmodell](#bkmk_DecTree)  
  
 [Arbeiten mit Abfrageergebnissen](#bkmk_Results)  
  
##  <a name="bkmk_ContentQuery"></a> Grundlegende Inhaltsabfragen  
 Sie können Inhaltsabfragen mit dem Generator für Vorhersageabfragen erstellen, die in SQL Server Management Studio enthaltenen Vorlagen für DMX-Inhaltsabfragen verwenden oder Abfragen direkt in DMX schreiben. Anders als bei Vorhersageabfragen müssen keine externen Daten verknüpft werden, sodass Inhaltsabfragen leicht zu schreiben sind.  
  
 Dieser Abschnitt bietet eine Übersicht über die Typen von Inhaltsabfragen, die Sie erstellen können.  
  
-   Abfragen der Miningstruktur oder der Falldaten liefern eine ausführliche Ansicht der Daten, die für das Training verwendet wurden.  
  
-   Abfragen des Modells können Muster, Attributlisten, Formeln usw. zurückgeben.  
  
###  <a name="bkmk_Structure"></a> Abfragen für Struktur- und Falldaten  
 DMX unterstützt Abfragen für zwischengespeicherte Daten, die zum Erstellen von Miningstrukturen und -modellen verwendet werden. Dieser Cache wird standardmäßig beim Definieren der Miningstruktur erstellt und beim Verarbeiten der Struktur oder des Modells aufgefüllt.  
  
> [!WARNING]  
>  Der Cache kann nicht gelöscht werden, falls Daten in Trainings- und Testsätze unterteilt werden müssen. Wenn der Cache gelöscht wird, können Sie keine Falldaten abfragen.  
  
 In den folgenden Beispielen werden allgemeine Schemas zum Erstellen von Abfragen für Falldaten oder Daten in der Miningstruktur erläutert:  
  
 **Abrufen aller Fälle für ein Modell**  
 `SELECT FROM <model>.CASES`  
  
 Verwenden Sie diese Anweisung, um angegebene Spalten aus den zum Erstellen eines Modells verwendeten Falldaten abzurufen. Sie müssen über Drillthroughberechtigungen für das Modell verfügen, um diese Abfrage auszuführen.  
  
 **Anzeigen aller Daten, die in der Struktur enthalten sind**  
 `SELECT FROM <structure>.CASES`  
  
 Verwenden Sie diese Anweisung, um alle in der Struktur enthaltenen Daten anzuzeigen, einschließlich Spalten, die nicht in einem bestimmten Miningmodell vorhanden sind. Sie müssen über Drillthroughberechtigungen für das Modell sowie für die Struktur verfügen, um Daten aus der Miningstruktur abzurufen.  
  
 **Abrufen des Wertebereichs**  
 `SELECT DISTINCT RangeMin(<column>), RangeMax(<column>) FROM <model>`  
  
 Verwenden Sie diese Anweisung, um den minimalen, maximalen und Mittelwert einer kontinuierlichen Spalte oder der Buckets einer DISCRETIZED-Spalte zu suchen.  
  
 **Abrufen unterschiedlicher Werte**  
 `SELECT DISTINCT <column>FROM <model>`  
  
 Verwenden Sie diese Anweisung, um alle Werte einer DISCRETE-Spalte abzurufen.  Verwenden Sie diese Anweisung nicht für DISCRETIZED-Spalten. Verwenden Sie stattdessen die **RangeMin** -Funktion und die **RangeMax** -Funktion.  
  
 **Suchen der Fälle, die zum Trainieren eines Modells oder einer Struktur verwendet wurden**  
 `SELECT  FROM <mining structure.CASES WHERE IsTrainingCase()`  
  
 Verwenden Sie diese Anweisung, um das vollständige Dataset abzurufen, das zum Trainieren eines Modells verwendet wurde.  
  
 **Suchen der Fälle, die zum Testen eines Modells oder einer Struktur verwendet werden**  
 `SELECT  FROM <mining structure.CASES WHERE IsTestingCase()`  
  
 Verwenden Sie diese Anweisung, um die Daten abzurufen, die zum Testen von Miningmodellen reserviert wurden, die sich auf eine bestimmte Struktur beziehen.  
  
 **Drillthroughs von einem bestimmten Modellmuster zu zugrunde liegenden Falldaten**  
 `SELECT FROM <model>.CASESWHERE IsTrainingCase() AND IsInNode(<node>)`  
  
 Verwenden Sie diese Anweisung, um ausführliche Falldaten von einem trainierten Modell abzurufen. Sie müssen einen bestimmten Knoten angeben: Beispielsweise benötigen Sie die Knoten-ID des Clusters, der spezifischen Verzweigung der Entscheidungsstruktur usw. Außerdem müssen Sie über Drillthroughberechtigungen für das Modell verfügen, um diese Abfrage auszuführen.  
  
###  <a name="bkmk_Patterns"></a> Abfragen für Modellmuster, Statistiken und Attribute  
 Der Inhalt eines Data Mining-Modells ist für viele Zwecke nützlich. Eine Modellinhaltsabfrage bietet folgende Möglichkeiten:  
  
-   Extrahieren von Formeln oder Wahrscheinlichkeiten, um eigene Berechnungen anzustellen.  
  
-   Abrufen der Regeln, die in einem Zuordnungsmodell verwendet werden, um eine Vorhersage zu generieren.  
  
-   Abrufen der Beschreibungen bestimmter Regeln, um die Regeln in einer benutzerdefinierten Anwendung zu verwenden.  
  
-   Anzeigen der von einem Zeitreihenmodell erkannten gleitenden Durchschnitte.  
  
-   Abrufen der Regressionsformel für ein Segment der Trendlinie.  
  
-   Abrufen aussagekräftiger Informationen zu Kunden, die als Teil eines bestimmten Clusters identifiziert wurden.  
  
 In den folgenden Beispielen werden einige allgemeine Schemas zum Erstellen von Abfragen für den Modellinhalt veranschaulicht:  
  
 **Abrufen von Mustern vom Modell**  
 `SELECT FROM <model>.CONTENT`  
  
 Verwenden Sie diese Anweisung, um ausführliche Informationen zu bestimmten Knoten im Modell abzurufen. Abhängig vom Algorithmustyp kann der Knoten Regeln und Formeln, unterstützende Daten und statistische Varianzdaten usw. enthalten.  
  
 **Abrufen der in einem trainierten Modell verwendeten Attribute**  
 `CALL System.GetModelAttributes(<model>)`  
  
 Verwenden Sie diese gespeicherte Prozedur, um die Liste der Attribute abzurufen, die von einem Modell verwendet wurden. Diese Informationen sind beispielsweise hilfreich, um die Attribute zu bestimmen, die aufgrund der Funktionsauswahl ausgeschlossen wurden.  
  
 **Abrufen des in einer Data Mining-Dimension gespeicherten Inhalts**  
 `SELECT FROM <model>.DIMENSIONCONTENT`  
  
 Verwenden Sie diese Anweisung, um die Daten aus einer Data Mining-Dimension abzurufen.  
  
 Dieser Abfragetyp dient hauptsächlich zur internen Verwendung. Allerdings wird diese Funktionalität nicht von allen Algorithmen unterstützt. Die Unterstützung wird von einem Flag im MINING_SERVICES-Schemarowset angegeben.  
  
 Wenn Sie einen eigenen Plug-In-Algorithmus entwickeln, könnten Sie diese Anweisung verwenden, um den Inhalt des Modells zu Testzwecken zu überprüfen.  
  
 **Abrufen der PMML-Darstellung eines Modells**  
 `SELECT * FROM <model>.PMML`  
  
 Ruft ein XML-Dokument ab, das das Modell im PMML-Format darstellt. Nicht alle Modelltypen werden unterstützt.  
  
##  <a name="bkmk_Examples"></a> Beispiele  
 Obwohl bestimmte Modellinhalte bei allen Algorithmen standardmäßig vorhanden sind, hängt der Inhalt des Modells stark vom Algorithmus ab, mit dem das Modell erstellt wurde. Beim Erstellen einer Inhaltsabfrage müssen Sie daher wissen, welche Informationen im Modell für ein spezifisches Modell am aussagekräftigsten sind.  
  
 In diesem Abschnitt werden einige Beispiele bereitgestellt, die veranschaulichen, wie sich die Auswahl des Algorithmus auf die Art von Informationen auswirkt, die im Modell gespeichert werden. Weitere Informationen zu den Miningmodellinhalten und zu den spezifischen Inhalten der einzelnen Modelltypen finden Sie unter [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Assoc"></a> Beispiel 1: Inhaltsabfrage eines Zuordnungsmodells  
 Die Anweisung `SELECT FROM <model>.CONTENT`gibt unterschiedliche Informationen zurück, je nachdem, welcher Modelltyp abgefragt wird. Bei einem Zuordnungsmodell ist eine der wichtigsten Informationen der *Knotentyp*. Knoten sind wie Container für Informationen im Modellinhalt. In einem Zuordnungsmodell haben Knoten, die Regeln repräsentieren, den NODE_TYPE-Wert 8, während Knoten, die Itemsets darstellen, den NODE_TYPE-Wert 7 aufweisen.  
  
 Die folgende Abfrage gibt daher die obersten 10 Itemsets geordnet nach Unterstützung (Standardreihenfolge) zurück.  
  
```  
SELECT TOP 10 NODE_DESCRIPTION, NODE_PROBABILITY, SUPPORT  
FROM <model>.CONTENT WHERE NODE_TYPE = 7  
```  
  
 Die folgende Abfrage baut auf diesen Informationen auf. Die Abfrage gibt drei Spalten zurück: die ID des Knotens, die vollständige Regel und das Produkt auf der rechten Seite des Itemsets, das heißt, das Produkt, das für die Zuordnung mit einem anderen Produkt im Rahmen eines Itemsets vorhergesagt wird.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME, NODE_DESCRIPTION,  
     (SELECT RIGHT(ATTRIBUTE_NAME, (LEN(ATTRIBUTE_NAME)-LEN('Association model name')))   
FROM NODE_DISTRIBUTION  
WHERE LEN(ATTRIBUTE_NAME)>2  
)   
AS RightSideProduct  
FROM [<Association model name>].CONTENT  
WHERE NODE_TYPE = 8   
ORDER BY NODE_SUPPORT DESC  
```  
  
 Das FLATTENED-Schlüsselwort gibt an, dass das geschachtelte Rowset in eine vereinfachte Tabelle konvertiert werden soll. Das Attribut, das das Produkt auf der rechten Seite der Regel darstellt, ist in der NODE_DISTRIBUTION-Tabelle enthalten. Daher rufen wir nur die Zeile ab, die einen Attributnamen enthält. Dazu wird die Anforderung hinzugefügt, dass die Länge größer als zwei sein muss.  
  
 Eine einfache Zeichenfolgenfunktion wird verwendet, um den Namen des Modells aus der dritten Spalte zu entfernen. (Üblicherweise wird den Werten geschachtelter Spalten der Modellname als Präfix vorangestellt.)  
  
 Die WHERE-Klausel gibt an, dass der NODE_TYPE-Wert 8 betragen sollte, um nur Regeln abzurufen.  
  
 Weitere Beispiele finden Sie unter [Beispiele für Zuordnungsmodellabfragen](../../analysis-services/data-mining/association-model-query-examples.md).  
  
###  <a name="bkmk_DecTree"></a> Beispiel 2: Inhaltsabfrage für ein Entscheidungsstrukturmodell  
 Ein Entscheidungsstrukturmodell kann für Vorhersagen und Klassifizierungen verwendet werden.  In diesem Beispiel wird davon ausgegangen, dass Sie mithilfe des Modells ein Ergebnis vorhersagen, aber gleichzeitig ermitteln möchten, welche Faktoren oder Regeln verwendet werden können, um das Ergebnis zu klassifizieren.  
  
 In einem Entscheidungsstrukturmodell werden Knoten verwendet, um sowohl Strukturen als auch Blattknoten darzustellen. Die Beschriftung jedes Knotens enthält die Beschreibung des Pfads zum Ergebnis. Um den Pfad zu einem bestimmten Ergebnis nachzuverfolgen, müssen Sie daher den Knoten identifizieren, der das Ergebnis enthält, und die Details für diesen Knoten abrufen.  
  
 In der Vorhersageabfrage fügen Sie die Vorhersagefunktion [PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md) hinzu, um die ID verwandten Knotens abzurufen, wie im folgenden Beispiel gezeigt:  
  
```  
SELECT  Predict([Bike Buyer]), PredictNodeID([Bike Buyer])   
FROM [<decision tree model name>]  
PREDICTION JOIN   
<input rowset>   
```  
  
 Sobald Sie die ID des Knotens, der das Ergebnis enthält, ermittelt haben, können Sie die Regel oder den Pfad abrufen, der die Vorhersage erklärt. Erstellen Sie dazu eine Inhaltsabfrage, die NODE_CAPTION beinhaltet, wie im Folgenden gezeigt:  
  
```  
SELECT NODE_CAPTION  
FROM [<decision tree model name>]   
WHERE NODE_UNIQUE_NAME= '<node id>'  
```  
  
 Weitere Beispiele finden Sie unter [Beispiele für Entscheidungsstruktur-Modellabfragen](../../analysis-services/data-mining/decision-trees-model-query-examples.md).  
  
##  <a name="bkmk_Results"></a> Arbeiten mit Abfrageergebnissen  
 Wie in den Beispielen veranschaulicht, werden von Inhaltsabfragen am häufigsten Tabellenrowsets zurückgegeben, sie können jedoch auch Informationen aus geschachtelten Spalten enthalten. Sie können das zurückgegebene Rowset zwar vereinfachen, dadurch könnte die Bearbeitung der Ergebnisse jedoch komplexer werden. Besonders der Inhalt des NODE_DISTRIBUTION-Knotens ist geschachtelt, enthält aber viele interessante Informationen zum Modell.  
  
 Weitere Informationen zum Arbeiten mit hierarchischen Rowsets finden Sie in der OLEDB-Spezifikation von MSDN.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zur Select-Anweisung von DMX](../../dmx/understanding-the-dmx-select-statement.md)   
 [Datamining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
