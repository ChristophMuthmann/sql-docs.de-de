---
title: catalog.create_execution (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5c557108a98a0063cb0dad14e0d40f10deb03698
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 Diese gespeicherte Prozedur verwendet den Standardserverprotokolliergrad.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.create_execution [@folder_name = folder_name  
     , [@project_name =] project_name  
     , [@package_name =] package_name  
  [  , [@reference_id =] reference_id ]  
  [  , [@use32bitruntime =] use32bitruntime ] 
  [  , [@runinscaleout =] runinscaleout ]
  [  , [@useanyworker =] useanyworker ] 
     , [@execution_id =] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumente  
 [@folder_name =] *folder_name*  
 Der Name des Ordners mit dem Paket, das ausgeführt werden soll. Der *folder_name* ist **nvarchar(128)**.  
  
 [@project_name =] *project_name*  
 Der Name des Projekts mit dem Paket, das ausgeführt werden soll. Der *project_name* ist **nvarchar(128)**.  
  
 [@package_name =] *package_name*  
 Der Name des Pakets, das ausgeführt werden soll. Der *package_name* ist **nvarchar(260)**.  
  
 [@reference_id =] *reference_id*  
 Ein eindeutiger Bezeichner für einen Umgebungsverweis. Dieser Parameter ist optional. Der *reference_id* ist **bigint**.  
  
 [@use32bitruntime =] *use32bitruntime*  
 Gibt an, ob die 32-Bit-Laufzeit verwendet werden soll, um das Paket unter einem 64-Bit-Betriebssystem auszuführen. Verwenden Sie den Wert 1, um das Paket mit der 32-Bit-Runtime auszuführen, wenn die Ausführung unter einem 64-Bit-Betriebssystem erfolgt. Verwenden Sie den Wert 0, um das Paket mit der 64-Bit-Laufzeit auszuführen, wenn die Ausführung unter einem 64-Bit-Betriebssystem erfolgt. Dieser Parameter ist optional. Das Argument *Use32bitruntime* ist vom Typ **bit**.  
 
 [@runinscaleout =] *runinscaleout*  
 Geben Sie an, ob die Ausführung in Scale Out erfolgen soll. Verwenden Sie den Wert 1, um das Paket in Scale Out auszuführen. Verwenden Sie den Wert 0, um das Paket ohne Scale Out auszuführen. Dieser Parameter ist optional. Wenn dieser Parameter nicht angegeben wird, wird der Wert auf DEFAULT_EXECUTION_MODE in [SSISDB].[catalog].[catalog_properties] festgelegt. Das Argument *runinscaleout* ist vom Typ **bit**. 
 
[@useanyworker =] *useanyworker*  
Geben Sie an, ob jeder Scale Out-Worker für die Ausführung zugelassen ist.

-   Verwenden Sie den Wert 1, um das Paket mit einem beliebigen Scale Out-Worker auszuführen. Wenn Sie `@useanyworker` auf „true“ setzen, steht jeder Worker, dessen maximale Taskanzahl (wie in der Workerkonfigurationsdatei angegeben) noch nicht erreicht ist, für die Ausführung des Pakets zur Verfügung. Weitere Informationen zur Konfigurationsdatei des Workers finden Sie unter [Integration Services (SSIS) Scale Out-Worker](../scale-out/integration-services-ssis-scale-out-worker.md).

-   Verwenden Sie den Wert 0, um anzugeben, dass nicht alle Scale Out-Worker für die Paketausführung zugelassen sind. Wenn Sie `@useanyworker` auf „false“ festlegen, müssen Sie mithilfe des Managers für horizontales Hochskalieren oder durch Aufrufen der gespeicherten Prozedur `[catalog].[add_execution_worker]` die Worker angeben, die zum Ausführen des Pakets zulässig sind. Wenn Sie einen Worker angeben, der bereits ein anderes Paket ausführt, schließt der Worker die Ausführung des aktuellen Pakets ab, bevor er eine weitere Ausführung anfordert.

Dieser Parameter ist optional. Wenn dieser Parameter nicht angegeben wird, wird der Wert auf 1 festgelegt. Das Argument *useanyworker* ist vom Typ **bit**. 
  
 [@execution_id =] *execution_id*  
 Gibt den eindeutigen Bezeichner für eine Ausführungsinstanz zurück. Der *execution_id* ist **bigint**.  

  
## <a name="remarks"></a>Remarks  
 Eine Ausführung wird verwendet, um die Parameterwerte anzugeben, die von einem Paket während einer einzelnen Instanz der Paketausführung verwendet werden.  
  
 Wenn ein Umgebungsverweis mit dem *reference_id*-Parameter angegeben wird, füllt die gespeicherte Prozedur den Projekt- und Paketparameter mit Literalwerten oder Werten, auf die verwiesen wird, der entsprechenden Umgebungsvariablen auf. Wird ein Umgebungsverweis angegeben, werden bei der Paketausführung Standardparameterwerte verwendet. Um genau zu bestimmen, welche Werte für eine bestimmte Ausführungsinstanz verwendet werden, verwenden Sie den *execution_id*-Ausgabeparameterwert dieser gespeicherten Prozedur, und fragen Sie die Sicht [execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) ab.  
  
 In einer Ausführung können nur Pakete angegeben werden, die als Einstiegspunktpakete gekennzeichnet sind. Wenn ein Paket angegeben wird, das kein Einstiegspunkt ist, schlägt die Ausführung fehl.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird „catalog.create_execution“ aufgerufen, um eine Ausführungsinstanz für das Paket „Child1.dtsx“ zu erstellen, das nicht in Scale Out vorhanden ist. Das Paket ist in Integration Services Projekt1 enthalten. Im Beispiel wird catalog.set_execution_parameter_value aufgerufen, um Werte für die Parameter Parameter1, Parameter2 und LOGGING_LEVEL festzulegen. Im Beispiel wird catalog.start_execution aufgerufen, um eine Instanz der Ausführung zu starten.  
  
```sql  
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
```  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ- und EXECUTE-Berechtigungen für das Projekt und ggf. READ-Berechtigungen für die Umgebung, auf die verwiesen wird  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  

 Wenn @runinscaleout auf „1“ festgelegt ist, erfordert diese gespeicherte Prozedur eine der folgenden Berechtigungen:
 
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**

-   Mitgliedschaft in der Datenbankrolle **ssis_cluster_executor**

-   Mitgliedschaft in der Serverrolle **sysadmin**
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die einen Fehler oder eine Warnung auslösen können:  
  
-   Das Paket ist nicht vorhanden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
-   Der Umgebungsverweis *reference_id* ist ungültig.  
  
-   Das angegebene Paket ist kein Einstiegspunktpaket.  
  
-   Der Datentyp der Umgebungsvariablen, auf die verwiesen wird, unterscheidet sich vom Datentyp des Projekt- oder Paketparameters.  
  
-   Das Projekt oder Paket enthält Parameter, die Werte erfordern, es wurden aber keine Werte zugewiesen.  
  
-   Die Umgebungsvariablen, auf die verwiesen wird, wurden nicht in der Umgebung gefunden, die vom Umgebungsverweis *reference_id* angegeben wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [catalog.start_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [catalog.add_execution_worker &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  
