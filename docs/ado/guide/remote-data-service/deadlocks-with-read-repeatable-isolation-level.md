---
title: Deadlocks bei Repeatable Read-Isolationsstufe | Microsoft Docs
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
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6fc1621022758189925587e32059a3e26a1de4a4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>Deadlocks bei Repeatable Read-Isolationsstufe
Wenn ein benutzerdefiniertes Geschäftsobjekt eine Isolationsstufe repeatable Read, verwendet um einen SQL-Server zugreifen, und das Geschäftsobjekt gleichzeitig aufgerufen wird, durch zwei Clients, die eine Abfrage senden und in der gleichen Transaktion zu aktualisieren, ist ein Deadlock möglich. Remote Data Service dient zum einen der Prozesse zu einem Timeout, um den Deadlock zu ermöglichen, aber das Update schlägt fehl, für den Client.  
  
 Verwenden der [Cursordiensts](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) **Befehlstimeout** dynamische Eigenschaft so ändern Sie die Länge der das Timeout.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



