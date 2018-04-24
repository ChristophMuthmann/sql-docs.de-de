---
title: Festlegen von DCOM-Stream Marshalling Format | Microsoft Docs
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
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 15d82c4896fb5c5b74da6e050d7bdf8b1476ddd8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="setting-dcom-stream-marshaling-format"></a>Festlegen von DCOM-Datenstrom, die Marshalling-Format
Ein Client-Computer, die mit der Komponenten von RDS 1.5 oder früher ist nicht kompatibel mit dem Server über Komponenten von RDS 2.0 oder höher. Wenn DCOM als zugrunde liegendes Protokoll verwendet wird, ist die Unterstützung für RDS 2.0 oder höher effizienter Transport [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekte. Wenn Ihr Client Komponenten von RDS 1.5 oder früher ausgeführt wird, können Sie den Server mit der vorherigen RDS-Unterstützung (so genannte RDS 1.0) oder neueren RDS-Unterstützung (RDS 2.0 oder höher) festlegen. Legen Sie entweder die folgenden Registrierungseinträge:  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -oder-  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


