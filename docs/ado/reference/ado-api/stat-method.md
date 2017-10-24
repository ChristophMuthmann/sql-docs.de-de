---
title: STAT-Methode | Microsoft Docs
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
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c19b5bed54d4bbb27a5aeb235b0e4ab529b9c836
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="stat-method"></a>STAT-Methode
Ruft Informationen zu einem [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **lange** Wert, der angibt, des Status des Vorgangs.  
  
#### <a name="parameters"></a>Parameter  
 *StatStg*  
 Eine STATSTG-Struktur, die mit Informationen über den Stream ausgefüllt wird. Die Implementierung der **Stat** vom ADO-Stream-Objekt verwendete Methode ist nicht in alle Felder der Struktur aufgefüllt.  
  
 *StatFlag*  
 Gibt an, dass diese Methode nicht Teil der Mitglieder in der STATSTG-Struktur, und speichern daher ein speicherbelegungsvorgang zurückgibt. Werte werden aus der Enumeration STATFLAG aufgefasst. Die STATFLAG-Enumeration hat zwei Werte  
  
|Konstante|Wert|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Hinweise  
 Die Version der Stat-Methode für das ADO-Stream-Objekt implementiert füllt die folgenden Felder der STATSTG-Struktur:  
  
 *pwcsName*  
 Eine Zeichenfolge, die mit dem Namen des Streams, sofern verfügbar und den Wert StatFlag STATFLAG_NONAME wurde nicht angegeben.  
  
 *cbSize*  
 Gibt die Größe des Datenstroms oder Bytearrays in Bytes an.  
  
 *mtime*  
 Gibt den Zeitpunkt der letzten Änderung dieses Speichers, Datenstroms oder Bytearrays an.  
  
 *CTime*  
 Gibt die Erstellungszeit dieses Speichers, Datenstroms oder Bytearrays Array an.  
  
 *atime*  
 Gibt die Uhrzeit des Letztes Zugriffs für dieses Speichers, Datenstroms oder Bytearrays Array an.  
  
 Wenn STATFLAG_NONAME im StatFlag-Parameter angegeben wird, wird der Name des Datenstroms nicht zurückgegeben.  
  
 Wenn STATFLAG_NONAME im StatFlag-Parameter nicht angegeben wurde und kein Name für den aktuellen Stream verfügbar ist, wird dieser Wert E_NOTIMPL sein.  
  
## <a name="applies-to"></a>Gilt für  
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)

