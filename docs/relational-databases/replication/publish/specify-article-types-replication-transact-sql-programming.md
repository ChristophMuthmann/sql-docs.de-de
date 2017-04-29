---
title: Angeben von Artikeltypen (Replikationsprogrammierung mit Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4595c34321877ac16b30a105d1d80f414166c47
ms.lasthandoff: 04/11/2017

---
# <a name="specify-article-types-replication-transact-sql-programming"></a>Angeben von Artikeltypen (Replikationsprogrammierung mit Transact-SQL)
  Die Standardartikeltypen für die Replikation sind Tabellen. Sie können aber auch andere Datenbankobjekte als Artikel veröffentlichen, einschließlich Sichten, gespeicherte Prozeduren, benutzerdefinierte Funktionen und die Ausführung von gespeicherten Prozeduren. Sie können gespeicherte Replikationsprozeduren verwenden, um einen Artikeltyp beim Definieren eines Artikels programmgesteuert anzugeben. Welche Prozeduren Sie verwenden, hängt vom Typ der Replikation und des Artikels ab.  
  
> [!NOTE]  
>  Beim Definieren von Artikeln für Tabellen, Sichten und gespeicherte Prozeduren gibt die Bezeichnung schema only an, dass nur die Objektdefinition repliziert wird.  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a>So veröffentlichen Sie einen Tabellenartikel in einer Transaktions- oder Momentaufnahmeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **logbased** &ndash; ein protokollbasierter Tabellenartikel, der der Standard für die Transaktions- und Momentaufnahmereplikation ist. Die Replikation generiert automatisch die gespeicherte Prozedur, die für das horizontale Filtern verwendet wird, sowie die Sicht, die einen vertikal gefilterten Artikel definiert.  
  
    -   **logbased manualfilter** &ndash; ein protokollbasierter, horizontal gefilterter Artikel, in dem die gespeicherte Prozedur für das horizontale Filtern manuell vom Benutzer erstellt und definiert sowie für **@filter**aus. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **logbased manualview** &ndash; ein protokollbasierter, vertikal gefilterter Artikel, in dem die Sicht, die den vertikal gefilterten Artikel definiert, vom Benutzer erstellt und definiert sowie für **@sync_object**aus. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) und [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **logbased manualboth** &ndash; ein protokollbasierter, horizontal und vertikal gefilterter Artikel, in dem sowohl die gespeicherte Prozedur für das horizontale Filtern als auch die Sicht, die den vertikal gefilterten Artikel definiert, vom Benutzer erstellt und definiert sowie für **@filter** und **@sync_object**angegeben werden. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) und [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Führen Sie für **logbased manualboth** -Artikel und **logbased manualfilter** -Artikel [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) aus, um die gespeicherte Filterprozedur für einen horizontal gefilterten Artikel zu generieren. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Führen Sie für Artikel vom Typ **logbased manualboth**, **logbased manualview**und **logbased manualfilter** [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) aus, um die Sicht zu generieren, die den vertikal gefilterten Artikel definiert. Weitere Informationen finden Sie unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a>So veröffentlichen Sie einen Artikel für eine Sicht oder eine indizierte Sicht in einer Transaktions- oder Momentaufnahmeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **indexed view logbased** &ndash; ein Artikel für eine protokollbasierte, indizierte Sicht. Die Replikation generiert automatisch die gespeicherte Prozedur, die für das horizontale Filtern verwendet wird, sowie die Sicht, die einen vertikal gefilterten Artikel definiert.  
  
    -   **view schema only** &ndash; ein Artikel für eine Sicht vom Typ schema only. Die Basistabelle muss ebenfalls repliziert werden.  
  
    -   **indexed view schema only** &ndash; ein Artikel für eine indizierte Sicht vom Typ schema only. Die Basistabelle muss ebenfalls repliziert werden.  
  
    -   **indexed view logbased manualfilter** &ndash; ein protokollbasierter, horizontal gefilterter Artikel für eine indizierte Sicht, in dem die gespeicherte Prozedur für das horizontale Filtern manuell vom Benutzer erstellt und definiert sowie für **@filter**aus. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **indexed view logbased manualview** &ndash; ein protokollbasierter, gefilterter Artikel für eine indizierte Sicht, in dem die Sicht, die einen vertikal gefilterten Artikel definiert, vom Benutzer erstellt und definiert sowie für **@sync_object**aus. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) und [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **indexed view logbased manualboth** &ndash; ein protokollbasierter, gefilterter Artikel für eine indizierte Sicht, in dem sowohl die gespeicherte Prozedur für das horizontale Filtern als auch die Sicht, die einen vertikal gefilterten Artikel definiert, vom Benutzer erstellt und definiert sowie für **@filter** und **@sync_object**angegeben werden. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) und [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Führen Sie für **logbased manualboth** -Artikel und **logbased manualfilter** -Artikel [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) aus, um die gespeicherte Filterprozedur für einen horizontal gefilterten Artikel zu generieren. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Führen Sie für Artikel vom Typ **logbased manualboth**, **logbased manualview**und **logbased manualfilter** [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) aus, um die Sicht zu generieren, die den vertikal gefilterten Artikel definiert. Weitere Informationen finden Sie unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a>So veröffentlichen Sie einen Artikel für eine gespeicherte Prozedur, für die Ausführung einer gespeicherten Prozedur oder für eine benutzerdefinierte Funktion in einer Transaktions- oder Momentaufnahmeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **proc schema only** &ndash; ein Artikel für eine gespeicherte Prozedur vom Typ schema only.  
  
    -   **proc exec** &ndash; repliziert die Ausführung der gespeicherten Prozedur auf alle Abonnenten des Artikels. Weitere Informationen finden Sie unter [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **serializable proc exec** &ndash; repliziert die Ausführung der gespeicherten Prozedur nur, wenn die Prozedur im Kontext einer serialisierbaren Transaktion ausgeführt wird. Weitere Informationen finden Sie unter [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **func schema only** &ndash; ein Artikel für eine benutzerdefinierte Funktion vom Typ schema only.  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a>So veröffentlichen Sie einen Tabellen- oder Sichtartikel in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)aus. Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **table** &ndash; ein Tabellenartikel.  
  
    -   **indexed view schema only** &ndash; ein Artikel für eine indizierte Sicht vom Typ schema only.  
  
    -   **view schema only** &ndash; ein Artikel für eine Sicht vom Typ schema only.  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a>So veröffentlichen Sie einen Artikel für eine gespeicherte Prozedur oder eine benutzerdefinierte Funktion in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)aus. Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **func schema only** &ndash; ein Artikel für eine benutzerdefinierte Funktion vom Typ schema only.  
  
    -   **proc schema only** &ndash; ein Artikel für eine gespeicherte Prozedur vom Typ schema only.  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
