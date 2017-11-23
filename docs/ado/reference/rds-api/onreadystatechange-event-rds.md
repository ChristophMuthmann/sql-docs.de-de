---
title: "\"onreadystatechange\" Ereignis (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7912a623ac6fabbbf2460025f38e2c76238af1e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="onreadystatechange-event-rds"></a>"onreadystatechange" Ereignis (RDS)
Die **"onreadystatechange"** Ereignis wird aufgerufen, immer den Wert des der [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) -Eigenschaft ändert.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
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


