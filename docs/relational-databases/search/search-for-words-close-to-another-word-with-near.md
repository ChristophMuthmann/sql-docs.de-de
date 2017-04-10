---
title: "Suchen von W&#246;rtern in der N&#228;he eines anderen Worts mit NEAR | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Wortsuchen [Volltextsuche]"
  - "NEAR-Option [Volltextsuche]"
  - "Suche nach Ausdrücken [Volltextsuche]"
  - "NEAR-Suchen [Volltextsuche]"
  - "Volltextsuche [SQL Server], NEAR-Suchen"
  - "Volltextabfragen [SQL Server], Näherung"
  - "Abfragen [Volltextsuche], Näherung"
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
caps.latest.revision: 65
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 63
---
# Suchen von W&#246;rtern in der N&#228;he eines anderen Worts mit NEAR
  Sie können in einem [CONTAINS](../../t-sql/queries/contains-transact-sql.md)-Prädikat oder in einer [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)-Funktion mithilfe eines NEAR-Begriffs nach Wörtern oder Wendungen suchen, die nahe beieinander liegen. Sie können auch die maximale Anzahl von nicht als Suchkriterium festgelegten Begriffen angeben, die zwischen dem ersten und dem letzten Suchbegriff liegen. Außerdem können Sie in einer beliebigen Reihenfolge oder in der angegebenen Reihenfolge nach Wörtern oder Ausdrücken suchen. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SQL Server 2016 unterstützt sowohl den früheren [generischen NEAR-Begriff](#Generic_NEAR) (mittlerweile veraltet) als auch den [benutzerdefinierten NEAR-Begriff](#Custom_NEAR) (neu in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]).  
  
##  <a name="Custom_NEAR"></a> Der benutzerdefinierte NEAR-Begriff  
 Mit dem benutzerdefinierten NEAR-Begriff werden die folgenden neuen Funktionen eingeführt:  
  
-   Sie können die maximale Anzahl von nicht als Suchkriterium angegebenen Begriffen oder den *maximalen Abstand* zwischen dem ersten Suchbegriff und dem letzten Suchbegriff angeben, bei dem eine Übereinstimmung zurückgegeben wird.  
  
-   Wenn Sie die maximale Anzahl von Begriffen angeben, können Sie auch angeben, dass Übereinstimmungen die Suchbegriffe in der angegebenen Reihenfolge enthalten müssen.  
  
 Um als Übereinstimmung zu gelten, muss eine Textzeichenfolge folgende Kriterien erfüllen:  
  
-   Sie muss mit einem der angegebenen Suchbegriffe beginnen und mit einem der anderen angegebenen Suchbegriffe enden.  
  
-   Sie muss alle angegebenen Suchbegriffe enthalten.  
  
-   Die Anzahl der nicht als Suchkriterien angegebenen Begriffe (einschließlich von Stoppwörtern), die zwischen dem ersten Suchbegriff und dem letzten Suchbegriff liegen, muss kleiner oder gleich dem ggf. festgelegten maximalen Abstand sein.  
  
 Die grundlegende Syntax lautet:  
  
 NEAR (  
  
 {  
  
 *search_term* [ ,…*n* ]  
  
 |  
  
 (*search_term* [ ,…*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
  
> [!NOTE]  
>  Weitere Informationen zur <custom_proximity_term>-Syntax finden Sie unter [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md).  
  
 Sie können z. B. innerhalb der zwei Begriffe von 'Smith' wie folgt nach 'John' suchen:  
  
```  
CONTAINS(column_name, 'NEAR((John, Smith), 2)')  
```  
  
 Zwei Beispiele für Übereinstimmungszeichenfolgen sind "`John Jacob Smith`" und "`Smith, John`." Die Zeichenfolge "`John Jones knows Fred Smith`" enthält drei dazwischenliegende Nicht-Suchbegriffe, daher handelt es sich um keine Übereinstimmung.  
  
 Um festzulegen, dass die Begriffe in der angegebenen Reihenfolge gefunden werden müssen, müssen Sie den NEAR-Begriff im Beispiel in `NEAR((John, Smith),2, TRUE).` ändern. Damit wird in zwei Begriffen von "`John`" nach "`Smith`" gesucht, jedoch nur, wenn "`John`" vor "`Smith`" enthalten ist. In einer von links nach rechts geschriebenen Sprache wie Englisch ist "`John Jacob Smith`" ein Beispiel für eine übereinstimmende Zeichenfolge.  
  
 Beachten Sie, dass das Volltextmodul bei von rechts nach links geschriebenen Sprachen (z. B. Arabisch oder Hebräisch) die angegebenen Begriffe in umgekehrter Reihenfolge anwendet. Auch der Objekt-Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] kehrt die Anzeigereihenfolge von angegebenen Wörtern in Sprachen mit einer Leserichtung von rechts nach links automatisch um.  
  
> [!NOTE]  
>  Weitere Informationen finden Sie unter [Weitere Überlegungen zu NEAR-Suchen](#Additional_Considerations) an späterer Stelle in diesem Thema.  
  
### Messen des maximalen Abstands  
 Ein bestimmter maximaler Abstand (z. B. 10 oder 25) gibt an, wie viele Nicht-Suchbegriffe (einschließlich von Stoppwörtern) in einer angegebenen Zeichenfolge zwischen dem Suchbegriff und dem letzten Suchbegriff auftreten können. `NEAR((dogs, cats, "hunting mice"), 3)` gibt z. B. die folgende Zeile zurück, in der die Gesamtzahl der Nicht-Suchbegriffe gleich 3 ist ("`enjoy`", "`but`" und "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 Derselbe NEAR-Begriff würde nicht die folgende Zeile zurückgeben, da der maximale Abstand durch die vier Nicht-Suchbegriffe ("`enjoy`", "`but`", "`usually`" und "`avoid`") überschritten wird:  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
### Kombinieren eines benutzerdefinierten NEAR-Begriffs mit anderen Begriffen  
 Sie können einen benutzerdefinierten NEAR-Begriff mit einigen anderen Begriffen kombinieren. Sie können einen benutzerdefinierten NEAR-Begriff mit AND (&), OR (|) oder AND NOT (&!) mit einem anderen benutzerdefinierten NEAR-Begriff, einem einfachen Begriff oder einem Präfixbegriff kombinieren. Beispiel:  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) AND *Begriff3*')  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) OR *Begriff3*')  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) AND NOT *Begriff3*')  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) AND NEAR((*Begriff3*,*Begriff4*),2)')  
  
-   CONTAINS('NEAR((*Begriff1*,*Begriff2*),5) OR NEAR((*Begriff3*,*Begriff4*),2, TRUE)')  
  
 Beispiel:  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 Sie können einen benutzerdefinierten NEAR-Begriff nicht mit einem generischen NEAR-Begriff (*Begriff1* NEAR *Begriff2*), einem Generierungsbegriff (ISABOUT …) oder einem gewichteten Begriff (FORMSOF …) kombinieren.  
  
### Beispiel: Verwenden des benutzerdefinierten NEAR-Begriffs  
 Im folgenden Beispiel wird die Tabelle `Production.Document` der Beispieldatenbank `AdventureWorks2012` nach allen Dokumentzusammenfassungen durchsucht, bei denen das Wort "reflector" im selben Dokument wie das Wort "bracket" enthalten ist.  
  
```  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 [In diesem Thema](#top)  
  
##  <a name="Additional_Considerations"></a> Weitere Überlegungen zu NEAR-Suchen  
 In diesem Abschnitt werden Aspekte erläutert, die sich sowohl auf generische als auch auf benutzerdefinierte NEAR-Suchen auswirken:  
  
-   Einander überschneidende Vorkommen von Suchbegriffen  
  
     In allen NEAR-Suchen wird ausschließlich nach einander nicht überschneidenden Vorkommen gesucht. Einander überschneidende Vorkommen von Suchbegriffen gelten nie als Übereinstimmungen. Betrachten Sie z. B. den folgenden NEAR-Begriff, der nach "`A`" und "`AA`" sucht, wobei diese Reihenfolge mit einem maximalen Abstand von zwei Begriffen gilt:  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     Die möglichen Übereinstimmungen sind "`AAA`", "`A.AA`" und "`A..AA`". Zeilen, die nur "`AA`" enthalten, sind keine Übereinstimmungen.  
  
    > [!NOTE]  
    >  Sie können Begriffe angeben, die einander überschneiden, z. B. `NEAR("mountain bike", "bike trails")` oder `(NEAR(comfort*, comfortable), 5)`. Durch das Angeben einander überschneidender Begriffe wird die Abfrage komplexer, da die möglichen Übereinstimmungspermutationen vergrößert werden. Wenn Sie eine große Anzahl von einander überschneidenden Begriffen angeben, verfügt die Abfrage möglicherweise nicht über ausreichende Ressourcen, und sie schlägt fehl. Vereinfachen Sie in einem solchen Fall die Abfrage, und führen Sie sie noch einmal aus.  
  
-   Sowohl das generische NEAR als auch das benutzerdefinierte NEAR (unabhängig von der Angabe eines maximalen Abstands) geben den logischen Abstand zwischen Begriffen und nicht deren absoluten Abstand an. Begriffe, die sich innerhalb eines Absatzes innerhalb verschiedener Ausdrücke oder Sätze befinden, werden beispielsweise als weiter voneinander entfernt behandelt als Begriffe im gleichen Ausdruck oder im gleichen Satz, und zwar unabhängig von ihrer tatsächlichen Nähe und unter der Annahme, dass sie weniger verwandt sind. Begriffe in anderen Absätzen werden entsprechend so behandelt, als wären sie noch weiter entfernt. Wenn sich eine Übereinstimmung über das Ende eines Satzes, Absatzes oder Kapitels erstreckt, wird die Lücke, die zum Generieren der Rangfolge eines Dokuments verwendet wird, um 8, 128 bzw. 1024 vergrößert.  
  
-   Auswirkungen von NEAR-Begriffen auf das Generieren der Rangfolge durch die CONTAINSTABLE-Funktion  
  
     Wenn NEAR in der CONTAINSTABLE-Funktion verwendet wird, wirken sich die Anzahl der Treffer in einem Dokument relativ zu seiner Länge sowie der Abstand zwischen dem ersten und dem letzten Suchbegriff in den einzelnen Treffern auf die Rangfolge des jeweiligen Dokuments aus. Wenn für einen generischen NEAR-Begriff die gefundenen Suchbegriffe >50 logische Begriffe auseinander liegen, ist der für ein Dokument zurückgegebene Rang gleich 0 (null). Wenn für einen benutzerdefinierten NEAR-Begriff keine ganze Zahl als maximaler Abstand angegeben ist, erhält ein Dokument, das nur Treffer mit einer Lücke >100 logische Begriffe aufweist, den Rang 0 (null). Weitere Informationen zum Generieren der Rangfolge bei benutzerdefinierten NEAR-Suchen finden Sie unter [Einschränken von Suchergebnissen mit RANK](../../relational-databases/search/limit-search-results-with-rank.md).  
  
-   **Füllwörtertransformation** (Serveroption)  
  
     Der Wert von **Füllwörtertransformation** wirkt sich darauf aus, wie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Stoppwörter behandelt werden, wenn diese in NEAR-Suchen angegeben sind. Weitere Informationen finden Sie unter [Füllwörtertransformation (Serverkonfigurationsoption)](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).  
  
 [In diesem Thema](#top)  
  
##  <a name="Generic_NEAR"></a> Der veraltete generische NEAR-Begriff  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Wir empfehlen, den [benutzerdefinierten NEAR-Begriff](#Custom_NEAR) zu verwenden.  
  
 Ein generischer NEAR-Begriff gibt an, dass die angegebenen Suchbegriffe alle in einem Dokument enthalten sein müssen, damit eine Übereinstimmung zurückgegeben wird, unabhängig von der Anzahl der nicht als Suchkriterium angegebenen Begriffe (der *Abstand* zwischen den Suchbegriffen). Die grundlegende Syntax lautet:  
  
 { *search_term* { NEAR | ~ } *search_term* } [ ,…*n* ]  
  
 In den folgenden Beispielen müssen die Wörter 'fox' und 'chicken' in beliebiger Reihenfolge enthalten sein, damit eine Übereinstimmung zurückgegeben wird:  
  
-   `CONTAINS(column_name, 'fox NEAR chicken')`  
  
-   `CONTAINSTABLE(table_name, column_name, 'fox ~ chicken')`  
  
> [!NOTE]  
>  Informationen zur <generic_proximity_term>-Syntax finden Sie unter [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md).  
  
 Weitere Informationen finden Sie unter [Weitere Überlegungen zu NEAR-Suchen](#Additional_Considerations) an späterer Stelle in diesem Thema.  
  
### Kombinieren eines generischen NEAR-Begriffs mit anderen Begriffen  
 Sie können einen generischen NEAR-Begriff mit AND (&), OR (|) oder AND NOT (&!) mit einem anderen generischen NEAR-Begriff, einem einfachen Begriff oder einem Präfixbegriff kombinieren. Beispiel:  
  
```  
CONTAINSTABLE (Production.ProductDescription,  
   Description,   
   '(light NEAR aluminum) OR  
   (lightweight NEAR aluminum)'  
)  
```  
  
 Sie können keinen generischen NEAR-Begriff mit einem benutzerdefinierten NEAR-Begriff (z. B. `NEAR((term1,term2),5)`), einem gewichteten Begriff (ISABOUT …) oder einem Generierungsbegriff (FORMSOF …) kombinieren.  
  
### Beispiel: Verwenden des generischen NEAR-Begriffs  
 Im folgenden Beispiel wird mit dem generischen NEAR-Begriff in dem Dokument nach dem Wort "reflector" gesucht, in dem auch das Wort "bracket" gesucht wird.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable INNER JOIN  
  CONTAINSTABLE(Production.Document, Document,  
  '(reflector NEAR bracket)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 Beachten Sie, dass Sie die Reihenfolge der Begriffe in CONTAINSTABLE auch umdrehen können und dasselbe Ergebnis erhalten:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(bracket NEAR reflector)' ) AS KEY_TBL  
```  
  
 Sie können das Tildezeichen (~) anstelle des NEAR-Schlüsselworts in der oben dargestellten Abfrage verwenden und erhalten dieselben Ergebnisse:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket)' ) AS KEY_TBL  
```  
  
 Es können mehr als zwei Wörter oder Ausdrücke in den Suchbedingungen angegeben werden. Folgendes kann beispielsweise geschrieben werden:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket ~ installation)' ) AS KEY_TBL  
```  
  
 Dies bedeutet, dass "reflector" im selben Dokument wie "bracket" enthalten sein muss und "bracket" im selben Dokument wie "installation".  
  
 [In diesem Thema](#top)  
  
## Siehe auch  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
  
  