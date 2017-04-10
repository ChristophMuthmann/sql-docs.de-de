---
title: "Konfigurieren einer Verbindung mit der Berichtsserver-Datenbank (SSRS-Konfigurations-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verbindungen [Reporting Services], Konfigurieren"
  - "Verbindungen [Reporting Services]"
  - "Berichtsserver [Reporting Services], Verbindungen"
  - "Berichtsserver-Datenbank"
  - "Datenbanken [Reporting Services], Verbindungen"
  - "Sicherheit [Reporting Services], Datenbankverbindungen"
ms.assetid: 9759a9fb-35e9-4215-969b-a9f1fea18487
caps.latest.revision: 11
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 11
---
# Konfigurieren einer Verbindung mit der Berichtsserver-Datenbank (SSRS-Konfigurations-Manager)
  Für jede Berichtsserverinstanz ist eine Verbindung mit der Berichtsserver-Datenbank erforderlich, in der die vom Server verwalteten Berichte, Berichtsmodelle, freigegebenen Datenquellen, Ressourcen und Metadaten gespeichert sind. Die Anfangsverbindung kann während einer Berichtsserverinstallation erstellt werden, wenn Sie die Standardkonfiguration installieren. In den meisten Fällen empfiehlt sich, die Verbindung mithilfe des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstools zu konfigurieren, wenn das Setup abgeschlossen ist. Sie können die Verbindung jederzeit bearbeiten, um den Kontotyp zu ändern oder Anmeldeinformationen neu festzulegen. Schritt-für-Schritt-Anweisungen zum Erstellen der Datenbank und Konfigurieren der Verbindung finden Sie unter [Erstellen einer Berichtsserver-Datenbank im einheitlichen Modus &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/create-a-native-mode-report-server-database-ssrs-configuration-manager.md).  
  
 In folgenden Situationen müssen Sie eine Berichtsserver-Datenbankverbindung konfigurieren:  
  
-   Konfigurieren eines Berichtsserver für den erstmaligen Einsatz.  
  
-   Konfigurieren eines Berichtsservers für die Verwendung einer anderen Berichtsserver-Datenbank.  
  
-   Ändern des Benutzerkontos oder -kennwortes, das für die Datenbankverbindung verwendet wird. Sie müssen die Datenbankverbindung nur dann aktualisieren, wenn die Kontoinformationen in der Datei RSReportServer.config gespeichert sind. Wenn Sie das Dienstkonto für die Verbindung verwenden (das die integrierte Sicherheit von Windows für die Anmeldeinformationen verwendet), wird das Kennwort nicht gespeichert, sodass es nicht notwendig ist, die Verbindungsinformationen zu aktualisieren. Weitere Informationen zum Ändern von Konten finden Sie unter [Konfigurieren des Berichtsserver-Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
-   Konfigurieren einer Berichtsserverbereitstellung für horizontales Skalieren. Beim Konfigurieren einer Bereitstellung für horizontales Skalieren müssen Sie mehrere Verbindungen zu einer Berichtsserver-Datenbank erstellen. Weitere Informationen zum Ausführen dieses Vorgangs mit mehreren Schritten finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure a native mode report server scale-out deployment.md).  
  
