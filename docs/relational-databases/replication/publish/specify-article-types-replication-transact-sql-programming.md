---
title: "Angeben von Artikeltypen (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Veröffentlichen [SQL Server-Replikation], Ausführung von gespeicherten Prozeduren"
  - "Artikel [SQL Server-Replikation], Transaktionsreplikationsoptionen"
  - "Artikel [SQL Server-Replikation], Mergereplikationsoptionen"
  - "Gespeicherte Prozeduren [SQL Server-Replikation], veröffentlichen"
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Angeben von Artikeltypen (Replikationsprogrammierung mit Transact-SQL)
  Die Standardartikeltypen für die Replikation sind Tabellen. Sie können aber auch andere Datenbankobjekte als Artikel veröffentlichen, einschließlich Sichten, gespeicherte Prozeduren, benutzerdefinierte Funktionen und die Ausführung von gespeicherten Prozeduren. Sie können gespeicherte Replikationsprozeduren verwenden, um einen Artikeltyp beim Definieren eines Artikels programmgesteuert anzugeben. Welche Prozeduren Sie verwenden, hängt vom Typ der Replikation und des Artikels ab.  
  
> [!NOTE]  
>  Beim Definieren von Artikeln für Tabellen, Sichten und gespeicherte Prozeduren gibt die Bezeichnung schema only an, dass nur die Objektdefinition repliziert wird.  
  
### So veröffentlichen Sie einen Tabellenartikel in einer Transaktions- oder Momentaufnahmeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **Logbased** -ein Protokollbasierter Tabellenartikel, der die Standardeinstellung für die Transaktions-und momentaufnahmereplikation ist. Die Replikation generiert automatisch die gespeicherte Prozedur, die für das horizontale Filtern verwendet wird, sowie die Sicht, die einen vertikal gefilterten Artikel definiert.  
  
    -   **Logbased Manualfilter** -ein Protokollbasierter, horizontal gefilterter Artikel, in dem die gespeicherte Prozedur für das horizontale Filtern manuell erstellt und vom Benutzer definierte und für angegebene **@filter**. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **Logbased Manualview** -ein Protokollbasierter, vertikal gefilterten Artikel, in dem die Ansicht, die den vertikal gefilterten Artikel definiert wird erstellt und vom Benutzer definierte und für angegebene **@sync_object**. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) und [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **Logbased Manualboth** -ein Protokollbasierter, horizontal und vertikal gefilterter Artikel, in denen sowohl die gespeicherte Prozedur für das horizontale Filtern und die Ansicht, die den vertikal gefilterten Artikel definiert erstellt und vom Benutzer definiert sind, und für die angegebene **@filter** und **@sync_object**, bzw.. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) und [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Für **Logbased Manualboth** und **Logbased Manualfilter** Artikel [Sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) die gespeicherte Filterprozedur für einen horizontal gefilterten Artikel zu generieren. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Für **Logbased Manualboth**, **Logbased Manualview**, und **Logbased Manualfilter** Artikel [Sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) zum Generieren der Ansicht, die den vertikal gefilterten Artikel definiert. Weitere Informationen finden Sie unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### So veröffentlichen Sie einen Artikel für eine Sicht oder eine indizierte Sicht in einer Transaktions- oder Momentaufnahmeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **indexed View Logbased** -ein Artikel für protokollbasierte indizierte Sicht. Die Replikation generiert automatisch die gespeicherte Prozedur, die für das horizontale Filtern verwendet wird, sowie die Sicht, die einen vertikal gefilterten Artikel definiert.  
  
    -   **nur** -Artikel für eine nur-Schema-Sicht. Die Basistabelle muss ebenfalls repliziert werden.  
  
    -   **Nur indizierte sichtschema** -ein Artikel nur Schemas indizierte Sicht. Die Basistabelle muss ebenfalls repliziert werden.  
  
    -   **indexed View Logbased Manualfilter** -ein Protokollbasierter, horizontal gefilterter indizierte Sichtartikel, in dem die gespeicherte Prozedur für das horizontale Filtern manuell erstellt und vom Benutzer definierte und für angegebene **@filter**. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **indexed View Logbased Manualview** -ein Protokollbasierter, gefilterter indizierte Sichtartikel, in dem die Ansicht, die einen vertikal gefilterten Artikel definiert wird erstellt und vom Benutzer definierte und für angegebene **@sync_object**. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) und [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **indexed View Logbased Manualboth** -ein Protokollbasierter, gefilterter indizierte Sichtartikel, in denen sowohl die gespeicherte Prozedur für das horizontale Filtern und die Ansicht, die einen vertikal gefilterten Artikel definiert werden erstellt und vom Benutzer definierte und für angegebene **@filter** und **@sync_object**, bzw.. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) und [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Für **Logbased Manualboth** und **Logbased Manualfilter** Artikel [Sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) die gespeicherte Filterprozedur für einen horizontal gefilterten Artikel zu generieren. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Für **Logbased Manualboth**, **Logbased Manualview**, und **Logbased Manualfilter** Artikel [Sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) zum Generieren der Ansicht, die den vertikal gefilterten Artikel definiert. Weitere Informationen finden Sie unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### So veröffentlichen Sie einen Artikel für eine gespeicherte Prozedur, für die Ausführung einer gespeicherten Prozedur oder für eine benutzerdefinierte Funktion in einer Transaktions- oder Momentaufnahmeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **Proc Schema nur** -ein Artikel nur die Schema-gespeicherten Prozedur.  
  
    -   **Proc Exec** -repliziert die Ausführung der gespeicherten Prozedur auf alle Abonnenten des Artikels. Weitere Informationen finden Sie unter [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **Serializable Proc Exec** -repliziert die Ausführung der gespeicherten Prozedur nur, wenn er im Kontext einer serialisierbaren Transaktion ausgeführt wird. Weitere Informationen finden Sie unter [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **Func Schema nur** -einen Artikel lediglich das Schema der benutzerdefinierten Funktion.  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### So veröffentlichen Sie einen Tabellen- oder Sichtartikel in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **Tabelle** -einen Tabellenartikel.  
  
    -   **Nur indizierte sichtschema** -ein Artikel nur Schemas indizierte Sicht.  
  
    -   **nur** -Artikel für eine nur-Schema-Sicht.  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### So veröffentlichen Sie einen Artikel für eine gespeicherte Prozedur oder eine benutzerdefinierte Funktion in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie einen der folgenden Werte für **@type** an, um den Typ des Artikels zu definieren:  
  
    -   **Func Schema nur** -einen Artikel lediglich das Schema der benutzerdefinierten Funktion.  
  
    -   **Proc Schema nur** -ein Artikel nur die Schema-gespeicherten Prozedur.  
  
     Damit wird ein neuer Artikel für die Veröffentlichung definiert. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Siehe auch  
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  