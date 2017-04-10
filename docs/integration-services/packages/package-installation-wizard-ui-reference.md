---
title: "Referenz zur Benutzeroberfl&#228;che des Paketinstallations-Assistenten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.deploymentwizard.welcome.f1"
  - "sql13.dts.deploymentwizard.confirminstallation.f1"
  - "sql13.dts.deploymentwizard.deploydtspackages.f1"
  - "sql13.dts.deploymentwizard.finish.f1"
  - "sql13.dts.deploymentwizard.configurepackages.f1"
  - "sql13.dts.deploymentwizard.selectinstfolder.f1"
  - "sql13.dts.deploymentwizard.packagevalidation.f1"
  - "sql13.dts.deploymentwizard.specifytargetsqlserver.f1"
helpviewer_keywords: 
  - "Paketinstallations-Assistent"
ms.assetid: 6fca44d9-5001-4644-bcf3-c2d10a674b97
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Referenz zur Benutzeroberfl&#228;che des Paketinstallations-Assistenten
  Mit dem **Paketinstallations-Assistenten** können Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt einschließlich der enthaltenen Pakete, verschiedenen Dateien und Paketabhängigkeiten bereitstellen.  
  
 Bevor Sie Pakete bereitstellen, können Sie Konfigurationen erstellen und diese dann mit den Paketen bereitstellen. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet Konfigurationen, um Eigenschaften von Paketen und Paketobjekten zur Laufzeit dynamisch zu aktualisieren. Beispielsweise kann die Verbindungszeichenfolge einer OLE DB-Verbindung zur Laufzeit dynamisch festgelegt werden, indem Sie eine Konfiguration erstellen, die der Eigenschaft, die die Verbindungszeichenfolge enthält, einen Wert zuordnet.  
  
 Der Paketinstallations-Assistent kann erst ausgeführt werden, nachdem Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt und ein Bereitstellungshilfsprogramm erstellt haben. Weitere Informationen finden Sie unter [Deploy Packages by Using the Deployment Utility](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md).  
  
 In den folgenden Abschnitten werden Seiten des Assistenten beschrieben.  
  
## Willkommen auf der Seite des Paketinstallations-Assistenten.  
 Mit dem **Paketinstallations-Assistenten** können Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt bereitstellen, für das Sie ein Paketbereitstellungshilfsprogramm erstellt haben.  
  
 **Diese Anfangsseite nicht mehr anzeigen**  
 Wählen Sie diese Option aus, um die Startseite bei der nächsten Ausführung des Assistenten auszulassen.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
## Seite "Pakete konfigurieren"  
 Mithilfe der Seite **Pakete konfigurieren** können Sie Paketkonfigurationen bearbeiten.  
  
### enthalten  
 **Konfigurationsdatei**  
 Bearbeiten Sie die Inhalte einer Konfigurationsdatei, indem Sie die Datei aus der Liste auswählen.  
  
 **Verwandte Themen:** [Erstellen von Paketkonfigurationen](../../integration-services/packages/create-package-configurations.md)  
  
 **Pfad**  
 Zeigen Sie den Pfad der zu konfigurierenden Eigenschaft an.  
  
 **Typ**  
 Zeigen Sie den Datentyp der Eigenschaft an.  
  
 **Wert**  
 Geben Sie den Wert der Konfiguration an.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
## Seite "Installation bestätigen"  
 Mithilfe der Seite **Installation bestätigen** können Sie die Installation von Paketen starten und den Status sowie die Informationen anzeigen, die der Assistent zum Installieren von Dateien aus dem angegebenen Projekt verwendet.  
  
 **Weiter**  
 Installiert die Pakete und die dazugehörigen Abhängigkeiten und wechselt nach Abschluss der Installation zur nächsten Seite des Assistenten.  
  
 **Status**  
 Zeigt den Fortschritt der Paketinstallation an.  
  
 **Fertig stellen**  
 Wechseln Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
