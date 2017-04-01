---
title: "Erstellen eines Bereitstellungs-Hilfsprogramms | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Bereitstellen von Paketen [Integration Services], Bereitstellungshilfsprogramm"
  - "Bereitstellungshilfsprogramm [Integration Services]"
ms.assetid: 354322a4-ae8c-4d92-8e71-42d29dbd0614
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Erstellen eines Bereitstellungs-Hilfsprogramms
  Der erste Schritt beim Bereitstellen von Paketen besteht im Erstellen eines Bereitstellungshilfsprogramms für ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt. Das Bereitstellungshilfsprogramm ist ein Ordner, der die Dateien enthält, die Sie zum Bereitstellen der in einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt enthaltenen Pakete auf einem anderen Server benötigen. Das Bereitstellungshilfsprogramm wird auf dem Computer erstellt, auf dem das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt gespeichert ist.  
  
 Sie erstellen ein Paketbereitstellungshilfsprogramm für ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt, indem Sie zuerst den Erstellungsprozess konfigurieren, mit dem ein Bereitstellungshilfsprogramm erstellt wird, und anschließend das Projekt erstellen. Wenn Sie das Projekt erstellen, werden alle Pakete und Paketkonfigurationen aus dem Projekt automatisch einbezogen. Wenn Sie zusammen mit dem Projekt zusätzliche Dateien – wie z. B. eine Readme-Datei – bereitstellen möchten, müssen Sie die Dateien in den **Miscellaneous** -Ordner des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts kopieren. Beim Erstellen des Projekts werden diese Dateien dann automatisch einbezogen.  
  
 Sie können jede Projektbereitstellung unterschiedlich konfigurieren. Bevor Sie das Projekt erstellen und das Paketbereitstellungshilfsprogramm erstellen, können Sie die Eigenschaften des Bereitstellungshilfsprogramms festlegen, um die Bereitstellung der im Projekt enthaltenen Pakete anzupassen. So können Sie z. B. angeben, ob die Paketkonfigurationen aktualisiert werden können, wenn das Projekt bereitgestellt wird. Zum Zugreifen auf die Eigenschaften eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekts klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Eigenschaften**.  
  
 In der folgenden Tabelle sind die Eigenschaften des Bereitstellungshilfsprogramms aufgeführt.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|AllowConfigurationChange|Ein Wert, der angibt, ob Konfigurationen während der Bereitstellung aktualisiert werden können.|  
|CreateDeploymentUtility|Ein Wert, der angibt, ob beim Erstellen des Projekts ein Paketbereitstellungshilfsprogramm erstellt wird. Diese Eigenschaft muss auf **True** festgelegt sein, um ein Bereitstellungshilfsprogramm zu erstellen.|  
|DeploymentOutputPath|Der Speicherort des Bereitstellungshilfsprogramms, relativ zur Position des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts.|  
  
 Wenn Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekt erstellen, wird eine Manifestdatei mit dem Namen „\<Projektname>.SSISDeploymentManifest.xml“ erstellt und zusammen mit Kopien der Projektpakete und Paketabhängigkeiten in den „bin\Deployment“-Ordner des Projekts oder zum Speicherort kopiert, der in der DeploymentOutputPath-Eigenschaft angegeben ist. Diese Manifestdatei enthält eine Auflistung der Pakete, der Paketkonfigurationen und aller sonstigen Dateien, die im Projekt enthalten sind.  
  
 Der Inhalt des Bereitstellungsordners wird bei jedem Erstellen des Projekts aktualisiert. Das bedeutet, dass alle in diesem Ordner gespeicherten Dateien, die durch den Erstellungsprozess nicht erneut in den Ordner kopiert werden, gelöscht werden. Beispielsweise werden die in den Bereitstellungsordnern gespeicherten Paketkonfigurationsdateien gelöscht.  
  
### So erstellen Sie ein Paketbereitstellungshilfsprogramm  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]die Projektmappe, die das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt enthält, für das ein Paketbereitstellungshilfsprogramm erstellt werden soll.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **\<Projektname>-Eigenschaftenseiten** auf **Bereitstellungshilfsprogramm**.  
  
4.  Wenn die Paketkonfigurationen beim Bereitstellen der Pakete aktualisiert werden sollen, legen Sie **AllowConfigurationChanges** auf **True**fest.  
  
5.  Legen Sie **CreateDeploymentUtility** auf **True**fest.  
  
6.  Aktualisieren Sie bei Bedarf den Speicherort des Bereitstellungshilfsprogramms, in dem Sie die **DeploymentOutputPath** -Eigenschaft ändern.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Erstellen**.  
  
9. Im **Ausgabe** -Fenster können Sie den Erstellungsprozess verfolgen, in dem auch Fehler bei der Erstellung angezeigt werden.  
  
## Siehe auch  
 [Paketkonfigurationen](../../integration-services/packages/package-configurations.md)   
 [Erstellen von Paketkonfigurationen](../../integration-services/packages/create-package-configurations.md)   
 [Bereitstellen von Paketen mithilfe des Bereitstellungshilfsprogramms](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)   
 [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)  
  
  