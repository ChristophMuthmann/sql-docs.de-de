---
title: 'Schritt 1: Erstellen von Arbeitsordnern und Umgebungsvariablen | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: de69cfa9d63daa6cd5638774aba2540fd2ffdbaa
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-1---creating-working-folders-and-environment-variables"></a>Lektion 1: 1-Erstellen von Arbeitsordnern und Umgebungsvariablen
In dieser Aufgabe erstellen Sie den Arbeitsordner (C:\DeploymentTutorial) und die neuen Systemumgebungsvariablen (`DataTransfer` und `LoadXMLData`), die in späteren Lernprogrammaufgaben verwendet werden.  
  
Der Arbeitsordner befindet sich im Stamm von Laufwerk C. Bei Bedarf können Sie ein anderes Laufwerk bzw. einen anderen Speicherort verwenden. Sie müssen sich diesen Speicherort jedoch notieren und immer dann verwenden, wenn im Lernprogramm auf den Speicherort des Arbeitsordners DeploymentTutorial verwiesen wird.  
  
In einer späteren Lektion stellen Sie Pakete bereit, die im Dateisystem in der sysssispackages-Tabelle der msdb-Datenbank von[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gespeichert werden. Idealerweise erfolgt die Bereitstellung der [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakete auf einem anderen Computer. Falls dies nicht möglich ist, können Sie dennoch viel von diesem Lernprogramm profitieren, indem Sie die Pakete auf einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf dem lokalen Computer bereitstellen. Die Umgebungsvariablen, die auf dem lokalen Computer und dem Zielcomputer verwendet werden, weisen die gleichen Variablennamen auf, doch werden unterschiedliche Werte in den Variablen gespeichert. So verweist z. B. der Wert der `DataTransfer` -Umgebungsvariablen auf dem lokalen Computer auf den Ordner C:\DeploymentTutorial, während die `DataTransfer` -Umgebungsvariable auf dem Zielcomputer auf den Ordner C:\DeploymentTutorialInstall verweist.  
  
Wenn Sie eine Bereitstellung auf dem lokalen Computer planen, müssen Sie nur einen Satz von Umgebungsvariablen erstellen. Es ist jedoch erforderlich, den Wert der Umgebungsvariablen vor der lokalen Bereitstellung auf einen geeigneten Wert zu aktualisieren.  
  
Wenn Sie planen, die Pakete auf einem anderen Computer bereitzustellen, müssen Sie zwei Sätze von Umgebungsvariablen erstellen: einen Satz für den lokalen Computer und einen Satz für den Zielcomputer. Zum jetzigen Zeitpunkt können Sie nur die Variablen für den Quellcomputer erstellen. Die Variablen für den Zielcomputer müssen später erstellt werden. Sie können die Pakete jedoch erst auf dem Zielcomputer installieren, wenn sowohl der Ordner als auch die Umgebungsvariablen auf dem Zielcomputer verfügbar sind.  
  
### <a name="to-create-the-local-working-folder"></a>So erstellen Sie den lokalen Arbeitsordner  
  
1.  Klicken Sie mit der rechten Maustaste auf das Menü Start, und klicken Sie dann auf Suchen.  
  
2.  Klicken Sie auf **Lokaler Datenträger (C:)**.  
  
3.  Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie anschließend auf **Ordner**.  
  
4.  Benennen Sie den neuen Ordner in **DeploymentTutorial**um.  
  
### <a name="to-create-local-environment-variables"></a>So erstellen Sie lokale Umgebungsvariablen  
  
1.  Klicken Sie im Menü **Start** auf **Systemsteuerung**.  
  
2.  Doppelklicken Sie in der Systemsteuerung auf **System**.  
  
3.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf die Registerkarte **Erweitert** , und klicken Sie dann auf **Umgebungsvariablen**.  
  
4.  Klicken Sie im Dialogfeld **Umgebungsvariablen** im Bereich **Systemvariablen** auf **Neu**.  
  
5.  Geben Sie im Dialogfeld **Neue Systemvariable** den Namen **DataTransfer** im Feld **Variablenname** und den Wert **C:\DeploymentTutorial\datatransferconfig.dtsconfig** im Feld **Variablenwert** ein.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Klicken Sie erneut auf **Neu** , und geben Sie **LoadXMLData** im Feld **Variablenname** und **C:\DeploymentTutorial\loadxmldataconfig.dtsconfig** im Feld **Variablenwert** ein.  
  
8.  Klicken Sie auf **OK** , um das Dialogfeld **Umgebungsvariablen** zu beenden.  
  
9. Klicken Sie auf **OK** , um das Dialogfeld **Systemeigenschaften** zu beenden.  
  
10. Führen Sie optional einen Neustart des Computers aus. Wenn Sie den Computer nicht neu starten, wird der Name der neuen Variablen nicht im Paketkonfigurations-Assistenten angezeigt, kann jedoch verwendet werden.  
  
### <a name="to-create-destination-environment-variables"></a>So erstellen Sie Zielumgebungsvariablen  
  
1.  Klicken Sie im Menü **Start** auf **Systemsteuerung**.  
  
2.  Doppelklicken Sie in der Systemsteuerung auf **System**.  
  
3.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf die Registerkarte **Erweitert** , und klicken Sie dann auf **Umgebungsvariablen**.  
  
4.  Klicken Sie im Dialogfeld **Umgebungsvariablen** unter **Systemvariablen** auf **Neu**.  
  
5.  Geben Sie im Dialogfeld **Neue Systemvariable** den Namen **DataTransfer** im Feld **Variablenname** und den Wert **C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig** im Feld **Variablenwert** ein.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Klicken Sie erneut auf **Neu** , und geben Sie **LoadXMLData** im Feld **Variablenname** und **C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig** im Feld **Variablenwert** ein.  
  
8.  Klicken Sie auf **OK** , um das Dialogfeld **Umgebungsvariablen** zu beenden.  
  
9. Klicken Sie auf **OK** , um das Dialogfeld **Systemeigenschaften** zu beenden.  
  
10. Führen Sie optional einen Neustart des Computers aus.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Schritt 2: Erstellen des Bereitstellungsprojekts](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
  
  

