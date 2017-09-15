---
title: "Festlegen von Optionen für ODBC-Verbindungspooling | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e22b3c2c09f4bc356b54ed2ecb73988f0de2764
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setting-odbc-connection-pooling-options"></a>Festlegen von Optionen für ODBC-Verbindungspooling
Verbindungspooling ermöglicht einer Anwendung eine Verbindung aus einem Pool von Verbindungen verwendet werden, die nicht für die einzelnen wiederhergestellt werden müssen. Können Sie die **Verbindungspooling** auf der Registerkarte die **ODBC-Datenquellenadministrator** Dialogfeld zum Aktivieren und Deaktivieren der Überwachung der Anwendungsleistung. Doppelklicken Sie auf eine Treibername den Timeoutzeitraum festlegen.  
  
 Der Ebene der Treiber ist Verbindungspooling durch den Registrierungswert "CPTimeout" aktiviert. Diese pro Treiber selektiven Aktivierung kann ein Systemadministrator zum Aktivieren des Verbindungspoolings nur die Treiber, die sie unterstützen können. Es wird durch Festlegen den Standardwert von CPTimeout während der Treiber-Setupprogramm erreicht. Doppelklicken Sie auf eine Treibername den Timeoutzeitraum festlegen.  
  
 Weitere Informationen zum Verbindungspooling finden Sie unter [ODBC-Verbindungspooling](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Überwachen der Leistung  
 Überwachung der Anwendungsleistung Wertentwicklung Verbindung durch die Aufzeichnung von einer Vielzahl von Statistiken. Diese Statistiken können der Entwickler die folgenden Elemente einschließen angepasst werden:  
  
|Leistungsindikator|Definition|  
|-------------|----------------|  
|ODBC-feste Verbindung Indikator pro Sekunde|Die Anzahl der tatsächlichen Verbindungen pro Sekunde, die mit dem Server hergestellt werden. Beim ersten Ihrer Umgebung ausgelastet, führt dieser Leistungsindikator nach sehr schnell, oben. Nach wenigen Sekunden wird auf 0 (null) gelöscht. Dies ist die normale Situation, wenn Verbindungspooling arbeitet. Wenn die Verbindungen mit dem Server hergestellt wurde, werden sie verwendet und im Pool für die Wiederverwendung platziert.|  
|ODBC-Festplatte trennen Indikator pro Sekunde|Die Anzahl der Festplatten trennt pro Sekunde an den Server ausgegeben. Hierbei handelt es sich um tatsächliche Verbindungen mit dem Server, die vom Verbindungspooling veröffentlicht werden. Dieser Wert wird von 0 (null) erhöhen, wenn Sie alle Clients auf dem System beenden und starten die Verbindungen zu einem Timeout führen.|  
|ODBC-Verbindung Soft Indikator pro Sekunde|Die Anzahl der Verbindungen, die durch den Pool pro Sekunde zufrieden – das heißt, Verbindungen aus, dass der Pool, die an den Benutzer übergeben wurden. Dieser Leistungsindikator gibt an, ob Verbindungspooling arbeitet. Abhängig von der Last auf dem Server ist es nicht ungewöhnlich, dass diese Option, um zwischen 40 und 60 weiche Verbindungen pro Sekunde angezeigt.|  
|ODBC-Soft Trennung Indikator pro Sekunde|Die Anzahl der pro Sekunde, die von den Anwendungen ausgestellt trennt die Verbindung. Wenn die Anwendung frei, oder trennt die Verbindung, wird die Verbindung wieder im Pool eingefügt.|  
|ODBC-Indikator für aktuellen aktive Verbindung|Die Anzahl der Verbindungen im Pool, die derzeit verwendet werden.|  
|ODBC-aktuelle freie Verbindung (Leistungsindikator)|Die aktuelle Anzahl der freien Verbindungen im Pool. Hierbei handelt es sich um live-Verbindungen, die für die Verwendung verfügbar sind.|  
|Derzeit aktiven Pools|Die Anzahl der derzeit aktiven Pools. Dieser Leistungsindikator wurde in Windows 8 für Treiber hinzugefügt, die Verbindungen im Verbindungspool zu verwalten. Weitere Informationen finden Sie unter [Treiberfähiges Verbindungspooling](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Erstellten Ressourcenpools|Die Anzahl von Pools aktiv ist, einschließlich active und entfernten Speicherpools. Dieser Leistungsindikator wurde in Windows 8 für Treiber hinzugefügt, die Verbindungen im Verbindungspool zu verwalten. Weitere Informationen finden Sie unter [Treiberfähiges Verbindungspooling](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Sie müssen eine eigene Überwachungsparameter angeben. Beispiele für die Leistungsüberwachung wurden in dieser Version von ODBC enthalten.
