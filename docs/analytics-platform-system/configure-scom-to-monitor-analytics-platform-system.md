---
title: "Konfigurieren von SCOM zum Überwachen von Analyseplattformsystem"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4dba9b50-1447-45fc-b219-b9fc99d47d8d
caps.latest.revision: "10"
ms.openlocfilehash: f9c8a778afad89abea9ad4fd092fefb15844a5ae
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-scom-to-monitor-analytics-platform-system"></a>Konfigurieren von SCOM zum Überwachen von Analyseplattformsystem
Führen Sie diese Schritte aus, um die System Center Operations Manager (SCOM) Management Packs für Analytics Platform System zu konfigurieren. Die Management Packs sind erforderlich, Analytics Platform System von SCOM überwacht.  
  
## <a name="BeforeBegin"></a>Vorbereitungen  
**Erforderliche Komponenten**  
  
System Center Operationsmanager 2007 R2 muss installiert und aktiv sein.  
  
Die Management Packs müssen installiert und konfiguriert werden. Finden Sie unter [installieren Sie die SCOM-Management Packs &#40; Analyseplattformsystem &#41; ](install-the-scom-management-packs.md) und [Importieren des SCOM-Management Packs für PDW &#40; Analyseplattformsystem &#41; ](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Konfigurieren von Ausführenden Profile in System Center  
Zum Konfigurieren von System Center müssen Sie folgende Schritte ausführen:  
  
-   Erstellen Sie die Ausführung als Konto für die **APS-Watcher** Domänenbenutzer und ordnen ihn der **Microsoft APS-Watcher-Konto.**  
  
-   Erstellen Sie die Ausführung als Konto für die **Monitoring_user** APS-Benutzer und ordnen ihn der **Microsoft APS-Aktionskonto**.  
  
Hier werden ausführliche Anleitungen, wie Sie dies tun können:  
  
1.  Erstellen der **APS-Watcher** ausführendes Konto mit **Windows** Kontotyp für die **APS-Watcher** Domänenbenutzer.  
  
    1.  Navigieren Sie zu der **Verwaltung** Bereich mit der rechten Maustaste auf **Ausführen als-Konfiguration** -> **Konten** , und wählen Sie **ausführendes Konto erstellen...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  Die **Ausführung als Konto Assistenten zum Erstellen von** Dialogfeld wird geöffnet. Auf der **Einführung** auf **Weiter**.  
  
    3.  Auf der **allgemeine Eigenschaften** Seite **Windows** aus **Ausführender Kontotyp** , und geben Sie "APS-Watcher" als die **Anzeigenamen**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  Auf der **Anmeldeinformationen** Seite Geben Sie Anmeldeinformationen des Domänenbenutzers "APS-Watcher".  
  
        ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  Auf der **Verteilungssicherheit** Seite **unsicherer** , und klicken Sie auf die **erstellen** Schaltfläche, um den Vorgang abzuschließen.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Wenn Sie sich entscheiden, verwendet der **sicherer** Option Sie manuell auf Computern, auf welche Anmeldeinformationen angeben müssen verteilt werden. Klicken Sie dazu nach dem Erstellen des ausführenden Kontos, mit der rechten Maustaste darauf, und wählen Sie **Eigenschaften**.  
  
        2.  Navigieren Sie zu der **Verteilung** Registerkarte und **hinzufügen** gewünschten Computer.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Legen Sie die **Microsoft APS-Watcher-Konto** zu verwendende Profil **APS-Watcher** ausführende Konto.  
  
    1.  Navigieren Sie zu **Verwaltung** -> **Ausführen als-> Konfiguration** -> **Profile**.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Klicken Sie mit der rechten Maustaste auf **Microsoft APS-Watcher-Konto** aus der Liste aus und wählen Sie **Eigenschaften**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  Die **Assistenten für ausführende Profile** Dialogfeld wird geöffnet. Überspringen der **Einführung** Seite, indem Sie auf **Weiter**.  
  
    4.  Auf der **allgemeine Eigenschaften** auf **Weiter**.  
  
    5.  Auf der **ausführende Konten** Seite klicken Sie auf die **hinzufügen...** Schaltfläche und wählen Sie das zuvor erstellte **APS-Watcher** ausführende Konto.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Klicken Sie auf **speichern** Profil Zuweisung abgeschlossen.  
  
3.  Warten Sie, bis der Abschluss der Ermittlung der APS-Einheiten.  
  
    1.  Navigieren Sie zu der **Überwachung** Bereich, und öffnen Sie die **SQL Server-Appliance** -> **Microsoft Analytics Platform System**  ->   **Dazu gehören softwarelastenausgleichsmodule** Statusansicht.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Warten Sie, bis das Gerät in der Liste angezeigt wird. Der Name der Anwendung sollte in der Registrierung angegebene gleich sein.  
  
    Nach Abschluss der Ermittlung sollten alle Geräte aufgeführt, aber nicht überwacht angezeigt werden. Führen Sie für die Überwachung funktioniert die nächsten Schritte aus.  
  
    > [!NOTE]  
    > Die nächsten Schritte können parallel abgeschlossen werden, während Sie, für die anfängliche Appliance-Ermittlung warten auf Fertig stellen.  
  
4.  Erstellen einer anderen neuen ausführenden Kontos abzufragende APS Datenabruf Integrität an.  
  
    1.  Beginnen Sie, erstellen ein neues ausführendes Konto aus, wie in Schritt 1 beschrieben.  
  
    2.  Auf der **allgemeine Eigenschaften** Seite **Standardauthentifizierung** Kontotyp.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  Auf der **Anmeldeinformationen** Netzteils gültige Anmeldeinformationen APS-Integritätsstatus DMVs auf Seite.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Konfigurieren der **Microsoft APS-Aktionskonto** Profils, das den neu erstellte ausführenden Konto für die APS-Instanz verwendet.  
  
    1.  Navigieren Sie zu der **Microsoft APS-Aktionskonto** Eigenschaften wie in Schritt 2 beschrieben.  
  
    2.  Auf der **ausführende Konten** auf **hinzufügen...** und wählen Sie den neu erstellte ausführenden Konto.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>Nächster Schritt  
Nun, dass Sie die Management Packs konfiguriert haben, können Sie beim Starten der Überwachung der Appliance. Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe von System Center Operations Manager &#40; Analyseplattformsystem &#41; ](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
