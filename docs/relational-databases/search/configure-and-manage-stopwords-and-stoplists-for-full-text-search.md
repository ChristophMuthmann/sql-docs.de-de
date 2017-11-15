---
title: "Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche | Microsoft-Dokumentation"
ms.custom: 
ms.date: 02/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], noise words
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
caps.latest.revision: "81"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3e72ed3be5d089e5b38c1a33d3772919981f7f99
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche
  Um zu verhindern, dass ein Volltextindex unnötig aufgebläht wird, verfügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] über einen Mechanismus, der häufig vorkommende, für die Suche nutzlose Zeichenfolgen ignoriert. Diese verworfenen Zeichenfolgen werden als *Stoppwörter*bezeichnet. Während der Indexerstellung lässt das Volltextmodul Stoppwörter vom Volltextindex weg. Dies bedeutet, dass Volltextabfragen nicht nach Stoppwörtern suchen.  
   
**Stoppwörter**. Ein Stoppwort kann ein Wort mit einer Bedeutung in einer bestimmten Sprache sein. Beispielsweise werden in der englischen Sprache Wörter wie "a", "and", "is" und "the" im Volltextindex ausgelassen, da sie erfahrungsgemäß keinen Beitrag zur Suche leisten. Ein Stoppwort kann auch ein *Token* ohne linguistische Bedeutung sein.  

**Stopplisten**. Stoppwörter werden über Objekte mit dem Namen "Stoplisten" in Datenbanken verwaltet. Eine *Stoppliste* ist eine Liste mit Stoppwörtern, die, wenn sie einem Volltextindex zugeordnet ist, auf Volltextabfragen für diesen Index angewendet wird.
   
## <a name="use-an-existing-stoplist"></a>Verwenden einer vorhandenen Stoppliste  
 Eine vorhandene Stoppliste können Sie folgendermaßen verwenden:  
  
-   Verwenden Sie die vom System bereitgestellte Stoppliste in der Datenbank. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] umfasst eine Systemstoppliste, die die am häufigsten verwendeten Stoppwörter für jede unterstützte Sprache enthält, d.h. für jede Sprache, die den jeweiligen Wörtertrennungen standardmäßig zugeordnet ist. Sie können die Systemstoppliste kopieren und Ihre Kopie durch das Hinzufügen und Entfernen von Stoppwörtern anpassen.  
  
     Die Systemstoppliste ist in der [Ressourcendatenbank](../../relational-databases/databases/resource-database.md) installiert.  
  
-   Verwenden Sie eine vorhandene benutzerdefinierte Stoppliste aus einer anderen Datenbank in der aktuellen Serverinstanz, und fügen Sie anschließend Stoppwörter nach Bedarf hinzu oder löschen sie sie.  
  
## <a name="create-a-new-stoplist"></a>Erstellen einer neuen Stoppliste 
### <a name="create-a-new-stoplist-with-transact-sql"></a>Erstellen einer neuen Stoppliste mit Transact-SQL
Verwenden Sie [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md).

### <a name="create-a-new-stoplist-with-management-studio"></a>Erstellen einer neuen Stoppliste mit Management Studio
  
1.  Erweitern Sie im Objekt-Explorer den Server.  
  
2.  Erweitern Sie **Datenbanken**, und erweitern Sie dann die Datenbank, in der die Volltext-Stopliste erstellt werden soll.  
  
3.  Erweitern Sie **Speicher**, und klicken Sie dann mit der rechten Maustaste auf **Volltext-Stopplisten**.  
  
4.  Wählen Sie **Neue Volltext-Stoppliste**.  
  
5.  Geben Sie den Namen der neuen Stoppliste ein.  
  
6.  Optional können Sie eine andere Person als Besitzer der Stoppliste angeben.  
  
