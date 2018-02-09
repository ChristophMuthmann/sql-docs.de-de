---
title: Stream-Eigenschaft | Microsoft Docs
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
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc56c9a655c4e85f76cae877579b9a344c11ff4d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
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
