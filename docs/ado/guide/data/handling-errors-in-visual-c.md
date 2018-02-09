---
title: Behandeln von Fehlern in Visual C++ | Microsoft Docs
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
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07761673140a15ca2d7f28504528b418e4fc399a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="handling-errors-in-visual-c"></a>Behandeln von Fehlern in Visual C++
In COM geben die meisten Vorgänge einen HRESULT-Rückgabecode, der angibt, ob eine Funktion wurde erfolgreich abgeschlossen. Die #import-Direktive Wrappercode um jede "unformatiert" Methode oder Eigenschaft generiert und überprüft das zurückgegebene HRESULT. Wenn das HRESULT Fehler weist darauf hin, löst der Wrappercode einen COM-Fehler vom aufrufenden _com_issue_errorex() mit dem HRESULT-Rückgabecode als Argument an. COM-Fehlerobjekte abgefangen werden können, einem **Try-Catch-** Block. (Aus Gründen der Effizienz fangen Sie einen Verweis auf ein _com_error-Objekt).  
  
 Beachten Sie, dass dies die ADO-Fehler sind: von der ADO-Vorgangsfehler führt. Der zugrunde liegende Anbieter zurückgegebene Fehler werden als **Fehler** Objekte in der **Verbindung** des Objekts **Fehler** Auflistung.  
  
 Die #import-Direktive erstellt nur Fehlerbehandlungsroutinen für Methoden und Eigenschaften, die in der ADO-DLL deklariert. Allerdings können Sie diese gleichen Fehlerbehandlungsmechanismus nutzen durch Ihre eigene Überprüfung von Fehlern Makro oder zur Inlinefunktion-Funktion schreiben. Finden Sie im Visual C++®-Erweiterungen für Beispiele.
