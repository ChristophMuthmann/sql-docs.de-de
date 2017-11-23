---
title: Sys. dm_exec_describe_first_result_set_for_object (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_describe_first_result_set_for_object_TSQL
- sys.dm_exec_describe_first_result_set_for_object
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_describe_first_result_set_for_object catalog view
ms.assetid: 63b0fde7-95d7-4ad7-a219-a9feacf1bd89
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f09208161dd4b36f1b798925a58fffaa475e6176
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecdescribefirstresultsetforobject-transact-sql"></a>sys.dm_exec_describe_first_result_set_for_object (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Diese dynamische Verwaltungsfunktion akzeptiert eine @object_id als Parameter und beschreibt die erste ergebnismetadaten für das Modul mit dieser ID an. Die @object_id angegeben, kann die ID des werden eine [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur oder eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Trigger. Wenn es sich um die ID eines beliebigen anderen Objekts (z. B. einer Sicht, Tabelle, Funktion oder CLR-Prozedur) handelt, wird in den Fehlerspalten des Ergebnisses ein Fehler angegeben.  
  
 **Sys. dm_exec_describe_first_result_set_for_object** hat die gleiche resultsetdefinition wie [Sys. dm_exec_describe_first_result_set &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) und ähnelt [Sp_describe_first_result_set &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_exec_describe_first_result_set_for_object   
    ( @object_id , @include_browse_information )  
```  
  
## <a name="arguments"></a>Argumente  
 *@object_id*  
 Die @object_id von einem [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur oder eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Trigger. @object_idTyp **Int**.  
  
 *@include_browse_information*  
 @include_browse_informationTyp **Bit**. Bei 1 werden alle Abfragen so analysiert, als ob die FOR BROWSE-Option in der Abfrage enthalten wäre. Gibt zusätzliche Schlüsselspalten und Quelltabelleninformationen zurück.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
 Diese allgemeinen Metadaten werden in den Ergebnismetadaten als Resultset mit einer Zeile für jede Spalte zurückgegeben. Jede Zeile beschreibt den Typ und die NULL-Zulässigkeit der Spalte in dem Format, das im folgenden Abschnitt beschriebenen wird. Wenn die erste Anweisung nicht für alle Steuerelementpfade vorhanden ist, wird ein Resultset mit 0 Zeilen zurückgegeben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit**|Gibt an, ob es sich um eine zusätzliche Spalte für Zwecke der Informationssuche handelt, die nicht im Resultset angezeigt wird.|  
|**column_ordinal**|**int**|Enthält die Ordnungsposition der Spalte im Resultset. Position der ersten Spalte wird mit 1 angegeben werden.|  
|**name**|**sysname**|Enthält den Namen der Spalte, wenn ein Name bestimmt werden kann. Andernfalls NULL.|  
|**is_nullable**|**bit**|Enthält den Wert 1, wenn die Spalte NULL-Werte zulässt, 0, wenn die Spalte keine NULL-Werte zulässt, und -1, wenn nicht ermittelt werden kann, ob die Spalte NULL-Werte zulässt.|  
|**system_type_id**|**int**|Enthält die System_type_id des Datentyps der Spalte, wie in sys.types angegeben. Bei CLR-Typen wird von dieser Spalte der Wert 240 zurückgegeben, obwohl von der system_type_name-Spalte NULL zurückgegeben wird.|  
|**system_type_name**|**nvarchar(256)**|Enthält den Namen des Datentyps. Enthält Argumente, die für den Datentyp der Spalte angegeben wurden (z. B. Länge, Genauigkeit, Skala). Wenn der Datentyp ein benutzerdefinierter Aliastyp ist, wird der zugrunde liegende Systemtyp hier angegeben. Bei einem benutzerdefinierten CLR-Typ wird NULL in dieser Spalte zurückgegeben.|  
|**max_length**|**smallint**|Maximale Länge (in Byte) für die Spalte.<br /><br /> -1 = Spaltendatentyp ist **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, oder **Xml**.<br /><br /> Für **Text** Spalten, die **Max_length** Wert ist 16 oder festlegen, indem **Sp_tableoption 'Text in Row'**.|  
|**Genauigkeit**|**tinyint**|Die Genauigkeit der Spalte, wenn sie auf numerischen Werten basiert. Andernfalls wird 0 zurückgegeben.|  
|**Skalierung**|**tinyint**|Die Skalierung der Spalte, wenn sie auf numerischen Werten basiert. Andernfalls wird 0 zurückgegeben.|  
|**Sortierungsname**|**sysname**|Name der Sortierung der Spalte, wenn diese zeichenbasiert ist. Andernfalls wird NULL zurückgegeben.|  
|**user_type_id**|**int**|Enthält bei CLR- und Aliastypen die user_type_id des Datentyps der Spalte, wie in sys.types angegeben. Andernfalls NULL.|  
|**user_type_database**|**sysname**|Enthält bei CLR- und Aliastypen den Namen der Datenbank, in der der Typ definiert wurde. Andernfalls NULL.|  
|**user_type_schema**|**sysname**|Enthält bei CLR- und Aliastypen den Namen des Schemas, in dem der Typ definiert wurde. Andernfalls NULL.|  
|**user_type_name**|**sysname**|Enthält bei CLR- und Aliastypen den Namen des Typs. Andernfalls NULL.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|Gibt bei CLR-Typen den Namen der Assembly und der Klasse zurück, die den Typ definieren. Andernfalls NULL.|  
|**xml_collection_id**|**int**|Enthält die xml_collection_id des Datentyps für die Spalte, wie in sys.columns angegeben. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML Schema Collection zugeordnet ist.|  
|**xml_collection_database**|**sysname**|Enthält die Datenbank, in der die XML-Schemaauflistung definiert ist, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML Schema Collection zugeordnet ist.|  
|**xml_collection_schema**|**sysname**|Enthält das Schema, in dem die XML-Schemaauflistung definiert ist, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML Schema Collection zugeordnet ist.|  
|**xml_collection_name**|**sysname**|Enthält den Namen der XML-Schemaauflistung, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML Schema Collection zugeordnet ist.|  
|**is_xml_document**|**bit**|Gibt 1 zurück, wenn der zurückgegebene Datentyp XML ist und für diesen Typ garantiert ist, dass es sich um ein vollständiges XML-Dokument (einschließlich eines Stammknotens) handelt, nicht um ein XML-Fragment. Andernfalls wird 0 zurückgegeben.|  
|**is_case_sensitive**|**bit**|Gibt 1 zurück, wenn die Spalte von einem Zeichenfolgentyp ist, bei dem die Groß-/Kleinschreibung beachtet wird, andernfalls 0.|  
|**is_fixed_length_clr_type**|**bit**|Gibt 1 zurück, wenn die Spalte von einem CLR-Typ mit fester Länge ist, andernfalls 0.|  
|**source_server**|**sysname**|Der Name des ursprünglichen Servers, der von der Spalte in diesem Ergebnis zurückgegeben wurde (bei einem Remoteserver). Der Name wird angegeben, wie er in "sys.servers" angezeigt wird.  Gibt NULL zurück, wenn die Spalte auf dem lokalen Server stammt oder wenn es nicht möglich bestimmt, welche Server sie stammt. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**Quelldatenbank**|**sysname**|Der Name der ursprünglichen Datenbank, die von der Spalte in diesem Ergebnis zurückgegeben wird. Gibt NULL zurück, wenn die Datenbank nicht ermittelt werden kann. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**source_schema**|**sysname**|Der Name des ursprünglichen Schemas, das von der Spalte in diesem Ergebnis zurückgegeben wird. Gibt NULL zurück, wenn das Schema nicht bestimmt werden kann. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**source_table**|**sysname**|Der Name der ursprünglichen Tabelle, die von der Spalte in diesem Ergebnis zurückgegeben wird. Gibt NULL zurück, wenn die Tabelle nicht bestimmt werden kann. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**source_column**|**sysname**|Der Name der ursprünglichen Spalte, die von der Spalte in diesem Ergebnis zurückgegeben wird. Gibt NULL zurück, wenn die Spalte nicht bestimmt werden kann. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**is_identity_column**|**bit**|Gibt 1 zurück, wenn die Spalte eine Identitätsspalte ist, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte eine Identitätsspalte ist.|  
|**is_part_of_unique_key**|**bit**|Gibt 1 zurück, wenn die Spalte Teil eines eindeutigen Index (einschließlich UNIQUE- und PRIMARY-Einschränkung) ist, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte Teil eines eindeutigen Indexes ist. Wird nur aufgefüllt, wenn die Suche nach Informationen erforderlich ist.|  
|**is_updateable**|**bit**|Gibt 1 zurück, wenn die Spalte aktualisiert werden kann, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte aktualisiert werden kann.|  
|**is_computed_column**|**bit**|Gibt 1 zurück, wenn die Spalte eine berechnete Spalte, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte eine berechnete Spalte ist.|  
|**is_sparse_column_set**|**bit**|Gibt 1 zurück, wenn die Spalte eine Sparsespalte ist, andernfalls 0. Gibt NULL zurück, wenn nicht ermittelt werden kann, ob die Spalte Teil eines Sparsespaltensatzes ist.|  
|**ordinal_in_order_by_list**|**smallint**|Position der Spalte in der ORDER BY-Liste. Gibt NULL zurück, wenn die Spalte nicht in der ORDER BY-Liste angezeigt wird oder die ORDER BY-Liste nicht eindeutig bestimmt werden kann.|  
|**order_by_list_length**|**smallint**|Die Länge der ORDER BY-Liste. Gibt NULL zurück, wenn keine ORDER BY-Liste vorhanden ist oder die ORDER BY-Liste nicht eindeutig bestimmt werden kann. Beachten Sie, dass dieser Wert für alle von sp_describe_first_result_set zurückgegebenen Zeilen gleich ist.|  
|**order_by_is_descending**|**"smallint" NULL**|Wenn Ordinal_in_order_by_list nicht NULL, ist die **Order_by_is_descending** Spalte meldet die Richtung der ORDER BY-Klausel für diese Spalte. Andernfalls wird NULL gemeldet.|  
|**error_number**|**int**|Enthält die von der Funktion zurückgegebene Fehlernummer. Enthält NULL, wenn in der Spalte kein Fehler aufgetreten ist.|  
|**error_severity**|**int**|Enthält den von der Funktion zurückgegebenen Schweregrad. Enthält NULL, wenn in der Spalte kein Fehler aufgetreten ist.|  
|**error_state**|**int**|Enthält die von der Funktion zurückgegebene Statusmeldung. Wenn kein Fehler ist aufgetreten ist, enthält die Spalte NULL.|  
|**error_message**|**nvarchar(4096)**|Enthält die von der Funktion zurückgegebene Meldung. Wenn kein Fehler aufgetreten ist, enthält die Spalte NULL.|  
|**error_type**|**int**|Enthält eine ganze Zahl, die den zurückgegebenen Fehler darstellt. Wird error_type_desc zugeordnet. Siehe Liste unter Hinweisen.|  
|**error_type_desc zugeordnet**|**nvarchar(60)**|Enthält eine kurze Zeichenfolge in Großbuchstaben, die den zurückgegebenen Fehler darstellt. Wird error_type zugeordnet. Siehe Liste unter Hinweisen.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion verwendet den gleichen Algorithmus wie **Sp_describe_first_result_set**. Weitere Informationen finden Sie unter [Sp_describe_first_result_set &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
 In der folgenden Tabelle werden die Fehlertypen und deren Beschreibungen aufgeführt.  
  
|error_type|error_type|Description|  
|-----------------|-----------------|-----------------|  
|1|MISC|Alle Fehler, die nicht anderweitig beschrieben sind.|  
|2|SYNTAX|Im Batch ist ein Syntaxfehler aufgetreten.|  
|3|CONFLICTING_RESULTS|Das Ergebnis konnte wegen eines Konflikts zwischen zwei möglichen ersten Anweisungen nicht ermittelt werden.|  
|4|DYNAMIC_SQL|Das Ergebnis konnte wegen einer dynamischen SQL-Abfrage nicht ermittelt werden, die potenziell das erste Ergebnis zurückgeben kann.|  
|5|CLR_PROCEDURE|Das Ergebnis konnte nicht ermittelt werden, da eine gespeicherte CLR-Prozedur potenziell das erste Ergebnis zurückgeben kann.|  
|6|CLR_TRIGGER|Das Ergebnis konnte wegen eines dynamischen CLR-Triggers nicht ermittelt werden, der potenziell das erste Ergebnis zurückgeben kann.|  
|7|EXTENDED_PROCEDURE|Das Ergebnis konnte nicht ermittelt werden, da eine erweiterte gespeicherte Prozedur potenziell das erste Ergebnis zurückgeben kann.|  
|8|UNDECLARED_PARAMETER|Das Ergebnis konnte nicht ermittelt werden, da der Datentyp einer oder mehrerer Resultsetspalten potenziell von einem nicht deklarierten Parameter abhängt.|  
|9|RECURSION|Das Ergebnis konnte nicht ermittelt werden, da der Batch eine rekursive Anweisung enthält.|  
|10|TEMPORARY_TABLE|Das Ergebnis konnte nicht ermittelt werden, da der Batch eine temporäre Tabelle enthält, und wird nicht von **Sp_describe_first_result_set** .|  
|11|UNSUPPORTED_STATEMENT|Das Ergebnis konnte nicht ermittelt werden, da der Batch eine Anweisung enthält, die von nicht unterstützt wird **Sp_describe_first_result_set** (z. B., FETCH, REVERT usw.).|  
|12|OBJECT_ID_NOT_SUPPORTED|Die @object_id an die Funktion übergeben wird nicht unterstützt (d. h. keine gespeicherte Prozedur)|  
|13|OBJECT_ID_DOES_NOT_EXIST|Die @object_id übergeben, um die Funktion wurde im Systemkatalog nicht gefunden.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigung zum Ausführen der @tsql Argument.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-metadata-with-and-without-browse-information"></a>A. Zurückgeben von Metadaten mit und ohne Suchinformationen  
 Das folgende Beispiel erstellt eine gespeicherte Prozedur namens TestProc2, die zwei Resultsets zurückgibt. Dann im Beispiel wird, dass veranschaulicht **dm_exec_describe_first_result_set** gibt Informationen über das erste Resultset in der Prozedur, mit und ohne Suchinformationen zurück.  
  
```  
CREATE PROC TestProc2  
AS  
SELECT object_id, name FROM sys.objects ;  
SELECT name, schema_id, create_date FROM sys.objects ;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set_for_object(OBJECT_ID('TestProc2'), 0) ;  
SELECT * FROM sys.dm_exec_describe_first_result_set_for_object(OBJECT_ID('TestProc2'), 1) ;  
GO  
```  
  
### <a name="b-combining-the-sysdmexecdescribefirstresultsetforobject-function-and-a-table-or-view"></a>B. Kombinieren der sys.dm_exec_describe_first_result_set_for_object-Funktion mit einer Tabelle oder Sicht  
 Im folgenden Beispiel wird sowohl die sys.procedures-Systemkatalogsicht und der **Sys. dm_exec_describe_first_result_set_for_object** -Funktion zur Anzeige von Metadaten für die Resultsets aller gespeicherten Prozeduren in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] die Datenbank.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT p.name, r.*   
FROM sys.procedures AS p  
CROSS APPLY sys.dm_exec_describe_first_result_set_for_object(p.object_id, 0) AS r;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_describe_first_result_set &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [Sp_describe_undeclared_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [Sys. dm_exec_describe_first_result_set &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)  
  
  
