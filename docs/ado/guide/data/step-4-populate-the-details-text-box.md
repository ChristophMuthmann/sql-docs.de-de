---
title: "Schritt 4: Füllen Sie das Textfeld Details | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 512ad22b6529adcf065cacb219d1f0acc025c306
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="step-4-populate-the-details-text-box"></a>Schritt 4: Füllen Sie das Textfeld "Details"
Um das Textfeld "Details" aufzufüllen, erstellen Sie eine neue Unterroutine namens **RecFields** und fügen Sie den folgenden Code:  
  
```  
Sub recFields(r As Record, l As ListBox, t As TextBox)  
    Dim f As Field  
    Dim s As Stream  
    Set s = New Stream  
    Dim str As String  
  
    For Each f In r.Fields  
        l.AddItem f.Name & ": " & f.Value  
    Next  
    t.Text = ""  
    If r!RESOURCE_CONTENTCLASS = "text/plain" Then  
        s.Open r, adModeRead, adOpenStreamFromRecord  
        str = s.ReadText(1)  
        s.Position = 0  
        If Asc(Mid(str, 1, 1)) = 63 Then '//63 = "?"  
            s.Charset = "ascii"  
            s.Type = adTypeText  
        End If  
        t.Text = s.ReadText(adReadAll)  
    End If  
End Sub  
```  
  
 Dieser Code füllt `lstDetails` mit den Feldern und Werten des einfachen Datensatzes übergeben `recFields`. Wenn die Ressource eine Textdatei ist, wird aus dem Datensatz der Computerressource Textstream geöffnet. Im Code wird ermittelt, ob der Zeichensatz ASCII und den Inhalt des Streams in kopiert `txtDetails`.  
  
## <a name="see-also"></a>Siehe auch  
 [Internet, die Publishing-Szenario](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Schritt 3: Auffüllen der Felder Listenfeld](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)

