---
title: State-Eigenschaft (ADO) | Microsoft Docs
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
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: efd795c5ae1095a11520215994185987e9cf2b32
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="state-property-ado"></a>State-Eigenschaft (ADO)
Gibt für alle entsprechenden Objekte an, ob der Zustand des Objekts offen oder geschlossen ist. Wenn das Objekt eine asynchrone Methode ausgeführt wird, gibt an, ob der aktuelle Zustand des Objekts Herstellen einer Verbindung, ausführen abgerufen wird.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **lange** , umfassen kann, ein [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) Wert. Der Standardwert ist **AdStateClosed**.  
  
## <a name="remarks"></a>Hinweise  
 Können Sie die **Zustand** -Eigenschaft können Sie den aktuellen Status eines angegebenen Objekts zu einem beliebigen Zeitpunkt zu bestimmen.  
  
 Des Objekts **Zustand** Eigenschaft kann eine Kombination von Werten aufweisen. Z. B. wenn eine Anweisung ausgeführt wird, diese Eigenschaft müssen einen kombinierten Wert des **AdStateOpen** und **AdStateExecuting**.  
  
 Die **Zustand** Eigenschaft ist schreibgeschützt.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Das Datensatzobjekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Siehe auch  
 ["ConnectionString" ConnectionTimeout und State-Eigenschaft (Beispiel) (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 ["ConnectionString" ConnectionTimeout und State-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   

