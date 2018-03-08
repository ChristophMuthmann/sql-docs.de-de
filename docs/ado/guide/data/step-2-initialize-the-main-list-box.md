---
title: 'Schritt 2: Initialisieren der wichtigsten Listenfeld | Microsoft Docs'
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
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60ece26fab2c6f691614b609d1dd3f07f42231e4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
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
  
 Dieser Code instanziiert die globalen Datensatz und Recordset-Objekte. Das Datensatzobjekt `grec`, mit einer angegebenen als ActiveConnection URL geöffnet wird. Wenn die URL vorhanden ist, wird sie geöffnet. Wenn es nicht bereits vorhanden ist, wird er erstellt. Beachten Sie, dass "http://servername/foldername/" durch eine gültige URL aus Ihrer Umgebung ersetzt werden soll.  
  
 Das Recordset-Objekt `grs`, geöffnet wird, auf die untergeordneten Elemente des Datensatzes, `grec`. Klicken Sie dann `lstMain` wird aufgefüllt, die Dateinamen der Ressourcen in der URL veröffentlicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Internet, die Publishing-Szenario](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Schritt 1: Einrichten von Visual Basic-Projekt](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Schritt 3: Auffüllen des Listenfelds „Fields“](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
