---
title: Kapitel-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7cfa863254391760a45f8857f002ac92f25dd07
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="chapter-property-ado"></a>Kapitel-Eigenschaft (ADO)
Ruft ab oder legt einen OLE DB- **Kapitel** Objekt vom bzw. auf eine [ADORecordsetConstruction Schnittstelle](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md) Objekt. Bei Verwendung von **Put_Chapter** festzulegende der **Kapitel** -Objekt ist eine Teilmenge von Zeilen in einer ADO aktiviert [Recordset-Objekts](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt. Dadurch wird das aktuelle Kapitel des der **Rowset**Objekt. Dies ist eine Eigenschaft mit Lese- und Schreibzugriff.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>Parameter  
 *plChapter*  
 Ein Zeiger auf das Handle des Kapitels.  
  
 *LChapter*  
 Das Handle des Kapitels.  
  
## <a name="return-values"></a>Rückgabewerte  
 Diese Eigenschaftsmethode gibt die standardmäßige HRESULT-Werte, einschließlich S_OK und E_FAIL zurück.  
  
## <a name="applies-to"></a>Gilt für  
 [ADORecordsetConstruction-Schnittstelle](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
