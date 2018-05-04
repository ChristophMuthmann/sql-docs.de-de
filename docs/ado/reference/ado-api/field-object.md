---
title: Field-Objekt | Microsoft Docs
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
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49960f2763b402a291531a2ab010ef6a0682107f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="field-object"></a>Field-Objekt
Stellt eine Spalte von Daten mit einem gemeinsamen Datentyp.  
  
## <a name="remarks"></a>Hinweise  
 Jede **Feld** -Objekt entspricht einer Spalte in der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Verwenden Sie die [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft **Feld** Objekte so festlegen oder Zurückgeben von Daten für den aktuellen Datensatz. Abhängig von den Funktionen der Anbieter verfügbar macht, einige Auflistungen, Methoden oder Eigenschaften eine **Feld** Objekt möglicherweise nicht zur Verfügung.  
  
 Mit den Auflistungen, Methoden und Eigenschaften von einer **Feld** -Objekts können Sie folgende Möglichkeiten:  
  
-   Zurückgeben der Name eines Felds mit dem [Namen](../../../ado/reference/ado-api/name-property-ado.md) Eigenschaft.  
  
-   Anzeigen oder ändern Sie die Daten in das Feld mit der **Wert** Eigenschaft. **Wert** ist die Standardeigenschaft eines der **Feld** Objekt.  
  
-   Zurückgeben der grundlegenden Merkmale eines Felds mit dem [Typ](../../../ado/reference/ado-api/type-property-ado.md), [Genauigkeit](../../../ado/reference/ado-api/precision-property-ado.md), und [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) Eigenschaften.  
  
-   Zurückgeben der deklarierten Größe eines Felds mit dem [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) Eigenschaft.  
  
-   Zurückgeben von der tatsächlichen Größe der Daten in einem bestimmten Feld mit der [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) Eigenschaft.  
  
-   Bestimmen, welche Arten von Funktionen unterstützt werden, für ein bestimmtes Feld mit der [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) Eigenschaft und [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
-   Bearbeiten Sie die Werte von Feldern, die lange Binär- oder Zeichendaten Daten mit den [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) und [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) Methoden.  
  
-   Wenn der Anbieter Batchaktualisierungen unterstützt, Auflösen von Diskrepanzen in Feldwerten während der Batchaktualisierung mit den [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) und [OriginalValue](../../../ado/reference/ado-api/underlyingvalue-property.md) Eigenschaften.  
  
 Alle Metadateneigenschaften (**Namen**, **Typ**, **DefinedSize**, **Genauigkeit**, und **NumericScale**) stehen vor dem Öffnen der **Feld** des Objekts **Recordset**. Festlegen von zu diesem Zeitpunkt eignet sich für das dynamische Erstellen von Formularen.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Feld-Objekteigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Fields-Auflistung (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
