---
title: Transaktionsverarbeitung | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55f563b145cf77dc64879801c4603bd51234b0f4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="transaction-processing"></a>Transaktionsverarbeitung
Ein *Transaktion* begrenzt Anfang und Ende einer Reihe von Datenzugriffsvorgänge über eine Verbindung ausgeführt. Unterliegen die Transaktionsfunktionen des Ihre Datenquelle anzuwenden die **Verbindung** Objekt auch bietet die Möglichkeit zum Erstellen und Verwalten von Transaktionen. Beispielsweise können mithilfe von Microsoft OLE DB-Anbieter für SQL Server auf eine Datenbank auf Microsoft SQL Server zugreifen, Sie mehrere geschachtelte Transaktionen für die Befehle erstellen, die Sie ausführen.  
  
 ADO wird sichergestellt, dass Änderungen mit einer Datenquelle, die aufgrund der Vorgänge in einer Transaktion erfolgreich zusammen oder überhaupt nicht auftreten.  
  
 Wenn Sie die Transaktion abbrechen oder wenn einer der Vorgänge ein Fehler auftritt, wird das Ergebnis sein, als ob keiner der Vorgänge in der Transaktion aufgetreten ist. Die Datenquelle bleibt wie vor dem Beginn der Transaktion.  
  
 ADO bietet die folgenden Methoden zum Steuern von Transaktionen: **BeginTrans**, **CommitTrans**, und **RollbackTrans**. Verwenden Sie diese Methoden mit einem **Verbindung** Objekt, wenn Sie speichern oder eine Reihe von Änderungen an den Quelldaten als einzelne Einheit abbrechen möchten. Z. B. zum Übertragen von Geld zwischen Konten Sie Subtrahieren eines, und fügen die gleiche Menge an die andere. Wenn entweder aktualisieren, dass ein Fehler auftritt, Wägen Sie die Konten nicht mehr. Diese Änderungen innerhalb einer geöffneten Transaktion wird sichergestellt, dass entweder alle oder keine der Änderungen durchlaufen.  
  
> [!NOTE]
>  Nicht alle Anbieter unterstützen Transaktionen. Überprüfen Sie, ob der Anbieter definierte Eigenschaft "**Transaktion DDL**" wird angezeigt, der **Verbindung** des Objekts [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung, die angibt, dass der Anbieter unterstützt Transaktionen. Wenn der Anbieter keine Transaktionen unterstützt, wird das Aufrufen einer der folgenden Methoden einen Fehler zurück.  
  
 Nach dem Aufruf der **BeginTrans** -Methode des Anbieters wird nicht mehr sofort ein Commit ausgeführt, bis zum Aufruf von **CommitTrans** oder **RollbackTrans** zum Beenden der die Transaktion.  
  
 Aufrufen der **CommitTrans** Methode innerhalb einer geöffneten Transaktion für die Verbindung vorgenommenen Änderungen gespeichert und beendet die Transaktion. Aufrufen der **RollbackTrans** Methode kehrt alle Änderungen innerhalb einer geöffneten Transaktion und beendet die Transaktion. Beide Methoden aufgerufen werden, wenn es keine Transaktion geöffnet ist, wird ein Fehler generiert.  
  
 Je nach den **Verbindung** des Objekts [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) -Eigenschaft, Aufrufen von entweder der **CommitTrans** oder **RollbackTrans** Methode möglicherweise automatisch eine neue Transaktion gestartet. Wenn die **Attribute** -Eigenschaftensatz auf **AdXactCommitRetaining**, der Anbieter startet automatisch eine neue Transaktion nach dem ein **CommitTrans** aufrufen. Wenn die **Attribute** -Eigenschaftensatz auf **AdXactAbortRetaining**, der Anbieter startet automatisch eine neue Transaktion nach dem ein **RollbackTrans** aufrufen.  
  
## <a name="transaction-isolation-level"></a>Transaction Isolation Level  
 Verwenden der **IsolationLevel** -Eigenschaft zum Festlegen der Isolationsstufe einer Transaktion auf eine **Verbindung** Objekt. Die Einstellung wird wirksam, bis zum nächsten Aufruf der [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) Methode. Wenn die Ebene der Isolation, die Sie anfordern, nicht verfügbar ist, kann der Anbieter das größere Potenzial der Isolation zurückgegeben. Finden Sie in der **IsolationLevel** Eigenschaft in der ADO-Programmierreferenz für Weitere Informationen zu gültigen Werten.  
  
## <a name="nested-transactions"></a>Geschachtelte Transaktionen  
 Für Anbieter, die geschachtelte Transaktionen unterstützen Aufrufen der **BeginTrans** Methode innerhalb einer geöffneten Transaktion wird eine neue, geschachtelte Transaktion gestartet. Der Rückgabewert gibt an, der Schachtelungsebene: ein Rückgabewert von "1" gibt an, Sie haben eine Transaktion der obersten Ebene geöffnet (d. h., die Transaktion ist nicht geschachtelte innerhalb einer anderen Transaktion), "2" gibt an, dass Sie eine Transaktion der zweiten Ebene (a geöffnet haben geschachtelten TRANSACTION-Anweisung innerhalb einer Transaktion auf der obersten Ebene), und so weiter. Aufrufen von **CommitTrans** oder **RollbackTrans** wirkt sich auf nur die zuletzt geöffnete Transaktion, und Sie müssen schließen oder Rollback für die aktuelle Transaktion aus, bevor Sie alle auf höherer Ebene Transaktionen auflösen können.
