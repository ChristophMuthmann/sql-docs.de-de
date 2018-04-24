---
title: Auswählen einer Sprache beim Erstellen eines Volltextindexes | Microsoft Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.prod_service: database-engine, sql-database
ms.component: search
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- languages [full-text search]
- full-text indexes [SQL Server], languages
- international considerations [full-text search]
- stemmers [full-text search]
- global considerations [full-text search]
- full-text search [SQL Server], international considerations
- languages [SQL Server], full-text indexes
- word breakers [full-text search]
ms.assetid: 670a5181-ab80-436a-be96-d9498fbe2c09
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8727bb46905582bb8959dfa9bfc658e4ac0d2bab
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="choose-a-language-when-creating-a-full-text-index"></a>Auswählen einer Sprache beim Erstellen eines Volltextindex

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Wenn Sie einen Volltextindex erstellen, müssen Sie für die indizierte Spalte eine Spaltensprache angeben. Die [Wörtertrennung und Wortstammerkennung](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) der angegebenen Sprache wird von Volltextabfragen für die Spalte verwendet. Bei der Wahl der Spaltensprache für die Erstellung eines Volltextindex sind mehrere Dinge zu bedenken. Diese beziehen sich darauf, wie der Text vom Volltextmodul in Token zerlegt und anschließend indiziert wird.  
  
