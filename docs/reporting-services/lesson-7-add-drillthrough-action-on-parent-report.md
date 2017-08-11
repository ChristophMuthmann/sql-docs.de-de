---
title: "Lektion 7: Hinzufügen einer Drillthroughaktion für den übergeordneten Bericht | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: aad2da1a-d7b1-4afa-a66a-1ff102e8306f
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9a9790c4afc44e66c521005a3556f8082527d260
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-7-add-drillthrough-action-on-parent-report"></a>Lektion 7: Hinzufügen einer Drillthroughaktion für den übergeordneten Bericht
Nachdem Sie der Websiteanwendung ein ReportViewer-Steuerelement hinzugefügt haben, fügen Sie im nächsten Schritt eine Drillthroughaktion für den übergeordneten Bericht hinzu.  
  
### <a name="to-add-drillthrough-action-on-the-parent-report"></a>So fügen Sie eine Drillthroughaktion für den übergeordneten Bericht hinzu  
  
1.  Wechseln Sie zum übergeordneten Bericht.  
  
2.  Wählen Sie das Textfeld mit dem Wert **Name**.  
  
3.  Klicken Sie mit der rechten Maustaste auf das Textfeld, und wählen Sie anschließend **Textfeldeigenschaften**aus.  
  
4.  Wechseln Sie zur Registerkarte **Aktion** , und wählen Sie die Option **Gehe zu Bericht** aus.  
  
5.  Geben Sie den Namen des untergeordneten Berichts im Abschnitt **Bericht angeben** ein.  
  
    > [!NOTE]
    > Die Erweiterung für den Namen des Berichts darf nicht enthalten sein.  
  
6.  Wählen Sie im Abschnitt **Diese Parameter zum Ausführen des Berichts verwenden** die Option **Hinzufügen** .  
  
7.  Geben Sie im Feld **Name** den Namen **productid** ein und wählen Sie in der Dropdownliste **Wert** die Option **ProductID** .  
  
8.  Wählen Sie **OK** , um den Vorgang abzuschließen.  
  
## <a name="next-task"></a>Nächste Aufgabe  
Sie haben dem übergeordneten Bericht erfolgreich eine Drillthroughaktion hinzugefügt. Anschließend erstellen Sie einen Datenfilter für die Datentabelle, die für den untergeordneten Bericht definiert wurde. Siehe [Lektion 8: Erstellen eines Datenfilters](../reporting-services/lesson-8-create-a-data-filter.md).  
  
  
  


