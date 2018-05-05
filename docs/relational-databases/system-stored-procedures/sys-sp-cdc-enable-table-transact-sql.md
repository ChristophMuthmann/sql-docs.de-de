---
title: Sys. sp_cdc_enable_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_enable_table_TSQL
- sp_cdc_enable_table_TSQL
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
ms.assetid: 26150c09-2dca-46ad-bb01-3cb3165bcc5d
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1cc9100153d04de7820c210142ae425801cccf95
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysspcdcenabletable-transact-sql"></a>sys.sp_cdc_enable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktiviert Change Data Capture für die angegebene Quelltabelle in der aktuellen Datenbank. Wenn eine Tabelle für Change Data Capture aktiviert ist, wird für jeden Vorgang der Datenbearbeitungssprache (Data Manipulation Language, DML), der auf die Tabelle angewendet wird, ein Datensatz in das Transaktionsprotokoll geschrieben. Der Change Data Capture-Prozess ruft diese Informationen aus dem Protokoll ab und schreibt sie in die Änderungstabellen, auf die über eine Reihe von Funktionen zugegriffen wird.  
  
 Change Data Capture ist nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_cdc_enable_table   
  [ @source_schema = ] 'source_schema',   
  [ @source_name = ] 'source_name' ,  [,[ @capture_instance = ] 'capture_instance' ]  
  [,[ @supports_net_changes = ] supports_net_changes ]  
  , [ @role_name = ] 'role_name'  
  [,[ @index_name = ] 'index_name' ]  
  [,[ @captured_column_list = ] 'captured_column_list' ]  
  [,[ @filegroup_name = ] 'filegroup_name' ]  
  [,[ @allow_partition_switch = ] 'allow_partition_switch' ]  
  [;]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@source_schema =** ] **"***Source_schema***"**  
 Der Name des Schemas, zu dem die Quelltabelle gehört. *Source_schema* ist **Sysname**, hat keinen Standardwert und darf nicht NULL sein.  
  
 [  **@source_name =** ] **"***Source_name***"**  
 Entspricht dem Namen der Quelltabelle, in der Change Data Capture zu aktivieren ist. *Source_name* ist **Sysname**, hat keinen Standardwert und darf nicht NULL sein.  
  
 *Source_name* muss in der aktuellen Datenbank vorhanden sein. Tabellen in der **cdc** Schema kann nicht für Change Data Capture aktiviert werden.  
  
 [  **@role_name =** ] **"***Rollenname***"**  
 Entspricht dem Namen der Datenbankrolle zum Sperren des Zugriffs auf die Änderungsdaten. *Rollenname* ist **Sysname** und muss angegeben werden. Wenn der Parameter explizit auf NULL festgelegt ist, wird keine Gatingrolle verwendet, um den Zugriff auf Änderungsdaten einzuschränken.  
  
 Wenn die Rolle derzeit vorhanden ist, wird sie verwendet. Ist die Rolle nicht vorhanden, wird versucht, eine Datenbankrolle mit dem angegebenen Namen zu erstellen. Vor dem Versuch zur Erstellung der Rolle wird der Rollenname um die in der Zeichenfolge rechts befindlichen Leerstellen gekürzt. Wenn der Aufrufer nicht berechtigt ist, Rollen in der Datenbank zu erstellen, tritt bei der gespeicherten Prozedur ein Fehler auf.  
  
 [  **@capture_instance =** ] **"***Capture_instance***"**  
 Entspricht dem Namen der Aufzeichnungsinstanz, die für die Benennung der instanzspezifischen Change Data Capture-Objekte verwendet wird. *Capture_instance* ist **Sysname** und darf nicht NULL sein.  
  
 Wenn nicht angegeben, wird der Name abgeleitet aus dem quellschemanamen und dem Quelltabellennamen im Format *Schemaname_sourcename*. *Capture_instance* darf 100 Zeichen nicht überschreiten und muss innerhalb der Datenbank eindeutig sein. Ob angegeben oder abgeleitet, *Capture_instance* der Zeichenfolge rechts befindlichen Leerstellen gekürzt wird.  
  
 Eine Quelltabelle kann maximal zwei Aufzeichnungsinstanzen aufweisen. Weitere Informationen finden Sie unter [sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md).  
  
 [  **@supports_net_changes =** ] *Supports_net_changes*  
 Gibt an, ob die Unterstützung zum Abfragen von Nettoänderungen für diese Aufzeichnungsinstanz zu aktivieren ist. *Supports_net_changes* ist **Bit** hat den Standardwert 1, wenn die Tabelle einen Primärschlüssel besitzt oder die Tabelle besitzt einen eindeutigen Index, das mit identifiziert wurde die @index_name Parameter. Andernfalls hat der Parameter den Standardwert 0.  
  
 Bei 0 werden nur die Unterstützungsfunktionen zum Abfragen aller Änderungen generiert.  
  
 Bei 1 werden auch die Funktionen generiert, die zum Abfragen der Nettoänderungen erforderlich sind.  
  
 Wenn *Supports_net_changes* ist auf 1 festgelegt, *Index_name* muss angegeben werden, oder die Quelltabelle muss einen Primärschlüssel definierten.  
  
 [  **@index_name =** ] **"*** Index_name*"  
 Entspricht dem Namen eines eindeutigen Indexes zur eindeutigen Identifizierung von Zeilen in der Quelltabelle. *Index_name* ist **Sysname** und kann NULL sein. Wenn angegeben, *Index_name* muss ein gültiger eindeutiger Index in der Quelltabelle sein. Wenn *Index_name* angegeben ist, wird die identifizierten Indexspalten Vorrang vor alle definierten Primärschlüsselspalten als eindeutiger Zeilenbezeichner für die Tabelle.  
  
 [  **@captured_column_list =** ] **"***Captured_column_list***"**  
 Identifiziert die Quelltabellenspalten, die in die Änderungstabelle aufzunehmen sind. *Captured_column_list* ist **nvarchar(max)** und kann NULL sein. Wenn der Wert NULL ist, werden alle Spalten in der Änderungstabelle eingeschlossen.  
  
 Spaltennamen müssen gültige Spalten in der Quelltabelle sein. In einem Primärschlüsselindex definierten Spalten oder Spalten in einem Index verweist definiert *Index_name* eingeschlossen werden müssen.  
  
 *Captured_column_list* ist eine durch Trennzeichen getrennte Liste mit Spaltennamen. Einzelne Spaltennamen innerhalb der Liste können optional mit doppelten Anführungszeichen ("") oder eckigen Klammern ([]) angegeben werden. Wenn ein Spaltenname ein eingebettetes Komma enthält, muss er in Anführungszeichen eingeschlossen sein.  
  
 *Captured_column_list* dürfen nicht die folgenden reservierten Spaltennamen: **__ $Start_lsn**, **__ $End_lsn**, **__ $Seqval**, **__ $ Vorgang**, und **__ $Update_mask**.  
  
 [  **@filegroup_name =** ] **"***Filegroup_name***"**  
 Entspricht der Dateigruppe, die für die Änderungstabelle zu verwenden ist, die für die Aufzeichnungsinstanz erstellt wurde. *Filegroup_name* ist **Sysname** und kann NULL sein. Wenn angegeben, *Filegroup_name* muss für die aktuelle Datenbank definiert werden. Wenn der Wert NULL ist, wird die Standarddateigruppe verwendet.  
  
 Es wird empfohlen, eine separate Dateigruppe für Change Data Capture-Änderungstabellen zu erstellen.  
  
 [  **@allow_partition_switch=** ] **"***Allow_partition_switch***"**  
 Gibt an, ob der SWITCH PARTITION-Befehl von ALTER TABLE für eine Tabelle ausgeführt werden kann, die für Change Data Capture aktiviert ist. *Allow_partition_switch* ist **Bit**, hat den Standardwert 1.  
  
 Bei nicht partitionierten Tabellen lautet die Schaltereinstellung immer 1, und die tatsächliche Einstellung wird ignoriert. Wenn der Schalter für eine nicht partitionierte Tabelle explizit auf 0 festgelegt ist, wird Warnung 22857 ausgegeben. Dies zeigt an, dass die Schaltereinstellung ignoriert wurde. Wenn der Schalter für eine partitionierte Tabelle explizit auf 0 festgelegt ist, wird die Warnung 22356 ausgegeben. Diese zeigt an, dass SWITCH PARTITION-Vorgänge für die Quelltabelle nicht zulässig sind. Wenn die Schaltereinstellung entweder explizit auf 1 festgelegt und der Standardwert 1 zugelassen und die aktivierte Tabelle partitioniert ist, wird die Warnung 22855 ausgegeben. Diese zeigt an, dass Partitionsschalter nicht blockiert werden. Falls Partitionsschalter auftreten, werden die aus dem Schalter resultierenden Änderungen von Change Data Capture nicht nachverfolgt. Dies führt bei der Nutzung der Änderungsdaten zu Inkonsistenzen.  
  
