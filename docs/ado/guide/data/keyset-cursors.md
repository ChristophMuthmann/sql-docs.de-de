---
title: KEYSET-Cursor | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8def959d69c353449c2f862638d6edd54f786624
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="keyset-cursors"></a>KEYSET-Cursor
Das Keyset-Cursor bietet Funktionalität zwischen statischen und einen dynamischen Cursor in der Fähigkeit, Änderungen zu erkennen. Wie ein statischer Cursor kann es nicht immer zum Ändern der Mitgliedschaft und Reihenfolge des Resultsets erkennen. Z. B. einen dynamischen Cursor erkennt er Änderungen auf die Werte der Zeilen im Resultset.  
  
 Keysetgesteuerte Cursor werden durch eine Reihe von eindeutigen Bezeichnern (Schlüssel) als das Keyset bezeichnet gesteuert. Die Schlüssel werden anhand einer Reihe von Spalten erstellt, die die Zeilen im Resultset eindeutig identifizieren. Das Keyset ist die Menge der Schlüsselwerte aus allen Zeilen, die von der abfrageanweisung zurückgegeben.  
  
 Mit keysetgesteuerte Cursor ein Schlüssel erstellt und für jede Zeile im Cursor gespeichert und auf der Clientarbeitsstation oder auf dem Server gespeichert. Zugriff auf jede Zeile wird der gespeicherte Schlüssel verwendet, um die aktuellen Datenwerte aus der Datenquelle abzurufen. Resultset ist in einem keysetgesteuerten Cursor fixiert, wenn das Keyset vollständig aufgefüllt wird. Hinzufügen oder Updates, die Mitgliedschaft sind danach nicht Teil des Resultsets, bis er wieder geöffnet wird.  
  
 Änderungen an Datenwerten (getroffen entweder vom Besitzer Keyset oder andere Prozesse) sind sichtbar, wenn der Benutzer über das Resultset einen Bildlauf durchführt. Außerhalb des Cursors (durch andere Prozesse) vorgenommene einfügungen sind sichtbar, nur dann, wenn der Cursor geschlossen und erneut geöffnet wird. Einfügungen, die von innerhalb der Cursor werden am Ende des Resultsets angezeigt.  
  
 Wenn ein keysetgesteuerter Cursor versucht, eine Zeile abzurufen, die gelöscht wurde, wird die Zeile als ein "Loch" im Resultset angezeigt. Der Schlüssel für die Zeile im Keyset vorhanden ist, aber die Zeile im Resultset nicht mehr vorhanden ist. Wenn die Schlüsselwerte in einer Zeile aktualisiert werden, die Zeile gilt gelöscht, und klicken Sie dann eingefügt werden, damit dieser Zeilen auch als Lücken im Resultset angezeigt. Während ein keysetgesteuerten Cursors immer durch andere Prozesse gelöschte Zeilen erkennen kann, können sie optional die Schlüssel für Zeilen entfernen, die er selbst löscht. Keysetgesteuerte Cursor, die hierfür darf nicht ihre eigenen Löschvorgänge zu erkennen, da der Beweis entfernt wurde.  
  
 Ein Update für eine Schlüsselspalte funktioniert wie ein Löschvorgang aus, der den alten Schlüssel und einer Einfügung des neuen Schlüssels. Der neue Schlüsselwert ist nicht sichtbar, wenn das Update nicht über den Cursor erfolgte. Wenn das Update über den Cursor erfolgte, ist der neue Tastenwert am Ende des Resultsets sichtbar.  
  
 Es ist eine Variation keysetgesteuerte Cursor keysetgesteuerte standard Cursor aufgerufen. In einem keysetgesteuerten standard Cursor sind die Mitgliedschaft der Zeilen im Resultset und die Reihenfolge der Zeilen bei Öffnungszeit Cursor jedoch Änderungen an Werten, die vom cursorbesitzer vorgenommen werden und per Commit ausgeführte Änderungen vorgenommen, die von anderen Prozessen sichtbar sind. Wenn eine Änderung eine Zeile für die Mitgliedschaft ausschließt oder wirkt sich die Reihenfolge einer Zeile, die Zeile nicht ausgeblendet oder verschieben, es sei denn, der Cursor geschlossen und erneut geöffnet wird. Eingefügte Daten werden nicht angezeigt, aber Änderungen an vorhandenen Daten werden angezeigt, wenn die Zeilen abgerufen werden.  
  
 Keysetgesteuerte Cursor ist schwierig, da die Sensitivität gegenüber Änderungen der Daten von vielen unterschiedlichen Situationen abhängt ordnungsgemäß zu verwenden, wie oben beschrieben. Wenn die Anwendung nicht gleichzeitige Updates betroffen ist, programmgesteuert, fehlerhafte Schlüssel behandeln kann und muss bestimmte schlüsselgebundenen Zeilen direkt zugreifen, funktioniert jedoch möglicherweise der keysetgesteuerte Cursor für Sie. Verwenden Sie die **AdOpenKeyset CursorTypeEnum** um anzugeben, dass Sie einen Keysetcursor in ADO verwenden möchten.  
  
## <a name="see-also"></a>Siehe auch  
 [Vorwärtscursor](../../../ado/guide/data/forward-only-cursors.md)   
 [Statische Cursor](../../../ado/guide/data/static-cursors.md)   
 [Dynamische Cursor](../../../ado/guide/data/dynamic-cursors.md)

