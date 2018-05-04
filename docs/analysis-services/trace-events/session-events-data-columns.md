---
title: Datenspalten für Sitzungsereignisse | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Session Events event category
ms.assetid: 35853451-6768-4a02-8b8f-81a8ae37a333
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 86340313bb0a2d490a3feff56ff778f044bee22e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="session-events-data-columns"></a>Datenspalten für Sitzungsereignisse
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Die Sitzungsereignisse-Ereigniskategorie weist folgende Ereignisklasse auf:  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|Vorhandene Benutzerverbindung.|  
|42|Vorhandene Sitzung|Vorhandene Sitzung.|  
|43|Sitzungsinitialisierung|Sitzungsinitialisierung.|  
  
 In der folgenden Tabelle sind die Datenspalten für diese Ereignisklasse aufgeführt.  
  
## <a name="existing-connection"></a>Existing Connection  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|NTUserName|32|8|Windows-Benutzername.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|ClientHostName|35|8|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird.|  
|ClientProcessID|36|1|Die Prozess-ID der Clientanwendung.|  
|ApplicationName|37|8|Der Name der Clientanwendung, die die Verbindung mit dem Server hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="existing-session"></a>Vorhandene Sitzung  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTUserName|32|8|Windows-Benutzername.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|ClientHostName|35|8|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird.|  
|ClientProcessID|36|1|Die Prozess-ID der Clientanwendung.|  
|ApplicationName|37|8|Der Name der Clientanwendung, die die Verbindung mit dem Server hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
|RequestProperties|45|9|XMLA-Anforderungseigenschaften.|  
  
## <a name="session-initialize"></a>Sitzungsinitialisierung  
  
|||||  
|-|-|-|-|  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTUserName|32|8|Windows-Benutzername.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|ClientHostName|35|8|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird.|  
|ClientProcessID|36|1|Die Prozess-ID der Clientanwendung.|  
|ApplicationName|37|8|Der Name der Clientanwendung, die die Verbindung mit dem Server hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
|RequestProperties|45|9|XMLA-Anforderungseigenschaften.|  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitsüberwachung-Ereigniskategorie](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  
