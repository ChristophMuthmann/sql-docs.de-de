---
title: catalog.create_customized_logging_level | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 027e2790bc59e3e9839de83c98984c19df1a982e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="catalogcreatecustomizedlogginglevel"></a>catalog.create_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Erstellt einen neuen benutzerdefinierten Protokolliergrad. Weitere Informationen zu benutzerdefinierten Protokolliergraden finden Sie unter [Integration Services &#40;SSIS&#41; Logging (SSIS-Protokollierung [SQL Server Integration Services])](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @event_value = ] event_value  
    , [ @level_id = ] level_id OUT   
```  
  
## <a name="arguments"></a>Argumente  
 [ @level_name = ] *level_name*  
 Der Name für den neuen benutzerdefinierten Protokolliergrad.  
  
 Das Argument *level_name* ist vom Typ **nvarchar(128)**.  
  
 [ @level_description = ] *level_description*  
 Die Beschreibung für den neuen benutzerdefinierten Protokolliergrad.  
  
 Das Argument *level_description* ist vom Typ **nvarchar(1024)**.  
  
 [ @profile_value = ] *profile_value*  
 Die Statistiken, die durch den neuen Protokolliergrad protokolliert werden sollen.  
  
 Die gültigen Werte für Statistiken werden im Folgenden aufgeführt. Diese Werte entsprechen denjenigen auf der Registerkarte **Statistik** des Dialogfelds **Verwaltung des angepassten Protokolliergrads**.  
  
-   Ausführung = 0  
  
-   Volume = 1  
  
-   Leistung = 2  
  
 Das Argument *profile_value* ist vom Typ **bigint**.  
  
 [ @event_value = ] *event_value*  
 Die Ereignisse, die durch den neuen Protokolliergrad protokolliert werden sollen.  
  
 Die gültigen Werte für Ereignisse werden im Folgenden aufgeführt. Diese Werte entsprechen denjenigen auf der Registerkarte **Ereignisse** des Dialogfelds **Verwaltung des angepassten Protokolliergrads**.  
  
|Ereignisse ohne Ereigniskontext|Ereignisse mit Ereigniskontext|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> Diagnostic = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext= 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 Das Argument *event_value* ist vom Typ **bigint**.  
  
 [ @level_id = ] *level_id* OUT  
 Die ID des neuen benutzerdefinierten Protokolliergrads.  
  
 Das Argument *level_id* ist vom Typ **bigint**.  
  
## <a name="remarks"></a>Remarks  
 Gehen Sie zum Kombinieren mehrerer Werte in Transact-SQL für das Argument *profile_value* oder *event_value* wie im folgenden Beispiel vor. Verwenden Sie zur Erfassung der Ereignisse OnError (8) und DiagnosticEx (15) als Berechnungsformel für *event_value* die Formel `2^8 + 2^15 = 33024`.  
  
## <a name="return-codes"></a>Rückgabecodes  
 0 (Erfolg)  
  
 Wenn die gespeicherte Prozedur fehlschlägt, wird ein Fehler ausgelöst.  
  
## <a name="result-set"></a>Resultset  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die gespeicherte Prozedur fehlschlägt.  
  
-   Der Benutzer verfügt nicht über die erforderlichen Berechtigungen.  
  
  
