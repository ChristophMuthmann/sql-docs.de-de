---
title: SaveOptionsEnum | Microsoft Docs
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
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5eb423643748725b1be3ac1c809e56efbee209d6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Gibt an, ob eine Datei erstellt oder werden, beim Speichern überschrieben von werden eine [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt. Die Werte sind möglich **AdSaveCreateNotExist** oder **AdSaveCreateOverWrite**...  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Standard. Erstellt eine neue Datei, wenn die Datei, wird angegeben die *FileName* Parameter noch nicht vorhanden.|  
|**adSaveCreateOverWrite**|2|Überschreibt die Datei mit den Daten aus den aktuell geöffneten **Stream** Objekt, wenn die angegebene Datei durch die *Filename* Parameter bereits vorhanden ist. Wenn die Datei, wird angegeben die *Filename* Parameter ist nicht vorhanden, wird eine neue Datei erstellt.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [SaveToFile-Methode](../../../ado/reference/ado-api/savetofile-method.md)
