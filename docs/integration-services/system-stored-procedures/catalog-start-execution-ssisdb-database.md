---
title: Catalog. start_execution (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8edb51596198f27f00c1b78ddc8b3075ad035143
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Startet eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>Argumente  
 [@execution_id =] *Execution_id*  
 Der eindeutige Bezeichner für die Instanz der Ausführung. Der *execution_id* ist **bigint**.
 
 [@retry_count =] *Retry_count*  
 Die Wiederholungsanzahl, wenn die Ausführung ein Fehler auftritt. Er wird wirksam, nur, wenn die Ausführung in horizontal skalieren ist. Dieser Parameter ist optional. Wenn nicht angegeben, wird der Wert auf 0 festgelegt. Die *Retry_count* ist **Int**.
  
## <a name="remarks"></a>Hinweise  
 Eine Ausführung wird verwendet, geben Sie die Parameterwerte, die von einem Paket während einer einzelnen Instanz der paketausführung verwendet wird. Nachdem eine Instanz der Ausführung erstellt wurde, wird möglicherweise das entsprechende Projekt erneut bereitgestellt, bevor die Instanz gestartet wurde. In diesem Fall verweist auf die Instanz der Ausführung eines Projekts, das veraltet ist. Diese ungültige Verweis bewirkt, dass die gespeicherte Prozedur fehlschlägt.  
  
> [!NOTE]  
>  Ausführungen können nur einmal gestartet werden. Um eine Instanz der Ausführung zu starten, muss er den Status "erstellt" (Wert `1` in der **Status** Spalte die [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) anzeigen).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird catalog.create_execution aufgerufen, um eine Ausführungsinstanz für das Paket Child1.dtsx zu erstellen. Das Paket ist in Integration Services Projekt1 enthalten. Im Beispiel wird catalog.set_execution_parameter_value aufgerufen, um Werte für die Parameter Parameter1, Parameter2 und LOGGING_LEVEL festzulegen. Im Beispiel wird catalog.start_execution aufgerufen, um eine Instanz der Ausführung zu starten.  
  
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
  
-   READ-Berechtigung und MODIFY-Berechtigung für die Instanz der Ausführung, READ-Berechtigung und EXECUTE-Berechtigung für das Projekt und ggf. READ-Berechtigungen für die Umgebung, auf die verwiesen wird  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
-   Der Ausführungsbezeichner ist ungültig.  
  
-   Die Ausführung wurde bereits gestartet oder bereits abgeschlossen. Ausführungen können nur einmal gestartet werden.  
  
-   Der dem Projekt zugeordnete Umgebungsverweis ist ungültig.  
  
-   Erforderliche Parameterwerte wurden nicht festgelegt.  
  
-   Die der Instanz der Ausführung zugeordnete Projektversion ist veraltet. Es kann nur die aktuelle Version eines Projekts ausgeführt werden.  
  
  

