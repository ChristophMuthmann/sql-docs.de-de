---
title: SMO and DMO XPs (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6922050ae1ff3451c6484319fced5973a416a460
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO and DMO XPs (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Option SMO and DMO XPs, um erweiterte gespeicherte Prozeduren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object (SMO) auf diesem Server zu aktivieren.  
  
 Beachten Sie, dass DMO beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt wurde.  
  
 Eine Beschreibung der möglichen Werte finden Sie in der folgenden Tabelle:  
  
|value|Bedeutung|  
|-----------|-------------|  
|0|SMO-XPs sind nicht verfügbar.|  
|1|SMO-XPS sind verfügbar. Dies ist die Standardeinstellung.|  
  
 Diese Einstellung wird sofort wirksam.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die erweiterten gespeicherten Prozeduren von SMO aktiviert.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Programmierungshandbuch für SQL Server Management Objects &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
