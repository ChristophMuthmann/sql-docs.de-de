---
title: DQS-Verwaltung| Microsoft-Dokumentation
ms.custom: 
ms.date: 10/01/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dab2f79fbd66389684bafcac726bcfe363f50f8e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="dqs-administration"></a>DQS-Administration
  Mit[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) können Sie verschiedene auf [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]ausgeführte DQS-Aktivitäten verwalten, auf DQS-bezogene Eigenschaften auf Serverebene, die Reference Data Service-Einstellungen und DQS-Protokolleinstellungen konfigurieren. Dies ist durch die Funktion Verwaltung **** in möglich [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. In Abhängigkeit von Ihrem Sicherheitszugriff (Rolle) in DQS wird Ihnen der Zugriff auf bestimmte Funktionen in diesem Bereich gewährt bzw. verweigert.  
  
 Abgesehen von diesen Verwaltungsaktivitäten enthält dieses Thema auch Informationen über eine Verwaltungsaktivität, Sichern und Wiederherstellen von DQS-Datenbanken, die nicht mithilfe von [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]ausgeführt wird.  
  
 Die Verwaltungsfunktion in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] bietet die folgenden Vorteile:  
  
-   Aktiviert Data Stewards, um verschiedene DQS-Aktivitäten auf einem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] von einem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]zu überwachen.  
  
-   Ermöglicht es DQS-Administratoren, die DQS-Aktivitäten auf einem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] von einem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]zu überwachen, und *beendet* eine ausgeführte Aktivität oder *beendet* einen laufenden Prozess innerhalb einer Aktivität nach Bedarf.  
  
-   Konfigurieren Sie die Einstellungen für Verweisdatendienste, beispielsweise das Einrichten der Konnektivität mit Windows Azure Marketplace und die direkte Verwaltung von Anbietern für Drittanbieter-Verweisdatendienste.  
  
-   Konfigurieren Sie Schwellenwerte für die Bereinigungs- und Abgleichsaktivitäten.  
  
-   Aktivieren bzw. deaktivieren Sie Benachrichtigungen in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
-   Konfigurieren Sie die Protokollierung auf Grundlage des Schweregrads der Ereignisse.  
  
##  <a name="AdminUsingClent"></a> Verwalten von Aktivitäten mithilfe des Data Quality-Clients  
 Diese Aktivitäten werden mit der Funktion Verwaltung **** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]ausgeführt.  
  
