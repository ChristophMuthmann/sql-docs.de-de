---
title: ALTER SEARCH PROPERTY LIST (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_SEARCH_PROPERTY_TSQL
- ALTER_SEARCH_PROPERTY_LIST_TSQL
- ALTER SEARCH PROPERTY LIST
- ALTER SEARCH PROPERTY
- ALTER_SEARCH_TSQL
- ALTER SEARCH
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], altering
- ALTER SEARCH PROPERTY LIST statement
ms.assetid: 0436e4a8-ca26-4d23-93f1-e31e2a1c8bfb
caps.latest.revision: 55
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be317f32f0308766e6ad50374d677c2784218ebc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-search-property-list-transact-sql"></a>ALTER SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Fügt der angegebenen Sucheigenschaftenliste eine angegebene Sucheigenschaft hinzu oder entfernt diese daraus.  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER SEARCH PROPERTY LIST list_name  
{  
   ADD 'property_name'  
     WITH   
      (   
          PROPERTY_SET_GUID = 'property_set_guid'  
        , PROPERTY_INT_ID = property_int_id  
      [ , PROPERTY_DESCRIPTION = 'property_description' ]  
      )  
 | DROP 'property_name'   
}  
;  
```  
  
## <a name="arguments"></a>Argumente  
 *list_name*  
 Der Name der Eigenschaftenliste, die geändert wird. *list_name* ist ein Bezeichner.  
  
 Mit der [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)-Katalogsicht können Sie die Namen der vorhandenen Eigenschaftenlisten wie folgt aufrufen:  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
 ADD  
 Fügt der durch *list_name* festgelegte Eigenschaftenliste eine angegebene Sucheigenschaft hinzu. Die Eigenschaft wird für die Sucheigenschaftenliste registriert. Bevor neu hinzugefügte Eigenschaften für die Eigenschaftensuche verwendet werden können, müssen die zugeordneten Volltextindizes wieder aufgefüllt werden. Weitere Informationen finden Sie unter [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
> [!NOTE]  
>  Um einer Sucheigenschaftenliste eine angegebene Sucheigenschaft hinzuzufügen, müssen Sie die Eigenschaftensatz-GUID (*property_set_guid*) und die ganzzahlige Eigenschafts-ID (*property_int_id*) bereitstellen. Weitere Informationen finden Sie unter "Abrufen von Eigenschaftensatz-GUIDS und -Bezeichnern" weiter unten in diesem Thema.  
  
 *property_name*  
 Gibt den Namen an, der in Volltextabfragen für die Eigenschaft verwendet werden soll. *property_name* muss die Eigenschaft innerhalb des Eigenschaftensatzes eindeutig bezeichnen. Eigenschaftsnamen können interne Leerzeichen enthalten. Die maximale Länge von *property_name* beträgt 256 Zeichen. Sie können entweder einen benutzerfreundlichen Namen wie „Autor“ oder „Privatadresse“ oder aber einen kanonischen Windows-Eigenschaftennamen wie **System.Author** oder **System.Contact.HomeAddress** verwenden.  
  
 Entwickler müssen den Wert verwenden, den Sie für *property_name* angeben, damit die Eigenschaft im [CONTAINS](../../t-sql/queries/contains-transact-sql.md)-Prädikat identifiziert werden kann. Daher ist es beim Hinzufügen einer Eigenschaft wichtig, einen Wert anzugeben, durch den die von der angegebenen Eigenschaftensatz-GUID (*property_set_guid*) und dem angegebenen Eigenschaftsbezeichner (*property_int_id*) definierte Eigenschaft aussagekräftig bezeichnet wird. Weitere Informationen zu Eigenschaftsnamen finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 Wenn Sie sich die Namen der Eigenschaften anzeigen lassen möchten, die derzeit in einer Sucheigenschaftenliste der aktuellen Datenbank vorhanden sind, können Sie die [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)-Katalogsicht wie folgt verwenden:  
  
```  
SELECT property_name FROM sys.registered_search_properties;  
```  
  
 PROPERTY_SET_GUID = '*property_set_guid*'  
 Gibt den Bezeichner des Eigenschaftensatzes an, zu dem die Eigenschaft gehört. Bei diesem handelt es sich um einen global eindeutigen Bezeichner (GUID, Globally Unique Identifier). Informationen zum Abrufen dieses Werts finden Sie weiter unten in diesem Thema unter "Hinweise".  
  
 Wenn Sie sich die Eigenschaftensatz-GUID der Eigenschaften anzeigen lassen möchten, die derzeit in einer Sucheigenschaftenliste der aktuellen Datenbank vorhanden sind, können Sie die [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)-Katalogsicht wie folgt verwenden:  
  
```  
SELECT property_set_guid FROM sys.registered_search_properties;  
```  
  
 PROPERTY_INT_ID = *property_int_id*  
 Gibt die ganze Zahl an, die die Eigenschaft innerhalb des Eigenschaftensatzes identifiziert. Informationen zum Abrufen dieses Werts finden Sie unter "Hinweise".  
  
 Wenn Sie sich den ganzzahliger Bezeichner der Eigenschaften anzeigen lassen möchten, die derzeit in einer Sucheigenschaftenliste der aktuellen Datenbank vorhanden sind, können Sie die [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)-Katalogsicht wie folgt verwenden:  
  
```  
SELECT property_int_id FROM sys.registered_search_properties;  
```  
  
> [!NOTE]  
>  Eine bestimmte Kombination von *property_set_guid* und *property_int_id* muss in einer Sucheigenschaftenliste eindeutig sein. Wenn Sie versuchen, eine vorhandene Kombination hinzuzufügen, kann ALTER SEARCH PROPERTY LIST nicht ordnungsgemäß ausgeführt werden, und es kommt zu einem Fehler. Dies bedeutet, dass Sie nur einen Namen für eine angegebene Eigenschaft definieren können.  
  
 PROPERTY_DESCRIPTION = '*property_description*'  
 Gibt eine benutzerdefinierte Beschreibung der Eigenschaft an. *property_description* ist eine Zeichenfolge mit bis zu 512 Zeichen. Diese Option ist optional.  
  
 DROP  
 Löscht die angegebene Eigenschaft aus der Eigenschaftenliste, die durch *list_name* festgelegt wurde. Durch das Löschen einer Eigenschaft wird ihre Registrierung aufgehoben und Sie können nicht mehr danach suchen.  
  
## <a name="remarks"></a>Remarks  
 Jeder Volltextindex kann nur eine Sucheigenschaftenliste aufweisen.  
  
 Um das Abfragen für eine bestimmte Sucheigenschaft zu aktivieren, müssen Sie sie der Sucheigenschaftenliste des Volltextindexes hinzufügen und diesen anschließend neu auffüllen.  
  
 Wenn Sie eine Eigenschaft angeben, können Sie die PROPERTY_SET_GUID, PROPERTY_INT_ID und die PROPERTY_DESCRIPTION-Klausel in Form einer Trennzeichen getrennten Liste in Klammern in beliebiger Reihenfolge angeben. Beispiel:  
  
```  
ALTER SEARCH PROPERTY LIST CVitaProperties  
ADD 'System.Author'   
WITH (   
      PROPERTY_DESCRIPTION = 'Author or authors of a given document.',  
      PROPERTY_SET_GUID   = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',   
      PROPERTY_INT_ID = 4   
      );  
