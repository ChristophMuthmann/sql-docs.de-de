---
title: Minimieren Verbrauch an Protokollspeicherplatz Datei | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccad217647f8aa2f7bde912f12914055d0f65808
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="minimizing-log-file-space-usage"></a>Minimieren Verbrauch an Protokollspeicherplatz Datei
Eine Protokolldatei kann schnell füllen (also den Server anhalten), wenn eine große Menge von Aktivität auf einer SQL Server-Datenbank vorhanden ist. Sie können die Protokolldatei festlegen, um **Truncate an Prüfpunkt** erheblich die Lebensdauer der Protokolldatei für eine Datenbank zu erweitern.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Um Truncate auf Prüfpunkt in Microsoft SQL Server 6.5 zu aktivieren.  
  
1.  Start Microsoft SQL Server Enterprise Manager, open the tree for the Server, and then open the Database Devices tree.  
  
2.  Doppelklicken Sie auf den Namen der Datenbank auf der diese Funktion aktiviert wird.  
  
3.  Aus der **Datenbank** Registerkarte **Truncate**.  
  
4.  Aus der **Optionen** Registerkarte **Truncate Log on Checkpoint**, und klicken Sie dann auf **OK**.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Um Truncate auf Prüfpunkt in Microsoft SQL Server 7.0 zu aktivieren.  
  
1.  Start Microsoft SQL Server Enterprise Manager, open the tree for the Server, and then open the Databases tree.  
  
2.  Mit der rechten Maustaste in des Namens der Datenbank auf dem diese Funktion aktiviert werden sollen, und wählen Sie **Eigenschaften**.  
  
3.  Aus der **Optionen** Registerkarte **Truncate Log on Checkpoint**, und klicken Sie dann auf **OK**.  
  
 Weitere Informationen zu den **Truncate an Prüfpunkt** Funktion, finden Sie in der Microsoft SQL Server-Dokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


