---
title: Error-Objekt | Microsoft Docs
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
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71609e69fa31adcaf1f336d9529ea8bd5fa62434
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="error-object"></a>Error-Objekt
Enthält Details über Data Access-Fehlern, die auf einem einzelnen Vorgang im Zusammenhang mit dem Anbieter beziehen.  
  
## <a name="remarks"></a>Hinweise  
 Jeder Vorgang im Zusammenhang mit ADO-Objekten kann eine oder mehrere Anbieterfehler generieren. Sobald ein Fehler auftritt, eine oder mehrere **Fehler** Objekte platziert werden, die der [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung von der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt. Wenn ein anderer ADO-Vorgang einen Fehler generiert die **Fehler** Auflistung deaktiviert ist, und die neue Gruppe von **Fehler** Objekte befindet sich der **Fehler** Auflistung.  
  
> [!NOTE]
>  Jede **Fehler** -Objekt stellt einen bestimmten Anbieterfehler, keinen ADO-Fehler dar. ADO-Fehler werden an den Mechanismus zur Ausnahmebehandlung zur Laufzeit verfügbar gemacht. Z. B. in Microsoft Visual Basic das Vorkommen einer ADO-spezifische Fehler wird ausgelöst, eine **On Error** Ereignis und in der **Fehler** Objekt. Eine vollständige Liste der ADO-Fehler finden Sie unter der [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) Thema.  
  
 Informieren Sie sich ein **Fehler** Eigenschaften des Objekts, um spezifische Details zu den einzelnen Fehlern, einschließlich der folgenden abzurufen:  
  
-   Die [Beschreibung](../../../ado/reference/ado-api/description-property.md) Eigenschaft, die den Text des Fehlers enthält. Dies ist die Standardeigenschaft.  
  
-   Die [Anzahl](../../../ado/reference/ado-api/number-property-ado.md) -Eigenschaft, die enthält die **lange** ganzzahligen Wert der Fehlerkonstante an den.  
  
-   Die [Quelle](../../../ado/reference/ado-api/source-property-ado-error.md) Eigenschaft, die das Objekt angibt, die den Fehler ausgelöst. Dies ist besonders nützlich, wenn Sie mehrere haben **Fehler** Objekte in der **Fehler** Auflistung, die nach einer Anforderung mit einer Datenquelle.  
  
-   Die [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) und [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) Eigenschaften, die Informationen aus der SQL-Datenquellen bereitstellen.  
  
 Wenn ein Anbieterfehler auftritt, wird Sie platziert die **Fehler** Auflistung von der **Verbindung** Objekt. ADO unterstützt die Rückgabe mehrerer Fehler durch einen einzelnen ADO-Vorgang, um Fehlerinformationen hängt von dem Anbieter zu ermöglichen. Zum Abrufen dieser ausführliche Fehlerinformationen in einem Fehlerhandler verwenden Sie die entsprechenden Fehlerbehebung Funktionen der Sprache oder Umgebung, die mit dem Sie arbeiten, verwenden Sie geschachtelte Schleifen auflisten die Eigenschaften der einzelnen **Fehler** Objekt in der **Fehler** Auflistung.  
  
> [!NOTE]
>  **Microsoft Visual Basic und VBScript Benutzer** ist keine gültige **Verbindung** -Objekt, müssen Sie zum Abrufen von Fehlerinformationen von der **Fehler** Objekt.  
  
 Zweck einfach als Anbieter ADO löscht die **OLE-Fehlerinformationen** -Objekt, bevor ein Aufruf einen neue Anbieterfehler potenziell generieren konnte. Allerdings die **Fehler** Auflistung auf der **Verbindung** Objekt ist deaktiviert und nur, wenn der Anbieter einen neuen Fehler erzeugt, oder wenn die [deaktivieren](../../../ado/reference/ado-api/clear-method-ado.md) Methode wird aufgerufen.  
  
 Einige Eigenschaften und Methoden zurück Warnungen, die als **Fehler** Objekte in der **Fehler** Auflistung jedoch die Ausführung des Programms nicht angehalten werden. Vor dem Aufrufen der [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), oder [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methoden auf einen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt; die [Öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) Methode auf eine **Verbindung** Objekt; oder legen Sie die [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft auf eine **Recordset** -Objekt, rufen Sie die **deaktivieren**Methode für die **Fehler** Auflistung. Auf diese Weise erfahren Sie die [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft von der **Fehler** zurückgegebene Auflistung zur Prüfung auf Warnungen.  
  
 Die **Fehler** Objekt ist nicht sicher für Skripting.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Error-Objekt – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState-Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Errors-Auflistung (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Anhang A: Daten und Dienstanbieter](../../../ado/guide/appendixes/appendix-a-providers.md)
