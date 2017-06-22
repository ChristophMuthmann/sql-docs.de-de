---
title: Funktionen und Tasks im SQL Server-Hilfsprogramm | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server utility [SQL Server]
- utility control point
- Utility growth rate
- Multiserver management
- UCP
- Multi-server management [SQL Server]
ms.assetid: 6e6cbd25-6b1c-4e21-9ade-4584e243fd8f
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8176e89f8acfd39b8075dde8d470189d14dfe843
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-utility-features-and-tasks"></a>Funktionen und Tasks im SQL Server-Hilfsprogramm
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kunden möchten ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Umgebung als Ganzes verwalten. Diese Anforderung wird in dieser Version mithilfe des Konzepts der Anwendungs- und Multiserververwaltung im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm erfüllt.  
  
## <a name="benefits-of-the-sql-server-utility"></a>Vorteile des SQL Server-Hilfsprogramms  
 Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm modelliert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-bezogene Entitäten eines Unternehmens in einer einheitlichen Ansicht. Die Blickpunkte des Hilfsprogramm-Explorers und des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) vermitteln Administratoren über eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die als Steuerungspunkt für das Hilfsprogramm (UCP) dient, eine ganzheitliche Sicht auf die Ressourcenintegrität in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Die Kombination aus Zusammenfassungsdaten und detaillierten Daten, die im UCP für Richtlinien sowohl für die Unter- als auch für die Überauslastung und für eine Vielzahl von Schlüsselparametern angezeigt werden, eröffnen neue Möglichkeiten der Ressourcenkonsolidierung und erleichtern die Erkennung von Ressourcen, die überausgelastet sind. Integritätsrichtlinien sind konfigurierbar und können angepasst werden, indem der obere oder untere Grenzwert für die Ressourcennutzung geändert wird. Sie können globale Überwachungsrichtlinien ändern oder einzelne Überwachungsrichtlinien für jede Entität konfigurieren, die im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verwaltet wird.  
  
##  <a name="typical_scenarios"></a> Erste Schritte mit dem SQL Server-Hilfsprogramm  
 Am Anfang eines typischen Benutzerszenarios steht die Erstellung eines Steuerungspunkts für das Hilfsprogramm, der den zentralen Ansatzpunkt für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm darstellt. Der UCP stellt eine konsolidierte Sicht der Ressourcenintegrität bereit, die von verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm gesammelt wurde. Registrieren Sie nach der Erstellung des UCP Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm, damit sie vom UCP verwaltet werden können.  
  
 Jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz und Datenebenenanwendung, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verwaltet wird, kann auf der Grundlage globaler oder individueller Richtliniendefinitionen überwacht werden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Erste Schritte mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm mithilfe der folgenden Themen:  
  
|||  
|-|-|  
|**Beschreibung**|**Thema**|  
|Beschreibt Überlegungen zum Konfigurieren eines Servers, um Sammlungssätze, die zum Hilfsprogramm und die nicht zum Hilfsprogramm gehören, auf der gleichen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]auszuführen.|[Überlegungen zum Ausführen von Hilfsprogramm- und Nicht-Hilfsprogramm-Sammlungssätzen auf derselben Instanz von SQL Server](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)|  
|Beschreibt, wie ein SQL Server-Steuerungspunkt für das Hilfsprogramm erstellt wird.|[Erstellen eines Steuerungspunkts für das SQL Server-Hilfsprogramm &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)|  
|Beschreibt, wie eine Verbindung mit einem SQL Server-Hilfsprogramm hergestellt wird.|[Verbinden mit einem SQL Server-Hilfsprogramm](../../relational-databases/manage/connect-to-a-sql-server-utility.md)|  
|Beschreibt, wie eine Instanz von SQL Server mit einem Steuerungspunkt für das Hilfsprogramm registriert wird.|[Registrieren einer Instanz von SQL Server &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)|  
|Beschreibt, wie der Hilfsprogramm-Explorer zum Verwalten des SQL Server-Hilfsprogramms verwendet wird.|[Verwenden des Hilfsprogramm-Explorers zum Verwalten des SQL Server-Hilfsprogramms](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)|  
|Beschreibt, wie Instanzen von SQL Server im SQL Server-Hilfsprogramm überwacht werden.|[Überwachen von SQL Server-Instanzen im SQL Server-Hilfsprogramm](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)|  
|Beschreibt, wie Ergebnisse zu Ressourcenintegritätsrichtlinien angezeigt werden.|[Anzeigen der Ergebnisse zu Ressourcenintegritätsrichtlinien &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)|  
|Beschreibt, wie Definitionen von Ressourcenintegritätsrichtlinien geändert werden.|[Ändern der Definition von Ressourcenintegritätsrichtlinien &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)|  
|Beschreibt, wie das UCP-Data Warehouse konfiguriert wird.|[Konfigurieren des Data Warehouse für den Steuerungspunkt für das Hilfsprogramm &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)|  
|Beschreibt, wie Integritätsrichtlinien für das Hilfsprogramm konfiguriert werden.|[Konfigurieren von Integritätsrichtlinien &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)|  
|Beschreibt, wie die Abschwächung in CPU-Auslastungsrichtlinien angepasst wird.|[Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)|  
|Beschreibt, wie eine Instanz von SQL Server aus einem UCP entfernt wird.|[Entfernen einer Instanz von SQL Server aus dem SQL Server-Hilfsprogramm](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)|  
|Beschreibt, wie das Proxykonto für den Hilfsprogramm-Datensammler auf einer verwalteten Instanz von SQL Server geändert wird.|[Ändern des Proxykontos für den Hilfsprogramm-Sammlungssatz auf einer verwalteten Instanz von SQL Server &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/change-proxy-account-for-utility-collection-on-managed-sql-server.md)|  
|Beschreibt, wie UCPs von einer SQL Server-Instanz in eine andere verschoben werden.|[Verschieben eines UCPs von einer SQL Server-Instanz in eine andere &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility.md)|  
|Beschreibt, wie ein UCP entfernt wird.|[Entfernen eines Steuerungspunkts für das Hilfsprogramm &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/remove-a-utility-control-point-sql-server-utility.md)|  
|Beschreibt, wie Fehler des SQL Server-Hilfsprogramms behoben werden.|[Problembehandlung beim SQL Server-Hilfsprogramm](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)|  
|Beschreibt, wie Fehler der SQL Server-Ressourcenintegrität behoben werden.|[Fehlerbehebung für die SQL Server-Ressourcenintegrität &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)|  
|Stellt Links zu UtilityExplorer-F1-Hilfethemen bereit.|[Hilfsprogramm-Explorer (F1-Hilfe)](../../relational-databases/manage/utility-explorer-f1-help.md)|  
  
  
