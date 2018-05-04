---
title: Was&#39;s in CLR-Integration | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 040f31cc5cfd3cc06cb20e298a275188fc616185
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="clr-integration---what39s-new"></a>CLR-Integration – was&#39;s neu
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die folgenden Funktionen sind neue CLR-Integrationsfunktionen in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   In Version 4 der CLR fangen CLR-Datenbankobjekte nicht länger Ausnahmen aufgrund eines beschädigten Status ab. Diese Ausnahmen werden jetzt in der CLR-Integrationshostingebene abgefangen. Diese Ausnahmen können weiterhin durch die CLR-Datenbankkomponenten abgefangen werden, indem ein Codeattribut ([\<LegacyCorruptedStateExceptionsPolicy >-Element](http://go.microsoft.com/fwlink/?LinkId=204954)). Diese Vorgehensweise wird jedoch nicht empfohlen, da die Ergebnisse nicht zuverlässig sind, wenn eine Ausnahme aufgrund eines beschädigten Status auftritt.  
  
-   Wegen der strengen Sicherheitsanforderungen von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] verwenden CLR-Datenbankkomponenten weiterhin das Codezugriffssicherheitsmodell, das in CLR, Version 2.0, definiert wurde.  
  
-   In CLR, Version 4, ein Formatfehler in einem **System.TimeSpan** Wert generiert eine **System.FormatExceptions**. Vor Version 4 der CLR ein Formatfehler in einem **System.TimeSpan** Wert wurde ignoriert. Datenbankanwendungen, die das Verhalten vor Version 4 der CLR benötigen sollte mit einer Datenbank-Kompatibilitätsgrad ausgeführt (**ALTER DATABASE Kompatibilitätsgrad**) von 100 oder niedriger. Weitere Informationen finden Sie unter [< TimeSpan_LegacyFormatMode >-Element](http://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   Version 4 der CLR unterstützt Unicode 5.1. Sortiervorgänge, die Akzentzeichen und Symbole einschließen, werden verbessert. Wenn die Anwendung das Legacysortierverhalten benötigt, können Kompatibilitätsprobleme auftreten. So aktivieren Sie die legacysortierung, Datenbank-Kompatibilitätsgrad (**ALTER DATABASE Kompatibilitätsgrad**) muss auf 100 oder niedriger festgelegt werden. Damit dies unterstützt wird, installiert [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] sort00001000.dll im .NET Framework 4-Verzeichnis (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Weitere Informationen finden Sie unter [ \<CompatSortNLSVersion >-Element](http://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Die folgenden Spalten wurden hinzugefügt, um [dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **Total_processor_time_ms**, **Total_allocated_memory_kb**, und **Survived_ Memory_kb**.  
  
  
