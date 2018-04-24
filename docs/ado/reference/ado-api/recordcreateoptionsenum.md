---
title: RecordCreateOptionsEnum | Microsoft Docs
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
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cc41adb9ab24afb357ce7d1528ffdd5b9fbed5b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
Gibt an, ob ein vorhandenes **Datensatz** sollte bereits geöffnet ist oder ein neues **Datensatz** erstellt, die für die [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt [öffnen](../../../ado/reference/ado-api/open-method-ado-record.md) Methode. Die Werte können mit einem AND-Operator kombiniert werden.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|Erstellt ein neues **Datensatz** auf den vom angegebenen Knoten *Quelle* Parameter, anstatt das Öffnen einer vorhandenen **Datensatz**. Wenn die Quelle auf einen vorhandenen Knoten zeigt dann ein Laufzeitfehler tritt auf, es sei denn, **AdCreateCollection** mit kombiniert **AdOpenIfExists** oder **AdCreateOverwrite**.|  
|**adCreateNonCollection**|0|Erstellt ein neues **Datensatz** des Typs [AdSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md).|  
|**adCreateOverwrite**|0x4000000|Ändert die Erstellung Flags **AdCreateCollection**, **AdCreateNonCollection**, und **AdCreateStructDoc**. Wenn oder mit diesem Wert und einen der Werte für die Erstellung Kennzeichen verwendet wird, wenn die Quell-URL auf einen vorhandenen Knoten verweist oder **Datensatz**, und klicken Sie dann den vorhandenen **Datensatz** überschrieben und durch einen neuen an seiner Stelle erstellt wird. Dieser Wert kann nicht verwendet werden, zusammen mit **AdOpenIfExists**.|  
|**adCreateStructDoc**|0x80000000|Erstellt ein neues **Datensatz** des Typs [AdStructDoc](../../../ado/reference/ado-api/recordtypeenum.md), anstatt das Öffnen einer vorhandenen **Datensatz**.|  
|**adFailIfNotExists**|-1|Standard. Führt zu einem Laufzeitfehler, wenn *Quelle* verweist auf einen nicht vorhandenen Knoten.|  
|**adOpenIfExists**|0x2000000|Ändert die Erstellung Flags **AdCreateCollection**, **AdCreateNonCollection**, und **AdCreateStructDoc**. Wenn oder mit diesem Wert und einen der Werte für die Erstellung Kennzeichen verwendet wird, wenn die Quell-URL auf einen vorhandenen Knoten verweist oder **Datensatz** Objekt, und klicken Sie dann der Anbieter der vorhandenen öffnen muss **Datensatz** anstatt beim Erstellen eines neuen ein. Dieser Wert kann nicht verwendet werden, zusammen mit **AdCreateOverwrite**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [Open-Methode (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)
