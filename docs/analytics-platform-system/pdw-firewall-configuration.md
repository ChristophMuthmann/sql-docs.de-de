---
title: PDW-Firewall-Konfiguration (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 191f292d-16bc-4166-b855-158854ad062d
caps.latest.revision: "28"
ms.openlocfilehash: e74ffd88f0b2c10a6120c4411e4647c2fb84f249
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-firewall-configuration"></a>PDW-Firewall-Konfiguration
Die **Firewall** Seite von SQL Server PDW-Konfigurations-Manager können Sie aktivieren oder deaktivieren die Firewallregeln, zulassen oder verhindern den Zugriff auf bestimmte Ports auf dem Gerät Analytics Platform System.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Verwalten von Ports und firewall-Regeln für die Appliance-Knoten  
  
1.  Starten Sie den Konfigurations-Manager. Weitere Informationen finden Sie unter [starten Sie den Konfigurations-Manager &#40; Analyseplattformsystem &#41; ](launch-the-configuration-manager.md).  
  
2.  Erweitern Sie im linken Bereich der Configuration Manager- **Parallel Data Warehouse-Topologie**, und klicken Sie dann auf **Firewall**.  
  
3.  Suchen Sie den Port oder eine Firewall-Regel aktualisieren in der Liste, und klicken Sie dann zu aktivieren oder deaktivieren das Kontrollkästchen neben diesem Element. Nur SQL Server PDW Admin konfigurierbare Optionen werden in dieser Liste, einschließlich öffnen und Schließen von Ports auf extern angezeigte Knoten angezeigt.  
  
4.  Klicken Sie auf **übernehmen** zum Speichern der Änderungen.  
  
![DWConfig-Anwendung PDW-Firewall](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Externe Ports  
Die folgenden Ports werden für Clientverbindungen stammen von außerhalb von PDW geöffnet.  
  
|Zweck|Port #|Knoten|  
|-----------|-----------|---------|  
|SQL Client-Zugriff für PDW (TDS)|17001|CTL|  
|Ladeprogramm Clientzugriff (Dwloader & SSIS)|8001|CTL|  
|Remotedesktopzugriff|3389|CTL CMP|  
|SSIS-BinaryLoaderDataChannel|16551|CTL|  
|Dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL-verschlüsselte Verbindungen (für die interne Kommunikation, um die Verwaltungskonsole zugreifen und Zugriff auf HDInsight-Cluster-Dienste)|443|Alle Knoten|  
|SQL Server PDW laden Ablaufsteuerung - Windows-Anmeldeinformationen|8002|CTL|  
|_Kerberos|88|AD01 und AD02|  
|_ldap|389|AD01 und AD02|  
  
## <a name="internal-ports"></a>Interne Ports  
Die folgenden Ports werden von PDW für die interne Kommunikation verwendet, aber nicht für die von außerhalb der PDW-Anwendung ausgehenden Verbindungen geöffnet.  
  
|Zweck|Port #|Knoten|  
|-----------|-----------|---------|  
|DMS-Steuerungskanal-Datenverkehr|16450|CTL CMP|  
|DMS-Datenkanal-Datenverkehr|16550|CTL CMP|  
|Interne Diagnose|16650|CTL CMP|  
|Der failoverstatus (DMS)|15000|CTL CMP|  
|Der failoverstatus (Datenbankmodul)|15001|CMP|  
|Dynamische (temporären) Portbereich|20000-65535|CTL CMP|  
|SQL Server-Portbereiche (TDS)|1433, 1500-1508|CTL CMP|  
  
> [!NOTE]  
> Erstellen externen Tabellen oder Daten aus externen Quellen verwendet standardmäßig den TCP-Port 8020. Diese Anweisungen können stattdessen andere Ports konfiguriert werden. Der Standardport für Hortonworks JOB_TRACKER_LOCATION ist 50300. Integration in andere Systeme und die Tools möglicherweise zusätzliche Ports erforderlich.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
