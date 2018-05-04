---
title: "\"onreadystatechange\" Ereignis (RDS) | Microsoft Docs"
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
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 152acad43fbecebc5ee7808284a1d1fba90e1380
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="onreadystatechange-event-rds"></a>"onreadystatechange" Ereignis (RDS)
Die **"onreadystatechange"** Ereignis wird aufgerufen, immer den Wert des der [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) -Eigenschaft ändert.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parameter  
 Keine.  
  
## <a name="remarks"></a>Hinweise  
 Die **ReadyState** Eigenschaft zeigt den Fortschritt einer [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt asynchron abgerufen, Daten in seiner [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt. Verwenden der **"onreadystatechange"** Ereignis zum Überwachen von Änderungen in der **ReadyState** Eigenschaft, wenn sie auftreten. Dies ist effizienter als die Prüfung in regelmäßigen Abständen den Wert der Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)


