---
title: "Unterstützung für hohe Verfügbarkeit | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2e0f6d3f-0536-46d9-8630-835e199515bf
caps.latest.revision: "5"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9792f20dfcb55685d1ebc5a49a611f1262bc0fd6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="high-availability-support"></a>Unterstützung für hohe Verfügbarkeit
  Der CDC Service for Oracle ist für Hochverfügbarkeit ausgelegt. Die folgenden Funktionen stellen einen Teil der Unterstützung für Hochverfügbarkeit dar:  
  
-   Der CDC Service for Oracle verwendet keine Dateiressource (lokal oder auf andere Weise). Der gesamte Status wird in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz gespeichert. Dies erleichtert das Starten des Diensts auf einem anderen Computer, der dieselbe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verwendet, falls auf dem Computer ein Fehler auftritt, auf dem der Dienst ausgeführt wird. Um die Wiederherstellungszeit zu reduzieren, werden lange Oracle-Transaktionen oder Oracle-Transaktionen mit langer Laufzeit in einer Stagingtabelle auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ziel vorgehalten. So wird verhindert, dass nach einem Fehler (oder Neustart des Diensts) eine große Zahl von Oracle-Transaktionsprotokollen neu gescannt werden muss.  
  
-   Der CDC Service for Oracle kann gruppierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen verwenden, damit er nach dem Failover der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz auf einem anderen Clusterknoten wiederhergestellt werden kann. Der Administrator des Oracle CDC Service-Computers muss die Verbindungsinformationen für die gruppierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz nur beim Erstellen eines Oracle CDC Service angeben.  
  
-   Der CDC Service for Oracle kann die Funktion [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**Always On** zur Datenbankspiegelung verwenden. Zur Unterstützung ist es erforderlich, dass sich die MSXDBCDC-Datenbank und alle CDC-Datenbanken in derselben Verfügbarkeitsgruppe befinden. Außerdem ist erforderlich, dass der Administrator des Oracle CDC Service-Computers die richtigen **Always On** -Verbindungsinformationen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verfügbarkeitsgruppe angibt (z.B. die Verbindungseigenschaften `Failover_Partner and Network=dbmssocn`). Auf diese Weise kann der CDC-Dienst die Verarbeitung nach einem Failover automatisch auf einer sekundären Replikation der Datenbanken fortsetzen.  
  
-   Der CDC Service for Oracle kann als generische Dienstressource auf einem Windows-Failovercluster konfiguriert werden (in Verbindung mit oder separat von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), sodass ein Failover und das Zurückgreifen auf die CDC-Verarbeitung mit dem Cluster leicht möglich ist. Um den CDC Service for Oracle als Ressource in einem Failovercluster zu konfigurieren, muss der Systemadministrator den CDC Service for Oracle auf jedem Knoten im Failovercluster als generische Dienstressource festlegen.  
  
-   Der CDC Service for Oracle unterstützt Oracle RAC, womit die Kommunikation mit der Oracle-Datenbank und den Prozessprotokollen auch dann möglich ist, wenn einer der Oracle RAC-Knoten in Oracle ausgefallen ist.  
  
  
