---
title: MSSQLSERVER_53 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "53"
helpviewer_keywords: 53 (Database Engine error)
ms.assetid: 1234f5a2-b3d1-425a-b29f-480fa792305f
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: d8d867fb206ee1571aebe6e1e62bc8eeab4a59e4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver53"></a>MSSQLSERVER_53
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|53|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name||  
|Meldungstext|Fehler beim Herstellen einer Verbindung mit dem Server.  Beim Herstellen einer Verbindung mit SQL Server kann dieser Fehler durch den Umstand verursacht werden, dass die Standardeinstellungen von SQL Server keine Remoteverbindungen zulassen. (Anbieter: Named Pipes-Anbieter, Fehler: 40 – Es konnte keine Verbindung mit SQL Server hergestellt werden) (.Net SqlClient-Datenanbieter)|  
  
## <a name="explanation"></a>Erklärung  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Client kann keine Verbindung mit dem Server herstellen. Dieser Fehler ist möglicherweise darauf zurückzuführen, dass entweder der Name des Servers durch den Client nicht aufgelöst werden kann oder der Name des Servers falsch ist.  
  
## <a name="user-action"></a>Benutzeraktion  
Stellen Sie sicher, dass Sie den richtigen Servernamen auf dem Client eingegeben haben und dass Sie den Namen des Servers auf dem Client auflösen können. Zum Überprüfen der TCP/IP-Namensauflösung können Sie den **ping**-Befehl im Windows-Betriebssystem verwenden.  
  
## <a name="see-also"></a>Siehe auch  
[Netzwerkprotokolle und Netzwerkbibliotheken](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Client-Netzwerkkonfiguration](~/database-engine/configure-windows/client-network-configuration.md)  
[Konfigurieren von Clientprotokollen](~/database-engine/configure-windows/configure-client-protocols.md)  
[Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
