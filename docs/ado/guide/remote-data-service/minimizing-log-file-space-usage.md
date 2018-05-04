---
title: Minimieren Verbrauch an Protokollspeicherplatz Datei | Microsoft Docs
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
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b0a0b3ba5bdaba5f334bce70acf87e52656c13b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="minimizing-log-file-space-usage"></a>Minimieren Verbrauch an Protokollspeicherplatz Datei
Eine Protokolldatei kann schnell füllen (also den Server anhalten), wenn eine große Menge von Aktivität auf einer SQL Server-Datenbank vorhanden ist. Sie können die Protokolldatei festlegen, um **Truncate an Prüfpunkt** erheblich die Lebensdauer der Protokolldatei für eine Datenbank zu erweitern.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Um Truncate auf Prüfpunkt in Microsoft SQL Server 6.5 zu aktivieren.  
  
1.  Starten Sie Microsoft SQL Server Enterprise Manager, öffnen Sie die Struktur für den Server, und öffnen Sie dann auf die Datenbankmedien-Struktur.  
  
2.  Doppelklicken Sie auf den Namen der Datenbank auf der diese Funktion aktiviert wird.  
  
3.  Aus der **Datenbank** Registerkarte **Truncate**.  
  
4.  Aus der **Optionen** Registerkarte **Truncate Log on Checkpoint**, und klicken Sie dann auf **OK**.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Um Truncate auf Prüfpunkt in Microsoft SQL Server 7.0 zu aktivieren.  
  
1.  Starten Sie Microsoft SQL Server Enterprise Manager, öffnen Sie die Struktur für den Server, und öffnen Sie dann die Struktur der Datenbanken.  
  
2.  Mit der rechten Maustaste in des Namens der Datenbank auf dem diese Funktion aktiviert werden sollen, und wählen Sie **Eigenschaften**.  
  
3.  Aus der **Optionen** Registerkarte **Truncate Log on Checkpoint**, und klicken Sie dann auf **OK**.  
  
 Weitere Informationen zu den **Truncate an Prüfpunkt** Funktion, finden Sie in der Microsoft SQL Server-Dokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


