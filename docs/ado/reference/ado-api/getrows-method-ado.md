---
title: GetRows-Methode (ADO) | Microsoft Docs
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
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efe7a21a26e99d089c64fcd3a627c693c5f7de09
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getrows-method-ado"></a>GetRows-Methode (ADO)
Ruft mehrere Datensätze eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt in ein Array.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Variant** , dessen Wert ist ein zweidimensionales Array.  
  
#### <a name="parameters"></a>Parameter  
 *Zeilen*  
 Optional. Ein [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) Wert, der die Anzahl der abzurufenden Datensätze angibt. Die Standardeinstellung ist **AdGetRowsRest**.  
  
 *Start*  
 Optional. Ein **Zeichenfolge** Wert oder **Variant** , ergibt das Lesezeichen für den Datensatz aus der die **GetRows** Vorgang beginnen soll. Sie können auch eine [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) Wert.  
  
 *Fields*  
 Optional. Ein **Variant** , die einen einzelnen Feldnamen oder Ordnungsposition oder ein Array von Feldnamen oder Ordnungsposition Zahlen darstellt. ADO gibt nur die Daten in diesen Feldern zurück.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **GetRows** Methode, um Datensätze aus Kopieren einer **Recordset** in ein zweidimensionales Array. Der erste Index identifiziert das Feld und die zweite die Datensatznummer. Die *Array* Variable automatisch in den richtigen dimensioniert ist wenn die Größe der **GetRows** Methode gibt die Daten zurück.  
  
 Wenn Sie einen Wert für nicht angeben der *Zeilen* Argument, das **GetRows** -Methode übernimmt alle Datensätze in der **Recordset** Objekt. Wenn Sie mehr Datensätze als verfügbar sind, anfordern **GetRows** gibt nur die Anzahl der verfügbaren Datensätze zurück.  
  
 Wenn die **Recordset** Objekt Lesezeichen unterstützt, Sie können angeben, bei welchem Datensatz der **GetRows** Methode beginnen soll, Abrufen von Daten durch Übergeben des Werts für diesen Datensatz [Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md)Eigenschaft in der *starten* Argument.  
  
 Wenn Sie die Felder beschränken möchten, die die **GetRows** Aufruf zurückgegeben wird, können Sie übergeben ein einzelnes Feld Name/Anzahl oder ein Array von Feldnamen/Nummern in der *Felder* Argument.  
  
 Nach dem Aufruf **GetRows**, der nächste ungelesene Datensatz wird zum aktuellen Datensatz, oder die [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) -Eigenschaftensatz auf **"true"** , wenn keine weiteren Datensätze vorhanden sind.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [GetRows-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows-Methode – Beispiel (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
