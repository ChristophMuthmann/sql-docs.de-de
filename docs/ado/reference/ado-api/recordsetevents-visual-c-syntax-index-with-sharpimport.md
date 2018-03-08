---
title: 'RecordsetEvents (Visual C++-Syntax Index mit #import) | Microsoft Docs'
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
- RecordsetEvents collection [ADO]
ms.assetid: b7021f11-8242-4e9f-92e9-1a4472673fb1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b30117acb4aa0a621b7bb1b2361b09b58912d99
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="recordsetevents-visual-c-syntax-index-with-import"></a>RecordsetEvents (Visual C++-Syntax Index mit #import)
## <a name="events"></a>Ereignisse  
  
```  
HRESULT WillChangeField( long cFields, const  
    _variant_t & Fields, enum     EventStatusEnum * adStatus, struct  
    _Recordset * pRecordset );  
  
HRESULT FieldChangeComplete( long cFields, const  
    _variant_t & Fields,     struct Error * pError, enum EventStatusEnum  
    * adStatus, struct     _Recordset * pRecordset );  
  
HRESULT WillChangeRecord( enum EventReasonEnum  
    adReason, long cRecords,     enum EventStatusEnum * adStatus, struct  
    _Recordset * pRecordset );  
  
HRESULT RecordChangeComplete( enum EventReasonEnum  
    adReason, long     cRecords, struct Error * pError, enum  
    EventStatusEnum * adStatus,     struct _Recordset * pRecordset );  
  
HRESULT WillChangeRecordset( enum EventReasonEnum  
    adReason, enum     EventStatusEnum * adStatus, struct _Recordset *  
    pRecordset );  
  
HRESULT RecordsetChangeComplete( enum  
    EventReasonEnum adReason, struct     Error * pError, enum  
    EventStatusEnum * adStatus, struct _Recordset *     pRecordset );  
  
HRESULT WillMove( enum EventReasonEnum adReason, enum  
    EventStatusEnum *     adStatus, struct _Recordset * pRecordset );  
  
HRESULT MoveComplete( enum EventReasonEnum adReason, struct  
    Error *     pError, enum EventStatusEnum * adStatus, struct  
    _Recordset * pRecordset );  
  
HRESULT EndOfRecordset( VARIANT_BOOL * fMoreData, enum  
    EventStatusEnum *     adStatus, struct _Recordset * pRecordset );  
  
HRESULT FetchProgress( long Progress, long MaxProgress,  
    enum     EventStatusEnum * adStatus, struct _Recordset * pRecordset );  
  
HRESULT FetchComplete( struct Error * pError, enum  
    EventStatusEnum *     adStatus, struct _Recordset * pRecordset );  
```
