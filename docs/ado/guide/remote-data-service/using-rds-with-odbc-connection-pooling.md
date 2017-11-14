---
title: Verwenden von RDS mit ODBC-Verbindungs-Pooling | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26342c07b2efe10a98a1cef4ff258d7fe5715094
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-rds-with-odbc-connection-pooling"></a>Verwenden von RDS mit ODBC-Verbindungs-Pooling
Wenn Sie eine ODBC-Datenquelle verwenden, können Sie das Verbindungspooling-Option in Internet Information Services (IIS), hohe Leistung Behandlung der Clientbelastung erreicht. Verbindungspooling ist eine Ressourcen-Manager für Verbindungen, verwalten den geöffneten Zustand bei häufig verwendeten Verbindungen.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Finden Sie in der Dokumentation zu Internetinformationsdienste (IIS), um Verbindungspooling zu aktivieren.  
  
 Beachten Sie, dass Verbindungspooling aktivieren den Webserver auf andere Einschränkungen, für die Themenbereichsdatenbank kann in der Microsoft Internet Information Services-Dokumentation nicht anders angegeben.  
  
 Um sicherzustellen, dass Verbindungspooling stabil ist, und zusätzliche Leistungssteigerungen bietet, müssen Sie Microsoft SQL Server zur Verwendung der TCP/IP-Sockets-Netzwerkbibliothek konfigurieren.  
  
 Zu diesem Zweck müssen Sie:  
  
-   Konfigurieren Sie die SQL Server-Computer, um TCP/IP-Sockets verwenden können.  
  
-   Konfigurieren Sie den Webserver für die TCP/IP-Sockets verwenden können.  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>Konfigurieren von SQL Server-Computer zur Verwendung von TCP/IP-Sockets  
 Führen Sie das SQL Server-Setup-Programm auf dem SQL Server-Computer, damit die Interaktionen mit der Datenquelle die TCP/IP-Sockets-Netzwerkbibliothek verwenden.  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>Angeben der TCP/IP-Sockets-Netzwerkbibliothek auf dem SQL Server-computer  
  
### <a name="in-microsoft-sql-server-65"></a>In Microsoft SQL Server 6.5:  
  
1.  Zeigen Sie über das Startmenü auf Programme, zeigen Sie auf Microsoft SQL Server 6.5, und klicken Sie dann auf SQL-Setup.  
  
2.  Klicken Sie zweimal auf Weiter.  
  
3.  In Microsoft SQL Server-Optionen (Dialogfeld), wählen Sie die Netzwerkunterstützung ändern, und klicken Sie dann auf Weiter.  
  
4.  Stellen Sie sicher, dass das TCP/IP-Sockets-Kontrollkästchen ausgewählt ist, und klicken Sie auf OK.  
  
5.  Klicken Sie auf Weiter, um den Vorgang abzuschließen, und beenden Sie Setup zu.  
  
### <a name="in-microsoft-sql-server-70"></a>In Microsoft SQL Server 7.0:  
  
1.  Zeigen Sie über das Startmenü auf Programme, zeigen Sie auf Microsoft SQL Server 7.0, und klicken Sie dann auf SQL Server-Netzwerkkonfiguration.  
  
2.  Klicken Sie auf der Registerkarte Allgemein des Dialogfelds auf Hinzufügen.  
  
3.  Klicken Sie auf "TCP/IP", klicken Sie im Dialogfeld Netzwerkbibliothekskonfiguration hinzufügen.  
  
4.  Die Portnummer und die Kontrollkästchen der Proxy-Adresse Geben Sie die Port-Nummer und Proxy Adresse vom zuständigen Netzwerkadministrator bereitgestellt.  
  
