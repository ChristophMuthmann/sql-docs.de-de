---
title: Catalog. set_execution_parameter_value (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 055d86c9-befd-4e63-acb1-6dfe833549d2
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 7b13e7b1c28bad6e573e829183372da4bb62f92d
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="catalogsetexecutionparametervalue-ssisdb-database"></a>catalog.set_execution_parameter_value (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Legt den Wert eines Parameters für eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 Ein Parameterwert kann nicht geändert werden, nachdem eine Instanz der Ausführung gestartet wurde.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.set_execution_parameter_value [ @execution_id = execution_id  
    , [ @object_type = ] object_type  
    , [ @parameter_name = ] parameter_name  
    , [ @parameter_value = ] parameter_value  
```  
  
## <a name="arguments"></a>Argumente  
 [ @execution_id =] *Execution_id*  
 Der eindeutige Bezeichner für die Instanz der Ausführung. Der *execution_id* ist **bigint**.  
  
 [ @object_type =] *Object_type*  
 Der Typ des Parameters.  
  
 Legen Sie für die folgenden Parameter *Object_type* auf 50  
  
-   LOGGING_LEVEL  
  
-   CUSTOMIZED_LOGGING_LEVEL  
  
-   DUMP_ON_ERROR  
  
-   DUMP_ON_EVENT  
  
-   DUMP_EVENT_CODE  
  
-   CALLER_INFO  
  
-   SYNCHRONIZED  
  
 Verwenden Sie den Wert `20` , um einen Projektparameter anzugeben, oder den Wert `30` , um einen Paketparameter anzugeben.  
  
 Die *Object_type* ist **"smallint"**.  
  
 [ @parameter_name =] *Parameter_name*  
 Der Name des Parameters. Der *parameter_name* ist **nvarchar(128)**.  
  
 [ @parameter_value =] *Parameter_value*  
 Der Wert des Parameters. Der *parameter_value* ist **sql_variant**.  
  
## <a name="remarks"></a>Hinweise  
 Um die Parameterwerte zu ermitteln, die für eine bestimmte Ausführung verwendet wurden, fragen Sie die catalog.execution_parameter_values-Sicht ab.  
  
 Um den Umfang der Informationen anzugeben, die während einer paketausführung protokolliert wird, legen *Parameter_name* auf LOGGING_LEVEL und *Parameter_value* auf einen der folgenden Werte.  
  
 Legen Sie die *Object_type* -Parameter auf 50.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Keine<br /><br /> Die Protokollierung ist deaktiviert. Nur der Status der Ausführung von Paketen wird protokolliert.|  
|1|Standard<br /><br /> Alle Ereignisse werden protokolliert, außer benutzerdefinierten und Diagnose-Ereignissen. Dies ist der Standardwert.|  
|2|Leistung<br /><br /> Nur Leistungsstatistiken sowie OnError- und OnWarning-Ereignisse werden protokolliert.|  
|3|Ausführlich<br /><br /> Alle Ereignisse werden protokolliert, einschließlich benutzerdefinierter Ereignisse und Diagnose-Ereignissen. <br />Zu den benutzerdefinierten Ereignissen zählen auch von Integration Services-Tasks protokollierte Ereignisse. Weitere Informationen finden Sie unter [Custom Messages for Logging](../../integration-services/performance/integration-services-ssis-logging.md#custom_messages)|  
|4|Runtimelineage<br /><br /> Erfasst die Daten, die zum Nachverfolgen von Datenherkunft im Datenfluss erforderlich.|  
|100|Benutzerdefinierter Protokolliergrad<br /><br /> Geben Sie die Einstellungen im CUSTOMIZED_LOGGING_LEVEL-Parameter. Weitere Informationen zu den Werten, die Sie angeben können, finden Sie unter [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md).<br /><br /> Weitere Informationen über benutzerdefinierte Protokolliergrade, finden Sie unter [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).|  
  
 Um festzulegen, dass der Integration Services-Server Dumpdateien generiert, wenn während einer Paketausführung ein Fehler auftritt, legen Sie die folgenden Parameterwerte für eine Ausführungsinstanz fest, die nicht ausgeführt wurde.  
  
|Parameter|Wert|  
|---------------|-----------|  
|*execution_id*|Der eindeutige Bezeichner für die Instanz der Ausführung|  
|*object_type*|50|  
|*Parametername*|‘DUMP_ON_ERROR|  
|*parameter_value*|1|  
  
 Um festzulegen, dass der Integration Services-Server Dumpdateien generiert, wenn während einer Paketausführung Ereignisse auftreten, legen Sie die folgenden Parameterwerte für eine Ausführungsinstanz fest, die nicht ausgeführt wurde.  
  
|Parameter|Wert|  
|---------------|-----------|  
|*execution_id*|Der eindeutige Bezeichner für die Instanz der Ausführung|  
|*object_type*|50|  
|*Parametername*|‘DUMP_ON_EVENT|  
|*parameter_value*|1|  
  
 Um die während einer Paketausführung auftretenden Ereignisse festzulegen, die Integration Services-Server zum Generieren von Dumpdateien veranlassen, legen Sie die folgenden Parameterwerte für eine Ausführungsinstanz fest, die nicht ausgeführt wurde. Trennen Sie mehrere Ereigniscodes mithilfe eines Semikolons.  
  
|Parameter|Wert|  
|---------------|-----------|  
|*execution_id*|Der eindeutige Bezeichner für die Instanz der Ausführung|  
|*object_type*|50|  
|*Parametername*|DUMP_EVENT_CODE|  
|*parameter_value*|Ein oder mehrere Ereigniscodes|  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird angegeben, dass der Integration Services-Server Dumpdateien generiert, wenn während einer Paketausführung ein Fehler auftritt.  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_ERROR',1  
```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird angegeben, dass der Integration Services-Server Dumpdateien generiert, wenn während einer Paketausführung Ereignisse auftreten. Zudem wird das Ereignis angegeben, das den Server zum Generieren der Dateien veranlasst.  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_EVENT',1  
  
declare @event_code nvarchar(50)  
set @event_code = '0xC020801C'  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_EVENT_CODE', @event_code  
```  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ- und MODIFY-Berechtigungen für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
-   Der Ausführungsbezeichner ist ungültig.  
  
-   Der Parametername ist ungültig.  
  
-   Der Datentyp des Parameterwerts stimmt nicht mit dem Datentyp des Parameters überein.  
  
## <a name="see-also"></a>Siehe auch  
 [Catalog. execution_parameter_values &#40; SSISDB-Datenbank &#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)   
 [Generieren von Dumpdateien für die Paketausführung](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
