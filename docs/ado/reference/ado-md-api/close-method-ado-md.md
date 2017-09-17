---
title: Close-Methode (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 55e17b5446e881c1671068c99f8ea03f13dcf82f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="close-method-ado-md"></a>Close-Methode (ADO MD)
Schließt eine offene Cellset dar.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Hinweise  
 Mithilfe der **schließen** Methode zum Schließen einer [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) Freigeben des Objekts wird der zugehörigen Daten, einschließlich der Daten in allen verknüpften [Zelle](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [Achse](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md), oder [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) Objekte. Schließen einer **Cellset** nicht aus dem Arbeitsspeicher entfernt, können Sie die eigenschafteneinstellungen ändern und öffnen Sie es später erneut. Um ein Objekt aus dem Arbeitsspeicher vollständig zu vermeiden, legen Sie die Objektvariable auf **nichts**.  
  
 Sie können später aufrufen, die [öffnen](../../../ado/reference/ado-md-api/open-method-ado-md.md) Methode, um erneut zu öffnen die **Cellset** mithilfe der gleichen oder einer anderen Quellzeichenfolge. Während der **Cellset** Objekt geschlossen ist, Abrufen von Eigenschaften oder zum Aufrufen von Methoden, die die zugrunde liegenden Daten verweisen oder Metadaten wird ein Fehler generiert.  
  
## <a name="applies-to"></a>Gilt für  
 [Cellset-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Achsenobjekt (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Cell-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Member-Objekt (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open-Methode (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Position-Objekt (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
