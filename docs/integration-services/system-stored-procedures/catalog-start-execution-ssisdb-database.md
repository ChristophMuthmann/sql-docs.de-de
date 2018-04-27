---
title: catalog.start_execution (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d49416bb284ab6073818f21583e1a2e532427c3d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Startet eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>Argumente  
 [@execution_id =] *execution_id*  
 Der eindeutige Bezeichner für die Instanz der Ausführung. Der *execution_id* ist **bigint**.
 
 [@retry_count =] *retry_count*  
 Die Anzahl von Wiederholungsversuchen, wenn bei der Ausführung ein Fehler auftritt. Dieses Argument wird nur wirksam, wenn die Ausführung in Scale Out erfolgt. Dieser Parameter ist optional. Wenn es nicht angegeben wird, wird der Wert auf 0 festgelegt. Das Argument *retry_count* ist vom Typ **Int**.
  
## <a name="remarks"></a>Remarks  
 Eine Ausführung wird verwendet, um die Parameterwerte anzugeben, die von einem Paket während einer einzelnen Instanz der Paketausführung verwendet werden. Nachdem eine Instanz der Ausführung erstellt wurde, wird möglicherweise das entsprechende Projekt erneut bereitgestellt, bevor die Instanz gestartet wurde. In diesem Fall verweist die Instanz der Ausführung auf ein veraltetes Projekt. Dieser ungültige Verweis führt dazu, dass bei der gespeicherten Prozedur ein Fehler auftritt.  
  
> [!NOTE]  
>  Ausführungen können nur einmal gestartet werden. Um eine Instanz der Ausführung zu starten, muss sie den Zustand „Erstellt“ (ein Wert `1` in der Spalte **status** der Sicht [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md)) aufweisen.  
  
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
 InclusionThresholdSetting  
  
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
  
  
