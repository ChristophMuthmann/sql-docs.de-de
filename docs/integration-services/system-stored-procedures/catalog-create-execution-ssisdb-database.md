---
title: Catalog. create_execution (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7e9d38935a91bba81359bee7fdbd64dba86d0d26
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [@folder_name =] *Ordnername*  
 Der Name des Ordners mit dem Paket, das ausgeführt werden soll. Der *folder_name* ist **nvarchar(128)**.  
  
 [@project_name =] *Project_name*  
 Der Name des Projekts, das das Paket enthält, das ausgeführt werden soll. Der *project_name* ist **nvarchar(128)**.  
  
 [@package_name =] *Paketname*  
 Der Name des Pakets, das ausgeführt werden soll. Der *package_name* ist **nvarchar(260)**.  
  
 [@reference_id =] *Reference_id*  
 Ein eindeutiger Bezeichner für einen Umgebungsverweis. Dieser Parameter ist optional. Der *reference_id* ist **bigint**.  
  
 [@use32bitruntime =] *use32bitruntime*  
 Gibt an, ob die 32-Bit-Laufzeit verwendet werden soll, um das Paket unter einem 64-Bit-Betriebssystem auszuführen. Verwenden Sie den Wert 1, um das Paket mit der 32-Bit-Laufzeit ausgeführt werden, wenn auf einem 64-Bit-Betriebssystem ausgeführt wird. Verwenden Sie den Wert 0, um das Paket mit der 64-Bit-Laufzeit auszuführen, wenn die Ausführung unter einem 64-Bit-Betriebssystem erfolgt. Dieser Parameter ist optional. Die *Use32bitruntime* ist **Bit**.  
 
 [@runinscaleout =] *Runinscaleout*  
 Geben Sie an, ob die Ausführung in horizontal skalieren ist. Verwenden Sie den Wert 1, um das Paket in horizontal skalieren auszuführen. Verwenden Sie den Wert 0, um das Paket ohne Horizontales Skalieren ausgeführt werden. Dieser Parameter ist optional. Wenn nicht angegeben, wird der Wert auf DEFAULT_EXECUTION_MODE in [SSISDB] festgelegt. [Catalog]. [Catalog_properties]. Die *Runinscaleout* ist **Bit**. 
 
 [@useanyworker =] *Useanyworker*  
  Geben Sie an, ob jeder Scale-Out-Arbeitsthread führen Sie die Ausführung zugelassen wird. Verwenden Sie den Wert 1, um das Paket mit jeder Scale-Out-Arbeitsthread auszuführen. Verwenden Sie den Wert 0, um anzugeben, dass nicht alle Scale Out Worker zulässig sind, um das Paket ausgeführt werden. Dieser Parameter ist optional. Wenn nicht angegeben, wird der Wert auf 1 festgelegt. Die *Useanyworker* ist **Bit**. 
  
 [@execution_id =] *Execution_id*  
 Gibt den eindeutigen Bezeichner für eine Ausführungsinstanz zurück. Der *execution_id* ist **bigint**.  

  
## <a name="remarks"></a>Hinweise  
 Eine Ausführung wird verwendet, um die Parameterwerte anzugeben, die von einem Paket während einer einzelnen Instanz der Paketausführung verwendet werden.  
  
 Wenn ein umgebungsverweis angegeben wird, mit der *Reference_id* Parameter der gespeicherten Prozedur füllt die Parameter für Projekt- und Paketparameter mit Literalwerten oder Werte aus der entsprechenden Umgebungsvariablen verwiesen wird. Wird ein Umgebungsverweis angegeben, werden bei der Paketausführung Standardparameterwerte verwendet. Um zu bestimmen, genau, welche Werte für eine bestimmte Instanz der Ausführung verwendet werden, verwenden die *Execution_id* -Ausgabeparameterwert dieser gespeicherten Prozedur und die Abfrage die [Execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) anzeigen.  
  
 In einer Ausführung können nur Pakete angegeben werden, die als Einstiegspunktpakete gekennzeichnet sind. Wenn ein Paket angegeben wird, das kein Einstiegspunkt ist, schlägt die Ausführung fehl.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird Catalog. create_execution eine Instanz der Ausführung für das Paket Child1.dtsx zu erstellen, die nicht in horizontal skalieren ist. Das Paket ist in Integration Services Projekt1 enthalten. Im Beispiel wird catalog.set_execution_parameter_value aufgerufen, um Werte für die Parameter Parameter1, Parameter2 und LOGGING_LEVEL festzulegen. Im Beispiel wird catalog.start_execution aufgerufen, um eine Instanz der Ausführung zu starten.  
  
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
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ- und EXECUTE-Berechtigungen für das Projekt und ggf. READ-Berechtigungen für die Umgebung, auf die verwiesen wird  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  

 Wenn @runinscaleout beträgt 1, die gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:
 
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**

-   Die Mitgliedschaft in der **Ssis_cluster_executor** -Datenbankrolle

-   Mitgliedschaft in der Serverrolle **sysadmin**
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, die einen Fehler oder eine Warnung auslösen können:  
  
-   Das Paket ist nicht vorhanden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
-   Der umgebungsverweis *Reference_id*, ist ungültig.  
  
-   Das angegebene Paket ist kein Einstiegspunktpaket.  
  
-   Der Datentyp der Umgebungsvariablen, auf die verwiesen wird, unterscheidet sich vom Datentyp des Projekt- oder Paketparameters.  
  
-   Das Projekt oder Paket enthält Parameter, die Werte erfordern, es wurden aber keine Werte zugewiesen.  
  
-   Die Umgebungsvariablen für die referenzierten können nicht gefunden werden, in der Umgebung, die vom umgebungsverweis *Reference_id*, angibt.  
  
## <a name="see-also"></a>Siehe auch  
 [Catalog. start_execution &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [Catalog.add_execution_worker &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  