> [!IMPORTANT]  
>  SWITCH PARTITION ist ein Metadatenvorgang, verursacht jedoch Datenänderungen. Die mit diesem Vorgang verbundenen Datenänderungen werden nicht in den Change Data Capture-Änderungstabellen aufgezeichnet. Beispiel: An einer Tabelle mit drei Partitionen werden Änderungen vorgenommen. Mit dem Aufzeichnungsprozess werden Einfüge-, Update- und Löschvorgänge verfolgt, die Benutzer in der Tabelle ausführen. Wenn jedoch eine Partition in eine andere Tabelle ausgelagert wird (z. B. zur Durchführung einer Massenlöschung), werden die verschobenen Zeilen in der Änderungstabelle nicht als gelöschte Zeilen aufgezeichnet. Wenn der Tabelle eine neue Partition mit vorab ausgefüllten Zeilen hinzugefügt wird, werden diese Zeilen auch nicht in der Änderungstabelle erfasst. Dies kann zu inkonsistenten Daten führen, wenn die Änderungen von einer Anwendung belegt und auf ein Ziel angewendet werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Bevor Sie eine Tabelle für Change Data Capture aktivieren können, muss die Datenbank aktiviert sein. Um zu bestimmen, ob die Datenbank für Change Data Capture aktiviert ist, Fragen den **Is_cdc_enabled** Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt. Verwenden Sie zum Aktivieren der Datenbank die [sp_cdc_enable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) gespeicherte Prozedur.  
  
 Wenn Change Data Capture für eine Tabelle aktiviert wird, werden eine Änderungstabelle und eine oder zwei Abfragefunktionen generiert. Die Änderungstabelle dient als Repository für die Änderungen der Quelltabelle, die durch den Aufzeichnungsprozess aus dem Transaktionsprotokoll extrahiert wurden. Die Abfragefunktionen werden verwendet, um Daten aus der Änderungstabelle zu extrahieren. Die Namen dieser Funktionen abgeleitet sind die *Capture_instance* Parameter auf folgende Weise:  
  
