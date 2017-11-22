---
title: Stream-Eigenschaft | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords: Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d55d9d2619f3739db97570e8195c7a199425252
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stream-property"></a>Streameigenschaft
Ruft ab oder legt einen OLE DB- **Stream** Objekt vom bzw. auf eine **ADOStreamConstruction** Objekt.  
  
 Lese-/Schreibzugriff.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>Parameter  
 *ppStream*  
 Zeiger auf einen OLE DB- **Stream** Objekt.  
  
 *pStream*  
 OLE DB- **Stream** Objekt.  
  
## <a name="return-values"></a>Rückgabewerte  
 Diese Eigenschaftsmethode gibt die standard-HRESULT-Werte zurück. Dies schließt S_OK und E_FAIL zurück.  
  
## <a name="applies-to"></a>Gilt für  
 [ADOStreamConstruction-Schnittstelle](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