```  
  
> [!NOTE]  
>  In diesem Beispiel wird der Eigenschaftsname `System.Author` verwendet, der dem Konzept kanonischer Eigenschaftsnamen in Windows Vista (kanonischer Windows-Name) ähnlich ist.  
  
## <a name="obtaining-property-values"></a>Abrufen von Eigenschaftswerten  
 Bei der Volltextsuche wird eine Sucheigenschaft anhand der Eigenschaftssatz-GUID und der ganzzahligen Eigenschaften-ID einem Volltextindex zugeordnet. Wie Sie diese Werte für die von Microsoft definierten Eigenschaften erhalten, erfahren Sie unter [Find Property Set GUIDs and Property Integer IDs for Search Properties (Suchen von Eigenschaftensatz-GUIDs und Integer-Eigenschaft-IDs für Sucheigenschaften)](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md). Weitere Informationen zu Eigenschaften, die von einem unabhängigen Softwareanbieter (ISV) definiert wurden, finden Sie in der Dokumentation des betreffenden Anbieters.  
  
## <a name="making-added-properties-searchable"></a>Hinzugefügte Eigenschaften als durchsuchbar festlegen  
 Durch Hinzufügen einer Sucheigenschaft zu einer Sucheigenschaftenliste wird die Eigenschaft registriert. Eine neu hinzugefügte Eigenschaft kann unmittelbar in [CONTAINS](../../t-sql/queries/contains-transact-sql.md)-Abfragen angegeben werden. Bei Volltextabfragen mit Eigenschaftenbereichen in einer neu hinzugefügten Eigenschaft werden erst dann Dokumente zurückgegeben, wenn der zugeordnete Volltextindex neu aufgefüllt wurde. So werden von der folgenden Abfrage mit Eigenschaftenbereich für die neu hinzugefügte Eigenschaft *new_search_property* erst dann Dokumente zurückgegeben, wenn der mit der Zieltabelle *table_name* verknüpfte Volltextindex neu aufgefüllt wird:  
  
```  
SELECT column_name  
FROM table_name  
WHERE CONTAINS( PROPERTY( column_name, 'new_search_property' ), 
               'contains_search_condition');  