## Herstellen einer Verbindung zwischen Reporting Services und Datenbankmodul  
 Der Zugriff des Berichtsservers auf eine Berichtsserver-Datenbank hängt von Anmeldeinformationen und Verbindungsinformationen sowie von Verschlüsselungsschlüsseln ab, die für die Berichtsserverinstanz gültig sind, die diese Datenbank verwendet. Gültige Verschlüsselungsschlüssel sind erforderlich, um vertrauliche Daten zu speichern und abzurufen. Verschlüsselungsschlüssel werden automatisch erstellt, wenn Sie die Datenbank zum ersten Mal konfigurieren. Nachdem die Schlüssel erstellt wurden, müssen Sie diese aktualisieren, wenn Sie die Identität des Berichtsserverdiensts ändern. Weitere Informationen zum Arbeiten mit Verschlüsselungsschlüsseln finden Sie unter [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-and-manage-encryption-keys-ssrs-configuration-manager.md).  
  
 Die Berichtsserver-Datenbank ist eine interne Komponente, auf die nur der Berichtsserver zugreift. Die Verbindungs- und Anmeldeinformationen, die Sie für die Berichtsserver-Datenbank angeben, werden ausschließlich vom Berichtsserver verwendet. Benutzer, die Berichte anfordern, benötigen für die Berichtsserver-Datenbank keine Datenbankberechtigungen und keinen Datenbank-Anmeldenamen.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet **System.Data.SqlClient**, um eine Verbindung zu [!INCLUDE[ssDE](../../includes/ssde-md.md)] herzustellen, wo die Berichtsserver-Datenbank gehostet wird. Wenn Sie eine lokale Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwenden, stellt der Berichtsserver die Verbindung mithilfe des gemeinsamen Arbeitsspeichers her. Wenn Sie einen Remote-Datenbankserver für die Berichtsserver-Datenbank verwenden, müssen Sie möglicherweise &ndash; je nach verwendeter Edition &ndash; Remoteverbindungen aktivieren. Wenn Sie die Enterprise Edition verwenden, sind Remoteverbindungen standardmäßig für TCP/IP aktiviert.  
  
 Um zu prüfen, ob die Instanz Remoteverbindungen akzeptiert, klicken Sie im Menü **Start** nacheinander **Alle Programme**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Konfigurationstools** und **SQL Server-Konfigurations-Manager**, und prüfen Sie dann, ob das TCP/IP-Protokoll für jeden Dienst aktiviert ist.  
  
 Wenn Sie Remoteverbindungen aktivieren, wird auch das Client- und Serverprotokoll aktiviert. Um zu prüfen, ob die Protokolle aktiviert sind, klicken Sie im Menü **Start**auf **Alle Programme**, zeigen Sie dann auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]und **Konfigurationstools**. Klicken Sie dann auf **SQL Server-Konfigurations-Manager**, auf **SQL Server-Netzwerkkonfiguration**und dann auf **Protokolle für MSSQLSERVER**. Weitere Informationen finden Sie unter [Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
## Definieren einer Berichtsserver-Datenbankverbindung  
 Zum Konfigurieren der Verbindung müssen Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager-Tool oder das **rsconfig** -Befehlszeilen-Hilfsprogramm verwenden. Ein Berichtsserver benötigt die folgenden Verbindungsinformationen:  
  
-   Der Name der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz, auf dem die Berichtsserverdatenbank gehostet wird.  
  
-   Der Name der Berichtsserverdatenbank. Wenn Sie zum ersten Mal eine Verbindung herstellen, können Sie eine neue Berichtsserverdatenbank erstellen oder eine vorhandene Datenbank auswählen. Weitere Informationen finden Sie unter [Erstellen einer Berichtsserver-Datenbank &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/create-a-report-server-database-ssrs-configuration-manager.md).  
  
-   Den Anmeldeinformationstyp. Sie können die Dienstkonten, ein Windows-Domänenkonto oder einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank-Anmeldenamen verwenden.  
  
-   Den Benutzernamen und das Kennwort (nur erforderlich, wenn Sie ein Windows-Domänenkonto oder einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen verwenden).  
  
 Den angegebenen Anmeldeinformationen muss Zugriff auf die Berichtsserver-Datenbank gewährt werden. Wenn Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool verwenden, wird dieser Schritt automatisch ausgeführt. Weitere Informationen über die Berechtigungen, die für den Zugriff auf die Datenbank erforderlich sind, finden Sie im Abschnitt "Datenbankberechtigungen" weiter unten in diesem Thema.  
  
### Speichern von Verbindungsinformationen für eine Datenbank  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] speichert und verschlüsselt die Verbindungsinformationen in den folgenden RSreportserver.config-Einstellungen. Verschlüsselte Werte für diese Einstellungen müssen Sie mithilfe des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstools oder des RSCONFIG-Hilfsprogramms erstellen.  
  
 Nicht alle Werte sind für jeden Verbindungstyp festgelegt. Wenn Sie die Verbindung mithilfe der Standardwerte konfigurieren (also die Dienstkonten zum Herstellen der Verbindung verwenden), sind \<**LogonUser**>, \<**LogonDomain**> und \<**LogonCred**> leer, wie nachfolgend dargestellt:  
  
```  
<Dsn></Dsn>  
<ConnectionType></ConnectionType>  
<LogonUser></LogonUser>  
<LogonDomain></LogonDomain>  
<LogonCred></LogonCred>  
```  
  
 Wurde die Verbindung für die Verwendung eines bestimmten Windows-Kontos oder Datenbank-Anmeldenamens konfiguriert, müssen Sie die gespeicherten Werte aktualisieren, falls Sie das Konto oder den Anmeldenamen später ändern.  
  
### Auswählen eines Anmeldeinformationentyps  
 Es gibt drei Typen von Anmeldeinformationen, die für eine Verbindung mit einer Berichtsserver-Datenbank verwendet werden können.  
  
-   Die integrierte Sicherheit von Windows, die das Berichtsserver-Dienstkonto verwendet. Da der Berichtsserver als Einzeldienst implementiert wird, wird nur für das Konto, unter dem der Dienst ausgeführt wird, Datenbankzugriff benötigt.  
  
-   Ein Windows-Benutzerkonto. Sind der Berichtsserver und die Berichtsserver-Datenbank auf demselben Computer installiert, können Sie ein lokales Konto verwenden. Andernfalls müssen Sie einen Domänenkonto verwenden.  
  
-   Einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen.  
  
> [!NOTE]  
>  Es ist nicht möglich, eine benutzerdefinierte Authentifizierungserweiterung für die Verbindung mit einer Berichtsserver-Datenbank zu verwenden. Benutzerdefinierte Authentifizierungserweiterungen werden verwendet, um einen Prinzipal für einen Berichtsserver zu authentifizieren. Sie haben keine Auswirkung auf Verbindungen mit der Berichtsserver-Datenbank oder mit externen Datenquellen, die Inhalte für Berichte enthalten.  
  
 Wenn die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] für die Windows-Authentifizierung konfiguriert wird und wenn diese sich in derselben Domäne wie der Berichtsserver-Computer oder einer vertrauenswürdigen Domäne befindet, können Sie die Verbindung so konfigurieren, dass das Dienstkonto oder ein Domänenbenutzerkonto verwendet wird, das Sie als Verbindungseigenschaft für das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool verwalten. Wenn sich der Datenbankserver in einer anderen Domäne befindet oder wenn Sie die Arbeitsgruppensicherheit verwenden, müssen Sie die Verbindung so konfigurieren, dass ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank-Anmeldename verwendet wird. Stellen Sie in diesem Fall sicher, dass die Verbindung verschlüsselt ist.  
  
