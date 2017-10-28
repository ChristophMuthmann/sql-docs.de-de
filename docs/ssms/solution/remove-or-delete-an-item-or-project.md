---
title: "Entfernen oder Löschen eines Elements oder Projekts| Microsoft-Dokumente"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b09e3ba21b75c91b4ceb5deb70379d60b644e49d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="remove-or-delete-an-item-or-project"></a>Entfernen oder Löschen eines Elements oder Projekts
Projektelemente in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]-Projekten sind Abfragen, Verbindungen und sonstige Dateien. Sie können Projektabfragen und sonstige Dateien aus der Projektmappe löschen, ohne die Dateien aus dem Speicher zu löschen. Entfernen Sie ein Projekt oder Element, wenn es in der aktuellen Projektmappe nicht nützlich ist und in eine andere Projektmappe eingefügt werden soll.  
  
### <a name="to-remove-a-project-item"></a>So entfernen Sie ein Projektelement  
  
1.  Wählen Sie im Projektmappen-Explorer das Projektelement aus, das Sie entfernen möchten.  
  
2.  Klicken Sie im Menü **Bearbeiten** auf **Entfernen**.  
  
3.  Klicken Sie im Bestätigungsdialogfeld auf **Entfernen** , um das Element aus dem Projekt zu entfernen.  
  
Ein entferntes Element ist weiterhin im Dateisystem vorhanden. Deshalb können Sie ein entferntes Element wieder zu seiner ursprünglichen oder zu einer anderen Projektmappe hinzufügen.  
  
#### <a name="to-remove-a-project"></a>So entfernen Sie ein Projekt  
  
1.  Wählen Sie im Projektmappen-Explorer das Projekt aus, das Sie entfernen möchten.  
  
2.  Klicken Sie im Menü **Bearbeiten** auf **Entfernen**.  
  
3.  Klicken Sie im Bestätigungsdialogfeld auf **OK**, um das Projekt aus der Projektmappe zu entfernen.  
  
Sie können ein Projekt dauerhaft löschen, müssen jedoch zuerst alle Verweise auf das Projekt aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] -Projektmappen entfernen und dann die zugeordneten Dateien mithilfe von [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Explorer dauerhaft aus dem Speicher löschen.  
  
#### <a name="to-delete-a-project"></a>So löschen Sie ein Projekt  
  
1.  Entfernen Sie im Projektmappen-Explorer das Projekt, das Sie löschen möchten, aus der Projektmappe.  
  
2.  Suchen und markieren Sie in Windows Explorer die Dateien, die dem zu löschenden Projekt oder Element zugeordnet sind.  
  
3.  Klicken Sie im Menü **Datei** auf **Löschen**.  
  
## <a name="see-also"></a>Siehe auch  
[Projektmappen-Explorer](../../ssms/solution/solution-explorer.md)  
[Hinzufügen neuer Elemente zu einem Projekt](../../ssms/solution/add-new-items-to-a-project.md)  
[Hinzufügen vorhandener Elemente zu einem Projekt](../../ssms/solution/add-existing-items-to-a-project.md)  
  

