---
title: SQL Server, FileTable Objekt | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLServer:FileTable
ms.assetid: 325f5e58-1095-450f-9321-dfacfe6fd55f
caps.latest.revision: 3
author: dagiro
ms.author: v-dagir
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6016445b8d844eb62291ee01df9575134dc7c35
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-filetable-object"></a>SQLServer, FileTable (Objekt)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Das Leistungsobjekt **SQLServer:FileTable** stellt Leistungsindikatoren für Statistiken bereit, die FileTable und dem nicht transaktionsgebundenen Zugriff zugeordnet sind.

In der folgenden Tabelle werden die SQL Server-Leistungsobjekte für **FileTable** beschrieben.

|**SQLServer FileTable (Leistungsindikatoren)**|Description|  
|-------------|-----------------|  
|**Durchschn. Zeit für FileTable-Elementlöschvorgang**|Die durchschnittliche Zeit (in Millisekunden) zum Löschen eines FileTable-Elements.|
|**Durchschn. FileTable-Aufzählungszeit**|Die durchschnittliche Zeit (in Millisekunden) einer Anforderung zum Aufzählen von FileTable-Elementen.|
|**Durchschn. Zeit für FileTable-Handleabbruch**|Die durchschnittliche Zeit (in Millisekunden) zum Abbrechen eines FileTable-Handles.|
|**Durchschn. Zeit für FileTable-Elementverschiebevorgang**|Die durchschnittliche Zeit (in Millisekunden) zum Verschieben eines FileTable-Elements.|
|**Durchschn. Zeit je Datei-E/A-Anforderung**|Die durchschnittliche Zeit (in Millisekunden) zur Behandlung einer eingehenden Datei-E/A-Anforderung.|
|**Durchschn. Zeit je Datei-E/A-Antwort**|Die durchschnittliche Zeit (in Millisekunden) zur Behandlung einer ausgehenden Datei-E/A-Antwort.|
|**Durchschn. Zeit für FileTable-Elementumbenennung**|Die durchschnittliche Zeit (in Millisekunden) zum Umbenennen eines FileTable-Elements.|
|**Durchschn. Zeit für FileTable-Elementabruf**|Die durchschnittliche Zeit (in Millisekunden) zum Abrufen eines FileTable-Elements.|
|**Durchschn. Zeit für FileTable-Elementupdate**|Die durchschnittliche Zeit (in Millisekunden) zum Aktualisieren eines FileTable-Elements.|
|**FileTable-Datenbankvorgänge/Sekunde**|Die Gesamtanzahl der von der FileTable-Speicherkomponente pro Sekunde verarbeiteten Ereignisse für die Datenbank.|
|**FileTable-Aufzählanforderungen/Sekunde**|Die Gesamtanzahl der Anforderungen zum Aufzählen von FileTable-Elementen pro Sekunde.|
|**FileTable-Datei-E/A-Anforderungen/Sekunde**|Die Gesamtanzahl der eingehenden Datei-E/A-Anforderungen für FileTable-Elemente pro Sekunde.|
|**FileTable-Datei-E/A-Antwort/Sekunde**|Die Gesamtanzahl der ausgehenden Datei-E/A-Antworten pro Sekunde.|
|**FileTable-Elementlöschanforderungen/Sekunde**|Die Gesamtanzahl der Anforderungen zum Löschen von FileTable-Elementen pro Sekunde.|
|**FileTable-Elementabrufanforderung/Sekunde**|Die Gesamtanzahl der Anforderungen zum Abrufen von FileTable-Elementen pro Sekunde.|
|**FileTable-Elementverschiebeanforderungen/Sekunde**|Die Gesamtanzahl der Anforderungen zum Verschieben von FileTable-Elementen pro Sekunde.|
|**FileTable-Elementumbenennungsanforderungen/Sekunde**|Die Gesamtanzahl der Anforderungen zum Umbenennen von FileTable-Anforderungen pro Sekunde.|
|**FileTable-Elementupdateanforderungen/Sekunde**|Die Gesamtanzahl der Anforderungen zum Aktualisieren von FileTable-Elementen pro Sekunde.|
|**FileTable-Handleabbruchvorgänge/Sekunde**|Die Gesamtanzahl der Abbruchvorgänge für FileTable-Handles pro Sekunde.|
|**FileTable-Tabellenvorgänge/Sekunde**|Die Gesamtanzahl der von der FileTable-Speicherkomponente pro Sekunde verarbeiteten Ereignisse für Tabellen.|
|**Basis für Zeit für FileTable-Elementlöschvorgang**|Nur zur internen Verwendung.|
|**Basis für FileTable-Aufzählungszeit**|Nur zur internen Verwendung.|
|**Basis für Zeit für FileTable-Handleabbruch**|Nur zur internen Verwendung.|
|**Basis für Zeit für FileTable-Elementverschiebevorgang**|Nur zur internen Verwendung.|
|**Basis für Zeit je Datei-E/A-Anforderung**|Nur zur internen Verwendung.|
|**Basis für Zeit je Datei-E/A-Antwort**|Nur zur internen Verwendung.|
|**Basis für Zeit für FileTable-Elementumbenennung**|Nur zur internen Verwendung.|
|**Basis für Zeit für FileTable-Elementabruf**|Nur zur internen Verwendung.|
|**Basis für Zeit für FileTable-Elementupdate**|Nur zur internen Verwendung.| 
 
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Überwachen der Ressourcenverwendung (Systemmonitor)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
