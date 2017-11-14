---
title: "Löschen von Datensätzen, die mit der Delete-Methode | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6975a45ddf15f1a42709fe7c4ab069ba0aa37bea
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="deleting-records-using-the-delete-method"></a>Löschen von Datensätzen, die mit der Delete-Methode
Mithilfe der **löschen** Methode kennzeichnet den aktuellen Datensatz oder eine Gruppe von Datensätzen in einer **Recordset** Objekt zum Löschen. Wenn die **Recordset** Objekt lässt keine Datensätze löschen, ein Fehler auftritt. Wenn Sie sich im sofortupdatemodus sind, werden Löschvorgänge sofort in der Datenbank. Wenn ein Datensatz (aufgrund der Datenbank Verletzungen der Integrität, z. B.) wurde erfolgreich gelöscht werden kann, der Datensatz bleibt im Bearbeitungsmodus nach dem Aufruf von **Update.** Dies bedeutet, dass Sie das Update mit abbrechen müssen [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) vor dem Verschieben aus dem aktuellen Datensatz (z. B. [schließen](../../../ado/reference/ado-api/close-method-ado.md), [verschieben](../../../ado/reference/ado-api/move-method-ado.md), oder [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Wenn Sie im Batchmodus Update ausgeführt werden, die Datensätze werden zum Löschen aus dem Cache markiert und das eigentliche löschen erfolgt beim Aufrufen der **UpdateBatch** Methode. (Die gelöschten Datensätze anzeigen möchten, legen Sie die **Filter** Eigenschaft **AdFilterAffectedRecords** nach **löschen** aufgerufen wird.)  
  
 Beim Abrufen von Feldwerten aus dem gelöschten Datensatz generiert einen Fehler. Nach dem Löschen des aktuellen Datensatzes, bleibt der gelöschte Datensatz aktuell, bis Sie zu einem anderen Datensatz wechseln. Nachdem Sie verschieben Weg von den gelöschten Datensatz nicht mehr darauf zugreifen können.  
  
 Wenn Sie Löschvorgänge in einer Transaktion schachteln, können Sie gelöschte Datensätze wiederherstellen, indem Sie mit der **RollbackTrans** Methode. Wenn im Batchmodus für Update erhalten können Sie Abbrechen einer ausstehende Löschung oder eine Gruppe von ausstehenden Löschvorgängen mithilfe der **CancelBatch** Methode.  
  
 Schlägt der Versuch zum Löschen von Datensätzen aufgrund eines Konflikts mit dem zugrunde liegenden Daten (z. B. ein Datensatz wurde bereits gelöscht von einem anderen Benutzer), der Anbieter gibt Warnungen, um die **Fehler** Auflistung jedoch nicht das Programm angehalten wurde die Ausführung. Ein Laufzeitfehler tritt nur dann, wenn auf den angeforderten Datensätzen Konflikte bestehen.  
  
 Wenn die **eindeutige Tabelle** dynamische Eigenschaft festgelegt ist und die **Recordset** ist das Ergebnis der Ausführung einer JOIN-Operation für mehrere Tabellen, die **löschen** Methode werden nur Zeilen löschen aus der Tabelle mit dem Namen der **eindeutige Tabelle** Eigenschaft.  
  
 Die **löschen** Methode nimmt ein optionales Argument, das können Sie angeben, welche Datensätze von betroffen sind der **löschen** Vorgang. Die einzigen gültigen Werte für dieses Argument sind eines der folgenden ADO **AffectEnum** -Enumerationskonstanten:  
  
-   **AdAffectCurrent** betrifft nur den aktuellen Datensatz.  
  
-   **AdAffectGroup** betrifft nur die Datensätze, die das aktuelle erfüllen **Filter** Einstellung der Eigenschaft. Die **Filter** Eigenschaft muss festgelegt werden, um eine **FilterGroupEnum** Wert oder ein Array von **Lesezeichen** zur Verwendung dieser Option.  
  
 Der folgende Code zeigt ein Beispiel für **AdAffectGroup** beim Aufrufen der **löschen** Methode. In diesem Beispiel fügt einige Datensätze, die die Stichprobe **Recordset** und aktualisiert die Datenbank. Anschließend Filtern die **Recordset** mithilfe der **AdFilterAffectedRecords** Filter Enumerationskonstante, die nur die neu hinzugefügte Datensätze im sichtbar bleibt die **Recordset.** Zum Schluss ruft es die **löschen** Methode und gibt an, dass alle Datensätze, die das aktuelle erfüllen **Filter** (neuer Datensätze) für die Einstellung der Eigenschaft gelöscht werden soll.  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```

