---
title: GetChunk-Methode (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4972e08f1db08bde4cdb1241fa36895f2f33ad7b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getchunk-method-ado"></a>GetChunk-Methode (ADO)
Gibt alle oder einen Teil des Inhalts eines große Text-oder Binärdaten [Feld](../../../ado/reference/ado-api/field-object.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Variant**.  
  
#### <a name="parameters"></a>Parameter  
 *Größe*  
 Ein **lange** Ausdruck, der gleich der Anzahl von Bytes oder Zeichen, die Sie abrufen möchten.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **GetChunk** Methode auf eine **Feld** Teil oder alle zugehörigen Daten lange Binär- oder Zeichendatentypen abzurufenden Objekts. In Situationen, in dem Systemspeicher beschränkt ist, können Sie die **GetChunk** Methode, um lange Werte in Teilen und nicht in ihrer Gesamtheit zu bearbeiten.  
  
 Die Daten, die eine **GetChunk** Aufruf gibt zugewiesen *Variable*. Wenn *Größe* ist größer als die übrigen Daten der **GetChunk** Methodenrückgabe nur die verbleibenden Daten ohne Auffüllung *Variable* mit Leerzeichen. Wenn das Feld leer ist, ist die **GetChunk** Methode gibt einen null-Wert zurück.  
  
 Jeder nachfolgende **GetChunk** Aufruf ruft Daten ab, aus denen der vorherigen **GetChunk** Aufruf unterbrochen wurde. Wenn beim Abrufen von Daten aus einem Feld aus, und klicken Sie dann festlegen oder lesen den Wert eines anderen Felds im aktuellen Datensatz nimmt ADO jedoch, dass Sie das Abrufen von Daten aus dem ersten Feld abgeschlossen haben. Beim Aufrufen der **GetChunk** Methode auf das erste Feld erneut ADO interpretiert den Aufruf als ein neues **GetChunk** Vorgang und beginnt mit der vom Anfang der Daten zu lesen. Zugriff auf Felder in anderen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekte, die nicht der ersten Klone sind **Recordset** Objekt wird nicht unterbrochen. **GetChunk** Vorgänge.  
  
 Wenn die **AdFldLong** bit in der [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) Eigenschaft eine **Feld** -Objekts festgelegt wird, um **"true"**, können Sie die **GetChunk**  Methode für dieses Feld.  
  
 Wenn kein aktueller Datensatz vorhanden ist, bei der Verwendung der **GetChunk** Methode auf eine **Feld** -Objekt Fehler 3021 (kein aktueller Datensatz) auftritt.  
  
> [!NOTE]
>  Die **GetChunk** Methode kann nicht ausgeführt werden, auf **Feld** Objekte von einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt. Es führt keine Vorgänge und einen Laufzeitfehler erzeugt.  
  
## <a name="applies-to"></a>Gilt für  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [AppendChunk und GetChunk Methoden Beispiel (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk und GetChunk Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk-Methode (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attribute-Eigenschaft (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)

