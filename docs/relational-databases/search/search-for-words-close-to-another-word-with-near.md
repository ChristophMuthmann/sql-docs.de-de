---
title: "Suchen von Wörtern in der Nähe eines anderen Worts mit NEAR | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- word searches [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- proximity searches [full-text search]
- full-text search [SQL Server], proximity searches
- full-text queries [SQL Server], proximity
- queries [full-text search], proximity
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
caps.latest.revision: 65
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aaff4768722fa830cccf9e2ee397945f0866ae07
ms.lasthandoff: 04/11/2017

---
# <a name="search-for-words-close-to-another-word-with-near"></a>Suchen von Wörtern in der Nähe eines anderen Worts mit NEAR
  Sie können in einem [CONTAINS](../../t-sql/queries/contains-transact-sql.md)-Prädikat oder in einer [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)-Funktion mithilfe des *Näherungsbegriffs* **NEAR** nach Wörtern oder Wendungen suchen, die nahe beieinander liegen. 
  
##  <a name="Custom_NEAR"></a> Übersicht über NEAR  
**NEAR** umfasst die folgenden Funktionen:  
-   Sie können die maximale Anzahl von nicht als Suchkriterium festgelegten Begriffen angeben, die zwischen dem ersten und dem letzten Suchbegriff liegen.

-   Sie können in einer beliebigen Reihenfolge oder in einer angegebenen Reihenfolge nach Wörtern oder Ausdrücken suchen.
  
-   Sie können die maximale Anzahl von nicht als Suchkriterium angegebenen Begriffen oder den *maximalen Abstand*zwischen dem ersten Suchbegriff und dem letzten Suchbegriff angeben, bei dem eine Übereinstimmung zurückgegeben wird.  

-   Wenn Sie die maximale Anzahl von Begriffen angeben, können Sie auch angeben, dass Übereinstimmungen die Suchbegriffe in der angegebenen Reihenfolge enthalten müssen.

 
 Um als Übereinstimmung zu gelten, muss eine Textzeichenfolge folgende Kriterien erfüllen:  
  
-   Sie muss mit einem der angegebenen Suchbegriffe beginnen und mit einem der anderen angegebenen Suchbegriffe enden.  
  
-   Sie muss alle angegebenen Suchbegriffe enthalten.  
  
-   Die Anzahl der nicht als Suchkriterien angegebenen Begriffe (einschließlich von Stoppwörtern), die zwischen dem ersten Suchbegriff und dem letzten Suchbegriff liegen, muss kleiner oder gleich dem ggf. festgelegten maximalen Abstand sein.  
  
## <a name="syntax-of-near"></a>Syntax von NEAR
Die grundlegende Syntax von **NEAR** lautet:  

``` 
 NEAR (  
  
 {  
  
 *search_term* [ ,…*n* ]  
  
 |  
  
 (*search_term* [ ,…*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
```

Weitere Informationen zur Syntax finden Sie unter [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md).  

## <a name="examples"></a>Beispiele
### <a name="example-1"></a>Beispiel 1
 Sie können z. B. innerhalb der zwei Begriffe von 'Smith' wie folgt nach 'John' suchen:  
  
```tsql
... CONTAINS(column_name, 'NEAR((John, Smith), 2)')
```  
  
 Zwei Beispiele für Übereinstimmungszeichenfolgen sind "`John Jacob Smith`" und "`Smith, John`." Die Zeichenfolge "`John Jones knows Fred Smith`" enthält drei dazwischenliegende Nicht-Suchbegriffe, daher handelt es sich um keine Übereinstimmung.  
  
 Um festzulegen, dass die Begriffe in der angegebenen Reihenfolge gefunden werden müssen, müssen Sie den NEAR-Begriff im Beispiel in `NEAR((John, Smith),2, TRUE).` ändern. Damit wird in zwei Begriffen von "`John`" nach "`Smith`" gesucht, jedoch nur, wenn "`John`" vor "`Smith`" enthalten ist. In einer von links nach rechts geschriebenen Sprache wie Englisch ist "`John Jacob Smith`" ein Beispiel für eine übereinstimmende Zeichenfolge.  
  
 Beachten Sie, dass das Volltextmodul bei von rechts nach links geschriebenen Sprachen (z. B. Arabisch oder Hebräisch) die angegebenen Begriffe in umgekehrter Reihenfolge anwendet. Auch der Objekt-Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] kehrt die Anzeigereihenfolge von angegebenen Wörtern in Sprachen mit einer Leserichtung von rechts nach links automatisch um.   

### <a name="example-2"></a>Beispiel 2
 Im folgenden Beispiel wird die Tabelle `Production.Document` der Beispieldatenbank `AdventureWorks` nach allen Dokumentzusammenfassungen durchsucht, bei denen das Wort "reflector" im selben Dokument wie das Wort "bracket" enthalten ist.  
  
```tsql
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
``` 
 
