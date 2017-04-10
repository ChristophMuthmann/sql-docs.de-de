---
title: "Datenbank&#252;bergreifende Transaktionen und verteilte Transaktionen f&#252;r Always On-Verf&#252;gbarkeitsgruppen und Datenbankspiegelung (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbankspiegelung [SQL Server], Interoperabilität"
  - "Datenbankübergreifende Transaktionen [SQL Server]"
  - "Transaktionen [Datenbankspiegelung]"
  - "Verfügbarkeitsgruppen [SQL Server], Interoperabilität"
  - "Problembehandlung [SQL Server], datenbankübergreifende Transaktionen"
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
caps.latest.revision: 33
ms.author: "mikeray"
manager: "jhubbard"
---
# Datenbank&#252;bergreifende Transaktionen und verteilte Transaktionen f&#252;r Always On-Verf&#252;gbarkeitsgruppen und Datenbankspiegelung (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

In diesem Thema wird die Unterstützung für datenbankübergreifende und verteilte Transaktionen für Always On-Verfügbarkeitsgruppen und die Datenbankspiegelung beschrieben.  
  
## Unterstützung für datenbankübergreifende Transaktionen innerhalb derselben SQL Server-Instanz  
Datenbankübergreifende Transaktionen innerhalb derselben SQL Server-Instanz werden für Always On-Verfügbarkeitsgruppen nicht unterstützt. Das heißt, dass keine zwei Datenbanken, die an einer datenbankübergreifenden Transaktion beteiligt sind, von derselben SQL Server-Instanz gehostet werden dürfen. Dies gilt auch, wenn diese Datenbanken Teil der gleichen Verfügbarkeitsgruppe sind.  
  
Datenbankübergreifende Transaktionen werden für die Datenbankspiegelung ebenfalls nicht unterstützt.  
  
##  <a name="dtcsupport"></a> Unterstützung für verteilte Transaktionen  
Verteilte Transaktionen werden mit den Always On-Verfügbarkeitsgruppen unterstützt. Dies gilt für verteilte Transaktionen zwischen Datenbanken, die von zwei verschiedene Instanzen von SQL Server gehostet werden. Dies gilt auch für verteilte Transaktionen zwischen SQL Server und einem anderen DTC-kompatiblen Server.  
 
Microsoft Distributed Transaction Coordinator (MSDTC oder DTC) ist ein Windows-Dienst, der eine Transaktionsinfrastruktur für verteilte Systeme bereitstellt. Mit MSDTC können Clientanwendungen mehrere Datenquellen in eine Transaktion aufnehmen. Für diese Transaktion wird dann auf allen Servern, die Teil der Transaktion sind, ein Commit ausgeführt. Sie können MSDTC beispielsweise dazu nutzen, um Transaktionen zu koordinieren, die mehrere Datenbanken auf verschiedenen Servern umfassen.

Mit der neuen Funktion von SQL Server 2016 können Sie verteilte Transaktionen selbst dann verwenden, wenn mindestens eine Datenbank in der Transaktion Teil zu einer Verfügbarkeitsgruppe gehören. Vor SQL Server 2016 wurden verteilte Transaktionen für Datenbanken in Verfügbarkeitsgruppen nicht unterstützt. In SQL Server 2016 können Sie einen Ressourcen-Manager pro Datenbank registrieren. Dank dieser neuen Funktion können verteilte Transaktionen jetzt auch Datenbanken in Verfügbarkeitsgruppen berücksichtigen.

  
 Die folgenden Anforderungen müssen erfüllt sein:  
  
