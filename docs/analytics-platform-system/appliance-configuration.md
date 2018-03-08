---
title: "Gerätekonfiguration (Analytics Platform System)"
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
ms.assetid: 064e7485-7026-4acf-8084-f5d30757d177
caps.latest.revision: "43"
ms.openlocfilehash: 05670f1727691b1abc0fd98dd5970c7697725b8e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="appliance-configuration"></a>Anwendungskonfiguration
Bietet Checklisten für die Aufgaben zum Konfigurieren von Analyseplattformsystem für Ihre Umgebung erforderlich. Diese Aufgaben sind erforderlich, bevor Sie das Gerät verwenden können.  
  
> [!WARNING]  
> Analyseplattformsystem mit**Configuration Manager** ist die beste Möglichkeit, und die einzige unterstützte Möglichkeit, zum Ausführen von Aufgaben im Tool verfügbar sind.  
  
## <a name="BeforeTasks"></a>Vorbereitungen  
  
### <a name="prerequisites"></a>Voraussetzungen  
  
1.  Das Gerät muss im Rechenzentrum installiert und mit Strom versorgt werden.  
  
2.  Stellen Sie sicher, dass Sie die folgende Informationen verfügen, das von Ihrem IHV bereitgestellt wird:  
  
    -   Externe IP-Adresse für den Knoten PDW (*PDW_region -*CTL01)  
  
    -   Appliance-Domänenname  
  
    -   Benutzername und Kennwort für den Domänenadministrator appliance  
  
3.  Ein vertrauenswürdiges Zertifikat zu erhalten. Sie importieren diese in einem späteren Schritt So ermöglichen Sie Clients für die Verbindung der **Admin Console** mit sicheren Verbindungen. Das Zertifikat mit dem Steuerungsknoten in einer kennwortgeschützten PFX-Datei gespeichert.  
  
4.  Starten Sie die **Configuration Manager**, verwenden die folgenden Schritte aus:  
  
    1.  Verwendung **Remotedesktop** für die Verbindung mit dem Steuerungsknoten PDW (*PDW_region*-CTL01). (Möglicherweise müssen für die CTL01 eine Verbindung mit der externen IP-Adresse.)  
  
    2.  Starten Sie die **Configuration Manager** aus der **starten** Menü des Knotens PDW-Steuerelement. Der erste Bildschirm der Configuration Manager zeigt die Anwendungstopologie, das von Ihrem IHV erstellt wurde. Es ist eine Liste der hardwareknoten, die von Ihrer SQL Server PDW-Software als Teil der Anwendung erkannt. Sie müssen keine Einstellungen auf dem Bildschirm Anwendungstopologie zu ändern.  
  
## <a name="CMTasks"></a>Ausführen von Aufgaben in Configuration Manager  
Die SQL Server-PDW**Configuration Manager** (PDWCM) ist eine Einheit-Verwaltungstool, Systemadministratoren für SQL Server PDW Appliance-Level-Vorgänge ausführen und die Appliance-Level-Einstellungen ändern. Verwenden Sie z. B. PDWCM Zurücksetzen von Kennwörtern, Festlegen der Zeitzone, IP-Adressen ändern, Konfigurieren von SSL-Zertifikaten, Remotezugriff über die Firewall, starten oder beenden das Gerät und sofortige Dateiinitialisierung festlegen.  
  
Verwendung **Configuration Manager** die folgenden Konfigurationsaufgaben ausführen.  
  
