---
title: Anwendung installieren und konfigurieren – Analytics Platform System | Microsoft Docs
description: Führt Analytics Platform System (APS) Appliance-Administratoren über die ersten Schritte zum Einrichten und erste Schritte mit Ihrer neuen Anwendung.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6aa75cdab85fce9ef308d3e853ddb0107c28ee
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Appliance-Installation und Konfiguration für Analytics Platform System
Führt Analytics Platform System (APS) Appliance-Administratoren über die ersten Schritte zum Einrichten und erste Schritte mit Ihrer neuen Anwendung.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. Installieren Sie die Hardware  
Ihre neue Anwendung wird auf Paletten Docks in Ihrem Rechenzentrum übermittelt werden.  
  
> [!IMPORTANT]  
> In einigen Fällen wird Ihre IHV entpacken, rack und schließen Sie die Einheit für die Sie in Ihrem Datencenter. Wenn also diese Anweisungen nicht erforderlich sind, und Sie können zu fortfahren die [3. Konfigurieren Sie die Appliance](#ConfigureAppliance) Abschnitt weiter unten.  
  
Wenn Ihre IHV nicht die Hardware-Installation ausgeführt werden, gehen Sie folgendermaßen vor, um die Hardware zu installieren.  
  
|||  
|-|-|  
|**Task**|**Beschreibung**|  
|Bestätigen Sie die Dokumentation|Vergewissern Sie sich, dass Sie alle erforderlichen Dokumente und Informationen von unabhängige Hardwarehersteller (IHVS) erhalten haben. Finden Sie unter [Informationen zum Abrufen von Ihrem IHV &#40;Analyseplattformsystem&#41;](information-to-obtain-from-your-ihv.md).|  
|Installieren von hardware|Stellen Sie sicher, dass das Rechenzentrum die Appliance aufnehmen kann. Verschieben Sie die Appliance-Komponenten im Rechenzentrum. Die Netzwerkswitches, Stomverteilereinheiten, Rack und Verkabelung. Finden Sie unter [Hardwareinstallation &#40;Analyseplattformsystem&#41;](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. Schalten Sie das Gerät  
  
|||  
|-|-|  
|**Task**|**Beschreibung**|  
|Schalten Sie das Gerät|Schalten Sie jede Einheit Komponentenknoten in der erforderlichen Reihenfolge, warten nach Bedarf, um sicherzustellen, dass keine Fehler auftreten.|  
  
## <a name="ConfigureAppliance"></a>3. Konfigurieren Sie die Anwendung  
  
|||  
|-|-|  
|**Task**|**Beschreibung**|  
|||  
|Konfigurieren Sie das Gerät mithilfe der SQL Server-PDW**Configuration Manager**|Verwenden Sie den Konfigurations-Manager, um Kennwörter Appliance, Zeitzonen, Netzwerk-und Firewalleinstellungen, Sicherheitszertifikate, und Leistung und andere Einstellungen auf Ihrer Anwendung festzulegen. Finden Sie unter [Anwendungskonfiguration &#40;Analyseplattformsystem&#41;](appliance-configuration.md).|  
  
> [!WARNING]  
> Änderungen an der Konfiguration sollte nur vorgenommen werden mithilfe der SQL Server-PDW**Configuration Manager**. Änderungen, die nicht durch verfügbar gemacht **Configuration Manager** werden nicht unterstützt. Die SQL Server PDW Appliance unterstützt z. B. nur die Spracheinstellung für US-Englisch.  
  
## <a name="SoftwareServicing"></a>4. Richten Sie die Wartung von Software  
  
|||  
|-|-|  
|**Task**|**Beschreibung**|  
|Anwenden von Updates für SQL Server PDW|(Optional) Sie müssen möglicherweise eine oder mehrere SQL Server PDW-Updates, um Ihre SQL Server PDW-Software auf die neueste Version aktualisieren anwenden. Finden Sie unter [gelten Analytics Platform System Hotfixes &#40;Analyseplattformsystem&#41;](apply-analytics-platform-system-hotfixes.md).|  
|Konfigurieren Sie Windows Server Update Services|Konfigurieren Sie das Gerät zum Empfangen von Updates von Windows Server Update Services für unterstützende Software. Finden Sie unter [herunter, und führen Sie Microsoft Updates &#40;Analyseplattformsystem&#41;](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Nächste Schritte  
Nachdem Sie alle vorherigen Schritte abgeschlossen haben, ist Ihre Einheit für die Verwendung bereit. Die folgenden Aufgaben können Sie oder andere Mitarbeiter an Ihrem Standort fortsetzen.  
  
|||  
|-|-|  
|**Task**|**Beschreibung**|  
|Installieren von SQL Server PDW-Treiber und Konnektivität konfigurieren|Konfigurieren Sie lokale Computer keine Verbindung mit SQL Server PDW mithilfe von SQL Server Data Tools, Sqlcmd, Business Intelligence-Software oder andere Tools. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Erstellen von Anmeldungen und Server-Rollen und Zuweisen von Berechtigungen|Planen und Erstellen von Anmeldungen und Server-Rollen, mit dem Benutzer mit den entsprechenden Berechtigungen in SQL Server PDW anmelden können. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Konfigurieren Sie das Azure Data Management Gateway|Das Gateway ermöglicht Azure Benutzern lokaler APS Datenzugriff von APS-Daten als OData Feeds secure verfügbar gemacht. Das Gateway ist bereits auf dem Knoten "Zugriffssteuerung" installiert. Bitten Sie Microsoft, um Unterstützung bei der Konfiguration.|  
|Monitor-Abfragen und Appliance-Benutzer|Verwenden Sie die Admin-Konsole und andere Ressourcen zum Überwachen der Abfragen und die Anwendung Benutzer aus. Finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Laden von Daten in SQL Server PDW|Laden Sie Daten in Ihrer Anwendung. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Erstellen eines Wiederherstellungsplans|Planen Sie, wie Sie schützt Ihre Daten vor Hardwarefehlern zu gewährleisten, oder Daten überschrieben. Erstellen eines Plans verwenden regelmäßige Sicherungen und Pläne im Falle von datenbeschädigung oder Datenverlust wiederherstellen. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Überwachen Sie die Anwendung|Überwachen Sie die Appliance Zustand, Integrität und Leistung mithilfe von Systemsichten, Protokolle und die Admin-Konsole an. Korrigieren oder Probleme melden. Finden Sie unter [Integritätsstatus des Monitors Appliance &#40;Analyseplattformsystem&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
