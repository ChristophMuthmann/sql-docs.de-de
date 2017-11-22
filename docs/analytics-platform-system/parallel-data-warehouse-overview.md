---
title: "Übersicht über die Parallel Data Warehouse"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "In diesem Thema wird erläutert, die Appliance-Software und die Software nicht Appliance Bestandteile Analytics Platform System."
ms.date: 01/05/2017
ms.topic: article
ms.assetid: db0c4a43-a66d-4c44-ab91-791c5785f71c
caps.latest.revision: "20"
ms.openlocfilehash: 587b1ce6720fc07d9ac24edde2c5b8cc2b30c89f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="parallel-data-warehouse-overview"></a>Übersicht über die Parallel Data Warehouse
In diesem Thema wird erläutert, die Appliance-Software und die Software nicht Appliance Bestandteile Analytics Platform System.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![Parallel Data Warehouse-Software](media/parallel-data-warehouse-software.png "Parallel Data Warehouse-Software")  
  
## <a name="sec1"></a>Softwareupdates – Abfragen, Verarbeitung und Speicherung von Daten  
  
### <a name="control-node"></a>Knoten "Zugriffssteuerung"  
MPP-Modul  
Das MPP-Modul ist das System enorm parallele Verarbeitung (MPP) des Gehirns. Sie führt die folgenden Aktionen aus:  
  
-   Parallele Abfragepläne erstellt, und koordiniert die parallele Ausführung von Abfragen auf den Serverknoten.  
  
-   Speichert und koordiniert die Anwendungsmetadaten und Daten für alle Datenbanken.  
  
-   SQL Server PDW-Datenbank-Authentifizierung und Autorisierung verwaltet.  
  
-   Verfolgt den Status der Hardware und Software.  
  
### <a name="data-movement-service-dms"></a>Datenverschiebungsdiensts (DMS)  
Daten Bewegung Service (DMS) ist Teil der "geheime Besonderheiten von" von PDW. Sie führt die folgenden Aktionen aus:  
  
-   Überträgt Daten an und von den SQL Server PDW-Knoten.  
  
-   Prozesse Abfragevorgänge an, für die Übertragung von Daten zwischen den Knoten erforderlich.  
  
-   Verbessert die abfrageleistung durch Optimieren der mindestgeschwindigkeiten für die Übertragung von Daten.  
  
### <a name="admin-console"></a>Verwaltungskonsole  
Die Verwaltungskonsole ist eine Webanwendung, in dem die Appliance Zustand, Integrität und Leistungsinformationen dargestellt.  
  
### <a name="configuration-manager"></a>Konfigurations-Manager  
Der Konfigurations-Manager (dwconfig.exe), ist das Tool, mit denen Appliance Administratoren Analytics Platform System zu konfigurieren.  
  
### <a name="control-node-databases"></a>Steuerelement-Datenbanken  
SQL Server verwaltet alle Datenbanken auf den Knoten "Zugriffssteuerung".  
  
-   Die Shelldatenbank verwaltet die Metadaten für alle verteilte Benutzerdatenbanken.  
  
-   TempDB enthält die Metadaten für alle Benutzer temporären Tabellen auf dem Gerät.  
  
-   Master ist die Mastertabelle für SQL Server auf den Knoten "Zugriffssteuerung".  
  
### <a name="compute-node"></a>Computeknoten  
Die Serverknoten werden parallele Datenverarbeitung und Speichereinheiten. Sie haben direkten angeschlossenen Speicher und SQL Server verwenden, um Benutzerdaten zu verwalten.  
  
### <a name="data-movement-service-dms"></a>Datenverschiebungsdiensts (DMS)  
Daten Bewegung Service (DMS) wird auf jede Compute-Knoten für die folgenden Aufgaben ausgeführt:  
  
-   Im Rahmen der Verarbeitung von parallelen Abfragen Datenübertragung DMS zu und von anderen Computerknoten und der Knoten "Zugriffssteuerung".  
  
-   DMS, die unter jeder Serverknoten empfängt riesige Datenmengen parallel. Daten werden direkt vom Server Laden für die Serverknoten parallel geladen.  
  
-   DMS werden Daten aus jeder Compute-Knoten direkt mit dem backup-Server übertragen.  
  
-   Mithilfe von PolyBase, überträgt DMS Daten an und von einem externen Hadoop-Cluster oder der HDInsight-Region, auf dem Gerät.  
  