|Konfigurationstask|Description|  
|----------------------|---------------|  
|Kennenlernen der physische Komponentennamen|[PDW und physische Einheit Fabric-Komponenten &#40; Analyseplattformsystem &#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Starten Sie SQL Server PDW-Konfigurations-Manager|[Starten Sie den Konfigurations-Manager &#40; Analyseplattformsystem &#41;](launch-the-configuration-manager.md)|  
|Ändern Sie das Administratorkennwort der Domäne|Das Gerät hat eine private Windows Active Directory Domain Services, die zum Authentifizieren von Knoten innerhalb der Anwendung verwendet wird.<br /><br />Ihre IHV richten Sie das Gerät mit einem Standard-Domänenadministratorkennwort. Dies muss ein Kennwort geändert werden, die sicher ist.<br /><br />Die **Configuration Manager** ist die einzige unterstützte Methode, ändern Sie das Domänenkennwort für den Administrator.<br /><br />Weitere Informationen finden Sie unter [&#40; Kennwort zurücksetzen Analyseplattformsystem &#41; ](password-reset.md).|  
|Ändern Sie das Kennwort für die **sa** Anmeldung|SQL Server PDW ist eine System-Administrator-Anmeldung mit dem Namen **sa**. Die **sa** Anmeldung verfügt über alle Berechtigungen. Sie können eine GRANT-, Deny- oder jede beliebige Berechtigung widerrufen. Sie können auch alle Systemsichten finden Sie unter.<br /><br />Weitere Informationen finden Sie unter [&#40; Kennwort zurücksetzen Analyseplattformsystem &#41; ](password-reset.md).|  
|Festlegen der Zeitzone des Geräts|Legen Sie die Uhrzeit (lokal oder andere gewünschte) für alle Appliance-Knoten.<br /><br />Weitere Informationen finden Sie unter [Appliance Zeitzonenkonfiguration &#40; Analyseplattformsystem &#41; ](appliance-time-zone-configuration.md).|  
|Geben Sie für die SQL Server PDW Appliance extern angezeigte Netzwerkeinstellungen|[Appliance-Netzwerkkonfiguration &#40; Analyseplattformsystem &#41;](appliance-network-configuration.md)|  
|Importieren Sie ein Sicherheitszertifikat für die Admin-Konsole|Ein Zertifikat bieten Secure Sockets Layer (SSL)-Verbindungen über HTTPS an die [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41; ](monitor-the-appliance-by-using-the-admin-console.md). Wird standardmäßig die **Admin Console** enthält ein selbst signiertes Zertifikat, das Datenschutz, aber keine Serverauthentifizierung bereitstellt. Dieses Zertifikat gibt auch einen Fehler zurück, in Internet Explorer besagt: "Es besteht ein Problem mit dem Sicherheitszertifikat dieser Website" Wenn der Benutzer eine Verbindung herstellt. Obwohl diese Verbindung in-Flight Daten zwischen dem Client und dem Server verschlüsselt, ist die Verbindung immer noch durch Angriffe gefährdet.<br /><br />SQL Server PDW-Administratoren sollten sofort ein Zertifikat erwerben, ist mit einer vertrauenswürdigen Zertifizierungsstelle, die von Clients, um über eine sichere Verbindung verfügen, und entfernen den Fehler, den Internet Explorer meldet erkannt verkettet. Dies erfordert einen vollqualifizierten Domänennamen, der des Steuerelementknoten virtuelle IP-Adresse (empfohlen) zugeordnet ist, oder ein Zertifikatsname, die mit dem Wert übereinstimmt, den Benutzer in ihrer Browser-Adresse eingeben Balken, um die Verwaltungskonsole zugreifen.<br /><br />Verwenden der **Configuration Manager** hinzufügen oder Entfernen vertrauenswürdiger Zertifikate. Direkt mit dem Microsoft Windows HTTP-Dienste Zertifikat-Konfigurationstool (`winHttpCertCfg.exe`) zum Verwalten von Zertifikaten werden nicht unterstützt.<br /><br />Weitere Informationen finden Sie unter [PDW Zertifikatbereitstellung &#40; Analyseplattformsystem &#41; ](pdw-certificate-provisioning.md).|  
|Aktivieren oder Deaktivieren von Windows-Firewall-Regeln, die zulassen oder verhindern den Zugriff auf bestimmte Ports auf der SQL Server PDW Appliance.|Ihre IHV konfigurieren und aktivieren Sie die Firewallregeln, die für die Anwendung den ordnungsgemäßen Betrieb erforderlich sind. In den meisten Fällen werden Sie nicht aktivieren oder Deaktivieren von Firewallregeln.<br /><br />Weitere Informationen finden Sie unter [PDW-Firewall-Konfiguration &#40; Analyseplattformsystem &#41; ](pdw-firewall-configuration.md).|  
|Starten Sie und beenden Sie den SQL Server PDW-Anwendung|Beendet wird, oder die SQL Server PDW-Anwendung startet. Weitere Informationen finden Sie unter [PDW-Dienststatus &#40; Analyseplattformsystem &#41; ](pdw-services-status.md).|  
|Sofortige Dateiinitialisierung-Optionen prüfen mithilfe der **Berechtigungen** (Dialogfeld)|Sofortige Dateiinitialisierung ist eine SQL Server-Funktion, die Datei Datenvorgänge schneller ausführen kann. Es wird auf SQL Server PDW nur aktiviert, wenn das Netzwerkdienstkonto die Berechtigung SE_MANAGE_VOLUME_NAME erteilt wurde. Es ist standardmäßig deaktiviert.<br /><br />Weitere Informationen finden Sie unter [Instant Dateikonfiguration Initialisierung &#40; Analyseplattformsystem &#41; ](instant-file-initialization-configuration.md).|  
|Stellen Sie die master-Datenbank aus einer Sicherung wieder her|Löscht die aktuelle **master** Datenbank und ersetzt es, mit einer Sicherung. Weitere Informationen finden Sie unter [Wiederherstellen der Master-Datenbank &#40; Analyseplattformsystem &#41; ](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Führen zusätzliche Konfigurationsaufgaben  
Nach dem Ausführen der **Configuration Manager** Aufgaben, die folgende Liste von zusätzliche Konfigurationsaufgaben aus. Einige dieser Aufgaben sind optional.  
  
|Konfigurationstask|Description|  
|----------------------|---------------|  
|Antivirensoftware eines Drittanbieters kann installiert und auf die SQL Server PDW Appliance für extern angezeigte Knoten konfiguriert werden.<br /><br />(Optional)|Weitere Informationen finden Sie unter [Antivirus-Software &#40; Analyseplattformsystem &#41; ](antivirus-software.md).|  
|Das Kennwort für den Verzeichnisdienst-Wiederherstellungsmodus kann geändert werden.<br /><br />(Optional)|Weitere Informationen finden Sie unter [Admin-Kennwort festlegen, für das Anmelden beim AD-Knoten im Modus "Verzeichnisdienste wiederherstellen" &#40; DSRM &#41; &#40; Analyseplattformsystem &#41; ](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Konfigurieren Sie die Anwendung den Empfang von Softwareupdates<br /><br />(Empfohlen)|Das Gerät muss konfiguriert werden, um Updates der zugrunde liegende Software und SQL Server PDW zu erhalten.<br /><br />Weitere Informationen finden Sie unter [Konfigurieren von Windows Server Update Services &#40; WSUS &#41; &#40; Analyseplattformsystem &#41; ](configure-windows-server-update-services-wsus.md). Weitere Informationen zu WSUS finden Sie unter [Software Wartung &#40; Analyseplattformsystem &#41; ](software-servicing.md).|  
|Konfigurieren Sie Verbindungen zu externen Daten, z. B. Hadoop oder Azure Blob-Speicher.<br /><br />(Optional)|Weitere Informationen finden Sie unter [Konfigurieren von PolyBase-Konnektivität mit externen Daten &#40; Analyseplattformsystem &#41; ](configure-polybase-connectivity-to-external-data.md).|  
|Konfigurieren von Antivirus-Software<br /><br />(Optional)|Drittanbieter-Antivirussoftware Lösungen können verwendet werden, um extern angezeigte Knoten schützen ist jedoch nicht erforderlich. Befolgen Sie die Richtlinien in.|  
|Konfigurieren Sie InfiniBand-Netzwerkadapter für die Sicherung und beim Laden der Server<br /><br />(Optional)|Um Sicherungs- und Laden von Servern, Herstellen einer Verbindung mit SQL Server PDW mithilfe des InfiniBand-Netzwerks zu konfigurieren, müssen Sie so konfigurieren Sie den Netzwerkadapter so, dass die Appliance DNS zum Auflösen der InfiniBand-Verbindungs mit dem derzeit aktiven InfiniBand-Netzwerk zu ermöglichen.|  
|So konfigurieren Sie, dass die Telemetriedaten an Microsoft senden<br /><br />(Optional)|Um Analytics Platform System zum Senden von Telemetriedaten an Microsoft zu konfigurieren, müssen Sie ein PowerShell-Skript auf den Knoten "Zugriffssteuerung" ausführen. Ausführliche Anweisungen finden Sie unter [Telemetrie Feedback mit Microsoft &#40; senden SQLServer-PDW &#41; ](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Siehe auch  
[Antivirus-Software &#40; Analyseplattformsystem &#41;](antivirus-software.md)  
[Konfigurieren von InfiniBand-Netzwerkadapter &#40; SQLServer-PDW &#41;](configure-infiniband-network-adapters.md)  
  
