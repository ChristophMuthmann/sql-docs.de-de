---
title: 'Schritt 3: Auffüllen der Felder Listenfeld | Microsoft Docs'
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
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b7f82e92cc9293781992eccdbb04a46f8ac788fa
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="step-3-populate-the-fields-list-box"></a>Schritt 3: Auffüllen der Felder Listenfeld
Im Listenfeld Felder ausgefüllt werden, legen Sie den folgenden Code in dem Click-Ereignishandler der `lstMain`:  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 Dieser Code deklariert und instanziiert lokale Datensatz und Recordset-Objekte `rec` und `rs`zugeordnet.  
  
 Die Zeile, die im ausgewählten Ressource entspricht `lstMain` erfolgt die aktuelle Zeile `grs`. Und klicken Sie dann im Listenfeld Details deaktiviert ist und `rec` wird geöffnet, mit der aktuellen Zeile `grs` als Quelle.  
  
 Wenn die Ressource Datensatzversion Auflistung entsprechend den Angaben von [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), das lokale Recordset `rs` in den untergeordneten Elementen Datensatztyp geöffnet wird. Klicken Sie dann `lstDetails` wird mit den Werten aus den Zeilen gefüllt `rs`.  
  
 Wenn die Ressource einen einfachen Datensatz `recFields` aufgerufen wird. Weitere Informationen zu `recFields`, finden Sie im nächsten Schritt.  
  
 Wenn die Ressource ein strukturiertes Dokument ist kein Code implementiert.  
  
## <a name="see-also"></a>Siehe auch  
 [Internet, die Publishing-Szenario](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Schritt 2: Initialisieren der wichtigsten Listenfeld](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [Schritt 4: Auffüllen des Texfelds „Details“](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
