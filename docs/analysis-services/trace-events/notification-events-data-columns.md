---
title: Datenspalten der Benachrichtigungsereignisse | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Notification Events event category
ms.assetid: 0ecf06da-1586-415a-9da8-60d4c634f030
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8d825bcc7fcdc548275cb46632229791855c275e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="notification-events-data-columns"></a>Datenspalten der Benachrichtigungsereignisse
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Benachrichtigungsereignisse sind Ereignisse, die nicht direkt vom Benutzer von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]verursacht werden. Zu Benachrichtigungen kommt es z. B., weil Benutzer zugrunde liegende Tabellen für das proaktive Zwischenspeichern aktualisieren.  
  
 Die Ereigniskategorie Benachrichtigungsereignisse besitzt die folgende Ereignisklasse:  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|39|Benachrichtigung|Benachrichtigungsereignis.|  
|40|Benutzerdefiniert|Benutzerdefiniertes Ereignis.|  
  
 In der folgenden Tabelle sind die Datenspalten für die Ereignisklasse aufgeführt:  
  
## <a name="notification"></a>Benachrichtigung  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> Die folgenden **Unterklassen-ID**:<br />                      **Unterklassenname** -Paare sind definiert:<br /><br /> 0: Proaktives Zwischenspeichern Anfang<br /><br /> 1: Proaktives Zwischenspeichern Ende<br /><br /> 2: Flight Recorder gestartet<br /><br /> 3: Flight Recorder beendet<br /><br /> 4: Konfigurationseigenschaften aktualisiert<br /><br /> 5: SQL-Ablaufverfolgung<br /><br /> 6: Objekt erstellt<br /><br /> 7: Objekt gelöscht<br /><br /> 8: Objekt geändert<br /><br /> 9: Proaktiver Zwischenspeicherabruf Anfang<br /><br /> 10: Proaktiver Zwischenspeicherabruf Ende<br /><br /> 11: Flight Recorder-Momentaufnahme Anfang<br /><br /> 12: Flight Recorder-Momentaufnahme Ende<br /><br /> 13: Proaktives Zwischenspeichern: anzeigepflichtiges Objekt aktualisiert<br /><br /> 14: Verzögertes Verarbeiten: Start der Verarbeitung<br /><br /> 15: Verzögertes Verarbeiten: Verarbeitung abgeschlossen<br /><br /> 16: SessionOpened-Ereignis Anfang<br /><br /> 17: SessionOpened-Ereignis Ende<br /><br /> 18: SessionClosing-Ereignis Anfang<br /><br /> 19: SessionClosing-Ereignis Ende<br /><br /> 20: CubeOpened-Ereignis Anfang<br /><br /> 21: CubeOpened-Ereignis Ende<br /><br /> 22: CubeClosing-Ereignis Anfang<br /><br /> 23: CubeClosing-Ereignis Ende<br /><br /> 24: Transaktionsabbruch angefordert|  
|CurrentTime|2|5|Enthält die aktuelle Zeit des Benachrichtigungsereignisses (wenn verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Enthält den Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Enthält die Uhrzeit, zu der das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Enthält die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|IntegerData|10|1|Enthält die mit dem Benachrichtigungsereignis verbundenen ganzzahligen Daten. Wenn die EventSubclass-Spalte 8 ist, sind die Werte:<br /><br /> 1 = Erstellt<br /><br /> 2 = Gelöscht<br /><br /> 3 = Geänderte Objekteigenschaften<br /><br /> 4 = Geänderte Eigenschaften der untergeordneten Elemente des Objekts<br /><br /> 6 = Untergeordnetes Element hinzugefügt<br /><br /> 7 = Untergeordnetes Element gelöscht<br /><br /> 8 = Objekt erfolgreich verarbeitet<br /><br /> 9 = Objekt teilweise verarbeitet<br /><br /> 10 = Objekt nicht verarbeitet<br /><br /> 11 = Objekt vollständig optimiert<br /><br /> 12 = Objekt teilweise optimiert<br /><br /> 13 = Objekt nicht optimiert|  
|ObjectID|11|8|Enthält die Objekt-ID, für die diese Benachrichtigung ausgegeben wird; dies ist ein Zeichenfolgenwert.|  
|ObjectType|12|1|Enthält den mit dem Benachrichtigungsereignis verbundenen Objekttyp.|  
|ObjectName|13|8|Enthält den mit dem Benachrichtigungsereignis verbundenen Objektnamen.|  
|ObjectPath|14|8|Enthält den mit dem Benachrichtigungsereignis verbundenen Objektpfad. Der Pfad wird als eine durch Trennzeichen getrennte Liste übergeordneter Elemente zurückgegeben und beginnt mit dem übergeordneten Element des Objekts.|  
|ObjectReference|15|8|Enthält den Objektverweis für das Fortschrittsbericht-Sendeereignis. Der Objektverweis wird von allen übergeordneten Elementen als XML codiert, und das Objekt wird mit Tags beschrieben.|  
|ConnectionID|25|1|Enthält die mit dem Benachrichtigungsereignis verbundene eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Enthält den Namen der Datenbank, in der das Benachrichtigungsereignis aufgetreten ist.|  
|NTUserName|32|8|Enthält den mit dem Benachrichtigungsereignis verbundenen Windows-Benutzernamen.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|SessionID|39|8|Enthält die mit dem Benachrichtigungsereignis verbundene Sitzungs-ID.|  
|NTCanonicalUserName|40|8|Enthält den mit dem Benachrichtigungsereignis verbundenen Windows-Benutzernamen. Der Benutzername liegt im kanonischen Format vor. Beispiel: engineering.microsoft.com/software/user.|  
|SPID|41|1|Enthält die SPID (Server Process ID), die die mit dem Benachrichtigungsereignis verbundene Benutzersitzung eindeutig kennzeichnet. Die SPID entspricht direkt dem von XMLA verwendeten Sitzungs-GUID.|  
|TextData|42|9|Enthält die mit dem Benachrichtigungsereignis verbundenen Textdaten.|  
|ServerName|43|8|Enthält den Namen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz, in der das Benachrichtigungsereignis aufgetreten ist.|  
|RequestProperties|45|9|Enthält die Eigenschaften der XMLA-Anforderung.|  
  
## <a name="user-defined"></a>Benutzerdefiniert  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Eine bestimmte Benutzerereignisunterklasse, die zusätzliche Informationen zu jeder Ereignisklasse enthält.|  
|CurrentTime|2|5|Enthält die aktuelle Zeit des Benachrichtigungsereignisses (wenn verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|IntegerData|10|1|Bestimmte benutzerdefinierte Ereignisinformationen.|  
|ConnectionID|25|1|Enthält die mit dem Benachrichtigungsereignis verbundene eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Enthält den Namen der Datenbank, in der das Benachrichtigungsereignis aufgetreten ist.|  
|NTUserName|32|8|Enthält den mit dem Benachrichtigungsereignis verbundenen Windows-Benutzernamen.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|SessionID|39|8|Enthält die mit dem Benachrichtigungsereignis verbundene Sitzungs-ID.|  
|NTCanonicalUserName|40|8|Enthält den mit dem Benachrichtigungsereignis verbundenen Windows-Benutzernamen. Der Benutzername liegt im kanonischen Format vor. Beispiel: engineering.microsoft.com/software/user.|  
|SPID|41|1|Enthält die SPID (Server Process ID), die die mit dem Benachrichtigungsereignis verbundene Benutzersitzung eindeutig kennzeichnet. Die SPID entspricht direkt dem von XMLA verwendeten Sitzungs-GUID.|  
|TextData|42|9|Enthält die mit dem Benachrichtigungsereignis verbundenen Textdaten.|  
|ServerName|43|8|Enthält den Namen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz, in der das Benachrichtigungsereignis aufgetreten ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Benachrichtigungsereignisse (Ereigniskategorie)](../../analysis-services/trace-events/notification-events-event-category.md)  
  
  
