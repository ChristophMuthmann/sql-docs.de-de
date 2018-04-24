---
title: CacheSize-Eigenschaft (ADO) | Microsoft Docs
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
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2aeb7b018a34e2efe17fde2b4aa3c7f7e7df9113
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="cachesize-property-ado"></a>CacheSize-Eigenschaft (ADO)
Gibt die Anzahl der Datensätze aus einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt, das lokal im Arbeitsspeicher zwischengespeichert werden.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **lange** Wert, der größer als 0 sein muss. Standard ist 1.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **CacheSize** Eigenschaft steuern, wie viele Datensätze gleichzeitig in den lokalen Arbeitsspeicher vom Anbieter abzurufen. Z. B. wenn die **CacheSize** ist 10, nach dem ersten Öffnen der **Recordset** -Objekt, der Anbieter Ruft die ersten 10 Datensätze in den lokalen Speicher ab. Beim Navigieren durch die **Recordset** Objekt, gibt der Anbieter die Daten aus dem lokalen Speicherpuffer zurück. Sobald Sie hinter dem letzten Datensatz in den Cache verschieben, ruft die nächsten 10 Datensätze aus der Datenquelle mit der Anbieter in den Cache ab.  
  
> [!NOTE]
>  **CacheSize** basiert auf der **maximale Anzahl geöffneter Zeilen** -anbieterspezifische Datenquelleneigenschaft (in der **Eigenschaften** Auflistung von der **Recordset** Objekt). Sie können nicht festgelegt **CacheSize** auf einen Wert größer als **maximale Anzahl geöffneter Zeilen**. Legen Sie zum Ändern der Anzahl der Zeilen, die vom Anbieter geöffnet werden können, **maximale Anzahl geöffneter Zeilen**.  
  
 Der Wert der **CacheSize** angepasst werden kann, während der Lebensdauer der **Recordset** Objekt, aber durch Ändern dieses Werts wirkt sich nur auf die Anzahl der Datensätze im Cache nach nachfolgendem Abrufen aus der Datenquelle. Ändern den Wert der Eigenschaft allein ändert sich nicht auf den aktuellen Inhalt des Caches aus.  
  
 Wenn weniger Datensätze als abrufen **CacheSize** gibt, gibt der Anbieter die übrigen Datensätze zurück, und kein Fehler auftritt.  
  
 Ein **CacheSize** Einstellung von 0 (null) ist nicht zulässig, und gibt einen Fehler zurück.  
  
 Datensätze, die aus dem Cache abgerufene widerspiegeln nicht gleichzeitige Änderungen, die andere Benutzer zu den Quelldaten vorgenommen haben. Um ein Update aller zwischengespeicherten Daten zu erzwingen, verwenden Sie die [Resync](../../../ado/reference/ado-api/resync-method.md) Methode.  
  
 Wenn **CacheSize** auf einen Wert größer als 1, die Navigationsmethoden festgelegt ist ([verschieben](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext und MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) möglicherweise Navigation zu einer Wenn gelöscht, nachdem die Datensätze abgerufen wurden, wird der Datensatz, gelöscht. Nach dem Abrufen werden nachfolgende Löschvorgänge nicht in Ihrem Datencache berücksichtigt werden, bis Sie versuchen, einen Datenwert aus einer gelöschten Zeile zugreifen. Allerdings festlegen **CacheSize** wird auf einen dieses Problem beseitigt, da gelöschte Zeilen nicht abgerufen werden können.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CacheSize (VB-Beispiel)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [CacheSize-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [CacheSize-Eigenschaft – Beispiel (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