GO   
```  
  
 Um eine vollständige Auffüllung zu starten, können Sie in Transact-SQL die folgende [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)-Anweisung verwenden:  
  
```  
USE database_name;  
GO  
ALTER FULLTEXT INDEX ON table_name START FULL POPULATION;  
GO  
```  
  
> [!NOTE]  
>  Die Neuauffüllung ist nicht erforderlich, nachdem eine Eigenschaft aus einer Eigenschaftenliste gelöscht wurde, da nur die Eigenschaften, die in der Sucheigenschaftenliste bleiben, für Volltextabfragen verfügbar sind.  
  
## <a name="related-references"></a>Verwandte Verweise  
 **So erstellen Sie eine Eigenschaftenliste**  
  
-   [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)  
  
 **So löschen Sie eine Eigenschaftenliste:**  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
 **So fügen Sie einem Volltextindex eine Eigenschaftenliste hinzu bzw. so entfernen Sie eine Eigenschaftenliste aus einem Volltextindex:**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **So führen Sie eine Auffüllung für einen Volltextindex aus:**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Berechtigungen  
 Erfordert CONTROL-Berechtigungen für die Eigenschaftenliste.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-adding-a-property"></a>A. Hinzufügen einer Eigenschaft  
 Im folgenden Beispiel werden der Eigenschaftenliste `Title` die Eigenschaften `Author`, `Tags` und `DocumentPropertyList` hinzugefügt.  
  
> [!NOTE]  
>  Ein Beispiel, in dem die Eigenschaftenliste `DocumentPropertyList` erstellt wird, finden Sie unter [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
   ADD 'Title'   
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 2,   
      PROPERTY_DESCRIPTION = 'System.Title - Title of the item.' );  
  
ALTER SEARCH PROPERTY LIST DocumentPropertyList   
    ADD 'Author'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 4,   
      PROPERTY_DESCRIPTION = 'System.Author - Author or authors of the item.' );  
  
ALTER SEARCH PROPERTY LIST DocumentPropertyList   
    ADD 'Tags'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 5,   
      PROPERTY_DESCRIPTION = 
          'System.Keywords - Set of keywords (also known as tags) assigned to the item.' );  
```  
  
> [!NOTE]  
>  Bevor Sie eine bestimmte Sucheigenschaftenliste für Abfragen mit Eigenschaftenbereichen verwenden können, müssen Sie sie einem Volltextindex zuordnen. Verwenden Sie dazu eine [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)-Anweisung, und geben Sie die SET SEARCH PROPERTY LIST-Klausel an.  
  
### <a name="b-dropping-a-property"></a>B. Löschen einer Eigenschaft  
 Im folgenden Beispiel wird die `Comments`-Eigenschaften aus der `DocumentPropertyList`-Eigenschaftenliste gelöscht.  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
DROP 'Comments' ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Suchen von Eigenschaftensatz-GUIDS und ganzzahligen Eigenschaft-IDs für Sucheigenschaften](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  