### <a name="compute-node-databases"></a>Berechnen Sie die Knoten-Datenbanken 
Jeder Compute-Knoten führt eine Instanz von SQL Server zum Verarbeiten von Abfragen und Verwalten von Benutzerdaten.  
  
## <a name="appliance-fabric"></a>Appliance-Fabric  
Die Appliance Fabric stellt das Betriebssystem, die Dienste und die Netzwerkinfrastruktur für die Anwendung bereit.  
  
### <a name="domain-controller"></a>Domänencontroller  
Active Directory (AD)-Domänendienste (DS)  
Analyseplattformsystem führt die Authentifizierung zwischen den Knoten Analytics Platform System und die Authentifizierung von SQL Server PDW-Windows-Authentifizierung Anmeldungen verwaltet.  
  
DNS-Dienst  
Windows Domain Name Service (DNS) löst Domänennamen in IP-Adressen für die Appliance Analytics Platform System.  
  
### <a name="windows-deployment-service"></a>Windows-Bereitstellungsdienste  
Windows-Verwaltungsinstrumentation (Windows Deployment Service, WDS) wird das Betriebssystem Windows Server, auf dem Gerät bereitgestellt. Es wird auf jedem Host und die virtuelle Maschine über das Gerät bereitgestellt werden.  
  
Der DHCP-Dienst erstellt IP-Adressen, damit die Hosts innerhalb der Domäne der Anwendung die Appliance-Netzwerk verbinden können, ohne eine vorkonfiguriert, dass IP-Adresse.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Analyseplattformsystem verwendet die Virtualisierung, um hohe Verfügbarkeit zu erzielen. Der Virtual Machine Manager hostet System Center zur Bereitstellung des Betriebssystems auf physischen Hosts.  
  
Windows Server Update Services (WSUS), zum Anwenden oder Entfernen von Windows-Updates auf allen Hosts und virtuellen Maschinen.  
  
### <a name="windows-server"></a>Windows Server  
Alle Hosts und virtuellen Maschinen in der Anwendung Windows Server-Betriebssystem ausgeführt.  
  
### <a name="failover-clustering"></a>Failoverclustering  
Windows-Failoverclustering bietet die Möglichkeit, Prozesse auf einem passiven Host neu zu starten, wenn ein Host ausfällt.  
  
### <a name="storage-spaces"></a>Speicherplätze  
Windows Storage Spaces verwaltet Benutzerdaten als einem Speicherpool für eine kleine Gruppe von Compute-Knoten. Wenn Compute-Knoten ein Fehler auftritt, sind die Daten immer noch zugegriffen werden kann, durch einen anderen Computeknoten in der Gruppe.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V-Server bietet eine einfache und zuverlässige Virtualisierungslösung. Analyseplattformsystem verwendet Virtualizations, um CPU-Ressourcen zu verteilen und hohe Verfügbarkeit für die PDW-Knoten und die Appliance Fabric-Komponenten bereitzustellen.  
  
## <a name="sec2"></a>Nicht-relationale Daten
PolyBase-Technologie integriert externe Hadoop-Daten, SQL Server PDW-Daten. Hadoop-Daten können auf diesen Hadoop-Datenquellen gespeichert werden:  
  
-   Hortonworks für Linux- oder WindowsServer  
  
-   Cloudera unter Linux  
  
-   HDInsight unter APS  
  
-   HDInsight-Daten, die auf Azure-Speicher-Blob gespeichert  
  
## <a name="query-tools"></a>Abfragetools   
  
Abfragen werden mit Transact geschrieben\-SQL so geändert, dass um die MPP Art der Abfragen zu passen. Alle Abfragen werden mit dem Steuerungsknoten gesendet, die zum Ausführen der Abfrage über die Serverknoten einen parallelen Abfrageplan generiert.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools in Visual Studio ausgeführt wird und unsere empfohlenen GUI-Tool für die Einreichung von Abfragen in SQL Server PDW ist. Ähnliches gilt für SQL Server Management Studio können Sie sich durch einen Objekt-Explorer navigieren.  
  
Wenn Sie Visual Studio noch nicht haben, können Sie die Tools herunterladen, die Sie kostenlos benötigen. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>Sqlcmd-Befehlszeilentool für Abfrage  
Sqlcmd wird das SQL Server-Befehlszeilentool zum Ausführen von Transact\-SQL-Anweisungen und Systembefehle aus. Es funktioniert mit SQL Server PDW und unsere empfohlenen Befehlszeilentool zum Abfragen von SQL Server PDW ist. Sie können mit Sqlcmd Transact ausführen\-SQL-Anweisungen interaktiv über die Befehlszeile als einer Batchdatei oder in Windows PowerShell.  
  
