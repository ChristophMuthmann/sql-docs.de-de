---
title: FieldStatusEnum | Microsoft Docs
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
f1_keywords: FieldStatusEnum
helpviewer_keywords: FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12e543a4baa7bbcc46ea39e906d57d001ea5f078
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
Gibt an, die [Status](../../../ado/reference/ado-api/status-property-ado-field.md) von einem [Field-Objekt](../../../ado/reference/ado-api/field-object.md).  
  
 Die **AdFieldPending\***  Werte geben die Operation, die aufgrund des Status festgelegt ist, und kann mit anderen Statuswerte kombiniert werden.  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|Gibt an, dass das angegebene Feld bereits vorhanden ist.|  
|**adFieldBadStatus**|12|Gibt an, dass ein gültiger Wert von ADO mit dem OLE DB-Anbieter gesendet wurde. Mögliche Ursachen sind ein OLE DB 1.0 oder 1.1-Anbieter oder eine falsche Kombination von [Wert](../../../ado/reference/ado-api/value-property-ado.md) und [Status](../../../ado/reference/ado-api/status-property-ado-field.md).|  
|**adFieldCannotComplete**|20|Gibt an, dass der Server der URL durch angegeben [Quelle](../../../ado/reference/ado-api/source-property-ado-record.md) der Vorgang konnte nicht abgeschlossen werden.|  
|**adFieldCannotDeleteSource**|23|Gibt an, dass bei einem Verschiebevorgang eine Struktur oder ein Unterverzeichnis an einem neuen Speicherort verschoben wurde, aber die Quelle nicht gelöscht werden konnte.|  
|**adFieldCantConvertValue**|2|Gibt an, dass das Feld kann nicht abgerufen werden oder, ohne dass Daten verloren gehen gespeichert.|  
|**adFieldCantCreate**|7|Gibt an, dass das Feld nicht hinzugefügt werden konnte, da der Anbieter eine Einschränkung (z. B. die Anzahl der Felder, die zulässig) überschritten.|  
|**adFieldDataOverflow**|6|Gibt an, dass die Daten, die vom Anbieter zurückgegebene den Datentyp des Felds ist übergelaufen.|  
|**adFieldDefault**|13|Gibt an, dass der Standardwert für das Feld beim Festlegen der Daten verwendet wurde.|  
|**adFieldDoesNotExist**|16|Gibt an, dass das angegebene Feld nicht vorhanden ist.|  
|**adFieldIgnore**|15|Gibt an, dass dieses Feld ausgelassen wurde, wenn die Einstellung Datenwerte in der Quelle. Der Anbieter festlegen keinen Wert.|  
|**adFieldIntegrityViolation**|10|Gibt an, dass das Feld kann nicht geändert werden, da es sich um ein berechneter oder abgeleiteter Entität handelt.|  
|**adFieldInvalidURL**|17|Gibt an, dass die URL der Datenquelle ein ungültiges Zeichen enthält.|  
|**adFieldIsNull**|3|Gibt an, dass der Anbieter hat einen VARIANT-Wert vom Typ VT_NULL zurückgegeben und das Feld nicht leer ist.|  
|**adFieldOK**|0|Standard. Gibt an, dass das Feld hinzugefügt oder gelöscht wurde.|  
|**adFieldOutOfSpace**|22|Gibt an, dass der Anbieter ist nicht genügend Speicherplatz zum Abschließen eines Verschiebe- oder Kopiervorgang zu erhalten.|  
|**adFieldPendingChange**|0x40000|Gibt an, entweder, die das Feld wurde gelöscht und dann erneut hinzugefügt, z. B. mit einem anderen Datentyp, oder der Wert des Felds, das zuvor den Status des **AdFieldOK** hat sich geändert. Die endgültige Form des Felds ändern die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung nach der [Update](../../../ado/reference/ado-api/update-method.md) -Methode aufgerufen wird.|  
|**adFieldPendingDelete**|0x20000|Gibt an, dass die **löschen** Vorgang verursacht hat, den Status festgelegt werden. Das Feld zum Löschen gekennzeichnet wurde die **Felder** Auflistung nach der **Update** -Methode aufgerufen wird.|  
|**adFieldPendingInsert**|0x10000|Gibt an, dass die **Append** Vorgang verursacht hat, den Status festgelegt werden. Die **Feld** zum hinzuzufügenden gekennzeichnet wurde die **Felder** Auflistung nach der **Update** Methode wird aufgerufen.|  
|**adFieldPendingUnknown**|0x80000|Gibt an, dass der Anbieter nicht bestimmen kann, welcher Vorgang verursacht Feldstatus festgelegt werden.|  
|**adFieldPendingUnknownDelete**|0x100000|Gibt an, dass der Anbieter nicht bestimmen kann, welcher Vorgang verursacht hat, Feldstatus festgelegt werden, und, dass das Feld aus gelöscht werden, die **Felder** Auflistung nach der **Update** -Methode aufgerufen wird.|  
|**adFieldPermissionDenied**|9|Gibt an, dass das Feld kann nicht geändert werden, da sie als schreibgeschützt definiert ist.|  
|**adFieldReadOnly**|24|Gibt an, dass das Feld in der Datenquelle als schreibgeschützt definiert ist.|  
|**adFieldResourceExists**|19|Gibt an, dass der Anbieter konnte nicht zum Ausführen des Vorgangs, da ein Objekt an die Ziel-URL ist bereits vorhanden, und es nicht auf das Objekt zu überschreiben kann.|  
|**adFieldResourceLocked**|18|Gibt an, dass der Anbieter konnte nicht zum Ausführen des Vorgangs, da die Datenquelle durch eine oder mehrere andere Anwendung oder ein Prozess gesperrt ist.|  
|**adFieldResourceOutOfScope**|25|Gibt an, dass eine Quelle oder Ziel-URL außerhalb des Bereichs des aktuellen Datensatzes ist.|  
|**adFieldSchemaViolation**|11|Gibt an, dass der Wert der Schema-Einschränkung für das Feld verletzt.|  
|**adFieldSignMismatch**|5|Gibt an, dass die vom Anbieter zurückgegebene Datenwert mit Vorzeichen handelte, aber der Datentyp des Feldwerts ADO kein Vorzeichen hatte.|  
|**adFieldTruncated**|4|Gibt an, dass Daten variabler Länge, beim Lesen aus der Datenquelle abgeschnitten wurden.|  
|**adFieldUnavailable**|8|Gibt an, dass der Anbieter den Wert beim Lesen aus der Datenquelle nicht ermitteln konnte. Die Zeile wurde gerade erstellt, der Standardwert für die Spalte war nicht verfügbar und ein neuer Wert wurde noch nicht angegeben.|  
|**adFieldVolumeNotFound**|21|Gibt an, dass der Anbieter konnte nicht das von der URL angegebene Speichervolume gefunden werden.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [Status-Eigenschaft (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)
