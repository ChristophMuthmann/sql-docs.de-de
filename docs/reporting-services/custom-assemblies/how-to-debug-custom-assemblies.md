---
title: 'Vorgehensweise: Debuggen von benutzerdefinierten Assemblys | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e33f560106e99062e89ec10bbe84de65a360118f
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="how-to-debug-custom-assemblies"></a>Vorgehensweise: Debuggen von benutzerdefinierten Assemblys
  Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] stellt mehrere Tools zum Debuggen, die Sie unterstützen der Analyse von Code der benutzerdefinierten Assembly und Fehlersuche im. Das beste Tool zu verwenden, hängt davon ab, was Sie erreichen möchten. In diesem Beispiel wird [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]verwendet.  
  
 Am besten können Sie benutzerdefinierte Assemblys für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] entwerfen, entwickeln und testen, wenn Sie eine Projektmappe erstellen, die sowohl Ihre Testberichte als auch Ihre benutzerdefinierte Assembly enthält.  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>So debuggen Sie Assemblys mithilfe einer Instanz von Visual Studio  
  
1.  So legen Sie ein neues Berichtsmodellprojekt mithilfe von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] an.  
  
     Während Sie ein Berichtsprojekt erstellen, wird von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] auch eine Projektmappe für das Projekt angelegt.  
  
2.  Fügen Sie der vorhandenen Projektmappe ein neues Klassenbibliotheksprojekt hinzu. Stellen Sie sicher, dass das Berichtsprojekt als Startprojekt festgelegt wird. Weitere Informationen hierzu finden Sie in Ihrer [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]-Dokumentation.  
  
3.  Wählen Sie die Projektmappe im Projektmappen-Explorer aus.  
  
4.  Auf der **Ansicht** Menü klicken Sie auf **Eigenschaftenseiten**.  
  
     Die **-Eigenschaftenseiten** Dialogfeld wird geöffnet.  
  
5.  Erweitern Sie im linken Bereich **allgemeine Eigenschaften** bei Bedarf, und klicken Sie auf **Projektabhängigkeiten**. Wählen Sie das Berichtsprojekt aus der **Projekt** Dropdown-Liste. Wählen Sie das Assemblyprojekt in der **Abhängigkeiten** Liste.  
  
6.  Klicken Sie auf **OK** um die Änderungen zu speichern und schließen Sie die **Eigenschaftenseiten** Dialogfeld.  
  
7.  Wählen Sie im Projektmappen-Explorer Ihr benutzerdefiniertes Assemblyprojekt aus.  
  
8.  Auf der **Ansicht** Menü klicken Sie auf **Eigenschaftenseiten**.  
  
     Die **Projekteigenschaftenseiten** Dialogfeld wird geöffnet.  
  
9. Klicken Sie auf die **erstellen** Registerkarte, wenn Sie sich in einem C#-Projekt befinden oder die **Kompilieren** Registerkarte, wenn Sie sich an einem [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] Projekt.  
  
10. Auf der **erstellen**/**Kompilieren** Seite, geben Sie den Pfad zum Ordner Berichts-Designers. Dies ist standardmäßig c:\Programme\Microsoft c:\Programme\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE) in der **Ausgabepfad** Textfeld. Damit wird eine aktualisierte Version der benutzerdefinierten Assembly erstellt und direkt im Berichts-Designer bereitgestellt, bevor der Bericht ausgeführt wird.  
  
11. Wenn Sie den Bericht entworfen und die benutzerdefinierte Assembly entwickelt haben, legen Sie die Breakpoints im Code der benutzerdefinierten Assembly fest.  
  
12. Führen Sie den Bericht unter **DebugLocal** Modus durch Drücken der Taste F5. Wenn der Bericht in der Popup-Vorschau ausgeführt wird, sucht der Debugger alle Breakpoints, die dem ausführbaren Code in Ihrer Assembly entsprechen. Verwenden Sie F11, um den Code der benutzerdefinierten Assembly schrittweise zu durchlaufen.  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>So debuggen Sie Assemblys mithilfe von zwei Instanzen in Visual Studio  
  
1.  Starten Sie [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], und öffnen Sie das Projekt der benutzerdefinierten Assembly.  
  
2.  Erstellen Sie das Projekt, und stellen Sie die benutzerdefinierte Assembly und die dazugehörige PDB-Datei im Berichts-Designer bereit. Weitere Informationen zur Bereitstellung finden Sie unter [Bereitstellen einer benutzerdefinierten Assembly](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md).  
  
3.  Öffnen Sie ein Berichtsprojekt, das Ihre benutzerdefinierte Assembly verwendet, ohne den Code der benutzerdefinierten Assembly in einer anderen Instanz von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] zu schließen.  
  
4.  Wechseln Sie zur [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]-Instanz, die das Projekt für die benutzerdefinierte Assembly enthält, und legen Sie einige Breakpoints im Code fest.  
  
5.  Das Projekt der benutzerdefinierten Assembly noch immer das aktive Fenster, und klicken Sie auf **an den Prozess anhängen** auf die **Debuggen** Menü.  
  
     Die **an den Prozess anhängen** Dialogfeld wird geöffnet.  
  
6.  Aus der Liste der Prozesse, wählen Sie den Prozess devenv.exe, der dem Berichtsprojekt entspricht, und klicken Sie auf **Anfügen**.  
  
7.  Definieren Sie die Ausdrücke, die Sie im Bericht aus der benutzerdefinierten Assembly verwenden möchten, und entwerfen Sie Ihren Bericht.  
  
8.  Wenn Sie den Bericht entworfen werden, klicken Sie auf die **Vorschau** Registerkarte.  
  
     Der Bericht wird ausgeführt, und der Code der benutzerdefinierten Assembly sollte an den vordefinierten Breakpoints unterbrochen werden.  
  
    > [!NOTE]  
    >  Mithilfe der **Vorschau** Registerkarte erzwingt keine Codeberechtigungen für die Assembly. Für einen vollständigen Test, d. h. alle Fehler der Codezugriffssicherheit, starten Sie das Berichtsprojekt unter der **DebugLocal** -Konfigurationseinstellung.  
  
9. Gehen Sie den Code schrittweise mit der F11-Taste durch. Weitere Informationen zum Debuggen mit [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], finden Sie unter der [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Dokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden benutzerdefinierter Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
