---
title: Catalog.set_customized_logging_level_description | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 6ceaa39f-2439-457b-b99f-f12d88a1be32
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3899e02c6b1eaa2cc76ad4411d9be3aded817728
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetcustomizedloggingleveldescription"></a>Catalog.set_customized_logging_level_description
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ändert die Beschreibung einer vorhandenen benutzerdefinierten Protokolliergrad entscheiden. Weitere Informationen über benutzerdefinierte Protokolliergrade, finden Sie unter [Integration Services &#40; SSIS &#41; Protokollierung](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.set_customized_logging_level_description [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
```  
  
## <a name="arguments"></a>Argumente  
 [ @level_name =] *Ebenenname*  
 Der Name eines vorhandenen benutzerdefinierten Protokolliergrads.  
  
 Die *Ebenenname* ist **vom Datentyp nvarchar(128)**.  
  
 [ @level_description =] *Level_description*  
 Die neue Beschreibung für den angegebenen benutzerdefinierten Protokolliergrads.  
  
 Die *Level_description* ist **nvarchar(1024)**.  
  
## <a name="remarks"></a>Hinweise  
  
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
  
  

