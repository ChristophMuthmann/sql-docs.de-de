---
title: "Transformation für Ausdrucksextrahierung | Microsoft Docs"
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
- sql13.dts.designer.termextractiontrans.f1
helpviewer_keywords:
- word boundaries [Integration Services]
- extracting data [Integration Services]
- sentence boundaries
- word extractions [Integration Services]
- Term Extraction transformation
- tagging words
- normalized data [Integration Services]
- tokenizing text [Integration Services]
- parts of speech [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- stemming words [Integration Services]
ms.assetid: d0821526-1603-4ea6-8322-2d901568fbeb
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1aff30861feebd429bf4c061a3b8cff3031c7528
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="term-extraction-transformation"></a>Transformation für Ausdrucksextrahierung
  Die Transformation für Ausdrucksextrahierung extrahiert Ausdrücke aus Text in einer Transformationseingabespalte und schreibt die Ausdrücke dann in eine Transformationsausgabespalte. Diese Transformation ist nur mit englischem Text kompatibel und verwendet ein eigenes englisches Wörterbuch und linguistische Informationen für Englisch.  
  
 Mit der Transformation für Ausdrucksextrahierung können Sie den Inhalt eines Datasets ermitteln. Beispielsweise kann Text in E-Mail-Nachrichten nützliches Feedback zu Produkten enthalten. Sie könnten also mit der Transformation für Ausdrucksextrahierung die betreffenden Themen in den Nachrichten extrahieren und auf diese Weise das Feedback analysieren.  
  
## <a name="extracted-terms-and-data-types"></a>Extrahierte Ausdrücke und Datentypen  
 Die Transformation für Ausdrucksextrahierung kann Nomen und/oder nominale Ausdrücke extrahieren. Ein Nomen ist ein einzelnes Nomen. Ein nominaler Ausdruck besteht aus mindestens zwei Wörtern, von denen eines ein Nomen und das andere ein Nomen oder Adjektiv ist. Wenn z. B. die Transformation nur Nomen extrahiert, werden Ausdrücke wie *bicycle* und *landscape*extrahiert. Wenn dagegen nominale Ausdrücke extrahiert werden, werden Ausdrücke wie *new blue bicycle*, *bicycle helmet*und *boxed bicycles*extrahiert.  
  
 Artikel und Pronomen werden nicht extrahiert. Beispielsweise extrahiert die Transformation für Ausdrucksextrahierung den Ausdruck *bicycle* aus dem Text *the bicycle*, *my bicycle*und *that bicycle*.  
  
 Die Transformation für Ausdrucksextrahierung generiert für jeden extrahierten Ausdruck ein Ergebnis. Das Ergebnis kann ein TFIDF-Wert oder die Häufigkeit sein, mit der der normalisierte Ausdruck in der Ausgabe auftritt. In beiden Fällen wird das Ergebnis durch eine reelle Zahl dargestellt, die größer als 0 ist. Beispielsweise könnte das TFIDF-Ergebnis den Wert 0,5 und die Häufigkeit den Wert 1,0 oder 2,0 aufweisen.  
  
 Die Ausgabe der Transformation für Ausdrucksextrahierung umfasst nur zwei Spalten. Eine Spalte enthält die extrahierten Ausdrücke, und die andere Spalte enthält das Ergebnis. Die Standardnamen der Spalten lauten **Term** und **Score**. Da die Textspalte in der Eingabe mehrere Ausdrücke enthalten kann, weist die Ausgabe der Transformation für Ausdrucksextrahierung in der Regel mehr Zeilen als die Eingabe auf.  
  
 Wenn die extrahierten Ausdrücke in eine Tabelle geschrieben werden, können sie von anderen Suchtransformationen wie z. B. Transformationen für Ausdruckssuche, Transformationen für Fuzzysuche und Transformationen für Suche, verwendet werden.  
  
 Die Transformation für Ausdrucksextrahierung kann nur mit Text in einer Spalte vom Datentyp DT_WSTR oder DT_NTEXT verwendet werden. Wenn eine Spalte Text enthält, aber keinen dieser Datentypen aufweist, kann mit der Transformation für Datenkonvertierung dem Datenfluss eine Spalte vom Datentyp DT_WSTR oder DT_NTEXT hinzugefügt werden, und die Spaltenwerte können in die neue Spalte kopiert werden. Die Ausgabe von der Transformation für Datenkonvertierung kann dann als Eingabe für die Transformation für Ausdrucksextrahierung verwendet werden. Weitere Informationen finden Sie unter [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="exclusion-terms"></a>Ausschlussausdrücke  
 Optional kann die Transformation für Ausdrucksextrahierung auf eine Spalte in einer Tabelle verweisen, die Ausschlussausdrücke enthält. Dabei handelt es sich um Ausdrücke, die von der Transformation beim Extrahieren von Ausdrücken aus einem Dataset ausgelassen werden sollen. Dies ist hilfreich, wenn bereits mehrere Ausdrücke in einer bestimmten Branche als belanglos identifiziert wurden. Dies ist normalerweise der Fall, wenn der Ausdruck so häufig vorkommt, dass er zu einem Füllwort wird. Wenn Sie z. B. Ausdrücke aus einem Dataset extrahieren, das Informationen zum Kundendienst für eine bestimmte Automarke enthält, könnte der Markenname selbst ausgeschlossen werden, weil er zu häufig erwähnt wird und deshalb bedeutungslos ist. Deshalb müssen die Werte in der Ausschlussliste an das von Ihnen verwendete Dataset angepasst werden.  
  
 Wenn Sie der Ausschlussliste einen Ausdruck hinzufügen, werden alle Ausdrücke – Wörter oder Substantivausdrücke –, die den Ausdruck enthalten, ebenfalls ausgeschlossen. Enthält die Ausschlussliste beispielsweise das einzelne Wort *Daten*, werden alle Ausdrücke, die dieses Worte enthalten, wie z. B. *data*, *data mining*, *data integrity*und *data validation* , ebenfalls ausgeschlossen. Wenn Sie nur zusammengesetzte Wörter ausschließen wollen, die das Wort *data*enthalten, müssen Sie diese zusammengesetzten Wörter explizit zur Ausschlussliste hinzufügen. Wenn Sie beispielsweise den Begriff *data*extrahieren, aber *data validation*ausschließen wollen, fügen Sie *data validation* der Ausschlussliste hinzu, und stellen Sie sicher, dass *data* aus der Ausschlussliste entfernt wird.  
  
 Die Verweistabelle muss eine Tabelle in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] - oder einer Access-Datenbank sein. Die Transformation für Ausdrucksextrahierung verwendet eine separate OLE DB-Verbindung, um eine Verbindung mit der Verweistabelle herzustellen. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Die Transformation für Ausdrucksextrahierung wird im vollständigen Zwischenspeicherungsmodus ausgeführt. Zur Laufzeit liest die Transformation für Ausdrucksextrahierung die Ausschlussausdrücke aus der Verweistabelle und speichert sie im privaten Arbeitsspeicher, bevor Transformationseingabezeilen verarbeitet werden.  
  
## <a name="extraction-of-terms-from-text"></a>Extrahieren von Ausdrücken aus Text  
 Die Transformation für Ausdrucksextrahierung führt die folgenden Tasks aus, um Ausdrücke aus Text zu extrahieren.  
  
### <a name="identification-of-words"></a>Identifikation von Wörtern  
 Zunächst identifiziert die Transformation für Ausdrucksextrahierung Wörter durch Ausführen der folgenden Tasks:  
  
-   Untergliedern von Text in Wörter, indem Leerzeichen, Zeilenumbrüche und sonstige Worttrennzeichen aus der englischen Sprache verwendet werden. Satzzeichen wie *?* und *:* sind Zeichen zum Trennen von Wörtern.  
  
-   Beibehalten von Wörtern, die durch Bindestriche oder Unterstriche verbunden sind. Beispielsweise bleiben die Wörter *copy-protected* und *read-only* als ein einziges Wort erhalten.  
  
-   Beibehaltung von Akronymen, die Punkte enthalten. Die *A.B.C* Company würde beispielsweise in die Token **ABC** und **Company**zerlegt.  
  
-   Aufteilen von Wörtern bei Sonderzeichen. Beispielsweise wird das Wort *date/time* als *date* und *time*extrahiert, *(bicycle)* als *bicycle*, und C# wird als C behandelt. Sonderzeichen werden ignoriert und können nicht lexikalisiert werden.  
  
-   Erkennen, wann Sonderzeichen, wie z. B. das Apostroph, Wörter nicht teilen sollten. Beispielsweise wird das Wort *bicycle's* nicht in zwei Wörter geteilt, und ergibt einen einzelnen Ausdruck *bicycle* (Substantiv).  
  
-   Teilen von Zeitausdrücken, Währungsausdrücken, E-Mail-Adressen und Anschriften. Das Datum *January 31, 2004* wird beispielsweise in die drei Tokens *January*, *31*und *2004*unterteilt.  
  
### <a name="tagged-words"></a>Markierte Wörter  
 Im zweiten Schritt kennzeichnet die Transformation für Ausdrucksextrahierung Wörter als eine der folgenden Wortarten:  
  
-   Ein Nomen im Singular. Beispielsweise *bicycle* und *potato*.  
  
-   Ein Nomen im Plural. Beispielsweise *bicycles* und *potatoes*. Für alle Nomen im Plural, die nicht lemmatisiert sind, wird der Wortstamm abgeleitet.  
  
-   Ein Eigenname im Singular. Beispielsweise *April* und *Peter*.  
  
-   Ein Eigenname im Plural. Beispielsweise *Aprils* und *Peters*. Damit für einen Eigennamen die Wortstammerkennung ausgeführt wird, muss er im internen Lexikon vorhanden sein, das auf englische Standardwörter begrenzt ist.  
  
-   Ein Adjektiv. Beispielsweise *blue*.  
  
-   Ein Komparativadjektiv, das zwei Dinge vergleicht. Beispielsweise *higher* und *taller*.  
  
-   Ein Superlativadjektiv, mit dem etwas identifiziert wird, das eine höhere oder niedrigere Qualität im Vergleich zu mindestens zwei anderen Dingen hat. Beispielsweise *highest* und *tallest*.  
  
-   Eine Zahl. Beispielsweise *62* und *2004*.  
  
 Wörter, die nicht zu diesen Wortarten gehören, werden verworfen. Beispielsweise werden Verben und Pronomen verworfen.  
  
> [!NOTE]  
>  Das Kennzeichnen von Wortarten basiert auf einem statistischen Modell und ist möglicherweise nicht hundertprozentig genau.  
  
 Falls die Transformation für Ausdrucksextrahierung so konfiguriert ist, dass nur Nomen extrahiert werden, werden nur die Wörter extrahiert, die als Singular oder Plural von Nomen und Eigennamen gekennzeichnet sind.  
  
 Falls für die Transformation für Ausdrucksextrahierung so konfiguriert ist, dass nur nominale Ausdrücke extrahiert werden, werden Wörter, die als Nomen, Eigennamen, Adjektive und Zahlen gekennzeichnet werden, möglicherweise zu einem nominalen Ausdruck kombiniert. Der Satz muss jedoch mindestens ein Wort enthalten, das als Singular oder Plural eines Nomens oder Eigennamens gekennzeichnet ist. Beispielsweise kombiniert der nominale Ausdruck *highest mountain* ein als Superlativadjektiv (*highest*) und ein als Nomen (*mountain*) gekennzeichnetes Wort.  
  
 Falls für die Transformation für Ausdrucksextrahierung so konfiguriert ist, dass sowohl Nomen als auch nominale Ausdrücke extrahiert werden, gelten die Regeln für Nomen sowie die Regeln für nominale Ausdrücke. Die Transformation extrahiert beispielsweise *bicycle* und *beautiful blue bicycle* aus dem Text *many beautiful blue bicycles*.  
  
> [!NOTE]  
>  Für die extrahierten Ausdrücke gelten weiterhin die maximale Ausdruckslänge und der Häufigkeitsschwellenwert, die von der Transformation verwendet werden.  
  
### <a name="stemmed-words"></a>Auf den Stamm zurückgeführte Wörter  
 Die Transformation für Ausdrucksextrahierung leitet für Nomen den Wortstamm ab, damit nur der Singular eines Nomens extrahiert wird. Beispielsweise extrahiert die Transformation *man* aus *men*, *mouse* aus *mice*und *bicycle* aus *bicycles*. Diese Transformation verwendet das interne Wörterbuch zum Ableiten des Wortstamms. Gerundien werden als Nomen behandelt, wenn sie im Wörterbuch vorhanden sind.  
  
 Die Transformation für Ausdrucksextrahierung erkennt den Wortstamm von Wörtern an ihrer Wörterbuchform, wie in diesen Beispielen gezeigt, und verwendet das interne Wörterbuch der Transformation für Ausdrucksextrahierung.  
  
-   Entfernen von *s* von Substantiven. Beispielsweise wird *bicycles* zu *bicycle*.  
  
-   Entfernen von *es* von Substantiven. Beispielsweise wird *stories* zu *story*.  
  
-   Abrufen des Singulars für unregelmäßige Nomen aus dem Wörterbuch. Beispielsweise wird *geese* zu *goose*.  
  
### <a name="normalized-words"></a>Normalisierte Wörter  
 Die Transformation für Ausdrucksextrahierung normalisiert Ausdrücke, die nur aufgrund ihrer Stellung im Satz groß geschrieben werden, und verwendet stattdessen die Kleinschreibung. In den Sätzen *Dogs chase cats* und *Mountain paths are steep*würden z. B. *Dogs* und *Mountain* in *dog* und *mountain*normalisiert.  
  
 Die Transformation für Ausdrucksextrahierung normalisiert Wörter, damit die groß geschriebene und die klein geschriebene Version von Wörtern nicht als unterschiedliche Ausdrücke behandelt werden. Beispielsweise werden im Text *You see many bicycles in Seattle* und *Bicycles are blue*die Wörter *bicycles* und *Bicycles* als derselbe Ausdruck erkannt, und die Transformation behält nur *bicycle*bei. Eigennamen und Wörter, die nicht im internen Wörterbuch aufgelistet sind, werden nicht normalisiert.  
  
### <a name="case-sensitive-normalization"></a>Normalisierung unter Beachtung der Groß-/Kleinschreibung  
 Die Transformation für Ausdrucksextrahierung kann so konfiguriert werden, dass klein geschriebene und groß geschriebene Wörter als unterschiedliche Ausdrücke oder als unterschiedliche Varianten desselben Ausdrucks betrachtet werden.  
  
-   Wenn für die Transformation die Beachtung der Groß-/Kleinschreibung konfiguriert ist, werden Ausdrücke wie *Method* und *method* als zwei unterschiedliche Ausdrücke extrahiert. Großgeschriebene Wörter, die nicht das erste Wort in einem Satz sind, werden niemals normalisiert und werden als Eigennamen gekennzeichnet.  
  
-   Wenn die Transformation so konfiguriert ist, dass die Groß-/Kleinschreibung nicht beachtet werden soll, werden Ausdrücke wie *Method* und *method* als Varianten eines einzelnen Ausdrucks erkannt. Die Liste der extrahierten Ausdrücke kann *Method* oder *method*einschließen, je nachdem, welches Wort zuerst im Eingabedataset vorkommt. Falls *Method* nur großgeschrieben ist, weil es sich um das erste Wort in einem Satz handelt, wird es in normalisierter Form extrahiert.  
  
## <a name="sentence-and-word-boundaries"></a>Satz- und Wortgrenzen  
 Die Transformation für Ausdrucksextrahierung trennt Text in Sätze, wobei die folgenden Zeichen als Satzgrenzen verwendet werden:  
  
-   ASCII-Zeilenumbruchzeichen 0x0d (Wagenrücklauf) und 0x0a (Zeilenvorschub). Um dieses Zeichen als Satzgrenze zu verwenden, müssen mindestens zwei Zeilenumbruchzeichen in einer Zeile vorhanden sein.  
  
-   Bindestriche (–). Um dieses Zeichen als Satzgrenze zu verwenden, darf weder das Zeichen links noch das Zeichen rechts vom Bindestrich ein Buchstabe sein.  
  
-   Unterstrich (_). Um dieses Zeichen als Satzgrenze zu verwenden, darf weder das Zeichen links noch das Zeichen rechts vom Bindestrich ein Buchstabe sein.  
  
-   Alle Unicode-Zeichen kleiner oder gleich 0x19 oder größer oder gleich 0x7b.  
  
-   Kombinationen aus Zahlen, Satzzeichen und Buchstaben. Beispielsweise gibt *A23B#99* den Ausdruck *A23B*zurück.  
  
-   The characters, %, @, &, $, #, \*, :, ;, ., **,** , !, ?, \<, >, +, =, ^, ~, |, \\, /, (, ), [, ], {, }, “, and ‘.  
  
    > [!NOTE]  
    >  Akronyme, die mindestens einen Punkt (.) enthalten, werden nicht in mehrere Sätze aufgeteilt.  
  
 Die Transformation für Ausdrucksextrahierung trennt dann den Satz in Wörter, wobei die folgenden Wortgrenzen verwendet werden:  
  
-   LeerZchn  
  
-   Registerkarte  
  
-   ASCII 0x0d (Wagenrücklauf)  
  
-   ASCII 0x0a (Zeilenvorschub)  
  
    > [!NOTE]  
    >  Falls ein Apostroph in einem Wort vorkommt und einen Widerspruch darstellt, wie z. B. *we're* oder *it's*, wird das Wort am Apostroph getrennt. Ansonsten werden die Buchstaben nach dem Apostroph gekürzt. Beispielsweise wird *we're* in *we* und *'re*aufgeteilt, und *bicycle's* wird auf *bicycle*gekürzt.  
  
## <a name="configuration-of-the-term-extraction-transformation"></a>Konfiguration der Transformation für Ausdrucksextrahierung  
 Die Transformation für Ausdrucksextrahierung verwendet interne Algorithmen und statische Modelle zum Generieren der Ergebnisse. Möglicherweise müssen Sie die Transformation für Ausdrucksextrahierung mehrmals ausführen und die Ergebnisse überprüfen, um die Transformation so zu konfigurieren, dass für Ihre Text Mining-Lösung die gewünschten Ergebnisse generiert werden.  
  
 Die Transformation für Ausdrucksextrahierung weist eine reguläre Eingabe, eine Ausgabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Transformations-Editor für Ausdrucksextrahierung** festlegen können:  
  
-   [Transformations-Editor für Ausdrucksextrahierung &#40;Registerkarte „Ausdrucksextrahierung“&#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)  
  
-   [Transformations-Editor für Ausdrucksextrahierung &#40;Registerkarte „Ausschluss“&#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-exclusion-tab.md)  
  
-   [Transformations-Editor für Ausdrucksextrahierung &#40;Registerkarte „Erweitert“&#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-advanced-tab.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Informationen zum Festlegen von Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
