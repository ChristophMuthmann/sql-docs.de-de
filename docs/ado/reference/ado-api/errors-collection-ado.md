---
title: Errors-Auflistung (ADO) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords: Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 66afd514c40c646fad62d5fc0302bc486af7e653
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="errors-collection-ado"></a>Errors-Auflistung (ADO)
Enthält alle der [Fehler](../../../ado/reference/ado-api/error-object.md) in Reaktion auf einen einzelnen anbieterbezogenen Fehler erstellten Objekte.  
  
## <a name="remarks"></a>Hinweise  
 Jeder Vorgang im Zusammenhang mit ADO-Objekten kann eine oder mehrere Anbieterfehler generieren. Sobald ein Fehler auftritt, eine oder mehrere **Fehler** Objekte platziert werden können, der **Fehler** Auflistung von der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt. Wenn ein anderer ADO-Vorgang einen Fehler generiert die **Fehler** Auflistung deaktiviert ist, und die neue Gruppe von **Fehler** Objekte platziert werden können, der **Fehler** Auflistung.  
  
 Jede **Fehler** -Objekt stellt einen bestimmten Anbieterfehler, keinen ADO-Fehler dar. ADO-Fehler werden an den Mechanismus zur Ausnahmebehandlung zur Laufzeit verfügbar gemacht. Z. B. in Microsoft Visual Basic das Vorkommen einer ADO-spezifische Fehler wird ausgelöst, eine [OnError](../../../ado/reference/rds-api/onerror-event-rds.md) Ereignis und in der **Err** Objekt.  
  
 ADO-Vorgänge, die keinen Fehler erzeugen haben keine Auswirkung auf die **Fehler** Auflistung. Verwenden der [deaktivieren](../../../ado/reference/ado-api/clear-method-ado.md) Methode manuell löschen, die **Fehler** Auflistung.  
  
 Der Satz von **Fehler** Objekte in der **Fehler** Auflistung beschreibt alle Fehler, die als Antwort auf eine einzelne Anweisung aufgetreten sind. Auflisten von den speziellen Fehlern in der **Fehler** Auflistung ermöglicht die Fehlerbehandlungsroutinen genauer bestimmen Sie die Ursache und den Ursprung eines Fehlers, und ergreifen geeignete Maßnahmen zur Wiederherstellung.  
  
 Einige Eigenschaften und Methoden zurück Warnungen, die als **Fehler** Objekte in der **Fehler** Auflistung jedoch die Ausführung des Programms nicht angehalten werden. Vor dem Aufrufen der [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), oder [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methoden auf eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt, das [Öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) Methode auf eine **Verbindung** -Objekt, oder legen Sie die [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft auf einen **Recordset** -Objekt, rufen Sie die **deaktivieren**Methode für die **Fehler** Auflistung. Auf diese Weise Sie erfahren die [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft von der **Fehler** zurückgegebene Auflistung zur Prüfung auf Warnungen.  
  
> [!NOTE]
>  Finden Sie unter der **Fehler** Objektthema für eine ausführlichere Erläuterung der Art und Weise, die ein einzelnen ADO-Vorgang kann mehrere Fehler generiert.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Fehler-Auflistungseigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Error-Objekt](../../../ado/reference/ado-api/error-object.md)   
 [Anhang A: Daten und Dienstanbieter](../../../ado/guide/appendixes/appendix-a-providers.md)
