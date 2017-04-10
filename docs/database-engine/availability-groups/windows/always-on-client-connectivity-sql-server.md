---
title: "Always On-Clientkonnektivit&#228;t (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server], Listener"
  - "Verfügbarkeitsgruppen [SQL Server], Voraussetzungen und Einschränkungen"
  - "Verfügbarkeitsgruppen [SQL Server], Clientkonnektivität"
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
caps.latest.revision: 22
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 21
---
# Always On-Clientkonnektivit&#228;t (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden Überlegungen zur Clientkonnektivität für Always On-Verfügbarkeitsgruppen beschrieben, einschließlich Voraussetzungen, Einschränkungen und Empfehlungen für Clientkonfigurationen und Einstellungen.  
  
 **In diesem Thema:**  
  
-   [Unterstützung für Clientkonnektivität](#ClientConnSupport)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="ClientConnSupport"></a> Unterstützung für Clientkonnektivität  
 Der folgende Abschnitt enthält Informationen zur [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Unterstützung für Clientverbindungen.  
  
 **Treiberunterstützung**  
  
 In der folgenden Tabelle ist die Treiberunterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]zusammengefasst:  
  
|Treiber|Multisubnetz-Failover|Anwendungszweck|Schreibgeschütztes Routing|Multisubnetz-Failover: Schnelleres Endpunktfailover in einzelnen Subnetzen|Multisubnetz-Failover: Auflösung benannter Instanzen für SQL-Clusterinstanzen|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|ja|Ja|Ja|Ja|Ja|  
|SQL Native Client 11.0 OLEDB|Nein|Ja|ja|Nein|Nein|  
|ADO.NET mit .NET Framework 4.0 mit Konnektivitätspatch*|Ja|Ja|Ja|Ja|ja|  
|ADO.NET mit .NET Framework 3.5 SP1 mit Konnektivitätspatch**|ja|Ja|Ja|Ja|ja|  
|Microsoft JDBC Driver 4.0 für SQL Server|ja|Ja|Ja|Ja|ja|  
  
 *Laden Sie das Konnektivitätspatch für ADO .NET mit .NET Framework 4.0 herunter: [http://support.microsoft.com/kb/2600211](http://support.microsoft.com/kb/2600211).  
  
 **Laden Sie das Konnektivitätspatch für ADO.NET mit .NET Framework 3.5 SP1 herunter: [http://support.microsoft.com/kb/2654347](http://support.microsoft.com/kb/2654347).  
  
> [!IMPORTANT]  
>  Ein Client muss eine TCP-Verbindungszeichenfolge verwenden, um eine Verbindung mit einem Verfügbarkeitsgruppenlistener herzustellen.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellung und Konfiguration von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Failoverclustering und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)   
 [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners, client connectivity, application failover.md)   
 [Informationen zum Clientverbindungszugriff auf Verfügbarkeitsreplikate &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Microsoft SQL Server Always On Solutions Guide for High Availability and Disaster Recovery (Microsoft SQL Server Always On-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung)](http://go.microsoft.com/fwlink/?LinkId=227600)   
 [SQL Server Always On Team Blogs: The official SQL Server Always On Team Blog (SQL Server Always On-Teamblogs: Der offizielle SQL Server Always On-Teamblog)](http://blogs.msdn.com/b/sqlAlways%20On/)   
 [Eine lange Verzögerung tritt auf, wenn Sie eine IPSec-Verbindung von einem Computer verbinden, auf dem Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 oder Windows Server 2008 R2 ausgeführt wird](http://support.microsoft.com/kb/980915)   
 [Der Clusterdienst dauert ungefähr 30 Sekunden zum Failover von IPv6-IP-Adressen in Windows Server 2008 R2](http://support.microsoft.com/kb/2578113)   
 [Langsamer Failovervorgang, wenn kein Router zwischen dem Cluster und einem Anwendungsserver vorhanden ist](http://support.microsoft.com/kb/2582281)  
  
  