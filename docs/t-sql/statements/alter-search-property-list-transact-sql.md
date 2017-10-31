---
title: ALTER SEARCH PROPERTY LIST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c93a8382bec0746ae3cfb8f43485da53a06184f0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-search-property-list-transact-sql"></a>ALTER SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 Der Name der Eigenschaftenliste, die geändert wird. *List_name* ist ein Bezeichner.  
  
 Um die Namen der vorhandenen Eigenschaftenlisten anzuzeigen, verwenden Sie die [Sys. registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) -Katalogsicht wie folgt:  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
 ADD  
 Fügt eine angegebene Sucheigenschaft der Eigenschaftenliste gemäß *List_name*. Die Eigenschaft ist für die sucheigenschaftenliste registriert. Bevor neu hinzugefügte Eigenschaften für die Eigenschaftensuche verwendet werden können, müssen die zugeordneten Volltextindizes wieder aufgefüllt werden. Weitere Informationen finden Sie unter [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
> [!NOTE]  
>  Um einer sucheigenschaftenliste eine angegebene Sucheigenschaft hinzuzufügen, müssen Sie angeben, die Eigenschaftensatz-GUID (*Property_set_guid*) und ganzzahlige Eigenschafts-ID (*Property_int_id*). Weitere Informationen finden Sie unter "Abrufen von Eigenschaftensatz-GUIDS und -Bezeichnern" weiter unten in diesem Thema.  
  
 *Eigenschaftsname*  
 Gibt den Namen an, der in Volltextabfragen für die Eigenschaft verwendet werden soll. *Property_name* muss die Eigenschaft innerhalb des Eigenschaftensatzes eindeutig bezeichnen. Eigenschaftsnamen können interne Leerzeichen enthalten. Die maximale Länge des *Property_name* beträgt 256 Zeichen. Dieser Name kann ein Benutzerfreundlicher Name, z. B. Autor "oder" Privatadresse oder möglich kanonische Windows-Name der Eigenschaft, z. B. **System.Author** oder **System.Contact.HomeAddress**.  
  
 Entwickler müssen den Wert zu verwenden, Sie für geben *Property_name* bezeichnen die Eigenschaft in der [CONTAINS](../../t-sql/queries/contains-transact-sql.md) Prädikat. Daher beim Hinzufügen einer Eigenschaft, die es wichtig ist, einen Wert angeben, mit dem die von der angegebenen Eigenschaft definierte Eigenschaft aussagekräftig Eigenschaftensatz-GUID (*Property_set_guid*) und Eigenschaftsbezeichner (*Property_int _id*). Weitere Informationen zu Eigenschaftsnamen finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 Verwenden Sie zum Anzeigen der Namen von Eigenschaften, die derzeit vorhanden sind in einer sucheigenschaftenliste der aktuellen Datenbank die [registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) -Katalogsicht wie folgt:  
  
```  
SELECT property_name FROM sys.registered_search_properties;  
```  
  
 PROPERTY_SET_GUID = "*Property_set_guid*"  
 Gibt den Bezeichner des Eigenschaftensatzes an, zu dem die Eigenschaft gehört. Bei diesem handelt es sich um einen global eindeutigen Bezeichner (GUID, Globally Unique Identifier). Informationen zum Abrufen dieses Werts finden Sie weiter unten in diesem Thema unter "Hinweise".  
  
 So zeigen Sie die Eigenschaft Eigenschaftensatz-GUID von Eigenschaften in einer sucheigenschaftenliste der aktuellen Datenbank, verwenden die [registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) -Katalogsicht wie folgt:  
  
```  
SELECT property_set_guid FROM sys.registered_search_properties;  
```  
  
 PROPERTY_INT_ID =*Property_int_id*  
 Gibt die ganze Zahl an, die die Eigenschaft innerhalb des Eigenschaftensatzes identifiziert. Informationen zum Abrufen dieses Werts finden Sie unter "Hinweise".  
  
 Verwenden Sie zum Anzeigen des ganzzahlige Bezeichners der Eigenschaften in einer sucheigenschaftenliste der aktuellen Datenbank die [registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) -Katalogsicht wie folgt:  
  
```  
SELECT property_int_id FROM sys.registered_search_properties;  
```  
  
> [!NOTE]  
>  Eine bestimmte Kombination von *Property_set_guid* und *Property_int_id* in einer sucheigenschaftenliste eindeutig sein. Wenn Sie versuchen, eine vorhandene Kombination hinzuzufügen, kann ALTER SEARCH PROPERTY LIST nicht ordnungsgemäß ausgeführt werden, und es kommt zu einem Fehler. Dies bedeutet, dass Sie nur einen Namen für eine angegebene Eigenschaft definieren können.  
  
 PROPERTY_DESCRIPTION = "*Property_description*"  
 Gibt eine benutzerdefinierte Beschreibung der Eigenschaft an. *Property_description* ist eine Zeichenfolge mit bis zu 512 Zeichen. Diese Option ist optional.  
  
 DROP  
 Löscht die angegebene Eigenschaft aus der Eigenschaftenliste gemäß *List_name*. Durch das Löschen einer Eigenschaft wird ihre Registrierung aufgehoben und Sie können nicht mehr danach suchen.  
  
## <a name="remarks"></a>Hinweise  
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
 Bei der Volltextsuche wird eine Sucheigenschaft anhand der Eigenschaftssatz-GUID und der ganzzahligen Eigenschaften-ID einem Volltextindex zugeordnet. Weitere Informationen zu diesen Eigenschaften zu erhalten, die von Microsoft definiert wurden, finden Sie unter [Suchen von Eigenschaftensatz-GUIDs und ganzzahligen Eigenschaft-IDs für Sucheigenschaften](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md). Weitere Informationen zu Eigenschaften, die von einem unabhängigen Softwareanbieter (ISV) definiert wurden, finden Sie in der Dokumentation des betreffenden Anbieters.  
  
## <a name="making-added-properties-searchable"></a>Hinzugefügte Eigenschaften als durchsuchbar festlegen  
 Durch Hinzufügen einer Sucheigenschaft zu einer Sucheigenschaftenliste wird die Eigenschaft registriert. Eine neu hinzugefügte Eigenschaft kann unmittelbar in angegeben [CONTAINS](../../t-sql/queries/contains-transact-sql.md) Abfragen. Bei Volltextabfragen mit Eigenschaftenbereichen in einer neu hinzugefügten Eigenschaft werden erst dann Dokumente zurückgegeben, wenn der zugeordnete Volltextindex neu aufgefüllt wurde. Z. B. die folgende Eigenschaft im Bereich einer Abfrage für eine neu hinzugefügte Eigenschaft *New_search_property*, erst zurückgegeben, wenn alle Dokumente Volltextindex, der Zieltabelle zugeordnet (*Table_name*) neu aufgefüllt wird:  
  
```  
SELECT column_name  
FROM table_name  
WHERE CONTAINS( PROPERTY( column_name, 'new_search_property' ), 
               'contains_search_condition');  
GO   
```  
  
 Um eine vollständige Auffüllung zu starten, verwenden Sie die folgenden [ALTER FULLTEXT INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-fulltext-index-transact-sql.md) Anweisung:  
  
```  
USE database_name;  
GO  
ALTER FULLTEXT INDEX ON table_name START FULL POPULATION;  
GO  
```  
  
> [!NOTE]  
>  Die Neuauffüllung ist nicht erforderlich, nachdem eine Eigenschaft aus einer Eigenschaftenliste gelöscht wurde, da nur die Eigenschaften, die in der Sucheigenschaftenliste bleiben, für Volltextabfragen verfügbar sind.  
  
## <a name="related-references"></a>Verwandte Verweise  
 **So erstellen eine Liste mit Eigenschaften**  
  
-   [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)  
  
 **So löschen Sie eine Liste mit Eigenschaften**  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
 **Zum Hinzufügen oder entfernen eine Eigenschaftenliste für einen Volltextindex**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **Um eine Auffüllung einen Volltextindex ausführen**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Berechtigungen  
 Erfordert CONTROL-Berechtigungen für die Eigenschaftenliste.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-adding-a-property"></a>A. Hinzufügen einer Eigenschaft  
 Im folgenden Beispiel werden der Eigenschaftenliste `Title` die Eigenschaften `Author`, `Tags` und `DocumentPropertyList` hinzugefügt.  
  
> [!NOTE]  
>  Ein Beispiel, das erstellt `DocumentPropertyList` Eigenschaftenliste finden Sie unter [CREATE SEARCH PROPERTY LIST &#40; Transact-SQL &#41; ](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
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
>  Bevor Sie eine bestimmte Sucheigenschaftenliste für Abfragen mit Eigenschaftenbereichen verwenden können, müssen Sie sie einem Volltextindex zuordnen. Verwenden Sie hierzu eine [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) Anweisung, und geben Sie die SET SEARCH PROPERTY LIST-Klausel.  
  
### <a name="b-dropping-a-property"></a>B. Löschen einer Eigenschaft  
 Im folgenden Beispiel wird die `Comments`-Eigenschaften aus der `DocumentPropertyList`-Eigenschaftenliste gelöscht.  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
DROP 'Comments' ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie die SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [Sys. registered_search_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [Sys. registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [dm_fts_index_keywords_by_property &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Suchen von Eigenschaftensatz-GUIDS und ganzzahligen Eigenschaft-IDs für Sucheigenschaften](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  

