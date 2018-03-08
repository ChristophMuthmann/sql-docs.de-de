---
title: "Transaktionen: Always On-Verfügbarkeitsgruppen und Datenbankspiegelung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
caps.latest.revision: "33"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 25e9efc5d7ffb6d4d0c09cc88e19671ed7f7b043
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="transactions---availability-groups-and-database-mirroring"></a>Transaktionen: Always On-Verfügbarkeitsgruppen und Datenbankspiegelung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In diesem Thema wird die Unterstützung für datenbankübergreifende und verteilte Transaktionen für Always On-Verfügbarkeitsgruppen und die Datenbankspiegelung beschrieben.  

## <a name="support-for-distributed-transactions"></a>Unterstützung für verteilte Transaktionen

SQL Server 2017 unterstützt verteilte Transaktionen für Datenbanken in Verfügbarkeitsgruppen. Diese Unterstützung schließt Datenbanken, die sich auf derselben Instanz von SQL Server befinden, genauso ein wie Datenbanken, die sich auf verschiedenen Instanzen von SQL Server befinden. Verteilte Transaktionen werden für Datenbanken unterstützt, die für die Datenbankspiegelung konfiguriert sind.

>[!NOTE]
>[!INCLUDE [SQL Server 2016]](../../../includes/sssql15-md.md)] SQL Server 2016 bot eine eingeschränkte Unterstützung für verteilte Transaktionen für Datenbanken in einer Verfügbarkeitsgruppe. Verteilte Transaktionen, die Datenbanken in einer Verfügbarkeitsgruppe verwenden, wurden nur dann unterstützt, wenn sich keine andere Datenbank in der Transaktion auf derselben Instanz von SQL Server befand. Weitere Informationen finden Sie unter [SQL Server 2016 DTC Support In Availability Groups (SQL Server 2016 DTC-Unterstützung in Verfügbarkeitsgruppen)](http://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-gr)

Weitere Informationen zum Konfigurieren einer Verfügbarkeitsgruppe für verteilte Transaktionen finden Sie unter [Configure Availability Group for Distributed Transactions (Konfigurieren einer Verfügbarkeitsgruppe für verteilte Transaktionen)](configure-availability-group-for-distributed-transactions.md).

Weitere Informationen finden Sie unter:

- [DTC Administration Guide (DTC-Administratorhandbuch)](http://msdn.microsoft.com/library/ms681291.aspx)
- [DTC Developers Guide (DTC-Entwicklerhandbuch)](http://msdn.microsoft.com/library/ms679938.aspx)
- [DTC Programmers Reference (DTC-Referenz für Programmierer)](http://msdn.microsoft.com/library/ms686108.aspx)

## <a name="sql-server-2016-and-before-support-for-cross-database-transactions-within-the-same-sql-server-instance"></a>SQL Server 2016 und früher: Unterstützung für datenbankübergreifende Transaktionen innerhalb derselben SQL Server-Instanz  

In SQL Server 2016 und früher werden datenbankübergreifende Transaktionen innerhalb derselben SQL Server-Instanz für Verfügbarkeitsgruppen nicht unterstützt. Das heißt, dass keine zwei Datenbanken, die an einer datenbankübergreifenden Transaktion beteiligt sind, von derselben SQL Server-Instanz gehostet werden dürfen. Dies gilt auch, wenn diese Datenbanken Teil der gleichen Verfügbarkeitsgruppe sind.  
  
Datenbankübergreifende Transaktionen werden für die Datenbankspiegelung ebenfalls nicht unterstützt.  
  
##  <a name="dtcsupport"></a> SQL Server 2016: Unterstützung für verteilte Transaktionen  
Verteilte Transaktionen werden mit den Verfügbarkeitsgruppen unterstützt. Dies gilt für verteilte Transaktionen zwischen Datenbanken, die von zwei verschiedene Instanzen von SQL Server gehostet werden. Dies gilt auch für verteilte Transaktionen zwischen SQL Server und einem anderen DTC-konformen Server.  
 
Microsoft Distributed Transaction Coordinator (MSDTC oder DTC) ist ein Windows-Dienst, der eine Transaktionsinfrastruktur für verteilte Systeme bereitstellt. Mit MSDTC können Clientanwendungen mehrere Datenquellen in eine Transaktion aufnehmen. Für diese Transaktion wird dann auf allen Servern, die Teil der Transaktion sind, ein Commit ausgeführt. Sie können MSDTC beispielsweise dazu nutzen, um Transaktionen zu koordinieren, die mehrere Datenbanken auf verschiedenen Servern umfassen.

Mit der neuen Funktion von SQL Server 2016 können Sie verteilte Transaktionen selbst dann verwenden, wenn mindestens eine Datenbank in der Transaktion Teil zu einer Verfügbarkeitsgruppe gehören. Vor SQL Server 2016 wurden verteilte Transaktionen für Datenbanken in Verfügbarkeitsgruppen nicht unterstützt. In SQL Server 2016 können Sie einen Ressourcen-Manager pro Datenbank registrieren. Dank dieser neuen Funktion können verteilte Transaktionen jetzt auch Datenbanken in Verfügbarkeitsgruppen berücksichtigen.
  
 Die folgenden Anforderungen müssen erfüllt sein:  
  
-   Verfügbarkeitsgruppen müssen auf Windows Server 2016 oder Windows Server 2012 R2 ausgeführt werden. Für Windows Server 2012 R2 müssen Sie die Aktualisierung in KB3090973 installieren, die unter [https://support.microsoft.com/en-us/kb/3090973](https://support.microsoft.com/en-us/kb/3090973)verfügbar ist.  
  
-   Verfügbarkeitsgruppen müssen mit dem Befehl **CREATE AVAILABILITY GROUP** und der Klausel **WITH DTC\_SUPPORT = PER_DB** erstellt werden. Zurzeit können Sie eine vorhandene Verfügbarkeitsgruppe nicht ändern.  

- Alle SQL Server-Instanzen, die in die Verfügbarkeitsgruppe einbezogen werden, müssen SQL Server 2016 oder höher entsprechen.
 
 ## <a name="non-support-for-distributed-transactions"></a>Keine Unterstützung für verteilte Transaktionen
 Besondere Fälle, in denen verteilte Transaktionen nicht unterstützt werden:
 
 - Wenn sich in SQL Server 2016 und früher mehr als eine Datenbank in der gleichen Verfügbarkeitsgruppe befindet, die an der Transaktion beteiligt ist.
 
 - Wenn sich in SQL Server 2016 und früher mindestens eine Datenbank in einer Verfügbarkeitsgruppe befindet und sich eine andere Datenbank auf der gleichen SQL Server-Instanz befindet. 
 
 - Wenn die Verfügbarkeitsgruppe nicht mit der Aktivierung von verteilten Transaktionen erstellt wurde.
 
 - Datenbankspiegelung
 
 > [!IMPORTANT]
 > Bestimmen Sie die geeigneten Standardergebnisse von Transaktionen, die für Ihre Umgebung von DTC nicht aufgelöst werden können.  Informationen zum Konfigurieren des Standardergebnisses finden Sie unter [Lösung für unklare Transaktion (Serverkonfigurationsoption)](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md).
  
## <a name="example-scenario-with-database-mirroring"></a>Beispielszenario mit Datenbankspiegelung  
 Im folgenden Beispiel zur Datenbankspiegelung wird verdeutlicht, wie eine logische Inkonsistenz auftreten kann. In diesem Beispiel fügt eine Anwendung über eine datenbankübergreifende Transaktion zwei Datenzeilen ein: Eine Zeile wird in eine Tabelle in einer gespiegelten Datenbank (A) eingefügt, und die andere Zeile wird in eine Tabelle in einer anderen Datenbank (B) eingefügt. Datenbank A wird im Modus für hohe Sicherheit mit automatischem Failover gespiegelt. Während des Commits der Transaktion fällt Datenbank A aus. Die Spiegelungssitzung führt automatisch ein Failover zum Spiegel von Datenbank A aus.  
  
 Nach dem Failover kann ein Commit der datenbankübergreifenden Transaktion möglicherweise erfolgreich für Datenbank B ausgeführt werden, jedoch nicht für die Datenbank, für die der Failover ausgeführt wurde. Dies wäre möglich, wenn der ursprüngliche Prinzipalserver für Datenbank A nicht das Protokoll für die datenbankübergreifende Transaktion vor dem Ausfall an den Spiegelserver gesendet hätte. Nach dem Failover wäre diese Transaktion auf dem neuen Prinzipalserver nicht vorhanden. Datenbanken A und B würden inkonsistent werden, da die in Datenbank B eingefügten Daten erhalten bleiben, während die in Datenbank A eingefügten Daten verloren gingen.  
  
 Ein vergleichbares Szenario kann bei einer MS DTC-Transaktion auftreten. Angenommen, der neue Prinzipal setzt sich nach dem Failover mit MS DTC in Verbindung. Der neue Prinzipalserver ist MS DTC jedoch nicht bekannt, deshalb beendet er alle Transaktionen, für die "ein Commit vorbereitet wird", für die in anderen Datenbanken jedoch bereits anscheinend ein Commit ausgeführt wurde.  
  
> [!NOTE]  
>  Die Verwendung der Datenbankspiegelung mit DTC oder die Verwendung von Verfügbarkeitsgruppen mit DTC auf nicht in diesem Thema genehmigte Weise wird nicht unterstützt.  Dies bedeutet nicht, dass Aspekte des Produkts, die nicht mit DTC in Zusammenhang stehen, nicht unterstützt werden; Probleme die aus der unsachgemäßen Verwendung von verteilten Transaktionen herrühren, werden jedoch nicht unterstützt.  
  
## <a name="next-steps"></a>Nächste Schritte  
 [Always On availability groups: Interoperability &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  
