---
title: Catalog.add_execution_worker (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8ce83f2678a1f3dcae6539f33beb33070b8e771b
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>Catalog.add_execution_worker (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Fügt eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker mit einer Instanz der Ausführung im horizontal skalieren.

## <a name="syntax"></a>Syntax

```tsql
add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>Argumente
[ @execution_id =] *Execution_id*  
 Der eindeutige Bezeichner für die Instanz der Ausführung. Der *execution_id* ist **bigint**.  
 
[@workeragent_id =] *Workeragent_id*  
Die Worker-Agent-Id von einem Scale Out Worker. Die *Workeragent_id* ist **"uniqueidentifier"**.

## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  

## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ- und MODIFY-Berechtigungen für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
 
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
 
- Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.

- Der ausführungsbezeichner ist ungültig.

- Der Worker-Agent-Id ist ungültig.

- Die Ausführung ist nicht in horizontal skalieren.

## <a name="see-also"></a>Siehe auch
[Ausführen von Paketen in horizontal skalieren](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).