5.  Klicken Sie auf OK, um den Vorgang abzuschließen, und beenden Sie Setup zu.  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>Konfigurieren des Webservers zur Verwendung von TCP/IP-Sockets  
 Es gibt zwei Optionen zum Konfigurieren des Webservers TCP/IP-Sockets verwendet werden. Was Sie tun abhängig, ob alle SQL Server aus dem Web-Server zugegriffen werden, oder nur eine bestimmte SQL-Server vom Webserver zugegriffen wird.  
  
 Wenn alle SQL Server, die vom Webserver zugegriffen wird, müssen Sie die SQL Server-Clientkonfigurationsprogramm auf dem Webservercomputer ausführen. Die folgenden Schritte ändern Sie die Standard-Netzwerkbibliothek für alle SQL Server-Verbindungen zwischen diesen IIS-Webserver und verwenden Sie die TCP/IP-Sockets-Netzwerkbibliothek hergestellt.  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>So konfigurieren Sie den Webserver (alle SQL Server)  
  
### <a name="for-microsoft-sql-server-65"></a>Für Microsoft SQL Server 6.5:  
  
1.  Zeigen Sie über das Startmenü auf Programme, zeigen Sie auf Microsoft SQL Server 6.5, und klicken Sie dann auf SQL Client-Konfigurationsprogramm.  
  
2.  Klicken Sie auf der Registerkarte Netzwerkbibliothek.  
  
3.  Wählen Sie im Feld Standardnetzwerk TCP/IP-Sockets.  
  
4.  Klicken Sie auf Änderungen zu speichern und beenden Sie das Dienstprogramm "Fertig" ändert.  
  
### <a name="for-microsoft-sql-server-70"></a>Für Microsoft SQL Server 7.0:  
  
1.  Zeigen Sie über das Startmenü auf Programme, zeigen Sie auf Microsoft SQL Server 7.0, und klicken Sie dann auf Server-Clientkonfiguration.  
  
2.  Klicken Sie auf der Registerkarte "Allgemein".  
  
3.  Klicken Sie auf "TCP/IP", in das standardmäßige Network Library.  
  
4.  Klicken Sie auf OK, um Änderungen zu speichern und beenden Sie das Dienstprogramm.  
  
 Wenn eine bestimmte SQL-Server von einem Webserver zugegriffen wird, müssen Sie die SQL Server-Clientkonfigurationsprogramm auf dem Webservercomputer ausführen. Um die Netzwerkbibliothek für eine bestimmte SQL Server-Verbindung zu ändern, konfigurieren Sie die SQL Server-Clientsoftware auf dem Webservercomputer folgendermaßen.  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>So konfigurieren Sie die Webserver (keinen spezifischen SQL Server)  
  
### <a name="for-microsoft-sql-server-65"></a>Für Microsoft SQL Server 6.5:  
  
1.  Zeigen Sie über das Startmenü auf Programme, zeigen Sie auf Microsoft SQL Server 6.5, und klicken Sie dann auf SQL Client-Konfigurationsprogramm.  
  
2.  Klicken Sie auf der Registerkarte "Erweitert".  
  
3.  Geben Sie im Feld Server den Namen des Servers für die Verbindung mit der Verwendung von TCP/IP-Sockets.  
  
4.  Wählen Sie im Feld Name der DLL TCP/IP-Sockets.  
  
5.  Klicken Sie auf hinzufügen/ändern. Alle Datenquellen auf diesem Server werden nun TCP/IP-Sockets verwendet.  
  
6.  Klicken Sie auf "Fertig" ändert.  
  
### <a name="for-microsoft-sql-server-70"></a>Für Microsoft SQL Server 7.0:  
  
1.  Zeigen Sie über das Startmenü auf Programme, zeigen Sie auf Microsoft SQL Server 7.0, und klicken Sie dann auf Clientkonfigurations-Hilfsprogramm.  
  
2.  Klicken Sie auf der Registerkarte "Allgemein".  
  
3.  Klicken Sie auf Hinzufügen.  
  
4.  Geben Sie den Alias des Servers im Server-Alias ein. Klicken Sie im Feld Netzwerk Bibliotheken auf TCP/IP. Geben Sie in das Feld Computername den Computernamen des Computers, der TCP/IP-Sockets-Clients überwacht. Geben Sie im Feld Port den Port auf dem SQL Server lauscht.  
  
5.  Klicken Sie auf OK, und anschließend erneut um das Hilfsprogramm zu beenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)























