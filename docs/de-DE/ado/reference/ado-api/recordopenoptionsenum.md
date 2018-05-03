---
title: RecordOpenOptionsEnum | Microsoft Docs
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
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0139f1a99a72c7df2f1ad9f11fe1b231d38b4c7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
Gibt Optionen zum Öffnen einer [Datensatz](../../../ado/reference/ado-api/record-object-ado.md). Diese Werte können kombiniert werden, mithilfe von oder.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|Gibt an, an den Anbieter, die mit die Feldern verknüpft die **Datensatz** anfänglich nicht abgerufen werden müssen, aber beim ersten Versuch Zugriff auf das Feld abgerufen werden können. Das Standardverhalten, das durch das Fehlen des dieses Flag angegeben wird, um alle abzurufen der **Datensatz** Objekt Felder.|  
|**adDelayFetchStream**|0x4000|Gibt an, an den Anbieter, der den Standarddatenstrom zugeordnet der **Datensatz** anfänglich nicht abgerufen werden müssen. Das Standardverhalten, angegeben durch das fehlen dieses Flags wird zum Abrufen der zugeordneten Standarddatenstrom der **Datensatz** Objekt.|  
|**adOpenAsync**|0x1000|Gibt an, dass die **Datensatz** Objekt im asynchronen Modus geöffnet wird.|  
|**adOpenExecuteCommand**|0x10000|Gibt an, dass die Quellzeichenfolge Befehlstext enthält, die ausgeführt werden soll. Dieser Wert entspricht der **AdCmdText** option **Recordset.Open**.|  
|**adOpenRecordUnspecified**|-1|Standard. Gibt an, dass keine Optionen angegeben sind.|  
|**adOpenOutput**|0x800000|Gibt an, dass, wenn die Quelle auf einen Knoten verweist, der ein ausführbares Skript enthält (z. B. ein. ASP-Seite), klicken Sie dann auf die geöffnete **Datensatz** enthält die Ergebnisse der ausgeführten Skripts. Dieser Wert ist nur gültig, wenn keines auflistungsdatenvertrags Datensätze.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [Open-Methode (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)
