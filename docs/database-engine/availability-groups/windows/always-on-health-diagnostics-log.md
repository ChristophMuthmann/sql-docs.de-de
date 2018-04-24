---
title: Integritätsdiagnoseprotokoll für Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
caps.latest.revision: 5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1888bcb32b61c45dd6a3761476ca5c931168280f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="always-on-availability-groups-health-diagnostics-log"></a>Integritätsdiagnoseprotokoll für Always On-Verfügbarkeitsgruppen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Ressourcen-DLL von SQL Server, die vom WSFC-Cluster (Windows Server Failover Clustering) ausgeführt wird, verwendet eine gespeicherte Prozedur in der SQL Server-Instanz namens [sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md), um die Integrität des primären Verfügbarkeitsreplikats zu überwachen.  
  
 Die Ressourcen-DLL von SQL Server verwaltete eine dedizierte offene Verbindung mit der SQL Server-Instanz. Über diese sendet die SQL Server-Instanz regelmäßig ausführliche Integritätsdiagnosen an die Ressourcen-DLL von SQL Server. Die Integritätsdiagnosen werden mit der Failoverrichtlinie gekoppelt, die in der Ressource der Verfügbarkeitsgruppe (die Eigenschaft „FailoverConditionLevel“) im Cluster konfiguriert wurde, und vom Cluster verwendet, um zu bestimmen, ob für die Ressource der Verfügbarkeitsgruppe ein Neustart oder ein Failover durchgeführt werden soll. Diese gespeicherte Prozedur stellt in SQL Server 2012 und höher den „Takt“ der Instanz für den WSFC-Cluster dar. Dieser ist präziser und zuverlässiger als in SQL Server 2008 R2 und früher. Dort wurde eine regelmäßige Verbindung zur Instanz mithilfe der Abfrage `SELECT @@SERVERNAME` hergestellt. Sie können dann die Bedingungen steuern, die ein Failover auslösen, indem Sie die Eigenschaft „FailoverConditionLevel“ der Verfügbarkeitsgruppe festlegen.  
  
 **Verwenden der Diagnoseprotokolle für SQL Server-Failovercluster**
 
 Alle Integritätsdiagnosen, die die Ressourcen-DLL von SQL Server von „sp_server_diagnostics“ erhält, werden automatisch im Standardverzeichnis für Protokolle der SQL Server-Instanz gespeichert (%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Log). Diese Protokolle werden als SQLDIAG-Protokolle bezeichnet und im XEL-Dateiformat (Expression Encoder Log File) für erweiterte Ereignisse gespeichert. Diese Dateien im SQL Server-Protokollverzeichnis weisen folgendes Format auf: \<HOSTNAME>_\<INSTANZNAME>_SQLDIAG_X_XXXXXXXXX.xel. Indem Sie die SQLDIAG-Protokolle verwenden, können Sie möglicherweise die Ursache von Fehlern in den Ressourcen von Verfügbarkeitsgruppen oder von Failoverereignissen bestimmen.  
  
 Ziehen Sie die XEL-Datei in SQL Server Management Studio, um ein SQLDIAG-Protokoll anzuzeigen.  
  
  