<!-- MISSING LINKS

If you don’t have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
Sie können Integration Services für SQL Server PDW-Abfrage verwenden. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>Verbindungsserver  
Mit einer Server-Verbindung mit SQL Server verknüpft, können Sie SQL Server Transact übermitteln\-SQL-Anweisungen in SQL Server PDW. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>Business Intelligence-Tools
  
Analysis Services  
SQL Server PDW ist eine gültige Datenquelle für Analysis Services-Datenbanken und Excel PowerPivot-Modelle. Den OLE DB-Anbieter können Sie einen Analysis Services-Cube zur Verwendung mehrdimensionale analytische onlineverarbeitung (MOLAP) oder relationale analytische onlineverarbeitung (ROLAP) Speicher konfigurieren.  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>Berichts-Generator  
Sie können SQL Server PDW als SQL Server-Datenquelle für Berichte verwenden, die Sie mithilfe von SQL Server Report Builder für Reporting Services zu entwickeln. Sie können auch SQL Server PDW als eine SQL Server-Datenquelle für Berichtsmodelle verwenden. Mithilfe von Berichts-Manager oder dem Berichtsserver API können Sie ein Modell aus einer SQL Server PDW-Datenbank generieren.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot für Excel  
Sie können in SQL Server PDW mit PowerPivot für Excel, kostenlos verbinden, die die Daten Analysefunktionen von Excel erheblich erweitert.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>Laden die Tools 
  
### <a name="integration-services"></a>Integration Services  
Installieren Sie PDW-spezifischen Ziel-Adapter, mit die SQL ServerIntegration Dienste zu verwenden, um Daten in SQL Server PDW laden können.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>Dwloader Command-Line-Ladeprogramm  
Dwloader ist ein Befehlszeilen laden-Tool, das Daten parallel von Ihrem Server laden, die SQL Server PDW-Serverknoten lädt. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase für Hadoop-Integration  
Mit der PolyBase-Technologie können Sie nicht relationaler Daten aus einem Hadoop-Cluster in einer relationalen Tabelle in SQL Server PDW laden. Hadoop-Daten können in einem externen Hadoop-Cluster, die auf APS HDI-Region oder in einem Azure-Blob-Speicher befinden.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>Datenbank sichern und Wiederherstellen  
SQL Server PDW verwendet Transact\-SQL sichern und Wiederherstellen von Datenbanken sichern und Wiederherstellen von Benutzerdatenbanken, parallel zu und von einem Sicherungsserver Befehle. SQL Server PDW schreibt die Sicherung in einem Verzeichnis in einer Windows-Dateifreigabe und anschließend werden Daten aus einer Windows-Dateifreigabe ebenso wiederhergestellt.  
  
Weitere Informationen finden Sie unter [für die Sicherung und Laden von Hardware planen](backup-and-loading-hardware.md) und [Sicherung und Wiederherstellung (Übersicht)](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>Remotetabelle kopieren  
Die Remotekopie Tabelle-Funktion können Sie Tabellen aus SQL Server PDW-Datenbanken auf entfernte (nicht-Appliance) – SMP – SQL Server-Datenbanken zu kopieren. Für SQL Server PDW aktiviert Hub- und Spoke-Szenarios.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>Überwachung  
Analyseplattformsystem stellt mehrere Methoden zum Überwachen der Appliance-Aktivität  
  
### <a name="admin-console"></a>Verwaltungskonsole  
Der Verwaltungskonsole können Sie aktuellen Status über den Zustand der Anwendung anzeigen. Dies führt zu einer Webanwendung auf den Knoten "Zugriffssteuerung" und über Https zugegriffen werden kann.  
  
Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>Systemsichten  
Die Admin-Konsole basiert auf System Sicht Abfragen. Sie können Abfragen, die Systemsichten einzeln, um die spezielle Information erhalten, die Sie benötigen.  

Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe von Systemsichten &#40; Analyseplattformsystem &#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operationsmanager  
Es sind System Center Operations Manager (SCOM) Management Packs für SQL Server PDW. 

Um die Einheit für SCOM konfigurieren zu können, finden Sie unter [überwachen Sie die Anwendung mithilfe von System Center Operations Manager &#40; Analyseplattformsystem &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
