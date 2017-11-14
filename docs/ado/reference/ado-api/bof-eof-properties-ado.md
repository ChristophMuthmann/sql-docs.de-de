---
title: BOF, EOF-Eigenschaften (ADO) | Microsoft Docs
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
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 93689aa347014fd3976645682a396230a38476e6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="bof-eof-properties-ado"></a>BOF, EOF-Eigenschaften (ADO)
-   **BOF** gibt an, die vor dem ersten Datensatz in die Position des aktuellen Datensatzes ist eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
-   **EOF** gibt an, die nach dem letzten Datensatz in die Position des aktuellen Datensatzes ist eine **Recordset** Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Die **BOF** und **EOF** Eigenschaften zurückgeben **booleschen** Werte.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **BOF** und **EOF** Eigenschaften, um zu bestimmen, ob eine **Recordset** -Objekt Datensätze enthält oder ob Sie die Grenzwerte überschritten haben eine **Recordset**  Objekt, wenn Sie von Datensatz zu Datensatz verschoben.  
  
 Die **BOF** -Eigenschaft gibt **"true"** (1), wenn die aktuelle Position des Datensatzes vor dem ersten Datensatz ist und **"false"** (0), wenn die Position des aktuellen Datensatzes auf oder nach dem ersten ist Datensatz.  
  
 Die **EOF** -Eigenschaft gibt **"true"** , wenn die Position des aktuellen Datensatzes hinter den letzten Datensatz und **"false"** die Position des aktuellen Datensatzes ist am oder vor dem letzten Datensatz.  
  
 Wenn entweder die **BOF** oder **EOF** Eigenschaft **"true"**, es ist kein aktueller Datensatz.  
  
 Wenn Sie öffnen ein **Recordset** Objekt, das keine Datensätze enthält die **BOF** und **EOF** Eigenschaften werden festgelegt, um **"true"** (finden Sie unter der [ RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) -Eigenschaft für Weitere Informationen zu diesem Zustand, der eine **Recordset**). Beim Öffnen einer **Recordset** -Objekt, das über mindestens ein Datensatz des ersten Datensatzes enthält, wird der aktuelle Datensatz und der **BOF** und **EOF** Eigenschaften sind **"false"** .  
  
 Wenn Sie den letzten verbleibenden Datensatz im Löschen der **Recordset** -Objekt, das **BOF** und **EOF** Eigenschaften bleiben möglicherweise **"false"** bis Es wurde versucht, den aktuellen Datensatz neu zu positionieren.  
  
 Diese Tabelle zeigt, welche **verschieben** Methoden mit verschiedenen Kombinationen von zulässig sind die **BOF** und **EOF** Eigenschaften.  
  
||MoveFirst,<br /><br /> MoveLast|MovePrevious,<br /><br /> < 0 verschieben|Verschieben von 0|MoveNext,<br /><br /> Verschieben Sie die > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**"true"**, **EOF**=**"false"**|Zulässig|Fehler|Fehler|Zulässig|  
|**BOF**=**"false"**, **EOF**=**"true"**|Zulässig|Zulässig|Fehler|Fehler|  
|Beide **"true"**|Fehler|Fehler|Fehler|Fehler|  
|Beide **"false"**|Zulässig|Zulässig|Zulässig|Zulässig|  
  
 Ermöglicht eine **verschieben** Methode kann nicht garantiert, dass die Methode einen Datensatz wurde erfolgreich ermittelt werden; es bedeutet, dass beim Aufrufen der angegebenen **verschieben** Methode generiert keinen Fehler.  
  
 Die folgende Tabelle zeigt, was geschieht, um die **BOF** und **EOF** eigenschaftseinstellungen, die beim Aufrufen von verschiedenen **verschieben** Methoden sind jedoch nicht erfolgreich einen Datensatz gefunden.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|Legen Sie auf **"true"**|Legen Sie auf **"true"**|  
|**Verschieben Sie** 0|Keine Änderung|Keine Änderung|  
|**MovePrevious**, **verschieben** < 0|Legen Sie auf **"true"**|Keine Änderung|  
|**MoveNext**, **verschieben** > 0|Keine Änderung|Legen Sie auf **"true"**|  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [BOF, EOF und Lesezeichen-Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF und Lesezeichen Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   

