---
title: MSSQLSERVER_11001 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- "12001"
helpviewer_keywords:
- 11001 (Database Engine error)
ms.assetid: 53d4d63a-61e3-441f-bfe9-9d44f7a05fd4
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a5c7624e83a1f4e5bda71e3c66ce37adb986b85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver11001"></a>MSSQLSERVER_11001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|11001|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name||  
|Meldungstext|Fehler beim Herstellen einer Verbindung mit dem Server.  Beim Herstellen einer Verbindung mit SQL Server kann dieser Fehler durch den Umstand verursacht werden, dass die Standardeinstellungen von SQL Server keine Remoteverbindungen zulassen. (Anbieter: TCP-Anbieter, Fehler: 0 – Host ist unbekannt.) (.Net SqlClient-Datenprovider)|  
  
## <a name="explanation"></a>Erklärung  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Client kann keine Verbindung mit dem Server herstellen. Der Fehler ist möglicherweise darauf zurückzuführen, dass entweder der Name des Servers durch den Client nicht aufgelöst werden kann oder der Name des Servers falsch ist.  
  
## <a name="user-action"></a>Benutzeraktion  
Stellen Sie sicher, dass Sie den richtigen Servernamen auf dem Client eingegeben haben und dass Sie den Namen des Servers auf dem Client auflösen können. Zum Überprüfen der TCP/IP-Namensauflösung können Sie den **ping**-Befehl im Windows-Betriebssystem verwenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Netzwerkprotokolle und Netzwerkbibliotheken](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Client-Netzwerkkonfiguration](~/database-engine/configure-windows/client-network-configuration.md)  
[Konfigurieren von Clientprotokollen](~/database-engine/configure-windows/configure-client-protocols.md)  
[Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
