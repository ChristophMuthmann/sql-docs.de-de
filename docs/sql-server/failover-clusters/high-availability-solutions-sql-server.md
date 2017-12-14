---
title: "Hochverfügbarkeitslösungen (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/19/2016
ms.prod: failover-clusters
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
caps.latest.revision: "84"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 2e3eacea1174a805abe0cce4474634f091ecd6ab
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="high-availability-solutions-sql-server"></a>Lösungen mit hoher Verfügbarkeit (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema werden mehrere Hochverfügbarkeitslösungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorgestellt, die die Verfügbarkeit von Servern oder Datenbanken verbessern. Eine Lösung mit hoher Verfügbarkeit unterdrückt die Auswirkungen eines Hardware- oder Softwarefehlers und hält die Verfügbarkeit von Anwendungen aufrecht, damit die Ausfallzeiten für Benutzer so gering wie möglich gehalten werden.    
    
   
>  **Hinweis!** Möchten Sie wissen, welche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Editionen eine bestimmte Hochverfügbarkeitslösung unterstützen? Informationen dazu finden Sie im Artikel [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)im Abschnitt „Hohe Verfügbarkeit (Always On)“.    
     
    
##  <a name="TermsAndDefinitions"></a> Übersicht über SQL Server-Hochverfügbarkeitslösungen    
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind mehrere Optionen zum Einrichten von Hochverfügbarkeit für einen Server oder eine Datenbank verfügbar. Die Hochverfügbarkeitsoptionen umfassen Folgendes:    
    
*  Always On-Failoverclusterinstanzen    
 Als Teil des Always On-Angebots von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nutzen Always On-Failoverclusterinstanzen die Funktionalität des Windows Server-Failoverclustering (WSFC), um durch Redundanz auf Serverinstanzebene (eine *Failoverclusterinstanz* [FCI]) lokale Hochverfügbarkeit zu bieten. Eine FCI ist eine einzelne Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Diese ist auf Windows Server-Failoverclustering-Knoten (WSFC) und möglicherweise auf mehreren Subnetzen installiert. In einem Netzwerk wird eine FCI als eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angezeigt, die auf einem einzelnen Computer ausgeführt wird. Die FCI bietet jedoch die Möglichkeit zur Failoverbereitstellung von einem WSFC-Knoten zu einem anderen, wenn der aktuelle Knoten nicht verfügbar ist.    
    
 Weitere Informationen finden Sie unter [Always On-Failoverclusterinstanzen &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)hostet.    
    
*  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]    
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ist eine Hochverfügbarkeits- und Notfallwiederherstellungslösung auf Unternehmensebene, die in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] eingeführt wurde und die Maximierung der Verfügbarkeit für mindestens eine Benutzerdatenbank ermöglicht. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] erfordert, dass sich die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen auf Windows Server-Failoverclusteringknoten (WSFC) befinden. Weitere Informationen finden Sie unter [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).    
    
  
>  **Hinweis!** Eine FCI kann [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] nutzen, um die Remotewiederherstellung im Notfall auf Datenbankebene bereitzustellen. Weitere Informationen finden Sie unter [Failoverclustering und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).    
    
*  Datenbankspiegelung **Hinweis!** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Stattdessen wird die Verwendung von [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] empfohlen.     
Die Datenbankspiegelung stellt eine Softwarelösung dar, mit der die Verfügbarkeit einer Datenbank erhöht wird, indem ein fast sofortiges Failover unterstützt wird. Mit der Datenbankspiegelung kann eine einzelne Datenbank, die sich im Standbymodus befindet, eine so genannte *Spiegeldatenbank*, für eine entsprechende Produktionsdatenbank, eine so genannte *Prinzipaldatenbank*, verwaltet werden. Weitere Informationen finden Sie unter [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).    
    
*  Protokollversand    
 Wie die [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] - und Datenbankspiegelung arbeitet auch der Protokollversand auf Datenbankebene. Sie können den Protokollversand verwenden, um eine oder mehrere Datenbanken im betriebsbereiten Standbymodus (*sekundäre Datenbanken*) für eine einzelne Produktionsdatenbank (*primäre Datenbank*) zu verwalten. Weitere Informationen zum Protokollversand finden Sie unter [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).    
    
##  <a name="RecommendedSolutions"></a> Empfohlene Lösungen zum Verwenden von SQL Server für das Schützen von Daten    
 Unsere Empfehlung zum Bereitstellen von Datenschutz für Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Umgebung:    
    
-   Für den Datenschutz über eine freigegebene Datenträgerlösung (ein SAN) eines Drittanbieters empfiehlt sich die Verwendung von Always On-Failoverclusterinstanzen.    
    
-   Für den Datenschutz über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sollten Sie [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]verwenden.    
    
       >  Wenn Sie eine Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen, die [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]nicht unterstützt, empfiehlt sich die Verwendung des Protokollversands. Informationen dazu, welche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Editionen [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]unterstützen, finden Sie im Artikel [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)im Abschnitt „Hohe Verfügbarkeit (Always On)“.    
    
## <a name="see-also"></a>Siehe auch    
 [Windows Server-Failoverclustering &#40;WSFC&#41; mit SQL Server](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)     
 [Datenbankspiegelung: Interoperabilität und Koexistenz &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)     
 [Als veraltet markierte Funktionen des Datenbankmoduls in SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)    
    
  

