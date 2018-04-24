---
title: ReadyState-Eigenschaft (RDS) | Microsoft Docs
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78a5b98cdf0eff5cb84165e8fd38b58c2b87e58a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="readystate-property-rds"></a>ReadyState-Eigenschaft (RDS)
Gibt den Status einer [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt abgerufen, Daten in seiner [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen der folgenden Werte zurück.  
  
|Wert|Description|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|Die aktuelle Abfrage wird weiterhin ausgeführt und haben keine Zeilen abgerufen wurden. Die **DataControl** des Objekts **Recordset** ist nicht für die Verwendung verfügbar.|  
|**adcReadyStateInteractive**|Ein anfänglichen Satz von Zeilen, die von der aktuellen Abfrage abgerufenen gespeichert wurde, der **DataControl** des Objekts **Recordset** und für die Verwendung verfügbar sind. Die übrigen Zeilen werden noch abgerufen.|  
|**adcReadyStateComplete**|Alle von der aktuellen Abfrage abgerufene Zeilen sind gespeichert der **DataControl** des Objekts **Recordset** und für die Verwendung verfügbar sind.<br /><br /> Dieser Status wird auch vorhanden sein, wenn eine Operation aufgrund eines Fehlers abgebrochen oder die **Recordset** Objekt wurde nicht initialisiert.|  
  
> [!NOTE]
>  Jede clientseitige ausführbare Datei, die diese Konstanten verwendet muss die Deklarationen für sie bereitstellen. Sie können Ausschneiden und Einfügen die Konstanten Deklarationen, die Sie aus der Datei Adcvbs.inc, in den standardmäßigen Installationsordner für die RDS-Bibliothek gespeichert werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der ["onreadystatechange"](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) Ereignis zum Überwachen von Änderungen in der **ReadyState** Eigenschaft während eines Vorgangs asynchrone Abfrage. Dies ist effizienter als der Wert der Eigenschaft in regelmäßigen Abständen geprüft wird.  
  
 Bei einem während einer asynchronen Operation Fehler der **ReadyState** eigenschaftsänderungen **AdcReadyStateComplete**, [Status](../../../ado/reference/ado-api/state-property-ado.md) eigenschaftsänderungen von **AdStateExecuting** auf **AdStateClosed**, und die **Recordset** Objekt [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft bleibt *nichts* .  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Eigenschaft ReadyState-Beispiel (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Cancel-Methode (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [ExecuteOptions-Eigenschaft (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


