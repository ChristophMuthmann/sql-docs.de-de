---
title: Resync-Methode | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 392dd82f2b6412c537a86cc68331cffc852069b8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="resync-method"></a>Resync-Methode
Aktualisiert die Daten in der aktuellen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt, oder [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt, aus der zugrunde liegenden Datenbank.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parameter  
 *AffectRecords*  
 Optional. Ein [AffectEnum](../../../ado/reference/ado-api/affectenum.md) Wert, der bestimmt, wie viele Datensätze die **Resync** Methode wirkt sich auf. Der Standardwert ist **AdAffectAll**. Dieser Wert ist nicht verfügbar, mit der **Resync** Methode der **Felder** Auflistung von einer **Datensatz** Objekt.  
  
 *ResyncValues*  
 Optional. Ein [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) Wert, der angibt, ob die zugrunde liegende Werte überschrieben werden. Der Standardwert ist **AdResyncAllValues**.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="recordset"></a>Recordset  
 Verwenden der **Resync** Methode, um Datensätze in der aktuellen resynchronisieren **Recordset** mit der zugrunde liegenden Datenbank. Dies ist hilfreich, wenn Sie einen statischen oder Vorwärtscursor Cursor verwenden, aber keine Änderungen in der zugrunde liegenden Datenbank angezeigt werden soll.  
  
 Wenn Sie festlegen, die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient**, **Resync** steht nur für nicht schreibgeschützte **Recordset** Objekte.  
  
 Im Gegensatz zu der [Requery](../../../ado/reference/ado-api/requery-method.md) -Methode, die **Resync** Methode wird nicht erneut ausgeführt. die **Recordset** Objekt Befehl zugrunde liegenden. Neue Datensätze aus der zugrunde liegenden Datenbank sind nicht sichtbar.  
  
 Schlägt der Versuch, führen Sie eine neusynchronisierung aufgrund eines Konflikts mit dem zugrunde liegenden Daten (z. B. ein Datensatz wurde wurde gelöscht von einem anderen Benutzer), der Anbieter gibt Warnungen, um die [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung und ein Laufzeitfehler auftritt. Verwenden der [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft (**vorliegt**) und die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) Eigenschaft, um Datensätze mit Konflikten zu suchen.  
  
 Wenn die [eindeutige Tabelle](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) und [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) dynamischen Eigenschaften werden festgelegt, und die **Recordset** ist das Ergebnis der Ausführung einer JOIN-Operation auf mehrere Tabellen, und klicken Sie dann auf die ** Zum erneuten Synchronisieren** Methode führt den Befehl in der **Resync Command** Eigenschaft nur für die Tabelle mit dem Namen der **eindeutige Tabelle** Eigenschaft.  
  
## <a name="fields"></a>Felder  
 Verwenden der **Resync** Methode, um die Werte der Resynchronisieren der **Felder** Auflistung von einer **Datensatz** Objekt mit der zugrunde liegenden Datenquelle. Die [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) -Eigenschaft wird von dieser Methode nicht beeinflusst.  
  
 Wenn *ResyncValues* festgelegt ist, um **AdResyncAllValues** (Standardwert), die [OriginalValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [Wert](../../../ado/reference/ado-api/value-property-ado.md), und [ OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) Eigenschaften des [Feld](../../../ado/reference/ado-api/field-object.md) Objekte in die Auflistung synchronisiert werden. Wenn *ResyncValues* festgelegt ist, um **AdResyncUnderlyingValues**, nur die **OriginalValue** Eigenschaft synchronisiert ist.  
  
 Der Wert des der **Status** Eigenschaft für die einzelnen **Feld** -Objekts zum Zeitpunkt des Aufrufs wirkt sich auch auf das Verhalten des **Resync**. Für **Feld** Objekte mit **Status** Werte **AdFieldPendingUnknown** oder **AdFieldPendingInsert**, **erneut synchronisieren ** hat keine Auswirkungen. Für **Status** Werte **AdFieldPendingChange** oder **AdFieldPendingDelete**, **Resync** Datenwerte für Felder synchronisiert, immer noch in der Datenquelle vorhanden.  
  
 **Resync** erfolgen keine Änderungen **Status** Werte der **Feld** Objekte, es sei denn, ein Fehler tritt auf, beim **Resync** aufgerufen wird. Angenommen, wenn das Feld nicht mehr vorhanden ist, der Anbieter zurück eine entsprechende **Status** Wert für die **Feld** Objekt, z. B. **AdFieldDoesNotExist**. Zurückgegebene **Status** Werte können logisch kombiniert werden, im Wert der **Status** Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Fields-Auflistung (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Resync-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Resync-(VC++-Methodenbeispiel)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear-Methode (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [OriginalValue-Eigenschaft](../../../ado/reference/ado-api/underlyingvalue-property.md)

