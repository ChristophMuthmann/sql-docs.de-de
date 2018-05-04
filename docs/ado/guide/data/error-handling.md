---
title: Fehlerbehandlung | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e302e38ee983f8057aa2ce1be321e195abe0afbb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="error-handling"></a>Fehlerbehandlung
ADO verwendet mehrere unterschiedliche Verfahren, um eine Anwendung von Fehlern zu benachrichtigen, die auftreten. Dieser Abschnitt beschreibt die Arten von Fehlern, die auftreten können, bei Verwendung von ADO und wie Ihre Anwendung informiert wird. Schließlich werden Vorschläge dazu, wie Sie diesen Fehler zu behandeln.  
  
## <a name="how-does-ado-report-errors"></a>Wie meldet ADO Fehler?  
 ADO informiert Sie über Fehler, die auf unterschiedliche Weise:  
  
-   ADO-Fehler generieren einen Laufzeitfehler. Behandeln Sie einen ADO-Fehler gleichen genauso wie jeder andere zur Laufzeit Fehler, z. B. mit einem **On Error** -Anweisung in Visual Basic.  
  
-   Das Programm kann Fehler von OLE DB-empfangen. Ein OLE DB-Fehler generiert ebenfalls ein Laufzeitfehler ausgegeben.  
  
-   Wenn der Fehler auf Ihren Datenanbieter, einen oder mehrere bestimmte **Fehler** Objekte platziert werden, die der **Fehler** Auflistung von der **Verbindung** -Objekt, das für den Datenzugriff verwendet wurde Speichern Sie, wenn der Fehler aufgetreten ist.  
  
-   Wenn der Prozess, der ein Ereignis ausgelöst, auch einen Fehler erzeugt, werden Fehlerinformationen in platziert eine **Fehler** -Objekt und das Ereignis als Parameter übergeben. Finden Sie unter [ADO-Ereignisse behandeln](../../../ado/guide/data/handling-ado-events.md) für Weitere Informationen zu Ereignissen.  
  
-   Problemen beim Verarbeiten von batch-Updates oder andere im Zusammenhang mit Massenvorgängen eine **Recordset** können ersichtlich sein, die **Status** Eigenschaft von der **Recordset**. Z. B. einschränkungsverletzungen Schema oder keine ausreichenden Berechtigungen können angegeben werden durch **RecordStatusEnum** Werte.  
  
-   Probleme im Zusammenhang mit einem bestimmten **Feld** im aktuellen Datensatz werden auch angezeigt, durch die **Status** -Eigenschaft jedes **Feld** in die **Felder**  Auflistung von der **Datensatz** oder **Recordset**. Beispielsweise Updates, die nicht abgeschlossen werden konnte oder inkompatible Datentypen können angegeben werden durch **FieldStatusEnum** Werte.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [ADO-Fehler](../../../ado/guide/data/ado-errors.md)  
  
-   [Anbieterfehler](../../../ado/guide/data/provider-errors.md)  
  
-   [Fehlerinformationen im Zusammenhang mit Feldern](../../../ado/guide/data/field-related-error-information.md)  
  
-   [Recordset-bezogene Fehlerinformationen](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [Behandeln von Fehlern in anderen Sprachen](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [Vorhersehen von Fehlern](../../../ado/guide/data/anticipating-errors.md)
