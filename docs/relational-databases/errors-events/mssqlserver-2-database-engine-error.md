---
title: MSSQLSERVER_2 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "2"
helpviewer_keywords: 2 (Database Engine error)
ms.assetid: 567fb571-7cda-4ce8-a702-cdff2df5d419
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: ce7e96fa9ef256a1b193d5a4979f7902646859ba
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver2"></a>MSSQLSERVER_2
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name||  
|Meldungstext|Fehler beim Herstellen einer Verbindung mit dem Server.  Beim Herstellen einer Verbindung mit SQL Server kann dieser Fehler durch den Umstand verursacht werden, dass die Standardeinstellungen von SQL Server keine Remoteverbindungen zulassen. (Anbieter: Named Pipes-Anbieter, Fehler: 40 – Es konnte keine Verbindung mit SQL Server hergestellt werden) (.Net SqlClient-Datenanbieter)|  
  
## <a name="explanation"></a>Erklärung  
Keine Antwort von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf die Clientanforderung, da der Server wahrscheinlich nicht gestartet wurde.  
  
## <a name="user-action"></a>Benutzeraktion  
Stellen Sie sicher, dass der Server gestartet wurde.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten der Datenbankmoduldienste](~/database-engine/configure-windows/manage-the-database-engine-services.md)  
[Konfigurieren von Clientprotokollen](~/database-engine/configure-windows/configure-client-protocols.md)  
[Netzwerkprotokolle und Netzwerkbibliotheken](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Client-Netzwerkkonfiguration](~/database-engine/configure-windows/client-network-configuration.md)  
[Konfigurieren von Clientprotokollen](~/database-engine/configure-windows/configure-client-protocols.md)  
[Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
