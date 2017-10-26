---
title: Clientnetzwerkkonfiguration | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- client configuration [SQL Server], connections
- Database Engine [SQL Server], network configurations
- connections [SQL Server], client configuration
- client connections [SQL Server], about client network connections
- client computers [SQL Server]
- client connections [SQL Server]
- network connections [SQL Server], client configuration
ms.assetid: c382eacd-0a0c-40a4-958f-9b774eb2d734
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d0cbddc4384df93a3a1987c12d3fbd2664d57e3b
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="client-network-configuration"></a>Client-Netzwerkkonfiguration
  Mithilfe von Clientsoftware sind Clientcomputer in der Lage, eine Verbindung mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einem Netzwerk herzustellen. Ein "Client" ist eine Front-End-Anwendung, die die von einem Server bereitgestellten Dienste verwendet, wie z. B. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Der Computer, auf dem sich diese Anwendung befindet, wird als *Clientcomputer*bezeichnet.  
  
 Auf der einfachsten Ebene kann sich ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Client auf demselben Computer wie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]befinden. In der Regel stellt jedoch ein Client eine Verbindung mit mindestens einem Remoteserver über ein Netzwerk her. Die Client/Server-Architektur von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht die problemlose Verwaltung mehrerer Clients und Server in einem Netzwerk. Die Standardclientkonfigurationen sind in den meisten Situationen ausreichend.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Anwendungen der unterschiedlichsten Typen gehören, beispielsweise folgende Anwendungen:  
  
-   OLE DB-Consumer  
  
     Diese Anwendungen verwenden den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieter, um eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]herzustellen. Der OLE DB-Anbieter dient als Mittler zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Clientanwendungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten als OLE DB-Rowsets verwenden. Das Eingabeaufforderungsprogramm **sqlcmd** und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]sind Beispiele für OLE DB-Anwendungen.  
  
-   ODBC-Anwendungen  
  
     Zu diesen Anwendungen gehören mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installierte Clienthilfsprogramme, wie z. B. das Befehlszeilenprogramm **osql** , sowie andere Anwendungen, die über den ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Verbindungen mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]herstellen.  
  
-   DB-Library-Clients  
  
     Zu diesen Anwendungen zählen das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **isql** command prompt utility and clients written to DB-Library. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Unterstützung für Clientanwendungen, die DB-Library verwenden, ist auf [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0-Funktionen beschränkt.  
  
> [!NOTE]  
>  Zwar werden Verbindungen von vorhandenen Anwendungen, die die DB-Library- und Embedded SQL-APIs verwenden, weiterhin von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] unterstützt, aber die zum Programmieren von Anwendungen, die diese APIs verwenden, erforderlichen Dateien bzw. die Dokumentation sind nicht mehr eingeschlossen. In zukünftigen Versionen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] werden Verbindungen von DB-Library- oder Embedded SQL-Anwendungen nicht mehr unterstützt. Verwenden Sie DB-Library bzw. Embedded SQL nicht zum Entwickeln neuer Anwendungen. Entfernen Sie alle Abhängigkeiten von DB-Library bzw. Embedded SQL, wenn Sie vorhandene Anwendungen ändern. Verwenden Sie anstelle dieser APIs den SQLClient-Namespace oder eine API wie OLE DB oder ODBC. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält die DB-Library-DLL nicht, die zum Ausführen dieser Anwendungen erforderlich ist. Zum Ausführen von DB-Library- oder Embedded SQL-Anwendungen muss die DB-Library-DLL von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 6.5, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 oder [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]verfügbar sein.  
  
 Unabhängig vom Anwendungstyp besteht die Verwaltung eines Clients in erster Linie darin, seine Verbindungen mit den Serverkomponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu konfigurieren. Abhängig von den Anforderungen des Standorts reichen die Aufgaben der Clientverwaltung vom bloßen Eingeben des Namens für den Servercomputer bis zum Erstellen einer Bibliothek mit benutzerdefinierten Konfigurationseinträgen, um ein Einbinden in eine komplexe Multiserverumgebung zu ermöglichen.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-DLL enthält die Netzwerkbibliotheken und wird vom Setupprogramm installiert. Die Netzwerkprotokolle werden während der Installation für neue Installationen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht aktiviert. Aktualisierte Installationen aktivieren die zuvor aktivierten Protokolle. Die zugrunde liegenden Netzwerkprotokolle werden als Teil von Windows Setup installiert (oder über die Anwendung Netzwerk in der Systemsteuerung). Die folgenden Tools können für die Verwaltung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Clients verwendet werden:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager  
  
     Client- und Server-Netzwerkkomponenten werden mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager verwaltet, der die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Netzwerkkonfiguration, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Clientkonfiguration und den Dienst-Manager aus früheren Versionen enthält. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ist ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] -MMC-Snap-In (Microsoft Management Console). Er wird auch als Knoten im Windows Computer Manager-Snap-In angezeigt. Einzelne Netzwerkbibliotheken können aktiviert, deaktiviert und konfiguriert werden. Außerdem kann ihnen mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager eine Priorität zugewiesen werden.  
  
-   Setup  
  
     Führen Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup aus, um die Netzwerkkomponenten auf einem Clientcomputer zu installieren. Einzelne Netzwerkbibliotheken können während des Setups aktiviert bzw. deaktiviert werden, wenn das Setup an der Eingabeaufforderung gestartet wird.  
  
-   ODBC-Datenquellen-Administrator  
  
     Mit dem ODBC-Datenquellen-Administrator können Sie ODBC-Datenquellen auf Computern erstellen und ändern, auf denen das Microsoft Windows-Betriebssystem ausgeführt wird.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Konfigurieren von Clientprotokollen](../../database-engine/configure-windows/configure-client-protocols.md)  
  
 [Erstellen oder Löschen eines Serveralias für die Verwendung durch einen Client &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
 [Anmelden an SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
 [Öffnen des ODBC-Datenquellen-Administrators](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
 [Überprüfen der Version des ODBC SQL Server-Treibers &#40;Windows&#41;](../../database-engine/configure-windows/check-the-odbc-sql-server-driver-version-windows.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Server-Netzwerkkonfiguration](../../database-engine/configure-windows/server-network-configuration.md)  
  
 [Verwalten der Datenbankmoduldienste](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  

