---
title: Erstellen Sie die SEARCH PROPERTY LIST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SEARCH_PROPERTY_LIST_TSQL
- CREATE SEARCH
- CREATE_SEARCH_TSQL
- CREATE_SEARCH_PROPERTY_TSQL
- CREATE SEARCH PROPERTY
- CREATE SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], creating
- CREATE SEARCH PROPERTY LIST statement
ms.assetid: 5440cbb8-3403-4d27-a2f9-8e1f5a1bc12b
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b055be4f948b62553ddbabb40613971a0e5619d8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-search-property-list-transact-sql"></a>CREATE SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Erstellt eine neue Sucheigenschaftenliste. Mit einer Sucheigenschaftenliste können eine oder mehrere Sucheigenschaften angegeben werden, die Sie in einen Volltextindex einschließen möchten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE SEARCH PROPERTY LIST new_list_name  
   [ FROM [ database_name. ] source_list_name ]  
   [ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>Argumente  
 *new_list_name*  
 Der Name der neuen Sucheigenschaftenliste. *New_list_name* ist ein Bezeichner mit maximal 128 Zeichen. *New_list_name* muss innerhalb aller Eigenschaftenlisten in der aktuellen Datenbank eindeutig sein und den Regeln für Bezeichner entsprechen. *New_list_name* wird verwendet, wenn der Volltextindex erstellt wird.  
  
 *database_name*  
 Der Name der Datenbank, in dem die Eigenschaftenliste gemäß *Source_list_name* befindet. Wenn nicht angegeben, *Database_name* Standardwerte auf die aktuelle Datenbank.  
  
 *Database_name* müssen den Namen einer vorhandenen Datenbank angeben. Der Anmeldename für die aktuelle Verbindung muss einer vorhandenen Benutzer-ID in der durch den angegebenen Datenbank zugeordnet werden *Database_name*. Darüber hinaus benötigen Sie die erforderlichen [Berechtigungen](#Permissions) für die Datenbank.  
  
 *source_list_name*  
 Gibt an, dass die neue Eigenschaftenliste erstellt wird, kopieren Sie eine vorhandene Eigenschaftenliste aus *Database_name*. Wenn *Source_list_name* ist nicht vorhanden, CREATE SEARCH PROPERTY LIST mit einem Fehler fehlschlagen. Die Sucheigenschaften in *Source_list_name* werden von geerbt *New_list_name*.  
  
 Autorisierung *Owner_name*  
 Gibt den Namen eines Benutzers oder einer Rolle als Besitzer der Eigenschaftenliste an. *Owner_name* muss der Name einer Rolle, der der aktuelle Benutzer angehört, oder der aktuelle Benutzer muss IMPERSONATE-Berechtigung verfügen, auf *Owner_name*. Wird kein Wert angegeben, wird der aktuelle Benutzer zum Besitzer.  
  
> [!NOTE]  
>  Der Besitzer kann geändert werden, indem die [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]  
>  Informationen zur Eigenschaft Listen im Allgemeinen finden Sie unter [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 Standardmäßig sind neue Sucheigenschaftenlisten leer, und Sie müssen diesen manuell Sucheigenschaften hinzufügen. Sie können jedoch auch eine vorhandene Sucheigenschaftenliste kopieren. In diesem Fall erbt die neue Liste die Sucheigenschaften ihrer Quelle. Sie können die neue Liste jedoch ändern und Sucheigenschaften hinzufügen oder entfernen. Alle Eigenschaften, die zur Zeit der nächsten vollständigen Auffüllung in der Sucheigenschaftenliste vorhanden sind, werden in den Volltextindex aufgenommen.  
  
 Unter jeder der folgenden Bedingungen tritt bei einer CREATE SEARCH PROPERTY LIST-Anweisung ein Fehler auf:  
  
-   Wenn die Datenbank angegeben werden, indem *Database_name* ist nicht vorhanden.  
  
-   Angabe einer Liste von *Source_list_name* ist nicht vorhanden.  
  
-   Wenn Sie nicht über die erforderlichen Berechtigungen verfügen.  
  
 **Zum Hinzufügen oder Entfernen von Eigenschaften aus einer Liste**  
  
-   [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)  
  
-   **So löschen Sie eine Liste mit Eigenschaften**  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
##  <a name="Permissions"></a> Berechtigungen  
 Erfordert CREATE FULLTEXT CATALOG-Berechtigungen in der aktuellen Datenbank sowie REFERENCES-Berechtigungen für jede Datenbank, aus der Sie eine Quelleigenschaftenliste kopieren.  
  
> [!NOTE]  
>  Die REFERENCES-Berechtigung ist erforderlich, um die Liste einem Volltextindex zuzuordnen. Die CONTROL-Berechtigung ist erforderlich, um Eigenschaften hinzuzufügen und zu entfernen oder die Liste zu löschen. REFERENCES-Berechtigungen oder CONTROL-Berechtigungen für die Liste können vom Besitzer der Eigenschaftenliste gewährt werden. Benutzer mit CONTROL-Berechtigung können anderen Benutzern auch eine REFERENCES-Berechtigung erteilen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-an-empty-property-list-and-associating-it-with-an-index"></a>A. Erstellen einer leeren Eigenschaftenliste und Zuordnen zu einem Index  
 Im folgenden Beispiel wird die neue Sucheigenschaftenliste `DocumentPropertyList` erstellt. Anschließend wird ein [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) Anweisung, um den Volltextindex, der die neue Eigenschaftenliste Zuordnen der `Production.Document` -Tabelle in der `AdventureWorks` Datenbank ohne eine Auffüllung ab.  
  
> [!NOTE]  
>  Ein Beispiel, das dieser sucheigenschaftenliste mehrere vordefinierte, bekannte Sucheigenschaften hinzufügt, finden Sie unter [ALTER SEARCH PROPERTY LIST &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-search-property-list-transact-sql.md). Wenn der Liste Sucheigenschaften hinzugefügt wurden, muss der Datenbankadministrator eine weitere ALTER FULLTEXT INDEX-Anweisung mit der START FULL POPULATION-Klausel verwenden.  
  
```  
CREATE SEARCH PROPERTY LIST DocumentPropertyList;  
GO  
USE AdventureWorks2012;  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList  
   WITH NO POPULATION;   
GO   
```  
  
### <a name="b-creating-a-property-list-from-an-existing-one"></a>B. Erstellen einer Eigenschaftenliste aus einer vorhandenen  
 Im folgenden Beispiel wird die neue Sucheigenschaftenliste `JobCandidateProperties` aus der in Beispiel A erstellten Liste `DocumentPropertyList` erstellt, die einem Volltextindex in der Datenbank `AdventureWorks2012` zugeordnet ist. Das Beispiel ordnet dann dem Volltextindex der `HumanResources.JobCandidate`-Tabelle in der `AdventureWorks2012`-Datenbank die neue Eigenschaftenliste mithilfe einer ALTER FULLTEXT INDEX-Anweisung zu. Mit dieser ALTER FULLTEXT INDEX-Anweisung wird eine vollständige Auffüllung gestartet, die das Standardverhalten der SET SEARCH PROPERTY LIST-Klausel darstellt.  
  
```  
CREATE SEARCH PROPERTY LIST JobCandidateProperties 
FROM AdventureWorks2012.DocumentPropertyList;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   SET SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [Sys. registered_search_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [Sys. registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [dm_fts_index_keywords_by_property &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Suchen von Eigenschaftensatz-GUIDS und ganzzahligen Eigenschaft-IDs für Sucheigenschaften](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  

