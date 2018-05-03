---
title: Springen zu einem Datensatz | Microsoft Docs
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
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4391866aa2e66aa406b87b973b0f1cea013868db
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="jumping-to-a-record"></a>Springen zu einem Datensatz
Die [verschieben](../../../ado/reference/ado-api/move-method-ado.md) Methode können Sie vorwärts oder rückwärts Verschieben der **Recordset** eine angegebene Anzahl von Datensätzen mithilfe der folgenden Syntax:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>Hinweise  
 Die **verschieben** Methode wird für alle unterstützt **Recordset** Objekte.  
  
 Wenn die *NumRecords* Argument ist größer als 0 (null), die Position des aktuellen Datensatzes rückt vor (gegen Ende der **Recordset**). Wenn *NumRecords* ist kleiner als 0 (null), die Position des aktuellen Datensatzes verschiebt diesen rückwärts (bis zum Anfang der **Recordset**).  
  
 Wenn die **verschieben** aufrufen würde die Position des aktuellen Datensatzes zu einem Zeitpunkt vor dem ersten Datensatz verschoben wird, ADO wird des aktuellen Datensatzes auf die Position vor dem ersten Datensatz in der **Recordset** (**BOF** ist **"true"**). Der Versuch, When rückwärts Verschieben der **BOF** Eigenschaft ist bereits **"true"** wird ein Fehler generiert.  
  
 Wenn die **verschieben** Aufruf würde die Position des aktuellen Datensatzes zu einem Zeitpunkt nach dem letzten Datensatz verschieben, ADO setzt den aktuellen Datensatz auf die Position hinter dem letzten Datensatz in der **Recordset** (**EOF** ist **"true"**). Der Versuch, forward When Verschieben der **EOF** Eigenschaft ist bereits **"true"** wird ein Fehler generiert.  
  
 Aufrufen der **verschieben** Methode aus einer leeren **Recordset** Objekt wird ein Fehler generiert.  
  
 Wenn Sie ein Lesezeichen im übergeben der *starten* Argument der Verschiebevorgang ist relativ zu dem Datensatz mit diesem Lesezeichen, vorausgesetzt die **Recordset** Objekt Lesezeichen unterstützt. Mithilfe ein Lesezeichens abgerufen wird die [Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md) Eigenschaft. Wenn nicht angegeben, ist die Verschiebung relativ zum aktuellen Datensatz.  
  
 Bei Verwendung der **CacheSize** Eigenschaft lokal Datensätze aus den Anbieter übergeben Zwischenspeichern ein *NumRecords* Argument, das die Position des aktuellen Datensatzes außerhalb der aktuellen Gruppe der zwischengespeicherten Datensätze verschiebt Erzwingt, dass ADO, um eine neue Gruppe von Datensätzen, beginnend mit dem Zieldatensatz abzurufen. Die **CacheSize** Eigenschaft bestimmt die Größe der neu abgerufenen Gruppe, und der Zieldatensatz ist der erste Datensatz abgerufen.
