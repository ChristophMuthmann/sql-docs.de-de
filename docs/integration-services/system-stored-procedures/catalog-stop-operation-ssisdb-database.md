---
title: catalog.stop_operation (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf33675e591fbb16417bc3b251a1a47693b59673
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogstopoperation-ssisdb-database"></a>catalog.stop_operation (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Beendet eine Überprüfung oder eine Ausführungsinstanz im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>Argumente  
 [ @operation_id = ] *operation_id*  
 Der eindeutige Bezeichner der Überprüfung oder Instanz der Ausführung. Der *operation_id* ist **bigint**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für die Überprüfung oder Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
-   Der Vorgangsbezeichner ist ungültig.  
  
-   Der Vorgang wurde bereits beendet.  
  
## <a name="remarks"></a>Hinweise  
 Ein Vorgang im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog darf immer nur von jeweils einem Benutzer beendet werden. Wenn mehrere Benutzer versuchen, den Vorgang zu beenden, gibt die gespeicherte Prozedur beim ersten Versuch Erfolg (der Wert `0`) zurück, bei anschließenden Versuchen wird jedoch ein Fehler ausgelöst.  
  
  
