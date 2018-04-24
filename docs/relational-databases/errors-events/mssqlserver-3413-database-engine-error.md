---
title: MSSQLSERVER_3413 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b54a228fe789921c45fab14b03fb03cb4706e30
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3413|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|MARKDB|  
|Meldungstext|Datenbank-ID %d. Die Datenbank konnte nicht als fehlerverdächtig gekennzeichnet werden. Fehler beim Getnext-Scan für NC für sys.databases.database_id. Identifizieren Sie die Ursache anhand vorheriger Fehlermeldungen im Fehlerprotokoll, und beheben Sie etwaige damit verbundene Probleme.|  
  
## <a name="explanation"></a>Erklärung  
Es ist ein unerwarteter Fehler aufgetreten, während versucht wurde, eine Benutzerdatenbank im Katalog als SUSPECT zu markieren. Der Status SUSPECT wird nicht beibehalten.  
  
## <a name="user-action"></a>Benutzeraktion  
Zeigen Sie vorherige Fehler an, und beheben Sie das Problem.  
  
