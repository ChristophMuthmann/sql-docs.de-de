---
title: Standard-Netzwerkkonfiguration von SQL Server | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- protocols [SQL Server], default settings
- default protocols, after install
ms.assetid: 635ea361-a797-4971-bd05-e3415862bc5c
caps.latest.revision: 4
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 95adc8c5246284a8f82131f853e6a28b91b8dc5f
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# Standard-Netzwerkkonfiguration von SQL Server
Um eine erhöhte Sicherheit zu gewährleisten, wird bei bestimmten Neuinstallationen von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] die Netzwerkkonnektivität deaktiviert. Die Netzwerkkonnektivität über TCP/IP wird nicht deaktiviert, wenn Sie Enterprise Edition, Standard Edition, Evaluation Edition oder Workgroup Edition verwenden oder wenn eine vorherige Installation von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] vorhanden ist. Für alle Installationen wird das Shared Memory-Protokoll aktiviert, um lokale Verbindungen mit dem Server zu ermöglichen. Der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Browser-Dienst wird möglicherweise beendet, je nach Installationsbedingungen und -optionen.

Verwenden Sie den Knoten [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Netzwerkkonfiguration des Konfigurations-Managers von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , um nach der Installation die Netzwerkprotokolle zu konfigurieren. Verwenden Sie den Knoten [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Dienste des Konfigurations-Managers von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , um den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Browserdienst so zu konfigurieren, dass er automatisch gestartet wird. Weitere Informationen finden Sie unter [Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).


## Standardkonfiguration

In der folgenden Tabelle wird die Konfiguration nach der Installation beschrieben.

Edition | Neuinstallation/vorherige Installation vorhanden | Shared Memory | TCP/IP    | Named Pipes
| -------- | -- | -- | -- | --  |  
Enterprise  | Neue Installation  | Aktiviert   | Aktiviert   | Deaktiviert für Netzwerkverbindungen
Standard    | Neue Installation  | Aktiviert   | Aktiviert   | Deaktiviert für Netzwerkverbindungen
Web | Neue Installation  | Aktiviert   | Aktiviert   | Deaktiviert für Netzwerkverbindungen
Entwickler   | Neue Installation  | Aktiviert   | Disabled  | Deaktiviert für Netzwerkverbindungen
Evaluation  | Neue Installation  | Aktiviert   | Aktiviert   | Deaktiviert für Netzwerkverbindungen
SQL Server Express  | Neue Installation  | Aktiviert   | Disabled  | Deaktiviert für Netzwerkverbindungen
Alle Editionen    | Vorherige Installation ist vorhanden, wird aber nicht aktualisiert.   | Wie für Neuinstallation  | Wie für Neuinstallation  | Wie für Neuinstallation
Alle Editionen    | Upgrade   | Aktiviert   | Einstellungen aus früherer Installation werden beibehalten.    | Einstellungen aus früherer Installation werden beibehalten.


>[!NOTE]
> Wenn die Instanz auf einem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Failovercluster ausgeführt wird, lauscht sie an allen Ports für alle IP-Adressen, die beim Ausführen des [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Setups für [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ausgewählt wurden.
 
>[!NOTE]
> Wenn Sie [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mit Eingabeaufforderungsargumenten installieren, können Sie die zu aktivierenden Protokolle mithilfe des `TCPENABLED` -Parameters und des `NPENABLED` -Parameters angeben. Weitere Informationen finden Sie unter [Installieren von SQL Server über die Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## Erstellen einer Verbindungszeichenfolge

Beispiele für Verbindungszeichenfolgen finden Sie in den folgenden Themen:
* [Erstellen einer gültigen Verbindungszeichenfolge mithilfe des Shared Memory-Protokolls](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
* [Erstellen einer gültigen Verbindungszeichenfolge mithilfe von TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)



## [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browsereinstellungen

Der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Browserdienst kann während der Installation so konfiguriert werden, dass er automatisch gestartet wird. Standardmäßig wird er unter folgenden Bedingungen automatisch gestartet:

* Beim Ausführen eines Upgrades für eine Installation.
* Beim gleichzeitigen Installieren mit einer anderen Instanz von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
* Beim Installieren in einem Cluster.
* Beim Installieren einer benannten Instanz des Datenbankmoduls, die alle Instanzen von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Express einschließt.
* Beim Installieren einer benannten Instanz von Analysis Services.

## Siehe auch

[Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

[Oberflächenkonfiguration](../../relational-databases/security/surface-area-configuration.md)  