##### Verwenden von Dienstkonten und der integrierten Sicherheit  
 Sie können die integrierte Sicherheit von Windows verwenden, um eine Verbindung über das Berichtsserver-Dienstkonto herzustellen. Das Dienstkonto erhält eine Anmeldeberechtigung für die Berichtsserver-Datenbank. Diese Art der Anmeldeinformationen wird standardmäßig vom Setupprogramm ausgewählt, wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der Standardkonfiguration installieren.  
  
 Das Dienstkonto ist ein vertrauenswürdiges Konto, das eine geringe Wartung bei der Verwaltung einer Berichtsserver-Datenbankverbindung ermöglicht. Da das Dienstkonto die integrierte Sicherheit von Windows zum Herstellen der Verbindung verwendet, müssen die Anmeldeinformationen nicht gespeichert werden. Wenn Sie nachfolgend das Kennwort oder die Identität des Dienstkontos ändern (indem Sie z.B. von einem integrierten Konto zu einem Domänenkonto wechseln), stellen Sie sicher, dass Sie die Änderung mithilfe des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Konfigurationstools vornehmen. Das Tool aktualisiert die Datenbankberechtigungen automatisch, damit die überarbeiteten Kontoinformationen verwendet werden. Weitere Informationen finden Sie unter [Konfigurieren des Berichtsserver-Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 Wenn Sie die Datenbankverbindung so konfigurieren, dass das Dienstkonto verwendet wird, muss das Konto über Netzwerkberechtigungen verfügen, falls sich die Berichtsserver-Datenbank auf einem Remotecomputer befindet. Verwenden Sie das Dienstkonto nicht, wenn die Berichtsserver-Datenbank sich in einer anderen Domäne befindet, hinter einer Firewall, oder wenn Sie Arbeitsgruppensicherheit anstelle von Domänensicherheit verwenden. Verwenden Sie stattdessen ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank-Benutzerkonto.  
  
##### Verwenden eines Domänenbenutzerkontos  
 Sie können ein Windows-Benutzerkonto für die Verbindung zwischen Berichtsserver und Berichtsserver-Datenbank angeben. Wenn Sie ein lokales oder ein Domänenkonto verwenden, müssen Sie die Berichtsserver-Datenbank jedes Mal aktualisieren, wenn Sie das Kennwort oder das Konto ändern. Verwenden Sie zum Aktualisieren der Verbindung immer das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool.  
  
##### Verwenden eines SQL Server-Anmeldenamens  
 Sie können einen einzelnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen festlegen, mit dem die Verbindung zur Berichtsserver-Datenbank hergestellt wird. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden und sich die Berichtsserver-Datenbank auf einem Remotecomputer befindet, sollten Sie die Übertragung der Daten zwischen den Servern mithilfe von IPSec schützen. Wenn Sie einen Datenbank-Anmeldenamen verwenden, müssen Sie die Berichtsserver-Datenbank jedes Mal aktualisieren, wenn Sie das Kennwort oder das Konto ändern.  
  
### Datenbankberechtigungen  
 Konten, über die eine Verbindung mit der Berichtsserver-Datenbank hergestellt wird, werden die folgenden Rollen zugewiesen:  
  
-   Die Rollen**public** und **RSExecRole** für die **ReportServer** -Datenbank.  
  
-   Die**RSExecRole** -Rolle für die Datenbanken **master**, **msdb**und **ReportServerTempDB** .  
  
 Wenn Sie die Verbindung anhand des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstools erstellen oder ändern, werden diese Berechtigungen automatisch erteilt. Wenn Sie das RSCONFIG-Hilfsprogramm verwenden und ein anderes Konto für die Verbindung angeben, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen für dieses neue Konto aktualisieren. Mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool können Sie Skriptdateien erstellen, mit deren Hilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename für den Berichtsserver aktualisiert wird.  
  
### Überprüfen des Datenbanknamens  
 Mithilfe des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstools können Sie feststellen, welche Berichtsserver-Datenbank von einer bestimmten Berichtsserverinstanz verwendet wird. Zum Ermitteln des Namens stellen Sie eine Verbindung mit der Berichtsserverinstanz her und öffnen dann die Seite Setup der Datenbank.  
  
## Verwenden einer anderen Berichtsserver-Datenbank oder Verschieben einer Berichtsserver-Datenbank  
 Durch das Ändern der Verbindungsinformationen können Sie eine Berichtsserverinstanz so konfigurieren, dass sie eine andere Berichtsserver-Datenbank verwendet. Der Wechsel der Datenbanken hängt häufig damit zusammen, dass ein Produktionsberichtsserver bereitgestellt wird. Der Wechsel von einer Datenbank auf einem Testberichtsserver zu einer Datenbank auf einem Produktionsberichtsserver ist typisch für die Inbetriebnahme eines Produktionsservers. Sie können eine Berichtsserver-Datenbank auch auf einen anderen Computer verschieben. Weitere Informationen finden Sie unter [Aktualisieren und Migrieren von Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation, .  
  
## Konfigurieren mehrerer Berichtsserver für die Verwendung der gleichen Berichtsserver-Datenbank  
 Es ist möglich, mehrere Berichtsserver so zu konfigurieren, dass sie dieselbe Berichtsserver-Datenbank verwenden. Diese Konfiguration wird als Bereitstellung für horizontales Skalieren bezeichnet. Diese Konfiguration ist eine Voraussetzung, wenn Sie mehrere Berichtsserver in einem Servercluster ausführen möchten. Sie können diese Konfiguration jedoch auch verwenden, wenn Sie Dienstanwendungen segmentieren oder wenn Sie die Installation und die Einstellungen einer neuen Berichtsserverinstanz testen möchten, um diese mit der Installation eines vorhandenen Berichtsservers zu vergleichen. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure a native mode report server scale-out deployment.md).  
  
## Siehe auch  
 [Erstellen einer Berichtsserver-Datenbank &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Verwalten eines Berichtsservers von Reporting Services im einheitlichen Modus](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Konfigurieren des Berichtsserver-Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  