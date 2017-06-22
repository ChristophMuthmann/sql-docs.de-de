---
title: Dialogfeld Eigenschaftenseiten Projekt | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.rpt.rptdesigner.projectpropertypages.general.f1
helpviewer_keywords:
- Project Property Pages dialog box
ms.assetid: 209d9e22-37fc-418f-8739-83adcf447d3f
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 659be9982440426eee0d8b5a2df8d54b4d32bbc4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---

# <a name="project-property-pages-dialog-box"></a>Projekt (Eigenschaftenseiten, Dialogfeld)

  Mithilfe der Eigenschaftenseiten für Projekte können Sie Bereitstellungseigenschaften für ein Berichtsserverprojekt konfigurieren. So öffnen das Dialogfeld über das **Projekt** Menü klicken Sie auf  *\<Berichtsprojektname >***Eigenschaften**.  
  
 Nachdem Sie Konfigurationseigenschaften definiert haben, können Sie auf der Symbolleiste aus der Dropdownliste **Projektmappenkonfigurationen** eine Konfiguration auswählen.  

![ssrs_project_properties](../../reporting-services/reports/media/ssrs-project-properties.png)
  
## <a name="options"></a>enthalten  
 **Konfiguration**  
 Wählen Sie die zu bearbeitende Konfiguration aus. Anfangs sind folgende Konfigurationen verfügbar: **Debuggen**, **DebugLocal**und **Release**. Die aktive Konfiguration wird zuerst angezeigt, z.B. **Aktiv (Debuggen)**.  
  
 Um Eigenschaften für mehr als eine Konfiguration gleichzeitig anzuzeigen, wählen Sie **Alle Konfigurationen** oder **Mehrere Konfigurationen**aus.  
  
 Klicken Sie zum Erstellen weiterer Konfigurationen auf der Menüleiste auf **Konfigurations-Manager** .  
  
 **Konfigurations-Manager**  
 Verwalten Sie Konfigurationen für die gesamte Projektmappe, oder fügen Sie zusätzliche Konfigurationen hinzu. Weitere Informationen finden Sie in der Dokumentation zu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .  
  
 **OutputPath**  
 Sie können den Pfad zum Speichern der Berichtsdefinition, die in der Erstellungsüberprüfung, Bereitstellung und Berichtsvorschau verwendet wird, eingeben oder einfügen. Der Pfad muss sich von dem für das Projekt verwendeten Pfad und einem relativen Pfad unterscheiden, der einem untergeordneten Ordner des Projektpfads entspricht.  
  
