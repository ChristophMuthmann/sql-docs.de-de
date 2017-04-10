---
title: "Bereitstellungs-Assistent f&#252;r Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.deploymentwizard.f1"
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Bereitstellungs-Assistent f&#252;r Integration Services
  Die **Bereitstellungs-Assistent für Integration Services** unterstützt zwei Bereitstellungsmodelle:
   - Projektbereitstellungsmodell
   - Paketbereitstellungsmodell 
   
 Das **Projektbereitstellungsmodell** ermöglicht Ihnen, ein SQL Server Integration Services-Projekt (SSIS) als eine einzelne Einheit im SSIS-Katalog bereitzustellen.
 
 Das **Paketbereitstellungsmodell** ermöglicht Ihnen, aktualisierte Pakete im SSIS-Katalog bereitzustellen, ohne dass Sie das ganze Projekt bereitstellen müssen. 
 
 > **HINWEIS:** Die standardmäßige Bereitstellung für den Assistenten ist das Projektbereitstellungsmodell.  
  
## Starten des Assistenten
Starten Sie den Assistenten auf eine der folgenden Arten:

 - Eingeben von **SQL Server Bereitstellungs-Assistent** in Windows Search 

**OR**

 - Suchen nach der ausführbaren Datei **ISDeploymentWizard.exe** im SQL Server-Installationsordner; Beispiel: „C:\Programme (x86) \Microsoft SQL Server\130\DTS\Binn“. 
 
 > **HINWEIS:** Falls Sie die Seite **Einführung** sehen, klicken Sie auf **Weiter**, um auf die Seite **Quellen auswählen** zu wechseln. 
 
 Die Einstellungen auf dieser Seite unterscheiden sich für jedes Bereitstellungsmodell. Führen Sie die Schritte im Abschnitt [Project Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#ProjectModel) oder im Abschnitt [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) aus, je nachdem welches Modell Sie auf dieser Seite gewählt haben.  
  
##  <a name="ProjectModel"></a> Projektbereitstellungsmodell  
  
### Quellen auswählen  
 Um eine von Ihnen erstellte Projektbereitstellungsdatei bereitzustellen, wählen Sie **Projektbereitstellungsdatei** aus, und geben Sie den Pfad für die ISPAC-Datei ein. Um ein Projekt bereitzustellen, das sich im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Katalog befindet, wählen Sie **Integration Services-Katalog**aus und geben dann den Servernamen und den Pfad zum Projekt im Katalog ein. Klicken Sie auf **Weiter** , um die Seite **Ziel auswählen** zu sehen.  
  
### Ziel auswählen  
 Um den Zielordner für das Projekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Katalog auszuwählen, geben Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz ein, oder klicken Sie auf **Durchsuchen** , um aus einer Liste von Servern auszuwählen. Geben Sie den Projektpfad in SSISDB ein, oder klicken Sie auf **Durchsuchen** , um ihn auszuwählen. Klicken Sie auf **Weiter** , um die Seite **Überprüfen** zu sehen.  
  
### Überprüfen (und Bereitstellen)  
 Diese Seite erlaubt Ihnen die Überprüfung der von Ihnen vorgenommenen Einstellungen. Sie können Ihre Auswahl ändern, indem Sie auf **Zurück**klicken oder indem Sie auf einen der Schritte im linken Bereich klicken. Klicken Sie auf **Bereitstellen** , um den Bereitstellungsprozess zu starten.  
  
### Ergebnisse  
 Nachdem der Bereitstellungsvorgang abgeschlossen ist, sollten Sie die Seite **Ergebnisse** sehen. Diese Seite zeigt an, ob die einzelnen Aktionen erfolgreich ausgeführt wurden oder ob Fehler aufgetreten sind. Ist die Aktion fehlerhaft, klicken Sie auf **Fehler** in der Spalte **Ergebnis** , um eine Erklärung über den Fehler anzuzeigen. Klicken Sie auf **Bericht speichern** , um die Ergebnisse in einer XML-Datei zu speichern, oder klicken Sie auf **Schließen** , um den Assistenten zu beenden.  
  
##  <a name="PackageModel"></a> Paketbereitstellungsmodell  
  
### Quellen auswählen  
 Die Seite **Quelle auswählen** im **Bereitstellungs-Assistenten für Integration Services** zeigt die Einstellungen speziell für das Paketbereitstellungsmodell an, wenn Sie die Option **Paketbereitstellung** als **Bereitstellungsmodell**gewählt haben.  
  
 Zum Auswählen der Quellpakete klicken Sie auf die Schaltfläche **Durchsuchen…** , um den **Ordner** that contains the packages or type the Ordner path in the **Packages Ordner path** ein, und klicken Sie die Schaltfläche **Aktualisieren** am unteren Seitenrand. Jetzt sollten Sie alle Pakete im angegebenen Ordner im Listenfeld sehen. Standardmäßig sind alle Pakete ausgewählt. Klicken Sie das **Kontrollkästchen** in der ersten Spalte, um auszuwählen, welche Pakete an den Server bereitgestellt werden sollen.  
  
 Beziehen Sie sich auf die Spalten **Status** und **Meldung** , um den Status des Pakets zu überprüfen. Falls der Status auf **Bereit** oder **Warnung**steht, würde der Bereitstellungs-Assistent den Bereitstellungsvorgang nicht blockieren. Falls hingegen der Status auf **Fehler**steht, setzt der Assistent die Bereitstellung der ausgewählten Pakete nicht fort. Klicken Sie auf den Link in der Spalte **Meldung**, um sich die detaillierteren Warn-/Fehlermeldungen anzeigen zu lassen.  
  
 Falls die sensiblen Daten oder Paketdaten mit einem Kennwort verschlüsselt sind, geben Sie das Kennwort in die Spalte **Kennwort** ein, und klicken Sie auf die Schaltfläche **Aktualisieren** , um zu überprüfen, ob das Kennwort akzeptiert wird. Falls das Kennwort korrekt ist, ändert sich der Status auf **Bereit** , und die Warnmeldung verschwindet. Falls es mehrere Pakete mit dem gleichen Kennwort gibt, wählen Sie die Pakete mit dem gleichen Verschlüsselungskennwort aus, geben Sie das Kennwort in das Textfeld **Kennwort** ein, und klicken Sie auf die Schaltfläche **Anwenden** . Das Kennwort würde auf die ausgewählten Pakete angewendet werden.  
  
 Falls der Status aller ausgewählten Pakete nicht auf **Fehler**steht, ist die Schaltfläche **Weiter** aktiviert. Sie können also mit dem Paketbereitstellungsvorgang fortfahren.  
  
### Ziel auswählen  
 Klicken Sie, nachdem Sie die Paketquellen ausgewählt haben, auf die Schaltfläche **Weiter** , um auf die Seite **Ziel auswählen** zu wechseln. Pakete müssen an ein Projekt im SSIS-Katalog (SSISDB) bereitgestellt werden. Stellen Sie daher vor der Bereitstellung von Paketen sicher, dass das Zielprojekt bereits im SSIS-Katalog existiert. , erstellen Sie andernfalls ein leeres Projekt. Auf der Seite **Ziel auswählen** geben Sie den Namen des Servers in das Textfeld **Servername** ein, oder klicken Sie auf die Schaltfläche **Durchsuchen…** , um eine Serverinstanz auszuwählen. Klicken Sie dann auf die Schaltfläche **Durchsuchen…** neben dem Textfeld **Pfad** , um das Zielprojekt anzugeben. Klicken Sie auf **Neues Projekt…** , um ein leeres Projekt als Zielprojekt zu erstellen, falls das Projekt noch nicht existiert. Das Projekt **MUSS** unter einem Ordner erstellt werden.  
  
### Überprüfen und bereitstellen  
 Klicken Sie auf der Seite **Ziel auswählen** auf **Weiter** , um auf die Seite **Überprüfung** im **Bereitstellungs-Assistenten für Integration Services**zu wechseln. Auf der Seite zur Überprüfung können Sie sich den Bericht zur Bereitstellungsaktion ansehen. Klicken Sie nach der Überprüfung auf die Schaltfläche **Bereitstellen** , um die Bereitstellungsaktion auszuführen.  
  
### Ergebnisse  
 Nachdem die Bereitstellung abgeschlossen ist, sollten Sie die Seite **Ergebnisse** sehen. Auf der Seite **Ergebnisse** sehen Sie die Ergebnisse aus jedem Schritt des Bereitstellungsvorgangs. Klicken Sie auf der Seite **Ergebnisse** entweder auf **Bericht speichern** zum Speichern des Bereitstellungsberichts oder auf **Schließen** zum Schließen des Assistenten.  
  
## Siehe auch  
 [Bereitstellen von Projekten auf dem Integration Services-Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md)   
 [Bereitstellung von Projekten und Paketen](https://msdn.microsoft.com/library/hh213290.aspx)  
  
  