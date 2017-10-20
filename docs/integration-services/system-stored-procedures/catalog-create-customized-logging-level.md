---
title: Catalog.create_customized_logging_level | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 126fa0af811033bb0be035b1f4c550620c696bb3
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatecustomizedlogginglevel"></a>Catalog.create_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Erstellt einen neuen benutzerdefinierten Protokolliergrad. Weitere Informationen über benutzerdefinierte Protokolliergrade, finden Sie unter [Integration Services &#40; SSIS &#41; Protokollierung](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Syntax  
  
```sql  
create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @event_value = ] event_value  
    , [ @level_id = ] level_id OUT  
  
```  
  
## <a name="arguments"></a>Argumente  
 [ @level_name =] *Ebenenname*  
 Der Name für die neue vorhandenen benutzerdefinierten Protokolliergrads.  
  
 Die *Ebenenname* ist **vom Datentyp nvarchar(128)**.  
  
 [ @level_description =] *Level_description*  
 Die Beschreibung für die neue vorhandenen benutzerdefinierten Protokolliergrads.  
  
 Die *Level_description* ist **nvarchar(1024)**.  
  
 [ @profile_value =] *Profile_value*  
 Die Statistiken, die die neue sollen Protokolliergrad, melden Sie sich an.  
  
 Gültige Werte für Statistiken zu zählen den folgende: Diese Werte entsprechen den Werten für die **Statistiken** auf der Registerkarte die **angepasst Logging Level Management** (Dialogfeld).  
  
-   Ausführung = 0  
  
-   Volume = 1  
  
-   Leistung = 2  
  
 Die *Profile_value* ist ein **"bigint"**.  
  
 [ @event_value =] *Event_value*  
 Die Ereignisse, die den neuen gewünschten Protokolliergrad, melden Sie sich an.  
  
 Gültige Werte für Ereignisse sind die folgenden. Diese Werte entsprechen den Werten für die **Ereignisse** auf der Registerkarte die **angepasst Logging Level Management** (Dialogfeld).  
  
|Ereignisse ohne Ereigniskontext|Ereignisse mit Ereigniskontext|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> Diagnose = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext = 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 Die *Event_value* ist ein **"bigint"**.  
  
 [ @level_id =] *Level_id* OUT  
 Die Id des neuen benutzerdefinierten Protokolliergrads.  
  
 Die *Level_id* ist ein **"bigint"**.  
  
## <a name="remarks"></a>Hinweise  
 Zum Kombinieren mehrerer Werte in Transact-SQL für die *Profile_value* oder *Event_value* Argument, führen Sie dieses Beispiel. Zum Erfassen der OnError (8) und DiagnosticEx (15) Ereignisse, die Formel zum Berechnen *Event_value* ist `2^8 + 2^15 = 33024`.  
  
## <a name="return-codes"></a>Rückgabecodes  
 0 (Erfolg)  
  
 Wenn die gespeicherte Prozedur fehlschlägt, wird ein Fehler ausgelöst.  
  
## <a name="result-set"></a>Resultset  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die gespeicherte Prozedur fehlschlägt.  
  
-   Der Benutzer besitzt nicht die erforderlichen Berechtigungen.  
  
  
