---
title: MSSQLSERVER_10060 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "10060"
helpviewer_keywords: 10060 (Database Engine error)
ms.assetid: 28c21277-cad8-406c-a955-07933a56982a
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8804ad6e01204446f1e5b3c2cab3b1e2bd85367f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10060"></a>MSSQLSERVER_10060
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10060|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name||  
|Meldungstext|Fehler beim Herstellen einer Verbindung mit dem Server.  Beim Herstellen einer Verbindung mit SQL Server kann dieser Fehler durch den Umstand verursacht werden, dass die Standardeinstellungen von SQL Server keine Remoteverbindungen zulassen. (Anbieter: TCP-Anbieter, Fehler: 0 – Ein Verbindungsversuch ist fehlgeschlagen, da die Gegenstelle nach einer bestimmten Zeitspanne nicht ordnungsgemäß reagiert hat, oder die hergestellte Verbindung fehlerhaft war, da der verbundene Host nicht reagiert hat.) (Microsoft SQL Server, Fehler: 10060)|  
  
## <a name="explanation"></a>Erklärung  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Client kann keine Verbindung mit dem Server herstellen. Dieser Fehler kann auftreten, weil entweder die Verbindung von der Firewall auf dem Server abgelehnt wurde oder der Server nicht so konfiguriert ist, dass er Remoteverbindungen annimmt.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie zum Beheben dieses Fehlers eine der folgenden Aktionen aus:  
  
-   Stellen Sie sicher, dass Sie die Firewall auf dem Computer konfiguriert haben, sodass diese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz Verbindungen annehmen kann.  
  
-   Verwenden Sie das Tool [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager, um zuzulassen, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Remoteverbindungen angenommen werden.  
  
## <a name="see-also"></a>Siehe auch  
[Konfigurieren einer Windows-Firewall für Datenbankmodulzugriff](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[Konfigurieren von Clientprotokollen](~/database-engine/configure-windows/configure-client-protocols.md)  
[Netzwerkprotokolle und Netzwerkbibliotheken](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Client-Netzwerkkonfiguration](~/database-engine/configure-windows/client-network-configuration.md)  
[Konfigurieren von Clientprotokollen](~/database-engine/configure-windows/configure-client-protocols.md)  
[Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
