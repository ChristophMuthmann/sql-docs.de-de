---
title: Wenn Fehler vorhergesehen | Microsoft Docs
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
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0fc74732fb812f1b13bcb52b8eda97311ae562d7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="anticipating-errors"></a>Vorhersehen von Fehlern
Fehler Verhinderung von Datenverlust sind mindestens so wichtig wie die Fehlerbehandlung. In diesem letzten Abschnitt enthält eine kurze Liste mit Vorsichtsmaßnahmen, die Ihre Anwendung um zu helfen, Fehler, die weniger wahrscheinlich auftreten kann.  
  
 Überprüfen des Status von Objekten durch Überprüfung des Werts der **Zustand** Eigenschaft vor dem Versuch, einen Vorgang über die Objekte auszuführen. Z. B., wenn Ihre Anwendung einen globalen verwendet **Verbindung**, überprüfen Sie ihre **Zustand** Eigenschaft, um festzustellen, ob sie bereits vor dem Aufruf geöffnet ist die **öffnen** Methode.  
  
-   Jedes Programm, das Daten von einem Benutzer akzeptiert, muss es sich um Code aus, um diese Daten zu überprüfen, vor dem Senden an den Datenspeicher enthalten. Sie können nicht auf die Datenspeicher, der Anbieter, ADO oder sogar Ihre Programmiersprache Sie über Probleme informieren basieren. Überprüfen Sie jedes Byte von Ihren Benutzern an, und stellen Sie sicher, dass die Daten der richtige Typ für dieses Feld ist und nicht erforderlichen Felder leer sind eingegeben.  
  
 Überprüfen Sie die Daten, bevor Sie versuchen, alle Daten in den Datenspeicher schreiben. Die einfachste Möglichkeit hierzu ist, behandelt der **WillMove** Ereignis oder den **WillUpdateRecordset** Ereignis. Eine ausführlichere Diskussion zur Behandlung von ADO-Ereignissen finden Sie unter [ADO-Ereignisse behandeln](../../../ado/guide/data/handling-ado-events.md).  
  
 Stellen Sie sicher, dass **Recordset** Objekte sind nicht über die Grenzen der der **Recordset** vor dem Versuch, die Zeiger für den Datensatz zu verschieben. Wenn Sie versuchen, **MoveNext** Wenn **EOF** ist "true" oder **MovePrev** Wenn **BOF** ist "true", wird eine Fehlermeldung angezeigt. Wenn Sie eine der Ausführen der **verschieben** Methoden Wenn beide **EOF** und **BOF** sind "true", wird ein Fehler generiert.  
  
 Außerdem kommt es zu Fehlern, wenn Sie versuchen, die Vorgänge wie z. B. **Seek** und **suchen** für eine leere **Recordset**.
