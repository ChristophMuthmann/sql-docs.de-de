---
title: Startprogramm für SQL-Volltextfilterdaemon (Registerkarte „Dienst“) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6aad7ebe-c4be-4d37-8536-61502f51faa2
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 366a60d753cb31bdc066051e9a3d84a8d8229a60
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-full-text-filter-daemon-launcher-service-tab"></a>Startprogramm für SQL-Volltextfilterdaemon (Registerkarte Dienst)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]wird der FDHOST (SQL-Volltextfilterdaemon)-Startprogrammdienst vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Volltext verwendet. Dieser Dienst muss ausgeführt werden, wenn Sie die Volltextsuche verwenden. Informationen über die Prozesse des Filterdaemonhosts finden Sie unter „Architektur der Volltextsuche“ in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
 Verwenden Sie im Startprogramm für SQL-Volltextfilterdaemon die Registerkarte **Dienst**im Dialogfeld **Eigenschaften des SQL Full-text Filter Daemon-Programmstarters** (SQL-Volltextfilterdaemon-LauncherProperties), um die folgenden Optionen anzuzeigen oder anzugeben.  
  
## <a name="options"></a>Tastatur  
 **Binärpfad**  
 Führt den Speicherort der Programmdateien auf, die von diesem Dienst verwendet werden.  
  
 **Fehlersteuerung**  
 1 steht für `SERVICE_ERROR_NORMAL`. Wenn der Dienst nicht zusammen mit dem Computer gestartet werden kann, wird der Fehler vom Startprogramm protokolliert und eine Popupmeldung angezeigt, der Startvorgang aber fortgesetzt. Dieser Wert kann nicht geändert werden.  
  
 **Exitcode**  
 Bei einem Fehler wird die dazu gehörende Nummer in diesem Feld angezeigt. Verwenden Sie diese Nummer für die Problembehandlung. Stellen Sie die Fehlernummer dem technischen Support zur Verfügung, oder durchsuchen Sie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
 **HostName**  
 Zeigt den Namen des Computers oder Clusters an, auf dem der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird.  
  
 **Name**  
 Zeigt den Anzeigenamen des Dienstes an.  
  
 **Prozess-ID**  
 Zeigt die Prozess-ID von Windows an.  
  
 **SQL-Diensttyp**  
 Zeigt den für aufrufende Prozesse bereitgestellten Diensttyp an. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden mehrere Dienste installiert.  
  
 **Startmodus**  
 Richten Sie den Dienst mit den folgenden Auswahlmöglichkeiten ein:  
  
-   Manuell: Dieser Dienst wird nicht automatisch zusammen mit dem Computer gestartet. Zum Starten des Dienstes verwenden Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager oder ein anderes Tool.  
  
-   Automatisch: Dieser Dienst wird zusammen mit dem Computer gestartet.  
  
-   Deaktiviert: Dieser Dienst kann nicht gestartet werden.  
  
 **Status**  
 Zeigt an, ob dieser Dienst ausgeführt wird, angehalten oder deaktiviert ist. "**…**" gibt einen ausstehenden Statuswechsel an.  
  
  
