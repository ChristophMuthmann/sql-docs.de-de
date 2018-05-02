---
title: Projektversionen (Dialogfeld) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: service
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84554c1ac7da7fedfdde85b0127c0c3e84c4eccc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="project-versions-dialog-box"></a>Projektversionen (Dialogfeld)
  Verwenden Sie das Dialogfeld **Projektversionen** , um Versionen eines Projekts anzuzeigen und eine frühere Version wiederherzustellen.  
  
 Sie können frühere Versionen auch in der Sicht [catalog.object_versions &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md) anzeigen und die gespeicherte Prozedur [catalog.restore_project &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md) verwenden, um frühere Versionen wiederherzustellen.  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Dialogfelds "Projektversionen"](#open_dialog)  
  
-   [Wiederherstellen einer Projektversion](#restore)  
  
##  <a name="open_dialog"></a> Öffnen des Dialogfelds "Projektversionen"  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server her.  
  
     Dies bedeutet, dass eine Verbindung mit der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz hergestellt werden muss, die als Host für die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datenbank fungiert.  
  
2.  Erweitern Sie im Objekt-Explorer die Struktur, um den Knoten **Integration Services-Kataloge** anzuzeigen.  
  
3.  Erweitern Sie den Knoten **Integration Services-Kataloge** , um den Knoten **SSISDB** anzuzeigen.  
  
4.  Der **SSISDB** -Knoten enthält einen oder mehrere Ordner, wovon jeder ein oder mehrere Projekte enthält. Erweitern Sie den Ordner, der das gewünschte Projekt enthält.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Versionen**.  
  
 Im Dialogfeld **Projektversionen** wird in der Tabelle **Versionen** die Liste der Versionen des Projekts angezeigt, die auf dem Server bereitgestellt wurden, und zwar mit Bereitstellungsdatum und -zeit der Version, Wiederherstellungsdatum und -zeit der Version (wenn eine Wiederherstellung stattgefunden hat), der Versionsbeschreibung und einem Versionsbezeichner. Die derzeit aktive Version wird durch ein Häkchen in der **aktuellen** Spalte der Tabelle angegeben.  
  
##  <a name="restore"></a> Wiederherstellen einer Projektversion  
 Um eine frühere Version eines Projekts wiederherzustellen, wählen Sie die Version in der Tabelle **Versionen** aus, und klicken Sie dann auf **Ausgewählte Version wiederherstellen**. Das Projekt wird in der ausgewählten Version wiederhergestellt, und diese Version wird mit einem Häkchen in der **aktuellen** Spalte der Tabelle **Versionen** angegeben.  
  
  
