---
title: 'RecordsetEvents (Visual C++-Syntax Index mit #import) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- RecordsetEvents collection [ADO]
ms.assetid: b7021f11-8242-4e9f-92e9-1a4472673fb1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9703ca2b2a3933842169a45efe5e0631bc002545
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
