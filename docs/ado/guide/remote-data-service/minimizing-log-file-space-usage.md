---
title: Minimieren Verbrauch an Protokollspeicherplatz Datei | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddb41dbe5a2d76bb26d1830d1b659dbd99ca1c21
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="minimizing-log-file-space-usage"></a>Minimieren Verbrauch an Protokollspeicherplatz Datei
Eine Protokolldatei kann schnell füllen (also den Server anhalten), wenn eine große Menge von Aktivität auf einer SQL Server-Datenbank vorhanden ist. Sie können die Protokolldatei festlegen, um **Truncate an Prüfpunkt** erheblich die Lebensdauer der Protokolldatei für eine Datenbank zu erweitern.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
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


