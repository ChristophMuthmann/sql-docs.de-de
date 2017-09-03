---
title: Das SSMS-Ausgabefenster | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Output Window [SQL Server Management Studio]
- Activity Monitor [SQL Server Management Studio]
- Object Explorer [SQL Server Management Studio]
ms.assetid: a2ce1a07-b4e2-471c-87d2-b8de5e6c6864
caps.latest.revision: 1
author: shueybubbles
ms.author: davidshi
manager: kenvh
ms.translationtype: HT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 69d3f6ecaaf9299a8816ac56d5587051548ac1df
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="output-window-in-sql-server-management-studio"></a>Das Ausgabefenster in SQL Server Management Studio
Das Ausgabefenster kann über das Menü „Ansicht“ oder mithilfe der Tastenkombination STRG + ALT + O geöffnet werden. Es stehen mehrere Ausgabekanäle zur Verfügung.

In der folgenden Tabelle finden Sie eine Übersicht über die Nachrichtentypen, die den einzelnen Ausgabekanälen zugeordnet sind.

|Channel|Description|
|-----------|---------------|  
|**Telemetrie**|Telemetrie ist der Datenstrom [anonymer Nutzungsdaten](sql-server-management-studio-ssms.md), die von Microsoft gesammelt werden. Diese Ereignisse könnten für Ihre eigene Dokumentation der SSMS-Nutzung hilfreich sein. Sie haben damit z.B. die Möglichkeit zu ermitteln, welche Objekt-Explorer-Knoten Sie erweitert und welche Befehle Sie während der SSMS-Sitzung ausgeführt haben, während das Ausgabefenster geöffnet war.|
|**Objekt-Explorers**|Dieser Kanal gibt den Abfragetext von und die verstrichene Zeit während SQL-Abfragen für Knotenerweiterungen im Objekt-Explorer aus. Für jede Abfrage werden jeweils die Ereignisse „Abfragebeginn“ und „Abfrageende“ protokolliert. Jedes Ereignis verfügt außerdem über einen Zeitstempel und den URN, der der abgefragten Entität zugeordnet ist. Der [URN](https://technet.microsoft.com/library/microsoft.sqlserver.management.smo.urn(v=sql.90).aspx) bezieht sich auf das zugrunde liegende SQL Management Object und besteht aus einer XPath-Hierarchie. Der URN für eine Tabelle mit dem Namen „Table1“ in der Datenbank „Db“ auf dem Server „MyServer“ wäre z.B. „Server[@Name='MyServer']/Database[@Name="Db"]/Table[/@Name="Table1"]“. Durch das Erweitern eines Knotens im Objekt-Explorer können mehrere solcher Abfragen mit verschiedenen Parametern ausgeführt werden. Das Ereignis „Abfrageende“ enthält die verstrichene Zeit der Abfrage zusammen mit dem TSQL-Text. Diese Abfragedaten können dann für Serverleistungsanalysen nützlich sein, wenn der Objekt-Explorer für das Erweitern eines bestimmten Knotens ungewöhnlich lange braucht. **Hinweis:** Nicht jeder Knoten im Objekt-Explorer stellt beim Erweitern so viele Details zur Abfrage bereit.|
|**Aktivitätsmonitor**|Dieser Kanal beginnt, wenn der [Aktivitätsmonitor](https://docs.microsoft.com/en-us/sql/relational-databases/performance-monitor/activity-monitor) für einen Server geöffnet wird. Dieser Datenstrom enthält Ereignisse, die einen Teil des Abfragetexts und des Zeitstempels jeder Abfrage zeigen. Außerdem enthält er Fehlermeldungen sowie Benachrichtigungen des Monitors, der wegen Verbindungsproblemen angehalten wird. Wenn sich der Aktivitätsmonitor im Leerlauf befindet oder ein Fehler beim Aktualisieren auftritt, finden Sie in diesem Ausgabekanal weitere Informationen.|






