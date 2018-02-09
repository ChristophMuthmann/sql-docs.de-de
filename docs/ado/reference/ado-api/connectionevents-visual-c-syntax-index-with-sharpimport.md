---
title: 'ConnectionEvents (Visual C++-Syntax Index mit #import) | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'ConnectionEvents collection [ADO], Visual C++ syntax index with #import'
ms.assetid: dd052d36-7730-4400-822b-0544fb1992b4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c99d265baba06dd965e0d85bebd88dd1603d88ba
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="connectionevents-visual-c-syntax-index-with-import"></a>ConnectionEvents (Visual C++-Syntax Index mit #import)
## <a name="events"></a>Ereignisse  
  
```  
HRESULT InfoMessage( struct Error * pError, enum  
    EventStatusEnum *     adStatus, struct _Connection * pConnection );  
  
HRESULT BeginTransComplete( long TransactionLevel,  
    struct Error * pError, enum EventStatusEnum * adStatus, struct  
    _Connection * pConnection );  
  
HRESULT CommitTransComplete( struct Error *  
    pError, enum EventStatusEnum     * adStatus, struct _Connection *  
    pConnection );  
  
HRESULT RollbackTransComplete( struct Error *  
    pError, enum     EventStatusEnum * adStatus, struct _Connection *  
    pConnection );  
  
HRESULT WillExecute( BSTR * Source, enum  
    CursorTypeEnum * CursorType,  
    enum LockTypeEnum * LockType, long * Options, enum EventStatusEnum *  
    adStatus, struct _Command * pCommand, struct _Recordset * pRecordset,  
    struct _Connection * pConnection );  
  
HRESULT ExecuteComplete( long RecordsAffected, struct  
    Error * pError,     enum EventStatusEnum * adStatus, struct _Command  
    * pCommand, struct     _Recordset * pRecordset, struct _Connection *  
    pConnection );  
  
HRESULT WillConnect( BSTR * ConnectionString, BSTR *  
    UserID, BSTR *     Password, long * Options, enum EventStatusEnum *  
    adStatus, struct     _Connection * pConnection );  
  
HRESULT ConnectComplete( struct Error *  
    pError, enum EventStatusEnum *     adStatus, struct _Connection *  
    pConnection );  
  
HRESULT Disconnect( enum EventStatusEnum *  
    adStatus, struct _Connection *     pConnection );  
```
