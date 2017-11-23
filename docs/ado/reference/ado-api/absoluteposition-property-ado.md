---
title: AbsolutePosition-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::AbsolutePosition
helpviewer_keywords: AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 491ed39340dd066955db2fd73ed986614744cff4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition-Eigenschaft (ADO)
Gibt die Ordnungsposition einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) aktuellen Datensatz des Objekts.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt für 32-Bit-Code oder gibt eine **lange** Wert zwischen 1 und die Anzahl der Datensätze in der **Recordset** Objekt ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)), oder gibt einen der der [ PositionEnum](../../../ado/reference/ado-api/positionenum.md) Werte.  
  
 Verwenden Sie für 64-Bit-Code einen Datentyp, der für die Speicherung von 64-Bit-Wert enthält. Beispielsweise können lange oder einen anderen Wert, der 64-Bit-Länge, z. B. DBORDINAL. Verwenden Sie keine **PositionEnum** Werte, da es auf 32-Bit-Länge beschränkt sind.  
  
## <a name="remarks"></a>Hinweise  
 Damit legen Sie die **AbsolutePosition** -Eigenschaft, ADO erfordert, dass der OLE DB-Anbieter verwenden Sie implementieren die [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) Schnittstelle.  
  
 Zugreifen auf die **AbsolutePosition** Eigenschaft eine **Recordset** , entweder mit geöffnet wurde, einen Vorwärtscursor oder dynamischer Cursor löst den Fehler **AdErrFeatureNotAvailable**. Mit anderen Cursortypen werden die richtige Position zurückgegeben, solange der OLE DB-Anbieter unterstützt die **IRowsetScroll:IRowsetLocate** Schnittstelle. Wenn vom Anbieter nicht unterstützt werden die **IRowsetScroll** -Schnittstelle, die Eigenschaft wird festgelegt, um **AdPosUnknown**. Finden Sie in der Dokumentation für den Anbieter aus, um zu bestimmen, ob er unterstützt **IRowsetScroll**.  
  
 Verwenden der **AbsolutePosition** -Eigenschaft verschieben auf einen Datensatz basierend auf ihre Ordnungsposition in der **Recordset** -Objekt, oder die Ordnungsposition des aktuellen Datensatzes ermitteln möchten. Der Anbieter muss die entsprechende Funktionalität für diese Eigenschaft verfügbar sein unterstützen.  
  
 Wie die [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) Eigenschaft **AbsolutePosition** ist 1-basiert und entspricht 1, wenn der aktuelle Datensatz der erste Datensatz im ist die **Recordset**. Sie erhalten die Gesamtanzahl von Datensätzen in der **Recordset** -Objekt aus der [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) Eigenschaft.  
  
 Beim Festlegen der **AbsolutePosition** -Eigenschaft, auch wenn es sich um einen Datensatz im aktuellen Cache ist ADO lädt den Cache mit einer neuen Gruppe von Datensätzen, die mit dem angegebenen Datensatz ab. Die [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) Eigenschaft bestimmt die Größe dieser Gruppe.  
  
> [!NOTE]
>  Verwenden Sie nicht die **AbsolutePosition** ein Ersatzzeichen Datensatznummer-Eigenschaft. Die Position eines bestimmten Datensatzes ändert, wenn Sie einen vorherigen Datensatz zu löschen. Es gibt auch keine Zusicherung, dass ein bestimmter Datensatz die gleiche hat **AbsolutePosition** Wenn die **Recordset** Objekt erneut abgefragt oder geöffnet wird. Lesezeichen werden nach wie vor die empfohlene Methode der beibehalten und die Rückgabe an einer angegebenen Position und sind die einzige Möglichkeit der Positionierung für alle Typen von **Recordset** Objekte.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [AbsolutePosition- und CursorLocation Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition- und CursorLocation Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage-Eigenschaft (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount-Eigenschaft (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
