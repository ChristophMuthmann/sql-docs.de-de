---
title: BeginTrans, CommitTrans und RollbackTrans-Methoden (ADO) | Microsoft Docs
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
- Connection15::raw_RollbackTrans
- Connection15::CommitTrans
- Connection15::raw_CommitTrans
- Connection15::raw_BeginTrans
- Connection15::BeginTrans
- Connection15::RollbackTrans
helpviewer_keywords:
- BeginTrans method [ADO]
- CommitTrans method [ADO]
- RollbackTrans method [ADO]
ms.assetid: d4683472-4120-4236-8640-fa9ae289e23e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0d1f3a607ed6b39100b5de5c2d166bc428fbae7f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans, CommitTrans und RollbackTrans-Methoden (ADO)
Diese Transaktionsmethoden verwalten transaktionsverarbeitung in einem [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt wie folgt:  
  
-   **BeginTrans** beginnt eine neue Transaktion.  
  
-   **CommitTrans** speichert Änderungen und beendet die aktuelle Transaktion. Es kann auch eine neue Transaktion starten.  
  
-   **RollbackTrans** bricht alle während der aktuellen Transaktion vorgenommenen Änderungen ab und beendet die Transaktion. Es kann auch eine neue Transaktion starten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **BeginTrans** kann aufgerufen werden, als eine Funktion, die gibt eine **lange** Variable, der angibt, der Schachtelungsebene der Transaktion.  
  
#### <a name="parameters"></a>Parameter  
 *Objekt*  
 Ein **Verbindung** Objekt.  
  
## <a name="connection"></a>Verbindung  
 Verwenden Sie diese Methoden mit einem **Verbindung** Objekt, wenn Sie speichern oder eine Reihe von Änderungen an den Quelldaten als einzelne Einheit abbrechen möchten. Z. B. zum Übertragen von Geld zwischen Konten Sie Subtrahieren eines, und fügen die gleiche Menge an die andere. Wenn entweder aktualisieren, dass ein Fehler auftritt, Wägen Sie die Konten nicht mehr. Diese Änderungen innerhalb einer geöffneten Transaktion wird sichergestellt, dass entweder alle oder keine der Änderungen durchlaufen.  
  
> [!NOTE]
>  Nicht alle Anbieter unterstützen Transaktionen. Überprüfen Sie, ob der Anbieter definierte Eigenschaft "**Transaktion DDL**" wird angezeigt, der **Verbindung** des Objekts [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung, die angibt, dass der Anbieter unterstützt Transaktionen. Wenn der Anbieter keine Transaktionen unterstützt, wird das Aufrufen einer der folgenden Methoden einen Fehler zurück.  
  
 Nach dem Aufruf der **BeginTrans** -Methode des Anbieters wird nicht mehr sofort ein Commit ausgeführt, bis zum Aufruf von **CommitTrans** oder **RollbackTrans** zum Beenden der die Transaktion.  
  
 Für Anbieter, die geschachtelte Transaktionen unterstützen Aufrufen der **BeginTrans** Methode innerhalb einer geöffneten Transaktion wird eine neue, geschachtelte Transaktion gestartet. Der Rückgabewert gibt an, der Schachtelungsebene: ein Rückgabewert von "1" gibt an, Sie haben eine Transaktion der obersten Ebene geöffnet (d. h., die Transaktion ist nicht geschachtelte innerhalb einer anderen Transaktion), "2" gibt an, dass Sie eine Transaktion der zweiten Ebene (a geöffnet haben geschachtelten TRANSACTION-Anweisung innerhalb einer Transaktion auf der obersten Ebene), und so weiter. Aufrufen von **CommitTrans** oder **RollbackTrans** wirkt sich auf nur die zuletzt geöffnete Transaktion, und Sie müssen schließen oder Rollback für die aktuelle Transaktion aus, bevor Sie alle auf höherer Ebene Transaktionen auflösen können.  
  
 Aufrufen der **CommitTrans** Methode innerhalb einer geöffneten Transaktion für die Verbindung vorgenommenen Änderungen gespeichert und beendet die Transaktion. Aufrufen der **RollbackTrans** Methode kehrt alle Änderungen innerhalb einer geöffneten Transaktion und beendet die Transaktion. Beide Methoden aufgerufen werden, wenn es keine Transaktion geöffnet ist, wird ein Fehler generiert.  
  
 Je nach den **Verbindung** des Objekts [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) -Eigenschaft, Aufrufen von entweder der **CommitTrans** oder **RollbackTrans** Methoden möglicherweise automatisch eine neue Transaktion gestartet. Wenn die **Attribute** -Eigenschaftensatz auf **AdXactCommitRetaining**, der Anbieter startet automatisch eine neue Transaktion nach dem ein **CommitTrans** aufrufen. Wenn die **Attribute** -Eigenschaftensatz auf **AdXactAbortRetaining**, der Anbieter startet automatisch eine neue Transaktion nach dem ein **RollbackTrans** aufrufen.  
  
## <a name="remote-data-service"></a>Remote Data Service  
 Die **BeginTrans**, **CommitTrans**, und **RollbackTrans** Methoden sind nicht verfügbar für eine clientseitige **Verbindung** Objekt.  
  
## <a name="applies-to"></a>Gilt für  
 [Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [BeginTrans, CommitTrans und RollbackTrans-Methoden (Beispiel) (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans, CommitTrans und RollbackTrans Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes-Eigenschaft (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
