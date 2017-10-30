---
title: Catalog.check_schema_version | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 56eacb6ed209f34f65ae406fe4dd520284b79e5b
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcheckschemaversion"></a>catalog.check_schema_version
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Bestimmt, ob die SSISDB-Katalogschema und die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Binärdateien (isserverexec-Assembly und SQLCLR-Assembly) kompatibel sind.  
  
 ISServerExec.exc protokolliert eine Fehlermeldung, wenn das Schema und die Binärdateien nicht kompatibel sind.  
  
 Die SSISDB-Schemaversion wird inkrementiert, wenn sich das Schema während der Anwendung von Patches und während der Upgrades ändert. Es wird empfohlen, dass Sie diese gespeicherte Prozedur ausführen, nachdem eine SSISDB-Sicherung wiederhergestellt wurde, um sicherzustellen, dass das Schema und die Binärdateien kompatibel sind.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.check_schema_version [@use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>Argumente  
 [ @use32bitruntime=] *use32bitruntime*  
 Wenn der Parameter auf **True**festgelegt wird, wird die 32-Bit-Version von dtexec aufgerufen. *use32bitruntime* ist **Bool**.  
  
## <a name="result-set"></a>Resultset  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert die folgende Berechtigung:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin** .  
  
  

