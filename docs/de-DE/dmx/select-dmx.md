---
title: SELECT (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SELECT
dev_langs:
- DMX
helpviewer_keywords:
- browsing mining model [Analysis Services]
- TOP clause, SELECT
- FLATTENED option
- predictions [DMX]
- ORDER BY clause [DMX]
- SELECT statement [DMX]
- mining models [Analysis Services], browsing
- statements [DMX], SELECT statement
- WHERE clause, DMX
ms.assetid: 32d9e8fd-796b-4e1c-ae59-73cd6f645485
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c22aff659dc4de5bd5a16cf927aaf391fa856af4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Die **wählen** -Anweisung in der Data Mining Extensions (DMX) ist für die folgenden Aufgaben im Datamining verwendet:  
  
-   Durchsuchen des Inhalts eines vorhandenen Miningmodells  
  
-   Erstellen von Vorhersagen aus einem vorhandenen Miningmodell  
  
-   Erstellen einer Kopie eines vorhandenen Miningmodells  
  
-   Durchsuchen der Miningstruktur  
  
 Obwohl die vollständige Syntax dieser Anweisung komplex ist, können die Hauptklauseln, die für das Durchsuchen eines Modells und der ihm zugrunde liegenden Struktur verwendet werden, wie folgt zusammengefasst werden:  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>FLATTENED  
 Einige Data Mining-Clients unterstützen keine Resultsets in hierarchischem Format von einem Data Mining-Anbieter. Der Client kann möglicherweise keine Hierarchie verwalten oder muss die Ergebnisse in einer einzelnen denormalisierten Tabelle speichern. Sollen die Daten aus geschachtelten Tabellen in vereinfachte Tabellen konvertiert werden, müssen Sie für die Anforderungsergebnisse fordern, dass sie vereinfacht werden.  
  
 Zum Vereinfachen der Abfrageergebnisse verwenden die **wählen** Syntax mit dem **FLATTENED** -Option wie im folgenden Beispiel gezeigt:  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>TOP \<n > und ORDER BY  
 Sie können die Ergebnisse einer Abfrage mithilfe eines Ausdrucks sortieren, und klicken Sie dann eine Teilmenge der Ergebnisse zurückgeben können, indem Sie eine Kombination der **ORDER BY** und **oben** Klauseln. Dies ist hilfreich für Szenarien wie gezieltes Mailing, in dem Sie Ergebnisse nur an die Personen senden möchten, die am wahrscheinlichsten antworten. Sie könnten Sortieren der Ergebnisse einer Vorhersageabfrage nach der vorhersagewahrscheinlichkeit mailing Ziel, und klicken Sie dann nur die oberste zurückgeben \<n > Ergebnisse.  
  
## <a name="select-list"></a>Wählen Sie aus  
 Die  *\<select-Liste >* können Verweise auf skalare Spalten, Vorhersagefunktionen und Ausdrücke enthalten. Welche Optionen verfügbar sind, hängt vom Algorithmus und den folgenden Kontexten ab:  
  
-   Wird eine Miningstruktur oder ein Miningmodell abgefragt?  
  
-   Werden Inhalte oder Fälle abgefragt?  
  
-   Handelt es sich bei den Quelldaten um eine relationale Tabelle oder um einen Cube?  
  
-   Werden Vorhersagen getroffen?  
  
 In vielen Fällen können Sie Aliasse verwenden, oder Sie erstellen einfache Ausdrücke basierend auf den Elementen in der Auswahlliste. Das folgende Beispiel zeigt einen einfachen Ausdruck in Modellspalten:  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 Im folgenden Beispiel wird ein Alias für eine Spalte erstellt, die die Ergebnisse einer Vorhersagefunktion enthält:  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 Sie können einschränken, die Fälle, die von der Abfrage, mithilfe zurückgegeben werden einer **, in denen** Klausel. Die **, in dem** -Klausel gibt an, dass Spaltenverweise im die **, in dem** -Ausdruck muss die gleiche Semantik wie Spaltenverweise im enthalten die  *\<select-Liste >* von der **wählen** -Anweisung und kann nur einen booleschen Ausdruck zurückgeben. Die Syntax für die **, in dem** -Klausel ist wie folgt  
  
```  
WHERE < condition expression >  
```  
  
 Der select-Liste und **, in denen** -Klausel eine **wählen** Anweisung muss die folgenden Regeln:  
  
-   Die Auswahlliste muss einen Ausdruck enthalten, der kein boolesches Ergebnis zurückgibt. Sie können den Ausdruck ändern, aber der Ausdruck muss nicht boolesche Ergebnisse zurückgeben.  
  
-   Die **, in dem** -Klausel muss einen Ausdruck, ein boolesches Ergebnis zurückgibt, enthalten. Sie können die Klausel ändern, aber sie muss ein boolesches Ergebnis zurückgeben.  
  
## <a name="predictions"></a>Vorhersagen (Predictions)  
 Für das Erstellen von Vorhersagen gibt es zwei Syntaxformen:  
  
-   [SELECT FROM &#60;Modell&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM &#60;Modell&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 Mit der ersten Form für Vorhersagen können Sie komplexe Vorhersagen in Echtzeit oder als Batch erstellen.  
  
 Die zweite Vorhersageform erstellt einen leeren PREDICTION JOIN für eine vorhersagbare Spalte in einem Miningmodell und gibt den wahrscheinlichsten Status der Spalte zurück. Die Ergebnisse einer solchen Abfrage basieren vollständig auf dem Inhalt des Miningmodells.  
  
 Sie können eine select-Anweisung in die Quellabfrage einer SELECT FROM PREDICTION JOIN-Anweisung einfügen, indem Sie mit der folgenden Syntax.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 Weitere Informationen zum Erstellen von Vorhersageabfragen finden Sie unter [Struktur und Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md).  
  
## <a name="clause-syntax"></a>Klauselsyntax  
 Wegen der Komplexität zusammen mit den **wählen** -Anweisung, ausführliche Syntaxelemente und Argumente Klauseln beschrieben. Weitere Informationen zu den einzelnen Klauseln erhalten Sie, wenn Sie auf ein Thema in der folgenden Liste klicken:  
  
 [SELECT DISTINCT FROM &#60;Modell &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM &#60;Modell&#62;. Inhalt &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM &#60;Modell&#62;. Fällen &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM &#60;Modell&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM &#60;Modell&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM &#60;Modell&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM &#60;Modell&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM &#60;Struktur&#62;. FÄLLE](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40;DMX&#41; -Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen & #40; DMX & #41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)  
  
  
