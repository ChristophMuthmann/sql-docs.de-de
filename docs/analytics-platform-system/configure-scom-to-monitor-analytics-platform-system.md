---
title: Konfigurieren von SCOM zum Überwachen von Analytics Platform System | Microsoft Docs
description: Führen Sie diese Schritte aus, um die System Center Operations Manager (SCOM) Management Packs für Analytics Platform System zu konfigurieren. Die Management Packs sind erforderlich, Analytics Platform System von SCOM überwacht.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4c2e8a42d488c18e705c9d7d8c1d53c9ff7c9cb8
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Konfigurieren Sie System Center Operationsmanager (SCOM), Analytics Platform System überwachen
Führen Sie diese Schritte aus, um die System Center Operations Manager (SCOM) Management Packs für Analytics Platform System zu konfigurieren. Die Management Packs sind erforderlich, Analytics Platform System von SCOM überwacht.  
  
## <a name="BeforeBegin"></a>Vorbereitungen  
**Erforderliche Komponenten**  
  
System Center Operationsmanager 2007 R2 muss installiert und aktiv sein.  
  
Die Management Packs müssen installiert und konfiguriert werden. Finden Sie unter [Installation der SCOM-Management Packs &#40;Analyseplattformsystem&#41; ](install-the-scom-management-packs.md) und [Importieren des SCOM-Management Packs für PDW &#40;Analyseplattformsystem&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Konfigurieren von Ausführenden Profile in System Center  
Um System Center konfigurieren, müssen Sie Schritte ausführen:  
  
-   Erstellen Sie die Ausführung als Konto für die **APS-Watcher** Domänenbenutzer und ordnen ihn der **Microsoft APS-Watcher-Konto.**  
  
-   Erstellen Sie die Ausführung als Konto für die **Monitoring_user** APS-Benutzer und ordnen ihn der **Microsoft APS-Aktionskonto**.  
  
Hier werden ausführliche Anleitungen für die Aufgaben aus:  
  
1.  Erstellen der **APS-Watcher** ausführendes Konto mit **Windows** Kontotyp für die **APS-Watcher** Domänenbenutzer.  
  
    1.  Navigieren Sie zu der **Verwaltung** Bereich mit der rechten Maustaste auf **Ausführen als-Konfiguration** -> **Konten** , und wählen Sie **ausführendes Konto erstellen...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  Die **Ausführung als Konto Assistenten zum Erstellen von** Dialogfeld wird geöffnet. Auf der **Einführung** auf **Weiter**.  
  
    3.  Auf der **allgemeine Eigenschaften** Seite **Windows** aus **Ausführender Kontotyp** , und geben Sie "APS-Watcher" als die **Anzeigenamen**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  Auf der **Anmeldeinformationen** Seite ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  Auf der **Verteilungssicherheit** Seite **unsicherer** , und klicken Sie auf die **erstellen** Schaltfläche, um den Vorgang abzuschließen.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Wenn Sie sich entscheiden, verwendet der **sicherer** auswählen, müssen Sie manuell Computer angeben, an die Anmeldeinformationen verteilt werden. Klicken Sie dazu nach dem Erstellen des ausführenden Kontos, mit der rechten Maustaste darauf, und wählen Sie **Eigenschaften**.  
  
        2.  Navigieren Sie zu der **Verteilung** Registerkarte und **hinzufügen** gewünschten Computer.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Legen Sie die **Microsoft APS-Watcher-Konto** zu verwendende Profil **APS-Watcher** ausführende Konto.  
  
    1.  Navigieren Sie zu **Verwaltung** -> **Ausführen als-> Konfiguration** -> **Profile**.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Klicken Sie mit der rechten Maustaste auf **Microsoft APS-Watcher-Konto** aus der Liste aus und wählen Sie **Eigenschaften**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  Die **Assistenten für ausführende Profile** Dialogfeld wird geöffnet. Überspringen der **Einführung** Seite, indem Sie auf **Weiter**.  
  
    4.  Auf der **allgemeine Eigenschaften** auf **Weiter**.  
  
    5.  Auf der **ausführende Konten** auf die **hinzufügen...** Schaltfläche und wählen Sie das zuvor erstellte **APS-Watcher** ausführende Konto.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Klicken Sie auf **speichern** Profil Zuweisung abgeschlossen.  
  
3.  Warten Sie, bis der Abschluss der Ermittlung der APS-Einheiten.  
  
    1.  Navigieren Sie zu der **Überwachung** Bereich, und öffnen Sie die **SQL Server-Appliance** -> **Microsoft Analytics Platform System**  ->   **Dazu gehören softwarelastenausgleichsmodule** Statusansicht.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Warten Sie, bis das Gerät in der Liste angezeigt wird. Der Name der Anwendung sollte in der Registrierung angegebene gleich sein. Nach Abschluss der Ermittlung sollten alle Geräte aufgeführt, aber nicht überwacht angezeigt werden. Führen Sie zur Ermöglichung der Überwachung, die nächsten Schritte aus.  
  
    > [!NOTE]  
    > Die nächsten Schritte können parallel abgeschlossen werden, während Sie, für die anfängliche Appliance-Ermittlung warten auf Fertig stellen.  
  
4.  Erstellen einer anderen neuen ausführenden Kontos abzufragende APS Datenabruf Integrität an.  
  
    1.  Beginnen Sie, erstellen ein neues ausführendes Konto aus, wie in Schritt 1 beschrieben.  
  
    2.  Auf der **allgemeine Eigenschaften** Seite **Standardauthentifizierung** Kontotyp.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  Auf der **Anmeldeinformationen** Seite, geben Sie gültige Anmeldeinformationen für den Zugriff auf APS-Integritätsstatus DMVs.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Konfigurieren der **Microsoft APS-Aktionskonto** Profils, das den neu erstellte ausführenden Konto für die APS-Instanz verwendet.  
  
    1.  Navigieren Sie zu der **Microsoft APS-Aktionskonto** Eigenschaften wie in Schritt 2 beschrieben.  
  
    2.  Auf der **ausführende Konten** auf **hinzufügen...** - und 
    3.  Wählen Sie den neu erstellte ausführenden Konto.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>Nächster Schritt  
Nun, dass Sie die Management Packs konfiguriert haben, können Sie beim Starten der Überwachung der Appliance. Weitere Informationen finden Sie unter [überwachen die Appliance by Using System Center Operations Manager &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