### <a name="activity-monitoring"></a>Aktivitätsüberwachung  
 Auf dem Bildschirm **Aktivitätsüberwachung** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] werden Informationen zu jeder Aktivität angezeigt, die auf einem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]ausgeführt werden. Dieser Bildschirm wird vom Data Steward hauptsächlich verwendet, um alle auf dem verbundenen [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , mit dem die [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Anwendung verbunden ist, ausgeführten Aktivitäten auf hoher Ebene zu überwachen. Über diesen Bildschirm kann keine Überwachung auf Systemebene durchgeführt werden. Zudem können DQS-Administratoren mit diesem Bildschirm bei Bedarf eine Aktivität oder einen Prozess innerhalb einer Aktivität durch Beenden einer ausgeführten Aktivität oder Anhalten eines laufenden Prozesses innerhalb einer Aktivität steuern. Die Daten werden für die Wissensermittlung, die Domänenverwaltung, die Abgleichsrichtlinie, die Bereinigung, den Abgleich und für die SSIS-basierte Bereinigung (SQL Server Integration Services) angezeigt.  
  
### <a name="configuration"></a>Konfiguration  
 Der Bildschirm **Konfiguration** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ermöglicht dem DQS-Administrator Folgendes:  
  
-   **Verweisdaten**: Konfigurieren Sie Verweisdaten-Dienstanbieter: Windows Azure Marketplace oder direkter Verweisdaten-Dienstanbieter. Nachdem Sie die Verweisdaten-Dienstanbieter eingerichtet haben, können Sie während einer Domänenverwaltungsaktivität in einer Wissensdatenbank den Verweisdaten eine Domäne bzw. Verbunddomäne zuordnen und anschließend die gleiche Wissensdatenbank für die Bereinigungsaktivität in einem Data Quality-Projekt verwenden. Damit können Sie auch die Proxyeinstellungen für die Verbindung mit dem Internet angeben, um Windows Azure Marketplace zu verwenden.  
  
-   **Allgemeine Einstellungen**: Geben Sie die Schwellenwerte für die Datenbereinigung und den Datenabgleich an und ob Sie Benachrichtigungen für die Profilerstellung in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]aktivieren möchten. Diese Schwellenwerte werden von DQS bei der computergestützten Bereinigung und bei Abgleichsaktivitäten in einem Data Quality-Projekt verwendet.  
  
-   **Protokolleinstellungen**: Die Protokolldateien in DQS zeichnen die in DQS ausgeführten Aktivitäten auf und eignen sich zum Nachverfolgen funktionaler Probleme während der Wartung und Problembehebung. Sie können die Meldungen filtern, die für verschiedene DQS-Funktionen (Domänenverwaltung, Wissensermittlung, Bereinigung, Abgleich und Verweisdatendienste) und DQS-Module auf Grundlage des Schweregrads der Ereignisse protokolliert werden sollen.  
  
> [!NOTE]  
>  Der Bildschirm **Konfiguration** ist nur für Benutzer verfügbar, die die "dqs_administrator"-Rolle in der Datenbank "DQS_MAIN" aufweisen.  
  
##  <a name="AdminOutsideClient"></a> Verwaltungsaktivitäten außerhalb des Data Quality-Clients  
 Folgende Aktivitäten werden außerhalb des Data Quality-Clients ausgeführt:  
  
-   **Sichern und Wiederherstellen von DQS-Datenbanken**: Das Sichern und Wiederherstellen von DQS-Datenbanken entspricht dem Sichern und Wiederherstellen von SQL Server-Datenbanken, wobei einige Aspekte jedoch spezifisch für DQS sind.  
  
-   **Trennen und Anfügen von DQS-Datenbanken**: Die Schritte zum Trennen und Anfügen von DQS-Datenbanken entsprechen dem Trennen und Anfügen von SQL Server-Datenbanken, wobei einige Aspekte jedoch spezifisch für DQS sind.  
  
 Weitere Informationen finden Sie unter [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt das Überwachen von Aktivitäten in DQS.|[Überwachen der DQS-Aktivitäten](../data-quality-services/monitor-dqs-activities.md)|  
|Beschreibt, wie Einstellungen für Verweisdaten in DQS konfiguriert werden.|[Konfigurieren von DQS zum Verwenden von Verweisdaten](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Beschreibt das Konfigurieren von Schwellenwerten für Bereinigungs- und Abgleichsaktivitäten.|[Konfigurieren der Schwellenwerte für Bereinigung und Abgleich](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|Beschreibt, wie Benachrichtigungen in DQS aktiviert und deaktiviert werden.|[Aktivieren oder Deaktivieren von Profilerstellungsbenachrichtigungen in DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|Beschreibt das Konfigurieren der DQS-Protokollierung auf Grundlage des Schweregrads der Ereignisse.|[Konfigurieren von Schweregraden für DQS-Protokolldateien](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|Beschreibt das Konfigurieren erweiterter Einstellungen für die DQS-Protokollierung.|[Konfigurieren der erweiterten Einstellungen für DQS-Protokolldateien](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|Beschreibt das Sichern und Wiederherstellen von DQS-Datenbanken.|[Sichern und Wiederherstellen von DQS-Datenbanken](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|Beschreibt das Trennen und Anfügen von DQS-Datenbanken.|[Trennen und Anfügen von DQS-Datenbanken](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Reference Data Services in DQS](../data-quality-services/reference-data-services-in-dqs.md)   
 [Verwalten von DQS-Protokolldateien](../data-quality-services/manage-dqs-log-files.md)   
 [Verwalten von DQS-Datenbanken](../data-quality-services/manage-dqs-databases.md)  
  
  
