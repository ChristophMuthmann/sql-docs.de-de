---
title: Verwenden von Anmerkungen in Paketen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- self-documenting packages
- adding annotations
- annotations [Integration Services]
ms.assetid: 48c8ed9a-b10d-490c-9ba7-4b77aa44e3dd
caps.latest.revision: "42"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d8e14bc3f81769d437e3d916f74128f96fe0bec
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="use-annotations-in-packages"></a>Verwenden von Anmerkungen in Paketen
  Der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer stellt Anmerkungen bereit, damit Pakete selbsterklärend und leichter zu verstehen und zu verwalten sind. Anmerkungen können der Ablaufsteuerung, dem Datenfluss und Ereignishandler-Entwurfsoberflächen des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers hinzugefügt werden. Anmerkungen können eine beliebige Art von Text enthalten. Sie sind hilfreich, um einem Paket Bezeichnungen, Hinweise und sonstige beschreibende Informationen hinzuzufügen. Anmerkungen sind eine reine Entwurfszeitfunktion. Beispielsweise werden sie nicht in Protokolle geschrieben.  
  
 Wenn Sie die EINGABETASTE drücken, wird der Text in die nächste Zeile umbrochen. Das Anmerkungsfeld wird automatisch vergrößert, wenn Sie weitere Textzeilen hinzufügen. Paketanmerkungen werden als Klartext im CDATA-Abschnitt der Paketdatei beibehalten.  
  
 Weitere Informationen zu Änderungen am Format der Paketdatei finden Sie unter [SSIS-Paketformat](http://msdn.microsoft.com/library/cfe0e5dc-5be3-4222-b721-fe83665edd94).  
  
 Wenn Sie ein Paket speichern, speichert der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer die Anmerkungen im Paket.  
  
## <a name="add-an-annotation-to-a-package"></a>Hinzufügen einer Anmerkung zu einem Paket  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, dem Sie eine Anmerkung hinzufügen möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer mit der rechten Maustaste auf eine beliebige Stelle in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung**, **Datenfluss**oder **Ereignishandler** , und klicken Sie dann auf **Anmerkung hinzufügen**. In der Entwurfsoberfläche der Registerkarte wird ein Textblock angezeigt.  
  
4.  Fügen Sie Text hinzu.  
  
    > [!NOTE]  
    >  Falls Sie keinen Text hinzufügen, wird der Textblock entfernt, wenn Sie außerhalb des Blockes klicken.  
  
5.  Wenn Sie die Größe oder das Format des Anmerkungstexts ändern möchten, klicken Sie mit der rechten Maustaste auf die Anmerkung, und klicken Sie dann auf **Schriftart für Textanmerkungen**festlegen.  
  
6.  Drücken Sie die EINGABETASTE; um eine zusätzliche Textzeile hinzuzufügen.  
  
     Das Anmerkungsfeld wird automatisch vergrößert, wenn Sie weitere Textzeilen hinzufügen.  
  
7.  Wenn Sie eine Anmerkung einer Gruppe hinzufügen möchten, klicken Sie mit der rechten Maustaste auf die Anmerkung, und klicken Sie dann auf **Gruppe**.  
  
8.  Klicken Sie im Menü **Datei** auf **Alle Speichern**, um das aktualisierte Paket zu speichern.  
