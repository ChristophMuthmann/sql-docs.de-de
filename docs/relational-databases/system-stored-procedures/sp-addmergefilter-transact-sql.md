---
title: Sp_addmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords:
- sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bae5cbac50c347247bba5b0488a7fb70ad8e71a3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spaddmergefilter-transact-sql"></a>sp_addmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einen neuen Mergefilter hinzu, um eine Partition auf der Basis eines Joins mit einer anderen Tabelle zu erstellen. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addmergefilter [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @filtername = ] 'filtername'   
        , [ @join_articlename = ] 'join_articlename'   
        , [ @join_filterclause = ] join_filterclause  
    [ , [ @join_unique_key = ] join_unique_key ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @filter_type = ] filter_type ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, in der der Mergefilter hinzugefügt wird. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article=** ] **"***Artikel***"**  
 Der Name des Artikels, für den der Mergefilter hinzugefügt wird. *Artikel* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@filtername=** ] **"***Filtername***"**  
 Der Name des Filters. *Filtername* ist ein erforderlicher Parameter. *Filtername*ist **Sysname**, hat keinen Standardwert.  
  
 [  **@join_articlename=** ] **"***Join_articlename***"**  
 Ist der übergeordnete Artikel, der gemäß den untergeordneten Artikel *Artikel*, muss verknüpft werden, die vom angegebenen Joinklausel mit *Join_filterclause*, um die Zeilen im untergeordneten Artikel zu bestimmen, die erfüllen das Filterkriterium des Mergefilters. *Join_articlename* ist **Sysname**, hat keinen Standardwert. Der Artikel muss sich in der Veröffentlichung, die vom *Veröffentlichung*.  
  
 [  **@join_filterclause=** ] *Join_filterclause*  
 Die Join-Klausel, die verwendet werden muss, um die angegebenen untergeordneten Artikels zu verknüpfen ist *Artikel*und vom angegebenen übergeordneten Artikels *Join_article*, um das Kriterium des Mergefilters erfüllen Zeilen zu bestimmen. *Join_filterclause* ist **nvarchar(1000)**.  
  
 [  **@join_unique_key=** ] *Join_unique_key*  
 Gibt an, ob der Join zwischen dem untergeordneten Artikel *Artikel*und dem übergeordneten Artikel *Join_article*ist 1: n-, 1: 1, n: 1- oder m: n-. *Join_unique_key* ist **Int**, hat den Standardwert 0. **0** gibt einen n: 1- oder m: n-Join. **1** gibt einen 1: 1- oder 1: n-Join. Dieser Wert ist **1** Wenn bilden die verknüpften Spalten einen eindeutigen Schlüssel in *Join_article*, oder wenn *Join_filterclause* zwischen einem Fremdschlüssel in *Artikel* und einen Primärschlüssel in *Join_article*.  
  
