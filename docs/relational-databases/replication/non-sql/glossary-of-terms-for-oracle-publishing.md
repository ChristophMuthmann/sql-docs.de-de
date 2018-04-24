---
title: Begriffe im Zusammenhang mit dem Veröffentlichen von Oracle-Daten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], glossary
ms.assetid: e21dfa4b-6144-4be7-9cbf-ca2709b2bd9f
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae58af18dc730467534d98db3360a7bb24f07db2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="glossary-of-terms-for-oracle-publishing"></a>Begriffe im Zusammenhang mit dem Veröffentlichen von Oracle-Daten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Beim Konfigurieren und Verwalten der Veröffentlichung von Oracle-Daten sollten Sie mit den im Folgenden genannten Oracle-Begriffen vertraut sein. Eine vollständige Liste der Oracle-Begriffe finden Sie in der Oracle-Onlinedokumentation.  
  
 Indexorganisierte Tabelle (Index Organized Table, IOT)  
 Tabelle, deren Daten auf dem Datenträger physisch in der Indexreihenfolge sortiert sind. Entspricht damit einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Tabelle mit einem gruppierten Index. IOTs werden als Tabellen mit gruppiertem Index auf die Abonnenten repliziert.  
  
 Instanz  
 Einer Oracle-Datenbank wird eine Instanz zugeordnet. Die Instanz umfasst die Speicher- und Hintergrundprozesse, die die Datenbank unterstützen. Oracle-Instanzen sind immer mit einer einzelnen Datenbank verknüpft, während [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzen viele Datenbanken enthalten können. Unter bestimmten Umständen können aber auch Oracle-Datenbanken mehrere Instanzen besitzen.  
  
 Oracle Listener  
 Wickelt den eingehenden Netzwerkverkehr für eine Oracle-Datenbankinstanz ab. Beim Konfigurieren der Netzwerkkonnektivität mit einer Oracle-Datenbank geben Sie das Protokoll, über das der Verkehr gesendet wird, und den Anschluss an, auf dem der Listener auf Verkehr lauscht. Der Listener wird in der Regel so konfiguriert, dass er auf demselben Computer wie die Oracle-Datenbankinstanz ausgeführt wird, und er kann so konfiguriert werden, dass er eine oder mehrere Instanz(en) bedient.  
  
 ROWID  
 Zeiger auf die Position einer bestimmten Zeile in einer Datenbank. Da das Abrufen von Zeilen mit der ROWID schneller geht als mit einem Table Scan oder Index, verwendet die Replikation bei der Verarbeitung veröffentlichter Tabellenänderungen vorübergehend die ROWID.  
  
 Sequenz  
 Datenbankobjekt, das zum Generieren eindeutiger Nummern verwendet wird. Die Replikation verwendet Sequenzen zur Anordnung von Änderungen, die an veröffentlichten Tabellen vorgenommen wurden.  
  
 SQL\*Plus  
 Anwendung, die zum Zugreifen auf und Abfragen von Oracle-Datenbanken verwendet wird. Sie ähnelt damit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sqlcmd**.  
  
 Synonym  
 Alias für ein Objekt. Das spezielle öffentliche Synonym **MSSQLSERVERDISTRIBUTOR** wird automatisch erstellt, wenn ein Oracle-Verleger konfiguriert wird. Das Synonym verweist auf die **HREPL_Distributor** -Tabelle und stellt einen logischen Zeiger auf den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler bereit, der den Verleger bedient.  
  
 Nach dem Veröffentlichen einer Oracle-Datenbank schlagen alle weiteren Versuche fehl, diesen Verleger mit einem anderen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verleger zu konfigurieren, weil das öffentliche Synonym diesen speziellen Verteiler als bereits für den Dienst am Verleger konfigurierten Verteiler identifiziert.  
  
 Tabellenbereich  
 Einheit des Datenbankspeichers, die in etwa einer Dateigruppe in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]entspricht.  
  
 TNS-Dienstname  
 TNS (Transparent Network Substrate) ist eine von Oracle-Datenbanken verwendete Kommunikationsschicht. Der TNS-Dienstname ist der Name, unter dem eine Oracle-Datenbankinstanz im jeweiligen Netzwerk geführt wird. Den TNS-Dienstnamen können Sie beim Konfigurieren der Konnektivität mit der Oracle-Datenbank zuweisen. Die Replikation verwendet den TNS-Dienstnamen zum Identifizieren des Verlegers und zum Einrichten der Verbindungen.  
  
 Benutzerschema  
 Ein Benutzerschema kann man sich wie einen Datenbankbenutzer vorstellen, der einen eigenen Satz Datenbankobjekte besitzt. Das administrative Benutzerschema der Replikation besitzt mit Ausnahme des öffentlichen Synonyms [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] MSSQLSERVERDISTRIBUTOR **alle Objekte, die vom** -Replikationsprozess in der Oracle-Datenbank erstellt wurden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Auf dem Oracle-Verleger erstellte Objekte](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)   
 [Nicht-SQL Server-Verleger](../../../relational-databases/replication/non-sql/non-sql-server-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
