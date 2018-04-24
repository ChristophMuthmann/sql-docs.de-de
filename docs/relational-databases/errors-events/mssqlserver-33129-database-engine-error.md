---
title: MSSQLSERVER_33129 | Microsoft-Dokumentation
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
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95d1624e61280fe8d7072a9410379f915121ab97
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver33129"></a>MSSQLSERVER_33129
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|33129|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SEC_CANNOT_DISABLE_WIN_GROUP|  
|Meldungstext|Kann ALTER_LOGIN mit dem DISABLE-Argument nicht dazu verwenden, den Zugriff auf eine Windows-Gruppe zu verweigern.|  
  
## <a name="explanation"></a>Erklärung  
Diese Meldung wird angezeigt, wenn Sie versuchen, den Anmeldenamen einer Windows-Gruppe zu deaktivieren.  
  
## <a name="user-action"></a>Benutzeraktion  
Der Anmeldename einer Windows-Gruppe kann nicht deaktiviert werden. Um die Zugriffsberechtigung einer Windows-Gruppe vorübergehend zu entfernen, heben Sie die CONNECT-Berechtigung des Anmeldenamens für die Windows-Gruppe mit REVOKE auf. Windows-Benutzer haben möglicherweise weiterhin über ihren individuellen Anmeldenamen oder eine andere Windows-Gruppe Zugriff. Im folgenden Beispiel wird die Verbindungsberechtigung für die Gruppe "Accounting" der Domäne WESTCOAST aufgehoben.  
  
```Transact-SQL  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