> [!NOTE]  
>  Um für einen Volltextindex eine Spaltensprache anzugeben, verwenden Sie beim Angeben der Spalte die Klausel *language_term*. Weitere Informationen finden Sie unter [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md) und [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
##  <a name="langsupp"></a> Sprachunterstützung in Volltextsuche  
 Dieser Abschnitt enthält eine Einführung in die Wörtertrennung und Wortstammerkennung und beschreibt, wie die Volltextsuche die LCID der Spaltensprache verwendet.  
  
### <a name="introduction-to-word-breakers-and-stemmers"></a>Einführung in Wörtertrennung und Wortstammerkennung  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höhere Versionen enthalten eine vollständig neue Familie von Wörtertrennungen und Wortstammerkennungen, die im Gegensatz zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]deutlich optimiert wurden.  
  
> [!NOTE]  
>  Die Microsoft Natural Language Group (MS NLG) hat diese neuen linguistischen Komponenten implementiert und bietet dazu Unterstützung an.  
  
 Die neuen Wörtertrennungen bieten die folgenden Vorteile:  
  
-   Stabilität  
  
     Tests haben gezeigt, dass die neuen Wörtertrennungen in anspruchsvollen Abfrageumgebungen stabil arbeiten.  
  
-   Security  
  
     Die neuen Wörtertrennungen sind in SQL Server standardmäßig aktiviert. Dies ist aufgrund von Sicherheitsverbesserungen der linguistischen Komponenten möglich. Es ist sehr zu empfehlen, dass Sie signierte externe Komponenten wie Wörtertrennungen und Filter verwenden, um die Gesamtsicherheit und Stabilität von SQL Server zu verbessern. Sie können Volltext wie folgt konfigurieren, um zu überprüfen, ob diese Komponenten signiert sind:  
  
    ```  
    EXEC sp_fulltext_service 'verify_signature';  
    ```  
  
-   Qualität  
  
     Die Wörtertrennungen wurden neu ausgearbeitet, und Tests haben gezeigt, dass die neuen Wörtertrennungen eine bessere semantische Qualität als ihre Vorgänger aufweisen. Auf diese Weise wird die Genauigkeit von Rückrufen erhöht.  
  
-   Für eine Vielzahl von Sprachen ist die Wörtertrennung standardmäßig in SQL Server enthalten und aktiviert.  
  
 Eine Liste der Sprachen, für die SQL Server eine Wörtertrennung und Wortstammerkennung enthält, finden Sie unter [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
  
### <a name="how-full-text-search-uses-the-name-of-the-column-level-language"></a>Verwenden des Namens der Spaltensprache durch die Volltextsuche  
 Beim Erstellen eines Volltextindex müssen Sie für jede Spalte einen gültigen Sprachennamen angeben. Wenn ein Sprachenname gültig ist, von der Katalogsicht [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) jedoch nicht zurückgegeben wird, greift die Volltextsuche, falls vorhanden, auf einen ähnlichen Sprachennamen der jeweiligen Sprachengruppe zurück. Andernfalls verwendet die Volltextsuche die neutrale Wörtertrennung. Dieses Verhalten kann sich ggf. auf die Genauigkeit der Rückrufe auswirken. Es ist daher sehr zu empfehlen, dass Sie beim Erstellen eines Volltextindex für jede Spalte einen gültigen und verfügbaren Sprachennamen angeben.  
  
> [!NOTE]  
>  Die LCID wird für alle Datentypen verwendet, die für die Volltextindizierung geeignet sind (z.&nbsp;B. **char** oder **nchar**). Auch wenn die Sortierreihenfolge einer Spalte vom Typ **char**, **varchar**oder **text** auf eine andere Sprache als die von der LCID vorgegebenen festgelegt ist, wird die LCID während der Volltextindizierung und -abfrage dieser Spalten trotzdem verwendet.  
  
  
##  <a name="breaking"></a> Worttrennung  
 Bei der Wörtertrennung wird der zu indizierende Text an den sprachspezifischen Wortgrenzen zerlegt. Aus diesem Grund unterscheidet sich das Wörtertrennungsverhalten für die einzelnen Sprachen. Wenn Sie eine Sprache „x“ verwenden, um mehrere Sprachen {x, y und z} zu indizieren, kann es ggf. zu unerwartetem Verhalten und Ergebnissen kommen. Ein Bindestrich (-) oder ein Komma (,) kann z. B. ein Wörtertrennungselement sein, das in einer Sprache verworfen wird, in einer anderen Sprache jedoch beibehalten wird. Außerdem kann ggf. auch unerwartetes Verhalten bei der Wortstammerkennung auftreten, da ein Wort für verschiedene Sprachen unterschiedliche Stämme aufweisen kann. Im Englischen sind Wortgrenzen z.&nbsp;B. meist Leerzeichen oder Satzzeichen. In anderen Sprachen, z.&nbsp;B. Deutsch, können dabei Wörter oder Zeichen kombiniert werden. Daher sollte die gewählte Spaltensprache die Sprache sein, die voraussichtlich in den Zeilen der Spalte gespeichert wird.  
  
### <a name="western-languages"></a>Westliche Sprachen  
 Wenn Sie bei den westlichen Sprachen unsicher sein sollten, welche Sprachen in einer Spalte gespeichert werden, oder wenn in Spalten mehr als eine Sprache gespeichert werden soll, können Sie als Lösung die Wörtertrennung für die komplexeste Sprache verwenden, die voraussichtlich in der Spalte gespeichert wird. Es kann z.&nbsp;B. sein, dass Sie englischen, spanischen und deutschen Text in einer Spalte speichern möchten. Diese drei westlichen Sprachen weisen sehr ähnliche Wörtertrennungsmuster auf, wobei die Muster von Deutsch am komplexesten sind. In diesem Fall wäre also die Wörtertrennung für Deutsch eine gute Wahl, weil auch der englische und spanische Text weitestgehend richtig verarbeitet werden würde. Im Gegensatz dazu würde die Wörtertrennung für Englisch den deutschen Text ggf. nicht richtig verarbeiten, weil im Deutschen viele Komposita verwendet werden.  
  
 Beachten Sie, dass durch die Verwendung der Wörtertrennung der komplexesten Sprache einer Gruppe von Sprachen nicht sichergestellt ist, dass jede Sprache der Gruppe richtig indiziert wird. Es können Ausnahmefälle auftreten, in denen die komplexeste Wörtertrennung Text, der in einer anderen Sprache geschrieben ist, nicht richtig verarbeiten kann.  
  
  
### <a name="non-western-languages"></a>Andere Sprachen als westliche Sprachen  
 Bei anderen Sprachen (wie Chinesisch, Japanisch, Hindi usw.) funktioniert die oben beschriebene Lösung aus linguistischen Gründen nicht immer. Für andere Sprachen als westliche Sprachen können Sie folgende Lösung in Betracht ziehen:  
  
-   Sprachen unterschiedlicher Sprachgruppen  
  
     Wenn eine Spalte sehr unterschiedliche Sprachen enthalten könnte, z.&nbsp;B. Spanisch und Japanisch, sollten Sie überlegen, ob die Sprachen in separaten Spalten gespeichert werden können. Dies würde es Ihnen ermöglichen, für jede Spalte die sprachspezifische Wörtertrennung zu verwenden. Wenn Sie diese Lösung wählen und die Abfragesprache zur Abfragezeit nicht kennen, müssen Sie die Abfrage ggf. für beide Spalten stellen, um sicherzustellen, dass die richtige Zeile bzw. das richtige Dokument gefunden wird.  
  
-   Für binären Inhalt (z.&nbsp;B. Microsoft Word-Dokumente)  
  
     Wenn der indizierte Inhalt den Typ **binary** aufweist, beachtet der Filter für die Volltextsuche, der den Text vor dem Senden an die Wörtertrennung verarbeitet, ggf. die in der binären Daten enthaltenen spezifischen Sprachtags. In diesem Fall gibt der Filter bei der Indizierung die richtige LCID für ein Dokument oder einen Abschnitt eines Dokuments aus. Das Volltextmodul ruft mit dieser LCID dann die Wörtertrennung für die Sprache auf. Nach dem Indizieren von mehrsprachigem Inhalt ist es jedoch ratsam, den Inhalt auf die richtige Indizierung zu überprüfen.  
  
-   Nur-Text-Inhalt  
  
     Wenn Sie Nur-Text-Inhalte verwenden, können Sie diese in den Datentyp **xml** konvertieren und Sprachtags hinzufügen, die für ein Dokument oder einen Dokumentabschnitt jeweils die entsprechende Sprache angeben. Dazu müssen Sie vor der Volltextindizierung jedoch die Sprache kennen.  
  
  
##  <a name="stemming"></a> Wortstammerkennung  
 Ein weiterer Aspekt, den Sie beim Wählen der Spaltensprache berücksichtigen sollten, ist die Wortstammerkennung. Als*Wortstammerkennung* wird bei Volltextabfragen die Suche nach allen Flexionsformen eines Worts in einer bestimmten Sprache bezeichnet. Wenn Sie zum Verarbeiten mehrerer Sprachen eine generische Wörtertrennung verwenden, funktioniert die Wortstammerkennung nur für die Sprache, die für die Spalte angegeben ist, jedoch nicht für andere in der Spalte enthaltene Sprachen. Die Wortstammerkennung für Deutsch funktioniert beispielsweise nicht für Englisch oder Spanisch usw. Dies kann sich je nach Sprache, die Sie zur Abfragezeit auswählen, auf Rückrufvorgänge auswirken.  
  
  
##  <a name="type"></a> Auswirkung des Spaltentyps auf Volltextsuche  
 Ein weiterer Aspekt bei der Wahl der Sprache ist die Art und Weise, wie die Daten dargestellt werden. Für Daten, die nicht in **varbinary(max)** -Spalten gespeichert sind, erfolgt keine spezielle Filterung. Stattdessen durchläuft der Text die Worteinheitenerkennungs-Komponente i. A. unverändert.  
  
 Die Wörtertrennung ist außerdem hauptsächlich für die Verarbeitung von geschriebenem Text konzipiert. Für Text mit speziellen Auszeichnungen (wie z. B. HTML) wird möglicherweise keine große linguistische Genauigkeit bei der Indizierung und Suche erreicht. In diesem Fall haben Sie zwei Möglichkeiten. Die bevorzugte Methode besteht darin, die Textdaten in einer **varbinary(max)** -Spalte zu speichern und den Dokumenttyp anzugeben, sodass die Daten gefiltert werden können. Ist dies nicht machbar, können Sie u.&nbsp;U. die neutrale Wörtertrennung verwenden und ggf. den Füllwortlisten Markupdaten (wie "br" in HTML) hinzufügen.  
  
> [!NOTE]  
>  Eine sprachbasierte Wortstammerkennung ist nicht möglich, wenn Sie die neutrale Sprache angeben.  
  
  
##  <a name="nondef"></a> Angeben einer nicht standardmäßigen Spaltensprache in einer Volltextabfrage  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]analysiert eine Volltextsuche standardmäßig die Abfrageausdrücke, indem die Sprache verwendet wird, die für die einzelnen Spalten angegeben ist, die in der Volltextklausel enthalten sind. Um dieses Verhalten zu überschreiben, geben Sie zur Abfragezeit eine nicht standardmäßige Sprache an. Für unterstützte Sprachen mit installierten Ressourcen können Sie die LANGUAGE *language_term* Klausel einer [CONTAINS](../../t-sql/queries/contains-transact-sql.md)-, [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)-, [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)- oder [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) -Abfrage verwenden, um die Sprache anzugeben, die für die Abfrageausdrücke in Bezug auf Wörtertrennung, Wortstammerkennung, Thesaurus und Stoppwörter genutzt wird.  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
