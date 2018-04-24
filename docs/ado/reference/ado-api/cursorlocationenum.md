---
title: CursorLocationEnum | Microsoft Docs
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
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e5dc3fa4f78881502f846e828484ea03329d91e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Gibt den Speicherort des Cursordiensts.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Verwendet die clientseitige Cursor, die von einer lokalen Cursorbibliothek bereitgestellt. Lokale Cursor Services ermöglichen häufig viele Funktionen, die Cursor-Treiber bereitgestellte möglicherweise nicht so verwenden diese Einstellung einen Vorteil im Hinblick auf Funktionen bereitgestellt werden, die konfiguriert werden. Um Abwärtskompatibilität zu gewährleisten, das Synonym **AdUseClientBatch** wird ebenfalls unterstützt.|  
|**adUseNone**|1|Wird kein Cursor Services verwendet werden. (Diese Konstante ist veraltet und wird aus Gründen der Abwärtskompatibilität angezeigt.)|  
|**adUseServer**|2|Standard. Verwendet für Cursor, die vom Datenanbieter oder Treiber angegeben. Diese Cursor sind mitunter sehr flexibel und zusätzliche Sensitivität gegenüber Änderungen, die andere Benutzer mit der Datenquelle vornehmen können. Allerdings einige Funktionen von der [der Microsoft-Cursordiensts für OLE DB-](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md), z. B. die Zuordnung aufgehoben<br /><br /> [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekte kann nicht mit serverseitiger Cursor simuliert werden, und diese Funktionen sind nicht verfügbar, wenn diese Einstellung.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>Gilt für  
 [CursorLocation-Eigenschaft (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