-   Verfügbarkeitsgruppen müssen auf Windows Server 2016 oder Windows Server 2012 R2 ausgeführt werden. Für Windows Server 2012 R2 müssen Sie die Aktualisierung in KB3090973 installieren, die unter [https://support.microsoft.com/en-us/kb/3090973](https://support.microsoft.com/en-us/kb/3090973) verfügbar ist.  
  
-   Verfügbarkeitsgruppen müssen mit dem Befehl **CREATE AVAILABILITY GROUP** und der Klausel **WITH DTC_SUPPORT = PER_DB** erstellt werden. Zurzeit können Sie eine vorhandene Verfügbarkeitsgruppe nicht ändern.  

- Alle SQL Server-Instanzen, die in die Verfügbarkeitsgruppe einbezogen werden, müssen SQL Server 2016 oder höher entsprechen.
  
 
 ## Keine Unterstützung für verteilte Transaktionen
 Besondere Fälle, in denen verteilte Transaktionen nicht unterstützt werden:
 
 -  Wenn sich mehr als eine Datenbank in der gleichen Verfügbarkeitsgruppe befindet, die an der Transaktion beteiligt ist.
 
 -  Wenn sich mindestens eine Datenbank in einer Verfügbarkeitsgruppe befindet und sich eine andere Datenbank auf der gleichen SQL Server-Instanz befindet. 
 
 -  Wenn die Verfügbarkeitsgruppe nicht mit der Aktivierung von verteilten Transaktionen erstellt wurde.
 
 -  Datenbankspiegelung
 
 ## Empfehlung
 Sie sollten den DTC-Dienst in der Produktionsumgebung gruppieren. Wenn Sie den DTC-Dienst nicht gruppieren, verwendet SQL Server den lokalen DTC-Dienst. Der lokale DTC-Dienst vermindert jedoch die allgemeine Verfügbarkeit der Lösung. Wenn DTC gruppiert ist, können In-Process-Transaktionen wiederhergestellt werden, wenn auf dem Clusterknoten ein Fehler auftritt.
 
 > [!IMPORTANT]
 > Bestimmen Sie die geeigneten Standardergebnisse von Transaktionen, die für Ihre Umgebung von DTC nicht aufgelöst werden können.  Informationen zum Konfigurieren des Standardergebnisses finden Sie unter [Lösung für unklare Transaktion (Serverkonfigurationsoption)](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md).
  
## Beispielszenario mit Datenbankspiegelung  
 Im folgenden Beispiel zur Datenbankspiegelung wird verdeutlicht, wie eine logische Inkonsistenz auftreten kann. In diesem Beispiel fügt eine Anwendung über eine datenbankübergreifende Transaktion zwei Datenzeilen ein: Eine Zeile wird in eine Tabelle in einer gespiegelten Datenbank (A) eingefügt, und die andere Zeile wird in eine Tabelle in einer anderen Datenbank (B) eingefügt. Datenbank A wird im Modus für hohe Sicherheit mit automatischem Failover gespiegelt. Während des Commits der Transaktion fällt Datenbank A aus. Die Spiegelungssitzung führt automatisch ein Failover zum Spiegel von Datenbank A aus.  
  
 Nach dem Failover kann ein Commit der datenbankübergreifenden Transaktion möglicherweise erfolgreich für Datenbank B ausgeführt werden, jedoch nicht für die Datenbank, für die der Failover ausgeführt wurde. Dies wäre möglich, wenn der ursprüngliche Prinzipalserver für Datenbank A nicht das Protokoll für die datenbankübergreifende Transaktion vor dem Ausfall an den Spiegelserver gesendet hätte. Nach dem Failover wäre diese Transaktion auf dem neuen Prinzipalserver nicht vorhanden. Datenbanken A und B würden inkonsistent werden, da die in Datenbank B eingefügten Daten erhalten bleiben, während die in Datenbank A eingefügten Daten verloren gingen.  
  
 Ein vergleichbares Szenario kann bei einer MS DTC-Transaktion auftreten. Angenommen, der neue Prinzipal setzt sich nach dem Failover mit MS DTC in Verbindung. Der neue Prinzipalserver ist MS DTC jedoch nicht bekannt, deshalb beendet er alle Transaktionen, für die "ein Commit vorbereitet wird", für die in anderen Datenbanken jedoch bereits anscheinend ein Commit ausgeführt wurde.  
  
> [!NOTE]  
>  Die Verwendung der Datenbankspiegelung mit DTC oder die Verwendung von Always On-Verfügbarkeitsgruppen mit DTC auf eine nicht in diesem Thema genehmigte Weise wird nicht unterstützt.  Dies bedeutet nicht, dass Aspekte des Produkts, die nicht mit DTC in Zusammenhang stehen, nicht unterstützt werden; Probleme die aus der unsachgemäßen Verwendung von verteilten Transaktionen herrühren, werden jedoch nicht unterstützt.  
  
## Siehe auch  
 [Always On-Verfügbarkeitsgruppen: Interoperabilität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  