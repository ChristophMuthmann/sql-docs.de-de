---
title: Konfigurieren von virtuellen Servern unter IIS | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 10edd98f77c0aaeae05d25e76ad76a15b99bc1ed
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-virtual-servers-on-iis"></a>Konfigurieren von virtuellen Servern unter IIS
Beim Erstellen von virtueller Servern in Internet Information Services 4.0 sind die folgenden zwei zusätzliche Schritte erforderlich, zum Konfigurieren des virtuellen Servers mit RDS arbeiten:  
  
1.  Überprüfen Sie beim Einrichten des Servers "Ausführungszugriff zulassen".  
  
2.  Verschieben msadcs.dll auf *Vroot*\msadc, wobei *Vroot* das Basisverzeichnis des virtuellen Servers ist.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



