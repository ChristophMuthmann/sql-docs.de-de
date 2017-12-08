---
title: PowerPivot-Dienstkonten konfigurieren | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76a85cd0-af93-40c9-9adf-9eb0f80b30c1
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aae3f818de4936974dd53f14c2b3fdbbea0b369f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-power-pivot-service-accounts"></a>Konfigurieren von Power Pivot-Dienstkonten
  Zu einer [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]-Installation gehören zwei Dienste, die Servervorgänge unterstützen. Der **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**-Dienst ist ein Windows-Dienst, der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Datenverarbeitung und -Abfrageunterstützung auf einem Anwendungsserver bietet. Das Anmeldekonto für diesen Dienst wird immer während des SQL Server-Setups angegeben, wenn Sie Analysis Services im integrierten SharePoint-Modus installieren.  
  
 Ein zweites Konto muss für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung angegeben werden, einen freigegebenen Webdienst, der unter einer Anwendungspoolidentität in einer SharePoint-Farm ausgeführt wird. Dieses Konto wird angegeben, wenn Sie mit dem [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]-Konfigurationstool oder PowerShell eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Installation konfigurieren.  
  
 Jeder Dienst sollte unter einem dedizierten Konto ausgeführt werden, damit Sie in der Farm Verbindungen überwachen oder das Kerberos-Authentifizierungsprotokoll aktivieren können.  
  
 Nach dem Festlegen der Dienstkonten müssen alle Änderungen an den Konten über die SharePoint-Zentraladministration vorgenommen werden. Wenn Sie alternative Tools (z. B. die Dienste-Konsolenanwendung, IIS-Manager oder SQL Server-Konfigurations-Manager) verwenden, werden Berechtigungen für den Datenbankzugriff in der Farm oder für den lokalen Dateizugriff auf dem physischen Server nicht aktualisiert.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Aktualisieren eines abgelaufenen Kennworts für eine Instanz von SQL Server Analysis Services (Power Pivot)](#bkmk_passwordssas)  
  
 [Aktualisieren eines abgelaufenen Kennworts für die Power Pivot-Dienstanwendung](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [Das Konto ändern, unter dem der jeweilige Dienst ausgeführt wird](#bkmk_newacct)  
  
 [Erstellen oder Ändern des Anwendungspools für eine Power Pivot-Dienstanwendung](#bkmk_appPool)  
  
 [Kontoanforderungen und Berechtigungen](#requirements)  
  
 [Problembehandlung: Manuelles Gewähren von Administratorberechtigungen](#updatemanually)  
  
 [Problembehandlung: Beheben von HTTP 503-Fehlern aufgrund abgelaufener Kennwörter für die zentrale Verwaltung oder den SharePoint Foundation-Webanwendungsdienst](#expired)  
  
##  <a name="bkmk_passwordssas"></a> Aktualisieren eines abgelaufenen Kennworts für eine Instanz von SQL Server Analysis Services (Power Pivot)  
  
1.  Zeigen Sie auf „Start“, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Dienste**. Doppelklicken Sie auf **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**. Klicken Sie auf **Anmelden**, und geben Sie dann ein neues Kennwort für das Konto ein.  
  
2.  Klicken Sie in der Zentraladministration im Abschnitt „Sicherheit“ auf **Verwaltete Konten konfigurieren**.  
  
3.  Klicken Sie auf **Bearbeiten** , um ein bestimmtes Konto zu ändern.  
  
4.  Wählen Sie **Kennwort jetzt ändern**aus.  
  
5.  Wählen Sie **Kontokennwort auf neuen Wert festlegen**aus. Alle Dienste, die unter dem verwalteten Konto ausgeführt werden, verwenden die aktualisierten Anmeldeinformationen.  
  
##  <a name="bkmk_passwordapp"></a> Aktualisieren eines abgelaufenen Kennworts für die Power Pivot-Dienstanwendung  
  
1.  Klicken Sie in der Zentraladministration im Abschnitt „Sicherheit“ auf **Verwaltete Konten konfigurieren**.  
  
2.  Klicken Sie auf **Bearbeiten** , um ein bestimmtes Konto zu ändern.  
  
3.  Wählen Sie **Kennwort jetzt ändern**aus.  
  
4.  Wählen Sie **Kontokennwort auf neuen Wert festlegen**aus. Alle Dienste, die unter dem verwalteten Konto ausgeführt werden, verwenden die aktualisierten Anmeldeinformationen.  
  
##  <a name="bkmk_newacct"></a> Das Konto ändern, unter dem der jeweilige Dienst ausgeführt wird  
  
1.  Klicken Sie in der Zentraladministration im Abschnitt „Sicherheit“ auf **Dienstkonten konfigurieren**.  
  
2.  Wählen Sie **Windows-Dienst - SQL Server Analysis Services** aus, um das Analysis Services-Dienstkonto zu ändern.  
  
3.  Wählen Sie unter **Select an account for this service**(Ein Konto für diesen Dienst auswählen) ein vorhandenes verwaltetes Konto aus, oder erstellen Sie ein neues. Das Konto muss ein Domänenbenutzerkonto sein.  
  
4.  Wählen Sie **Service Application Pool - SharePoint Web Services System** (Dienstanwendungspool – Systemstandard für SharePoint-Webdienste) aus, um die Anwendungspoolidentität der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Standarddienstanwendung zu ändern. Je nach Konfiguration der Installation wird der Dienst möglicherweise unter einem vorhandenen Dienstanwendungspool ausgeführt, der für SharePoint Services erstellt wurde. Standardmäßig wird der Dienst vom [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Konfigurationstool als **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Standarddienstanwendung ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung)** registriert.  
  
     Wenn der Dienst von einem SharePoint-Administrator manuell konfiguriert wurde, verfügt der Dienst sehr wahrscheinlich über einen eigenen Dienstanwendungspool.  
  
5.  Wählen Sie unter **Select an account for this service**(Ein Konto für diesen Dienst auswählen) ein vorhandenes verwaltetes Konto aus, oder erstellen Sie ein neues. Das Konto muss ein Domänenbenutzerkonto sein.  
  
6.  Klicken Sie auf **OK**.  
  
##  <a name="bkmk_appPool"></a> Erstellen oder Ändern des Anwendungspools für eine Power Pivot-Dienstanwendung  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Wählen Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung aus, aber klicken Sie nicht darauf. Wenn Sie auf einen Anwendungsnamen klicken, wird das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard geöffnet. Dort wird jedoch kein Link zu der Eigenschaftenseite bereitgestellt, auf der der Anwendungspool angegeben ist.  Sie können auf die leere weiße Fläche in der Zeile oder auf den Typnamen klicken, um die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung auszuwählen.  
  
3.  Klicken Sie im Menüband auf **Eigenschaften** .  
  
4.  Wählen Sie **Einen neuen Anwendungspool erstellen**aus. Geben Sie einen Namen für den Anwendungspool und ein verwaltetes Konto für die Identität des Anwendungspools an.  
  
##  <a name="requirements"></a> Kontoanforderungen und Berechtigungen  
 Wenn Sie eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung planen, müssen Sie die folgenden Dienstkonten einplanen.  
  
-   Analysis Services-Dienstkonto. Analysis Services verarbeitet [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Abfragen und -Datenaktualisierungsaufträge in der Farm. Dieses Konto wird immer während des SQL Server-Setups angegeben, wenn Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint installieren.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Dienstanwendungspool. Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung ist mit einem [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst verbunden, der die SharePoint-Integration und -Infrastruktur für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Abfrageverarbeitung in einer Farm bereitstellt. Der Anwendungspool, den Sie für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung angeben, ist die Dienstidentität des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdiensts. Eine Farm kann mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen enthalten. Jede erstellte Anwendung sollte in einem eigenen Anwendungspool ausgeführt werden.  
  
#### <a name="analysis-services-service-account"></a>Analysis Services-Dienstkonto  
  
|Anforderung|Description|  
|-----------------|-----------------|  
|Bereitstellungsanforderung|Dieses Konto muss beim SQL Server-Setup auf der Seite **Analysis Services - Konfiguration** des Installationsassistenten (oder bei einem Befehlszeilensetup im Installationsparameter **ASSVCACCOUNT** ) angegeben werden.<br /><br /> Sie können den Benutzernamen oder das Kennwort über die Zentraladministration, PowerShell oder das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstool ändern. Die Verwendung anderer Tools zum Ändern von Konten und Kennwörtern wird nicht unterstützt.|  
|Domänenbenutzerkonto-Anforderung|Bei diesem Konto muss es sich um ein Windows-Domänenbenutzerkonto handeln. Integrierte Computerkonten (z. B. Netzwerkdienst oder Lokaler Dienst) sind nicht zulässig. SQL Server-Setup erzwingt die Domänenbenutzerkonto-Anforderung, indem die Installation blockiert wird, sobald ein Computerkonto angegeben wird.|  
|Berechtigungsanforderungen|Dieses Konto muss ein Mitglied der SQLServerMSASUser$\<Server > $PowerPivot Sicherheitsgruppe und der WSS_WPG-Sicherheitsgruppen auf dem lokalen Computer. Diese Berechtigungen sollten automatisch gewährt werden. Weitere Informationen zur Überprüfung oder zum Gewähren von Berechtigungen finden Sie unter [Manuelle Gewährung von Kontoverwaltungsberechtigungen für den PowerPivot-Service](#updatemanually) in diesem Thema und unter [Anfängliche Konfiguration (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146).|  
|Anforderungen für horizontales Skalieren|Falls Sie mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Serverinstanzen in einer Farm installieren, müssen alle Analysis Services-Serverinstanzen unter dem gleichen Domänenbenutzerkonto ausgeführt werden. Wenn Sie z.B. die erste [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] -Instanz für die Ausführung als Contoso\ssas-srv01 konfigurieren, müssen alle zusätzlichen [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] -Instanzen, die Sie danach in der gleichen Farm bereitstellen, auch als Contoso\ssas-srv01 (bzw. unter dem entsprechenden aktuellen Konto) ausgeführt werden.<br /><br /> Durch das Konfigurieren aller Dienstinstanzen für die Ausführung unter dem gleichen Konto hat der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst die Möglichkeit, Abfrageverarbeitungs- oder Datenaktualisierungsaufträge jeder beliebigen Analysis Services-Dienstinstanz in der Farm zuzuordnen. Außerdem wird die Verwendung des Features Verwaltetes Konto in der Zentraladministration für Analysis Services-Serverinstanzen ermöglicht. Indem Sie das gleiche Konto für alle [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] -Instanzen verwenden, müssen Sie das Konto oder Kennwort nur einmal ändern, dann werden alle Dienstinstanzen, die die Anmeldeinformationen verwenden, automatisch aktualisiert.<br /><br /> In SQL Server-Setup wird die Verwendung eines identischen Kontos erzwungen. In einer Bereitstellung für horizontales Skalieren, in der bereits eine Instanz von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint in einer SharePoint-Farm installiert ist, blockiert Setup die Neuinstallation, wenn sich das angegebene [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] -Konto von dem bereits in der Farm verwendeten Konto unterscheidet.|  
  
#### <a name="power-pivot-service-application-pool"></a>Power Pivot-Dienstanwendungspool  
  
|Anforderung|Description|  
|-----------------|-----------------|  
|Bereitstellungsanforderung|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Beim Systemdienst handelt es sich um eine in der Farm freigegebene Ressource, die verfügbar wird, wenn Sie eine Dienstanwendung erstellen. Der Dienstanwendungspool muss bei der Erstellung der Dienstanwendung angegeben werden. Er kann auf zwei Arten angegeben werden: mithilfe des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstools oder durch PowerShell-Befehle.<br /><br /> Sie haben die Anwendungspoolidentität möglicherweise so konfiguriert, dass sie unter einem eindeutigen Konto ausgeführt wird. Andernfalls sollten Sie erwägen, dies jetzt zu ändern, dass sie unter einem anderen Konto ausgeführt wird.|  
|Domänenbenutzerkonto-Anforderung|Die Anwendungspoolidentität muss ein Windows-Domänenbenutzerkonto sein. Integrierte Computerkonten (z. B. Netzwerkdienst oder Lokaler Dienst) sind nicht zulässig.|  
|Berechtigungsanforderungen|Dieses Konto benötigt keine lokalen Systemadministratorberechtigungen auf dem Computer. Dieses Konto muss Analysis Services-Systemadministratorberechtigungen auf dem lokalen [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] -Computer aufweisen, der auf dem gleichen Computer installiert ist. Diese Berechtigungen werden automatisch von SQL Server-Setup oder beim Festlegen oder Ändern der Anwendungspoolidentität in der Zentraladministration gewährt.<br /><br /> Administratorberechtigungen sind erforderlich, damit das Weiterleiten von Abfragen an den [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]-Computer erfolgen kann. Sie sind auch zum Überwachen des Zustands, zum Schließen inaktiver Sitzungen und zum Lauschen auf Ablaufverfolgungsereignisse erforderlich.<br /><br /> Das Konto muss über Verbindungs-, Lese- und Schreibberechtigungen für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungsdatenbank verfügen. Diese Berechtigungen werden automatisch gewährt, wenn die Anwendung erstellt wird, und automatisch aktualisiert, wenn Sie Konten oder Kennwörter in der Zentraladministration ändern.<br /><br /> Die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung überprüft, ob ein SharePoint-Benutzer berechtigt ist, Daten vor dem Abrufen der Datei anzuzeigen, sie nimmt jedoch nicht die Identität des Benutzers an. Es gibt keine Berechtigungsanforderungen für Identitätswechsel.|  
|Anforderungen für horizontales Skalieren|Keine.|  
  
##  <a name="updatemanually"></a> Problembehandlung: Manuelles Gewähren von Administratorberechtigungen  
 Administratorberechtigungen werden nicht aktualisiert, wenn die Person, die die Anmeldeinformationen aktualisiert, kein lokaler Administrator auf dem Computer ist. Wenn dies auftritt, können Sie Administratorberechtigungen manuell gewähren. Die einfachste Möglichkeit hierzu besteht darin, den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Zeitgeberauftrag für die Konfiguration in der Zentraladministration auszuführen. Mit dieser Vorgehensweise können Sie Berechtigungen für alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Server in der Farm zurücksetzen. Beachten Sie, dass dieser Ansatz nur funktioniert, wenn der SharePoint-Zeitgeberauftrag sowohl als Farmadministrator als auch als lokaler Administrator auf dem Computer ausgeführt wird.  
  
1.  Klicken Sie in Monitoring auf **Auftragsdefinitionen überprüfen**.  
  
2.  Wählen Sie **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfiguration**aus.  
  
3.  Klicken Sie auf **Jetzt ausführen**.  
  
 Als letzten Ausweg können Sie die richtige Berechtigungen sicherstellen, durch das Erteilen von Analysis Services systemverwaltungsberechtigungen für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -dienstanwendung, und dann ausdrücklich hinzufügen die dienstanwendungsidentität SQLServerMSASUser$\<Servername > $PowerPivot Windows-Sicherheitsgruppe. Sie müssen diese Schritte für jede Analysis Services-Instanz wiederholen, die mit der SharePoint-Farm integriert ist.  
  
 Sie müssen lokaler Administrator sein, um Windows-Sicherheitsgruppen zu aktualisieren.  
  
1.  In SQL Server Management Studio eine Verbindung mit Analysis Services-Instanz als \<Servername > \POWERPIVOT.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Servernamen, und wählen Sie **Eigenschaften**aus.  
  
3.  Klicken Sie auf **Sicherheit**.  
  
4.  Klicken Sie auf **Hinzufügen**.  
  
5.  Geben Sie den Namen des Kontos an, das für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungspool verwendet wird, und klicken Sie auf **OK**.  
  
6.  Klicken Sie unter „Verwaltung“ auf **Computerverwaltung**.  
  
7.  Öffnen Sie **Lokale Benutzer und Gruppen**.  
  
8.  Öffnen Sie **Gruppen**.  
  
9. Doppelklicken Sie auf SQLServerMSASUser$\<Servername > $PowerPivot.  
  
10. Klicken Sie auf **Hinzufügen**.  
  
11. Geben Sie den Namen des Kontos an, das für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungspool verwendet wird, und klicken Sie auf **OK**.  
  
##  <a name="expired"></a> Problembehandlung: Beheben von HTTP 503-Fehlern aufgrund abgelaufener Kennwörter für die zentrale Verwaltung oder den SharePoint Foundation-Webanwendungsdienst  
 Wenn der zentrale Verwaltungsdienst oder der SharePoint Foundation-Webanwendungsdienst aufgrund der Rücksetzung eines Kontos oder des Ablaufs eines Kennworts aufhört zu arbeiten, erhalten Sie die Fehlermeldung HTTP 503 "Dienst nicht verfügbar", wenn Sie versuchen, die zentrale SharePoint-Verwaltung oder eine SharePoint-Website zu öffnen. Führen Sie folgende Schritte aus, um den Server online zurückzubringen. Sobald die zentrale Verwaltung verfügbar ist, können Sie damit fortfahren, abgelaufene Kontoinformationen zu aktualisieren.  
  
1.  Klicken Sie in der Verwaltung auf **Internetinformationsdienste-Manager**.  
  
2.  Wenn die Identität der Website oder Zentraladministrationsanwendungspools ein Domänenbenutzerkonto ist, das ein abgelaufenes Kennwort hat, gehen Sie wie folgt vor:  
  
    1.  Klicken Sie mit der rechten Maustaste auf den Namen des Anwendungspools, und wählen Sie **Erweiterte Einstellungen**aus.  
  
    2.  Wählen Sie **Identität** aus, und klicken Sie auf die Schaltfläche zum Öffnen des Dialogfelds für die Identität des Anwendungspools.  
  
    3.  Klicken Sie auf **Festlegen**.  
  
    4.  Geben Sie den Benutzernamen und das Kennwort ein.  
  
3.  Führen Sie IISRESET aus. Öffnen Sie hierzu eine Administratoreingabeaufforderung, und geben Sie bei der Eingabeaufforderung **iisreset** ein.  
  
4.  Wählen Sie in der zentralen SharePoint-Verwaltung unter „Sicherheit“ die Option **Verwaltete Konten konfigurieren**aus.  
  
5.  Klicken Sie auf **Bearbeiten** , um die Informationen des verwalteten Kontos mit dem abgelaufenen Kennwort zu aktualisieren.  
  
6.  Wählen Sie **Kennwort jetzt ändern**aus.  
  
7.  Klicken Sie auf **Vorhandenes Kennwort verwenden**.  
  
8.  Geben Sie das Kennwort ein, und klicken Sie dann auf **OK**.  
  
 Wenn Reporting Services installiert ist, aktualisieren Sie Kennwörter für den Berichtsserver und die Verbindung zur Berichtsserver-Datenbank mithilfe des Reporting Services-Konfigurations-Managers. Weitere Informationen finden Sie unter [Konfiguration und Verwaltung eines Berichtsservers &#40;SharePoint-Modus von Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Starten oder Beenden eines Power Pivot für SharePoint-Servers](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)   
 [Konfigurieren des PowerPivot-Kontos für die unbeaufsichtigte Datenaktualisierung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
  
