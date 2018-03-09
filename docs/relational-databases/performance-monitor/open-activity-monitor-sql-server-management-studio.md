---
title: "Öffnen des Aktivitätsmonitors (SQL Server Management Studio) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: a126a0839ed1b43307f017196507da6dba85d160
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>Öffnen des Aktivitätsmonitors (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
   
 Der Aktivitätsmonitor führt Abfragen auf der überwachten Instanz aus, um Informationen für die Anzeigebereiche des Aktivitätsmonitors abzurufen. Wenn für das Intervall für die automatische Aktualisierung weniger als 10 Sekunden festgelegt sind, kann die für die Ausführung der Abfragen benötigte Zeit die Serverleistung beeinträchtigen.  
  
  
##  <a name="Permissions"></a> Überprüfen Sie Ihre Berechtigungen!  
 Zum Anzeigen der tatsächlichen Aktivität müssen Sie über die VIEW SERVER STATE-Berechtigung verfügen. Sie müssen zum Anzeigen des Abschnitts "Datendatei-E/A" des Aktivitätsmonitors neben VIEW SERVER STATE über die CREATE DATABASE-, ALTER ANY DATABASE- oder VIEW ANY DEFINITION-Berechtigung verfügen.  
  
 Zum Ausführen von KILL für einen Prozess muss ein Benutzer Mitglied der festen Serverrolle sysadmin oder processadmin sein.  
  
  
## <a name="open-activity-monitor"></a>Öffnen des Aktivitätsmonitors  

### <a name="keyboard-shortcut"></a>Tastenkombination  
 - Geben Sie **STRG+ALT+A** ein, um den Aktivitätsmonitor jederzeit zu öffnen.

 >**Tipp:** Bewegen Sie den Mauszeiger über ein Symbol in SSMS, um zu erfahren, wozu es dient und über welche Tastenkombination es aktiviert wird.

### <a name="toolbar"></a>Symbolleiste

Klicken Sie auf der Standardsymbolleiste auf das Symbol **Aktivitätsmonitor** . Es befindet sich in der Mitte, rechts neben den Schaltflächen „Rückgängig“ bzw. „Wiederholen“.
![Activity_Monitor_icon](../../relational-databases/performance-monitor/media/activity-monitor-icon.png)  
  
Stellen Sie das Dialogfeld **Verbindung mit Server herstellen** fertig, wenn Sie nicht bereits mit einer Instanz von SQL Server verbunden sind, die Sie überwachen möchten.
  
## <a name="launch-activity-monitor-and-object-explorer-on-startup"></a>Starten des Aktivitätsmonitors und Objekt-Explorers beim Start
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
2.  Erweitern Sie im Dialogfeld **Optionen** die Option **Umgebung**, und wählen Sie dann **Start**aus.  
  
3.  Wählen Sie in der Dropdownliste **Beim Start** die Option **Objekt-Explorer und Aktivitätsmonitor öffnen**aus.  

4.  Klicken Sie auf **OK**.
  
![open_object_explorer](../../relational-databases/performance-monitor/media/open-object-explorer.png)
  
  
## <a name="set-the-activity-monitor-refresh-interval"></a>Festlegen des Aktualisierungsintervalls für den Aktivitätsmonitor  
  
1.   Öffnen Sie Aktivitätsmonitor.  
  
2.   Klicken Sie mit der rechten Maustaste auf **Übersicht**, wählen Sie **Aktualisierungsintervall**aus, und wählen Sie anschließend das Intervall aus, in dem der Aktivitätsmonitor neue Instanzinformationen abrufen soll.  
  
  
