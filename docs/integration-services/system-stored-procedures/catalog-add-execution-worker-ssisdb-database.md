---
title: Catalog.add_execution_worker (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5ecc54863b47ef55269a068353cbc25bbd5d008
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>Catalog.add_execution_worker (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Fügt einen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Scale Out Worker einer Instanz der Ausführung in Scale Out hinzu.

## <a name="syntax"></a>Syntax

```sql
catalog.add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>Argumente
[ @execution_id = ] *execution_id*  
 Der eindeutige Bezeichner für die Instanz der Ausführung. Der *execution_id* ist **bigint**.  
 
[@workeragent_id = ] *workeragent_id*  
Die Worker-Agent-ID für den Scale Out-Worker. Die *workeragent_id* ist **uniqueIdentifier**.

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

- Der Ausführungsbezeichner ist ungültig.

- Die Worker-Agent-ID ist ungültig.

- Die Ausführung erfolgt nicht in horizontaler Hochskalierung.

## <a name="see-also"></a>Siehe auch
[Ausführen von Paketen in horizontaler Hochskalierung](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).

