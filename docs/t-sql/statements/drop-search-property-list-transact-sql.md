---
title: DROP SEARCH PROPERTY LIST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SEARCH_PROPERTY_LIST_TSQL
- DROP SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- DROP SEARCH PROPERTY LIST statement
- search property lists [SQL Server], dropping
- search property lists [SQL Server], deleting
ms.assetid: 7c7ce52a-6b77-4a1c-9abf-d5feb664bea8
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 970fd636239f6de212d667ef6ec22edfa182859c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-search-property-list-transact-sql"></a>DROP SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Löscht eine Eigenschaftenliste aus der aktuellen Datenbank, wenn die Sucheigenschaftenliste derzeit keinem Volltextindex in der Datenbank zugeordnet ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP SEARCH PROPERTY LIST property_list_name  
;  
```  
  
## <a name="arguments"></a>Argumente  
 *property_list_name*  
 Der Name der Sucheigenschaftenliste, die gelöscht werden soll. *Property_list_name* ist ein Bezeichner.  
  
 Um die Namen der vorhandenen Eigenschaftenlisten anzuzeigen, verwenden Sie die [Sys. registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) -Katalogsicht wie folgt:  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
## <a name="remarks"></a>Hinweise  
 Sie können keine Sucheigenschaftenliste aus einer Datenbank löschen, während diese einem Volltextindex zugeordnet ist. Um einer sucheigenschaftenliste aus einem angegebenen Volltextindex zu löschen, verwenden Sie die [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) -Anweisung, und geben Sie die SET SEARCH PROPERTY LIST-Klausel mit Off oder der Namen einer anderen sucheigenschaftenliste.  
  
 **Zum Anzeigen der Eigenschaft enthält, auf einer Serverinstanz**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 **Wenn Sie die Eigenschaft anzeigen Eigenschaftenlisten Volltextindizes zugeordneten**  
  
-   [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
 **So entfernen Sie eine Eigenschaftenliste aus einem Volltextindex**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Berechtigungen  
 Erfordert CONTROL-Berechtigungen für die Sucheigenschaftenliste.  
  
> [!NOTE]  
>  Der Besitzer der Eigenschaftenliste kann CONTROL-Berechtigungen für die Liste erteilen. Besitzer der Sucheigenschaftenliste ist standardmäßig der Benutzer, der sie erstellt. Der Besitzer kann geändert werden, indem die [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `JobCandidateProperties`-Eigenschaftenliste aus der `AdventureWorks2012`-Datenbank gelöscht.  
  
```  
DROP SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [Erstellen Sie die SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Sys. registered_search_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [Sys. registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
  