> [!NOTE]  
>  Sie können mehrere Konfigurationen verwenden, um abhängig von der auszuführenden Aufgabe unter verschiedenen Pfaden zu wechseln.  
  
 **ErrorLevel**  
 Geben Sie den Schweregrad der Erstellungsprobleme ein, die als Fehler gemeldet werden. Probleme mit einem Schweregrad kleiner oder gleich dem Wert von **ErrorLevel** werden als Fehler gemeldet. Andernfalls werden die Probleme als Warnungen gemeldet. Jeder Fehler führt dazu, dass die Erstellung fehlschlägt. Die gültigen Schweregrade sind 0 bis einschließlich 4. Der Standardwert ist 2.  
  
 **StartItem**  
 Wählen Sie den Bericht aus, der nach der Veröffentlichung des Projekts auf dem Berichtsserver im Webbrowser oder beim Ausführen des Projekts auf dem lokalen Computer im Vorschaufenster angezeigt wird. Ein Startelement ist für Konfigurationen erforderlich, die das Projekt zwar erstellen, nicht jedoch bereitstellen sowie für die Verwendung des **Debug** -Befehls (**F5**). Dieser Schritt ist für Konfigurationen notwendig, die das Projekt bereitstellen.  
  
 **OverwriteDataSources**  
 Wählen Sie **TRUE** aus, um die Datenquelle auf dem Server mit der Datenquelle im Projekt zu überschreiben, wenn die Berichte veröffentlicht werden. Wählen Sie **False** aus, um die vorhandene Datenquelle auf dem Server zu belassen.  
  
 **TargetServerVersion**  
 Wählen Sie entweder die geeignete Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oder **Version erkennen** aus, um automatisch die Version zu ermitteln, die auf dem von der **TargetServer URL** -Eigenschaft angegebenen Server installiert ist. Der Standardwert ist **SQL Server 2016**.  
  
 **TargetDataSourceFolder**  
 Der Name des Ordners, in dem die veröffentlichten, freigegebenen Datenquellen gespeichert werden sollen. Wenn Sie keinen Ordner angeben, wird die Datenquelle im gleichen Ordner wie der Bericht veröffentlicht. Falls der Ordner nicht auf dem Berichtsserver vorhanden ist, erstellt der Berichts-Designer den Ordner, wenn die Berichte veröffentlicht werden.  
  
 Wenn Sie auf einem Berichtsserver veröffentlichen, der im einheitlichen Modus ausgeführt wird, geben Sie den vollständigen Pfad der Ordnerhierarchie mit Beginn beim Stamm an. Beispielsweise Folder1/Folder2/Folder3.  
  
 Wenn Sie auf einem Berichtsserver veröffentlichen, der im integrierten SharePoint-Modus ausgeführt wird, verwenden Sie eine URL zur SharePoint-Bibliothek. Beispiel: `http:\\<servername>\<site>\Documents\MyFolder`.  
  
 **TargetReportFolder**  
 Der Name des Ordners, in dem die veröffentlichten Berichte gespeichert werden sollen. Standardmäßig ist dies der Name des Berichtsprojekts. Falls der Ordner nicht auf dem Berichtsserver vorhanden ist, erstellt der Berichts-Designer den Ordner, wenn die Berichte veröffentlicht werden.  
  
 Wenn Sie auf einem Berichtsserver veröffentlichen, der im einheitlichen Modus ausgeführt wird, geben Sie den vollständigen Pfad der Ordnerhierarchie mit Beginn beim Stamm an. Wenn ein Ordner in einem anderen Ordner enthalten ist, geben Sie den Pfad zum Ordner mit Beginn beim Stamm an, wie beispielsweise Folder1/Folder2/Folder3.  
  
 Wenn Sie auf einem Berichtsserver veröffentlichen, der im integrierten SharePoint-Modus ausgeführt wird, verwenden Sie eine URL zur SharePoint-Bibliothek. Beispiel: `http:\\<servername>\\<site>\Documents\MyFolder`.  
  
 **TargetServerURL**  
 Die URL des Zielberichtsservers. Diese Eigenschaft müssen Sie vor dem Veröffentlichen eines Berichts auf eine gültige URL eines Berichtsservers festlegen.  
  
 Verwenden Sie die URL des virtuellen Verzeichnisses des Berichtsservers, wenn der Bericht auf einem Berichtsserver veröffentlicht wird, der im einheitlichen Modus ausgeführt wird. Beispiel: `http:\\<server>\reportserver`. Dies ist das virtuelle Verzeichnis des Berichtsservers, nicht des Berichts-Managers. Standardmäßig wird der Berichtsserver in dem virtuellen Verzeichnis "reportserver" installiert.  
  
 Verwenden Sie eine URL für eine SharePoint-Stammwebsite oder -Unterwebsite, wenn der Bericht auf einem Berichtsserver veröffentlicht wird, der im integrierten SharePoint-Modus ausgeführt wird. Wenn Sie keine Website angeben, wird die standardmäßige Stammwebsite verwendet. Beispiel: 
+ `http:\\<servername>`, 
+ `http:\\<servername\<site>` 
+ `http:\\<servername>\<site>\<subsite>`.  

## <a name="next-steps"></a>Nächste Schritte

[Veröffentlichen von Berichten](http://msdn.microsoft.com/library/ef5a514e-e818-4041-a8b0-15835f9a046b)   
[Veröffentlichen eines Berichts in einer SharePoint-Bibliothek](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
[Festlegen von Bereitstellungseigenschaften &#40; Reporting Services &#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[Berichts-Designer (F1-Hilfe)](../../reporting-services/tools/report-designer-f1-help.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
