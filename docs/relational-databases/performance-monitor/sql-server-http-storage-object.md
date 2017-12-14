---
title: SQL Server, HTTP_STORAGE_OBJECT | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6519427db4b2e2fcb16826c1d595b132d7fb4e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-httpstorageobject"></a>SQL Server, HTTP_STORAGE_OBJECT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das **SQLServer:HTTP_STORAGE_OBJECT**-Leistungsobjekt umfasst Leistungsindikatoren, mit denen das Microsoft Azure-Speicherkonto überwacht wird. Mithilfe des Features [SQL Server-Datendateien in Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) können Sie Datenbankdateien in Microsoft Azure-Speicherblobs speichern. Dieses Leistungsobjekt behandelt jedes Windows Azure-Speicherkonto als getrenntes Laufwerk.  
  
|Indikatorname|Beschreibung|  
|------------------|-----------------|  
|**Gelesene Bytes/s**|Die bei Lesevorgängen pro Sekunde aus dem HTTP-Speicher übertragene Datenmenge.|  
|**Geschriebene Bytes/s**|Die bei Schreibvorgängen pro Sekunde aus dem HTTP-Speicher übertragene Datenmenge.|  
|**Gesamtanzahl Bytes/s**|Die bei Lese- oder Schreibvorgängen pro Sekunde aus dem HTTP-Speicher übertragene Datenmenge.|  
|**Lesevorgänge/s**|Die Anzahl der Lesevorgänge im HTTP-Speicher pro Sekunde.|  
|**Schreibvorgänge/s**|Die Anzahl der Schreibvorgänge im HTTP-Speicher pro Sekunde.|  
|**Übertragungen/s**|Die Anzahl der Lese- und Schreibvorgänge im HTTP-Speicher pro Sekunde.|  
|**Mittlere Bytes/Lesevorgang**|Die durchschnittliche Anzahl von Bytes, die pro Lesevorgang aus dem HTTP-Speicher übertragen wurde.|  
|**Mittlere Bytes/Lesevorgang (Basis)**|Nur zur internen Verwendung.|
|**Mittlere Bytes/Übertragung**|Die durchschnittliche Anzahl von Bytes, die während Lese- oder Schreibvorgängen aus dem HTTP-Speicher übertragen wurde.|  
|**Mittlere Bytes/Übertragung (Basis)**|Nur zur internen Verwendung.|
|**Mittlere Bytes/Schreibvorgang**|Die durchschnittliche Anzahl von Bytes, die pro Schreibvorgang aus dem HTTP-Speicher übertragen wurde.|  
|**Mittlere Bytes/Schreibvorgang (Basis)**|Nur zur internen Verwendung.|
|**Durchschn. Mikrosekunden/Lesevorgang**|Die durchschnittliche Anzahl von Mikrosekunden, die ein Lesevorgang aus dem HTTP-Speicher dauert.|  
|**Durchschn. Mikrosekunden/Lesevorgang (Basis)**|Nur zur internen Verwendung.|
|**Durchschn. Mikrosekunden/Lesevorgang (Abschluss)**|Die durchschnittliche Anzahl Mikrosekunden, die der Abschluss eines HTTP-Lesezugriffs auf den Speicher benötigt.| 
|**Durchschn. Mikrosekunden/Lesevorgang (Abschluss, Basis)**|Nur zur internen Verwendung.|
|**Durchschn. Mikrosekunden/Schreibvorgang**|Die durchschnittliche Anzahl von Mikrosekunden, die ein Schreibvorgang in den HTTP-Speicher dauert.|  
|**Durchschn. Mikrosekunden/Übertragung**|Die durchschnittliche Anzahl von Mikrosekunden, die eine Übertragung in den HTTP-Speicher dauert.|  
|**Durchschn. Mikrosekunden/Übertragung (Basis)**|Nur zur internen Verwendung.|
|**Durchschn. Mikrosekunden/Schreibvorgang (Basis)**|Nur zur internen Verwendung.|
|**Durchschn. Mikrosekunden/Schreibvorgang (Abschluss)**|Die durchschnittliche Anzahl Mikrosekunden, die der Abschluss eines HTTP-Schreibzugriffs auf den Speicher benötigt.|  
|**Durchschn. Mikrosekunden/Schreibvorgang (Abschluss, Basis)**|Nur zur internen Verwendung.|
|**Ausstehende HTTP-Speicher-E/A-Vorgänge**|Die Gesamtanzahl ausstehender E/A-Vorgänge für einen HTTP-Speicher.|  
|**E/A-Zugriffsfehler auf den HTTP-Speicher/s**|Die Anzahl der Schreibanforderungen mit Fehler, die pro Sekunde an den HTTP-Speicher gesendet werden.| 
|**Wiederholungen für HTTP-Speicher-E/A-Vorgänge/s**|Die Anzahl der an den HTTP-Speicher pro Sekunde gesendeten Wiederholungsanforderungen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