## <a name="how-maximum-distance-is-measured"></a>Messen des maximalen Abstands  
 Ein bestimmter maximaler Abstand (z. B. 10 oder 25) gibt an, wie viele Nicht-Suchbegriffe (einschließlich von Stoppwörtern) in einer angegebenen Zeichenfolge zwischen dem Suchbegriff und dem letzten Suchbegriff auftreten können. `NEAR((dogs, cats, "hunting mice"), 3)` gibt z. B. die folgende Zeile zurück, in der die Gesamtzahl der Nicht-Suchbegriffe gleich 3 ist ("`enjoy`", "`but`" und "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 Derselbe NEAR-Begriff würde nicht die folgende Zeile zurückgeben, da der maximale Abstand durch die vier Nicht-Suchbegriffe ("`enjoy`", "`but`", "`usually`" und "`avoid`") überschritten wird:  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
## <a name="combine-near-with-other-terms"></a>Kombinieren von NEAR mit anderen Begriffen  
 Sie können NEAR mit einigen anderen Begriffen kombinieren. Sie können einen benutzerdefinierten NEAR-Begriff mit AND (&), OR (|) oder AND NOT (&!) mit einem anderen benutzerdefinierten NEAR-Begriff, einem einfachen Begriff oder einem Präfixbegriff kombinieren. Zum Beispiel:  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) AND *Begriff3*')  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) OR *Begriff3*')  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) AND NOT *Begriff3*')  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) AND NEAR((*Begriff3*,*Begriff4*),2)')  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) OR NEAR((*Begriff3*,*Begriff4*),2, TRUE)')  
  
 Beispiel:  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 NEAR kann nicht mit einem Generierungsbegriff (ISABOUT …) oder einem gewichteten Begriff (FORMSOF …) kombiniert werden.  
  
##  <a name="Additional_Considerations"></a> Weitere Informationen zur NEAR-Suche  
   
-   Einander überschneidende Vorkommen von Suchbegriffen  
  
     In allen NEAR-Suchen wird ausschließlich nach einander nicht überschneidenden Vorkommen gesucht. Einander überschneidende Vorkommen von Suchbegriffen gelten nie als Übereinstimmungen. Betrachten Sie z. B. den folgenden NEAR-Begriff, der nach "`A`" und "`AA`" sucht, wobei diese Reihenfolge mit einem maximalen Abstand von zwei Begriffen gilt:  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     Die möglichen Übereinstimmungen sind "`AAA`", "`A.AA`" und "`A..AA`". Zeilen, die nur "`AA`" enthalten, sind keine Übereinstimmungen.  
  
    > [!NOTE]  
    >  Sie können Begriffe angeben, die einander überschneiden, z. B. `NEAR("mountain bike", "bike trails")` oder `(NEAR(comfort*, comfortable), 5)`. Durch das Angeben einander überschneidender Begriffe wird die Abfrage komplexer, da die möglichen Übereinstimmungspermutationen vergrößert werden. Wenn Sie eine große Anzahl von einander überschneidenden Begriffen angeben, verfügt die Abfrage möglicherweise nicht über ausreichende Ressourcen, und sie schlägt fehl. Vereinfachen Sie in einem solchen Fall die Abfrage, und führen Sie sie noch einmal aus.  
  
-   NEAR gibt (unabhängig von der Angabe eines maximalen Abstands) den logischen Abstand zwischen Begriffen und nicht deren absoluten Abstand an. Begriffe, die sich innerhalb eines Absatzes innerhalb verschiedener Ausdrücke oder Sätze befinden, werden beispielsweise als weiter voneinander entfernt behandelt als Begriffe im gleichen Ausdruck oder im gleichen Satz, und zwar unabhängig von ihrer tatsächlichen Nähe und unter der Annahme, dass sie weniger verwandt sind. Begriffe in anderen Absätzen werden entsprechend so behandelt, als wären sie noch weiter entfernt. Wenn sich eine Übereinstimmung über das Ende eines Satzes, Absatzes oder Kapitels erstreckt, wird die Lücke, die zum Generieren der Rangfolge eines Dokuments verwendet wird, um 8, 128 bzw. 1024 vergrößert.  
  
-   Auswirkungen von NEAR-Begriffen auf das Generieren der Rangfolge durch die CONTAINSTABLE-Funktion  
  
    Wenn NEAR in der CONTAINSTABLE-Funktion verwendet wird, wirken sich die Anzahl der Treffer in einem Dokument relativ zu seiner Länge sowie der Abstand zwischen dem ersten und dem letzten Suchbegriff in den einzelnen Treffern auf die Rangfolge des jeweiligen Dokuments aus. Wenn für einen generischen NEAR-Begriff die gefundenen Suchbegriffe >50 logische Begriffe auseinander liegen, ist der für ein Dokument zurückgegebene Rang gleich 0 (null). Wenn für einen benutzerdefinierten NEAR-Begriff keine ganze Zahl als maximaler Abstand angegeben ist, erhält ein Dokument, das nur Treffer mit einer Lücke >100 logische Begriffe aufweist, den Rang 0 (null). Weitere Informationen zum Generieren der Rangfolge bei benutzerdefinierten NEAR-Suchen finden Sie unter [Einschränken von Suchergebnissen mit RANK](../../relational-databases/search/limit-search-results-with-rank.md).  
  
-   **Füllwörtertransformation** (Serveroption)  
  
     Der Wert von **Füllwörtertransformation** wirkt sich darauf aus, wie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Stoppwörter behandelt werden, wenn diese in NEAR-Suchen angegeben sind. Weitere Informationen finden Sie unter [Füllwörtertransformation (Serverkonfigurationsoption)](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).   
  
## <a name="see-also"></a>Siehe auch  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md)   

