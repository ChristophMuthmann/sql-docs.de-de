---
title: Catalog.rename_customized_logging_level | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b1a57d5e-3f03-4901-8b2b-bb8b371b595b
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 00c2cd8fa5f8423a7791d663d02aecbf27b8ab41
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrenamecustomizedlogginglevel"></a>Catalog.rename_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Benennt einen vorhandenen benutzerdefinierten Protokolliergrad entscheiden. Weitere Informationen über benutzerdefinierte Protokolliergrade, finden Sie unter [Integration Services &#40; SSIS &#41; Protokollierung](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
rename_customized_logging_level [ @old_name = ] old_name  
    , [ @new_name = ] new_name  
  
```  
  
## <a name="arguments"></a>Argumente  
 [ @old_name =] *Old_name*  
 Der Name des vorhandenen angepasste Protokolliergrad umbenennen.  
  
 Der *old_name* ist **nvarchar(128)**.  
  
 [ @new_name =] *Neuer_Name*  
 Der neue Name für den angegebenen benutzerdefinierten Protokolliergrads.  
  
 Der *new_name* ist **nvarchar(128)**.  
  
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
  
  
