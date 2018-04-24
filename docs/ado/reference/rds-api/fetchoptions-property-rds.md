---
title: FetchOptions-Eigenschaft (RDS) | Microsoft Docs
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
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 91b6a6c4c40bd3b31a539c42d89a6711953f582b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="fetchoptions-property-rds"></a>FetchOptions-Eigenschaft (RDS)
Gibt den Typ des asynchronen abrufen.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="setting-and-return-values"></a>Festlegen und Rückgabewerte  
 Legt fest oder gibt einen der folgenden Werte zurück.  
  
|Konstante|Description|  
|--------------|-----------------|  
|**adcFetchUpFront**|Alle Datensätze von der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) abgerufen werden, bevor die Steuerung an die Anwendung zurückgegeben wird. Die vollständige **Recordset** abgerufen wird, bevor die Anwendung mit ihm keine Wirkung.|  
|**adcFetchBackground**|Steuerelement kann an die Anwendung zurückgegeben, sobald der erste Batch von Datensätzen abgerufen wurde. Eine nachfolgende Lesen von der **Recordset** Zugriffsversuche auf einen Datensatz, der nicht der erste Batch abgerufen werden verzögert, bis der gesuchte Datensatz tatsächlich abgerufen wird, zu diesem Zeitpunkt Steuerung an die Anwendung zurückgegeben.|  
|**adcFetchAsync**|Standard. Steuerelementrückgabe unmittelbar an die Anwendung während der Datensätze im Hintergrund abgerufen werden. Wenn die Anwendung versucht, einen Datensatz zu lesen, die noch nicht abgerufen wurde, die dem gesuchten Datensatz am nächsten Datensatz gelesen wird und Steuerung wird sofort zurückgegeben werden, zeigt an, dass das aktuelle Ende der **Recordset** wurde erreicht. Z. B. einen Aufruf von [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) wird zum letzten Datensatz tatsächlich abgerufen, die Position des aktuellen Datensatzes verschoben, obwohl mehrere Datensätze zum Auffüllen weiterhin der **Recordset**.|  
  
> [!NOTE]
>  Jede clientseitige ausführbare Datei, die diese Konstanten verwendet muss die Deklarationen für sie bereitstellen. Sie können Ausschneiden und Einfügen die Konstanten Deklarationen, die Sie aus der Datei Adcvbs.inc, in den standardmäßigen Installationsordner für die RDS-Bibliothek gespeichert werden soll.  
  
## <a name="remarks"></a>Hinweise  
 In einer Web-Anwendung wird in der Regel soll **AdcFetchAsync** (Standardwert), da es sich um eine bessere Leistung bietet. In einer kompilierten Clientanwendung wird in der Regel soll **AdcFetchBackground**.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ExecuteOptions und FetchOptions Eigenschaften Beispiel (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel-Methode (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


