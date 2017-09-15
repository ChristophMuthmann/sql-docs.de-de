---
title: Source-Eigenschaft (ADO-Recordset) | Microsoft Docs
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
- Recordset15::putref_Source
- Recordset15::Source
- Recordset15::PutSource
- Recordset15::get_Source
- Recordset15::GetSource
- Recordset15::PutRefSource
- Recordset15::put_Source
helpviewer_keywords:
- Source property [ADO Recordset]
ms.assetid: a05ba2c9-2821-4343-8607-4de9b764ec91
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ea45eae107fa55355adeb195e7e4fc5cf0a3c762
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="source-property-ado-recordset"></a>Source-Eigenschaft (ADO-Recordset)
Gibt an, die die Datenquelle für eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt eine **Zeichenfolge** Wert oder [Befehl](../../../ado/reference/ado-api/command-object-ado.md) -Objektverweis; gibt nur eine **Zeichenfolge** -Wert, der die Quelle der gibt an, die **Recordset**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Quelle** -Eigenschaft an eine Datenquelle für eine **Recordset** -Objekt mithilfe eines der folgenden: eine **Befehl** Objekt-Variable, eine SQL-Anweisung, eine gespeicherte Prozedur oder einen Tabellennamen an.  
  
 Wenn Sie festlegen der **Quelle** Eigenschaft, um eine **Befehl** -Objekt, der [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft der **Recordset** Objekt übernimmt die der Wert der **ActiveConnection** -Eigenschaft für das angegebene **Befehl** Objekt. Jedoch Lesen der **Quelle** keinen Eigenschaft zurückgibt eine **Befehl** Objekt; stattdessen wird die [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft der **Befehl** -Objekt an die Sie festlegen, die **Quelle** Eigenschaft.  
  
 Wenn die **Quelle** Eigenschaft ist eine SQL-Anweisung, eine gespeicherte Prozedur oder einen Tabellennamen, Optimieren der Leistung kann durch Übergeben der entsprechenden *Optionen* Argument mit den [Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md)-Methodenaufruf.  
  
 Die **Quelle** Eigenschaft ist Lese-/Schreibzugriff für geschlossen **Recordset** Objekte "und" Read-only für offene **Recordset** Objekte.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel der Source-Eigenschaft (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Source-Eigenschaft (ADO-Fehler)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source-Eigenschaft (ADO-Datensatz)](../../../ado/reference/ado-api/source-property-ado-record.md)