7.  Wählen Sie eine der folgenden Optionen zur Erstellung der Stoppliste:  
  
    -   **Leere Stoppliste erstellen**  
  
    -   **Aus der Systemstoppliste erstellen**  
  
    -   **Aus vorhandener Volltext-Stoppliste erstellen**  
  
     Weitere Informationen finden Sie unter [Neue Volltext-Stoppliste &#40;Seite 'Allgemein'&#41;](http://msdn.microsoft.com/library/97f8e82d-82ab-4525-91c9-1ee3ae217309).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="use-a-stoplist-in-full-text-queries"></a>Verwenden einer Stoppliste in Volltextabfragen  
 Wenn Sie eine Stoppliste in Abfragen verwenden möchten, müssen Sie diese einem Volltextindex zuordnen. Sie können einem Volltextindex eine Stoppliste zuordnen, wenn Sie den Index erstellen, oder Sie können den Index später ändern, um eine Stoppliste hinzuzufügen.  
  
### <a name="create-a-full-text-index-and-associate-a-stoplist-with-it"></a>Erstellen eines Volltextindexes und Zuordnen zu einer Stoppliste
Verwenden Sie [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).
  
### <a name="associate-or-disassociate-a-stoplist-with-an-existing-full-text-index"></a>Zuordnen oder Aufheben der Zuordnung einer Stoppliste zu einem vorhandenen Volltextindex
Verwenden Sie [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md). 
  
## <a name="change-the-stopwords-in-a-stoplist"></a>Ändern der Stoppwörter in einer Stoppliste  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-transact-sql"></a>Hinzufügen oder Löschen von Stoppwörtern auf einer Stoppliste mit Transact-SQL
Verwenden Sie [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md).
  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-management-studio"></a>Hinzufügen oder Löschen von Stoppwörtern auf einer Stoppliste mit Management Studio  
  
1.  Erweitern Sie im Objekt-Explorer den Server.  
  
2.  Erweitern Sie **Datenbanken**und dann die Datenbank.  
  
3.  Erweitern Sie **Speicher**, und wählen Sie dann **Volltext-Stopplisten**.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Stoppliste, deren Eigenschaften Sie ändern möchten, und wählen Sie **Eigenschaften**aus.  
  
5.  Im Dialogfeld [Volltext-Stopplisten-Eigenschaften](http://msdn.microsoft.com/library/2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f) :  
  
    1.  Wählen Sie im Listenfeld **Aktion** eine der folgenden Aktionen aus: **Stoppwort hinzufügen**, **Stoppwort löschen**, **Alle Stoppwörter löschen**oder **Inhalt der Stoppliste löschen**.  
  
    2.  Wenn das Textfeld **Stoppwort** für die ausgewählte Aktion aktiviert ist, geben Sie ein einzelnes Stoppwort ein. Dieses Stoppwort muss eindeutig sein; das heißt, es darf noch nicht in dieser Stoppliste für die Sprache, die Sie auswählen, enthalten sein.  
  
    3.  Wenn das Listenfeld **Volltextsprache** für die ausgewählte Aktion aktiviert ist, wählen Sie eine Sprache aus.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="manage-stoplists-and-their-usage"></a>Verwalten von Stopplisten und ihre Verwendung
  
### <a name="view-all-the-stopwords-in-a-stoplist"></a>Anzeigen aller Stoppwörter in einer Stoppliste
Verwenden Sie [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md). 
  
### <a name="get-info-about-all-the-stoplists-in-the-current-database"></a>Abrufen von Informationen zu allen Stopplisten in der aktuellen Datenbank
Verwenden Sie [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md) und  [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md).
  
### <a name="view-the-tokenization-result-of-a-word-breaker-thesaurus-and-stoplist-combination"></a>Anzeigen des Tokenisierungsergebnisses einer Kombination aus Wörtertrennung, Thesaurus und Stopplisten
Verwenden Sie [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).

### <a name="suppress-an-error-message-if-stopwords-cause-a-boolean-operation-on-a-full-text-query-to-fail"></a>Unterdrücken einer Fehlermeldung, wenn ein boolescher Vorgang für eine Volltextabfrage aufgrund von Stoppwörtern fehlschlägt
Verwenden Sie die [Füllwörtertransformation (Serverkonfigurationsoption)](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md). 
   
## <a name="more-info-about-stopword-position"></a>Weitere Informationen zur Stoppwortposition
 Obwohl der Volltextindex die Inklusion von Stoppwörtern ignoriert, berücksichtigt er ihre Position. Als Beispiel sei der Ausdruck "Instructions are applicable to these Adventure Works Cycles models" angeführt. In der folgenden Tabelle sind die Positionen der Wörter im Ausdruck angegeben:  
  
|Wort|Position|  
|----------|--------------|  
|Instructions|1|  
|are|2|  
|applicable|3|  
|in|4|  
|these|5|  
|Adventure|6|  
|Works|7|  
|Cycles|8|  
|Modelle|9|  
  
 Die Stoppwörter "are", "to" und "these" an den Positionen 2, 4 und 5 werden im Volltextindex ausgelassen. Die Positionsinformationen bleiben jedoch erhalten, sodass die Positionen der anderen Wörter im Ausdruck unverändert bleiben.   
  
## <a name="upgrade-noise-words-from-sql-server-2005"></a>Aktualisieren von Füllwörtern von SQL Server 2005  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Füllwörter wurden durch Stoppwörter ersetzt. Wenn eine Datenbank von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]aktualisiert wird, werden die Füllwortdateien nicht mehr verwendet. Die Füllwortdateien werden jedoch im Ordner "FTDATA\FTNoiseThesaurusBak" gespeichert, und Sie können sie später beim Aktualisieren oder Erstellen der entsprechenden Stoplisten verwenden. Informationen zum Upgrade von Füllwortdateien auf Stoplisten finden Sie unter [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md).  
  
  
  