-   Funktion für alle Änderungen: **CDC. fn_cdc_get_all_changes_ < Capture_instance >**  
  
-   Funktion für nettoänderungen: **CDC. fn_cdc_get_net_changes_ < Capture_instance >**  
  
 **Sys. sp_cdc_enable_table** erstellt außerdem die aufzeichnungs- und cleanupaufträge Aufträge für die Datenbank aus, wenn die Quelltabelle ist die erste Tabelle in der Datenbank für Change Data Capture aktiviert werden und keine transaktionsveröffentlichungen für die Datenbank vorhanden sind. Es legt die **Is_tracked_by_cdc** Spalte in der [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) -Katalogsicht auf 1.  
  
> [!NOTE]  
>  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent muss nicht aktiv sein, wenn Change Data Capture für eine Tabelle aktiviert wird. Das Transaktionsprotokoll und in die Änderungstabelle geschriebene Einträge werden jedoch erst vom Aufzeichnungsprozess verarbeitet, wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent ausgeführt wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Db_owner** festen Datenbankrolle "".  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-enabling-change-data-capture-by-specifying-only-required-parameters"></a>A. Aktivieren von Change Data Capture durch das Angeben von nur erforderlichen Parametern  
 Im folgenden Beispiel wird Change Data Capture für die `HumanResources.Employee`-Tabelle aktiviert. Nur die erforderlichen Parameter werden angegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Employee'  
  , @role_name = N'cdc_Admin';  
GO  
```  
  
### <a name="b-enabling-change-data-capture-by-specifying-additional-optional-parameters"></a>B. Aktivieren von Change Data Capture durch das Angeben zusätzlicher optionaler Parameter  
 Im folgenden Beispiel wird Change Data Capture für die `HumanResources.Department`-Tabelle aktiviert. Alle Parameter außer `@allow_partition_switch` werden angegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Department'  
  , @role_name = N'cdc_admin'  
  , @capture_instance = N'HR_Department'   
  , @supports_net_changes = 1  
  , @index_name = N'AK_Department_Name'   
  , @captured_column_list = N'DepartmentID, Name, GroupName'   
  , @filegroup_name = N'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_cdc_disable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sp_cdc_help_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)  
  
  
