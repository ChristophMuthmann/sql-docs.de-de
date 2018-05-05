---
title: ConnectionValidSharedMemory-Funktion in dbmslpcn.dll Shared Memory | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8431da78ff750e84feb170c1d50f639adb6c9d1f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>ConnectionValidSharedMemory-Funktion in dbmslpcn.dll Shared Memory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Die Funktion bestimmt, ob SQL Server Shared Memory installiert und aktiv ist.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parameter  
 *szServerName*  
  
-   Typ: **Char\***  
  
-   Der Name des SQL-Servers.  
  
## <a name="return-value"></a>Rückgabewert  
 Typ: **BOOL**  
  
 Gibt 0, wenn er nicht gültig ist; Gibt andernfalls ungleich NULL zurück.  
  
  
