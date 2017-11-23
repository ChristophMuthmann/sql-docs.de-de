---
title: LocalDBStartTracing-Funktion | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: LocalDBStartTracing
apilocation: sqluserinstance.dll
apitype: DLLExport
ms.assetid: c7b83833-6d2a-4a06-9cb7-42767bed52c6
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5550575a093f1b1e9f0fc40a61918bdf23d5f8a7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="localdbstarttracing-function"></a>LocalDBStartTracing-Funktion
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Aktiviert die Ablaufverfolgung der API-Aufrufe für alle SQL Server Express LocalDB-Instanzen, die von der aktuellen Windows-Benutzer gehören.  
  
 **Headerdatei:** sqlncli.h  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT LocalDBStartTracing();  
```  
  
## <a name="returns"></a>Rückgabewert  
 S_OK  
 Die Funktion wurde erfolgreich ausgeführt.  
  
 [LOCALDB_ERROR_XEVENT_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-xevent-failed.md)  
 Fehler beim Starten des XEvent-Moduls innerhalb der LocalDB-Instanz-API.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Ein unerwarteter Fehler ist aufgetreten. Weitere Informationen finden Sie im Ereignisprotokoll.  
  
## <a name="remarks"></a>Hinweise  
 Ein Codebeispiel, in dem die LocalDB-API verwendet wird, finden Sie unter [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Express LocalDB-Header und -Versionsinformationen](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