> [!CAUTION]  
>  Legen Sie diesen Parameter nur an **1** , wenn eine Einschränkung für die verknüpfte Spalte in der zugrunde liegenden Tabelle für den übergeordneten Artikel vorliegt, die die Eindeutigkeit sicherstellt. Wenn *Join_unique_key* festgelegt ist, um **1** fälschlicherweise mangelnder Konvergenz der Daten auftreten.  
  
 [  **@force_invalidate_snapshot=** ] *Force_invalidate_snapshot*  
 Bestätigt, dass durch die von dieser gespeicherten Prozedur ausgeführte Aktion möglicherweise eine vorhandene Momentaufnahme ungültig wird. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Mergeartikel nicht die Momentaufnahme ungültig werden. Wenn die gespeicherte Prozedur erkennt, dass die Änderung eine neue Momentaufnahme erforderlich ist, wird eine Fehlermeldung angezeigt, und keine Änderungen vorgenommen.  
  
 **1** gibt an, dass Änderungen am Mergeartikel kann dazu führen, dass die Momentaufnahme ungültig wird, und wenn es sind Abonnements vorhanden, die eine neue Momentaufnahme erfordern die Berechtigung erteilt, die vorhandene Momentaufnahme als veraltet zu markieren und eine neue Momentaufnahme generiert.  
  
 [  **@force_reinit_subscription=** ] *Force_reinit_subscription*  
 Bestätigt, dass die von dieser gespeicherten Prozedur ausgeführte Aktion die erneute Initialisierung vorhandener Abonnements erfordern kann. *Force_reinit_subscription* ist ein **Bit**, hat den Standardwert 0.  
  
 **0** gibt an, dass Änderungen am Mergeartikel nicht werden dazu, dass das Abonnement erneut initialisiert werden. Wenn die gespeicherte Prozedur erkennt, dass die Änderung die erneute Initialisierung von Abonnements erfordert, tritt ein Fehler auf, und es werden keine Änderungen durchgeführt.  
  
 **1** gibt an, dass Änderungen am Mergeartikel bewirken, dass vorhandene Abonnements erneut initialisiert werden, werden und die Berechtigung für den erneuten Initialisierung der Abonnements erteilt.  
  
 [  **@filter_type=** ] *Filter_type*  
 Gibt den Typ des Filters an, der hinzugefügt wird. *Filter_type* ist **"tinyint"**, und kann einen der folgenden Werte.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Nur Joinfilter. Zur Unterstützung von erforderlich [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten.|  
|**2**|Nur logische Datensatzbeziehung.|  
|**3**|Sowohl Joinfilter als auch logische Datensatzbeziehung.|  
  
 Weitere Informationen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addmergefilter** wird bei der Mergereplikation verwendet.  
  
 **Sp_addmergefilter** kann nur mit Tabellenartikeln verwendet werden. Artikel für Sichten und indizierte Sichten werden nicht unterstützt.  
  
 Dieses Verfahren kann auch verwendet werden, um eine logische Beziehung zwischen zwei Artikeln hinzuzufügen, zwischen denen möglicherweise ein Joinfilter vorhanden ist. *Filter_type* wird verwendet, um anzugeben, ob der Mergefilter hinzugefügt wird, einen joinfilter, eine logische Beziehung oder beides ist.  
  
 Um logische Datensätze verwenden zu können, müssen die Veröffentlichung und die Artikel eine Reihe von Anforderungen erfüllen. Weitere Informationen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 Diese Option wird normalerweise für einen Artikel verwendet, in dem ein Fremdschlüsselverweis auf eine veröffentlichte Primärschlüsseltabelle vorhanden ist und in dem für die Primärschlüsseltabelle ein Filter für den Artikel definiert ist. Mithilfe der Teilmenge von Primärschlüsselzeilen werden die Fremdschlüsselzeilen ermittelt, die auf den Abonnenten repliziert werden.  
  
 Wenn die Quelltabellen für zwei veröffentlichte Artikel denselben Tabellenobjektnamen aufweisen, können Sie keinen Joinfilter für die beiden Artikel hinzufügen. In einem solchen Fall kann kein Joinfilter erstellt werden, selbst wenn beide Tabellen im Besitz unterschiedlicher Schemas sind und eindeutige Artikelnamen aufweisen.  
  
 Werden sowohl ein parametrisierter Zeilenfilter als auch ein Joinfilter für einen Tabellenartikel verwendet, ermittelt die Replikation, ob eine Zeile der Partition eines Abonnenten angehört. Dies erfolgt durch das Auswerten der filternden Funktion oder des joinfilters (mithilfe der [OR](../../t-sql/language-elements/or-transact-sql.md) Operator), statt durch Auswerten der Schnittmenge der beiden Bedingungen (mithilfe der [AND](../../t-sql/language-elements/and-transact-sql.md) Operator).  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addmergefilter**.  
  
## <a name="see-also"></a>Siehe auch  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definieren und Ändern eines Verknüpfungsfilters zwischen Mergeartikeln](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [Sp_helpmergefilter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