## Seit "SSIS-Paket bereitstellen"  
 Mithilfe der Seite **SSIS-Pakete bereitstellen** können Sie angeben, an welcher Stelle [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete und ihre Abhängigkeiten installiert werden sollen.  
  
### enthalten  
 **Bereitstellung im Dateisystem**  
 Stellen Sie Pakete und Abhängigkeiten in einem bestimmten Ordner im Dateisystem bereit.  
  
 **Bereitstellung in SQL Server**  
 Stellen Sie Pakete und Abhängigkeiten in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereit. Verwenden Sie diese Option, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Pakete zwischen Servern freigibt. Bestehende Paketabhängigkeiten werden im angegebenen Ordner im Dateisystem installiert.  
  
 **Pakete nach der Installation überprüfen**  
 Geben Sie an, ob Pakete nach der Installation überprüft werden sollen.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
## Seite "Paketüberprüfung"  
 Auf der Seite **Paketüberprüfung** können Sie den Fortschritt und die Ergebnisse der Paketüberprüfung anzeigen.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
## Seite "Installationsordner auswählen"  
 Mithilfe der Seite **Installationsordner auswählen** können Sie den Dateisystemordner angeben, in dem die Pakete und deren Abhängigkeiten installiert werden sollen.  
  
### enthalten  
 **Ordner**  
 Geben Sie den Pfad und den Ordner an, in den das Paket und seine Abhängigkeiten kopiert werden sollen.  
  
 **Durchsuchen**  
 Suchen Sie den Zielordner im Dialogfeld **Ordner suchen**.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
## Seite "Zielserver mit SQL Server angeben"  
 Auf der Seite **Zielserver mit SQL Server angeben** können Sie Optionen zur Bereitstellung des Pakets für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz angeben.  
  
### enthalten  
 **Servername**  
 Geben Sie den Namen des Servers an, auf dem die Pakete bereitgestellt werden sollen.  
  
 **Windows-Authentifizierung verwenden**  
 Geben Sie an, ob für die Anmeldung beim Server die Windows-Authentifizierung verwendet werden soll. Im Sinne einer größeren Sicherheit wird die Windows-Authentifizierung empfohlen.  
  
 **SQL Server-Authentifizierung verwenden**  
 Geben Sie an, ob vom Paket für die Anmeldung beim Server die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendet werden soll. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, müssen Sie einen Benutzernamen und ein Kennwort angeben.  
  
 **Benutzername**  
 Geben Sie einen Benutzernamen an.  
  
 **Kennwort**  
 Geben Sie ein Kennwort an.  
  
 **Paketpfad**  
 Geben Sie den Namen des logischen Ordners an, oder geben Sie / für den Standardordner ein.  
  
 Klicken Sie zum Auswählen des Ordners im Dialogfeld **SSIS-Paket** auf die Schaltfläche zum Durchsuchen (...). Allerdings bietet das Dialogfeld keine Möglichkeit, den Standardordner auszuwählen. Wenn Sie den Standardordner verwenden möchten, müssen Sie im Textfeld / eingeben.  
  
> [!NOTE]  
>  Wenn Sie keinen gültigen Paketpfad eingeben, wird die folgende Fehlermeldung angezeigt: "Mindestens ein Argument ist ungültig."  
  
 **Serverspeicher für die Verschlüsselung verwenden**  
 Wählen Sie diese Option aus, um die Pakete mithilfe von Sicherheitsfunktionen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu sichern.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
## Seite "Fertigstellen des Assistenten"  
 Auf der Seite **Fertigstellen des Assistenten** können Sie eine Übersicht über die Ergebnisse der Paketinstallation anzeigen. Die Seite enthält verschiedene Detailinformationen, z. B. den Namen des bereitgestellten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts, die Namen der installierten Pakete, die Konfigurationsdateien und den Installationsspeicherort.  
  
 **Fertig stellen**  
 Durch Klicken auf **Fertig stellen** beenden Sie den Assistenten.  
  
## Siehe auch  
 [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)  
  
  