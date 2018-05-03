---
title: 'Schritt 2: Initialisieren der wichtigsten Listenfeld | Microsoft Docs'
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
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afef142bef13daea6ba03fa967f87198c6ebe662
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="step-2-initialize-the-main-list-box"></a>Schritt 2: Initialisieren der wichtigsten Listenfeld
Um globale Datensatz und Recordset-Objekte zu deklarieren, fügen Sie den folgenden Code in die (Allgemein) (Deklarationen) für Form1 ein:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 Dieser Code deklariert globale Objektverweise für Aufzeichnung und Recordset-Objekte, die weiter unten in diesem Szenario verwendet werden soll.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>Zum Herstellen einer Verbindung mit einer URL und Auffüllen von IstMain  
 Legen Sie den folgenden Code in der Form Load-Ereignishandler für Form1:  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=http://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 Dieser Code instanziiert die globalen Datensatz und Recordset-Objekte. Das Datensatzobjekt `grec`, mit einer angegebenen als ActiveConnection URL geöffnet wird. Wenn die URL vorhanden ist, wird sie geöffnet. Wenn es nicht bereits vorhanden ist, wird er erstellt. Beachten Sie, die ersetzt werden soll "http://servername/foldername/" durch eine gültige URL aus Ihrer Umgebung.  
  
 Das Recordset-Objekt `grs`, geöffnet wird, auf die untergeordneten Elemente des Datensatzes, `grec`. Klicken Sie dann `lstMain` wird aufgefüllt, die Dateinamen der Ressourcen in der URL veröffentlicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Internet, die Publishing-Szenario](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Schritt 1: Einrichten von Visual Basic-Projekt](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Schritt 3: Auffüllen des Listenfelds „Fields“](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
