---
title: 'Schritt 4: Hinzufügen eines Datenflusstasks zum Paket | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ac7ed52b1ecd8db03b0515cdd112da119d1ea73e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="lesson-1-4---adding-a-data-flow-task-to-the-package"></a>Lektion 1-4: Hinzufügen eines Datenflusstasks zum Paket
Nach dem Erstellen des Verbindungs-Managers für die Quell- und Zieldaten besteht die nächste Aufgabe im Hinzufügen eines Datenflusstasks zu Ihrem Paket. Der Datenflusstask kapselt das Datenflussmodul, von dem Daten zwischen Quellen und Zielen verschoben werden, und bietet die Funktionalität für das Transformieren, das Cleanup und das Ändern von Daten beim Verschieben. Im Datenflusstask wird der Hauptteil eines ETL-Prozesses (Extract, Transform, Load - Extrahieren, Transformieren, Laden) durchgeführt.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Trennt den Datenfluss von der Ablaufsteuerung.  
  
### <a name="to-add-a-data-flow-task"></a>So fügen Sie einen Datenflusstask hinzu  
  
1.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
2.  Erweitern Sie in der **SSIS-Toolbox**die Option **Favoriten**, und ziehen Sie anschließend einen **Datenflusstask** auf die Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** .  
  
    > [!NOTE]  
    > Wenn die SSIS-Toolbox nicht verfügbar ist, wählen Sie im Hauptmenü SSIS und dann SSIS-Toolbox aus, um die SSIS-Toolbox anzuzeigen.  
  
3.  Klicken Sie auf der **Ablaufsteuerung** -Entwurfsoberfläche mit der rechten Maustaste auf den neu hinzugefügten **Datenflusstask**, klicken Sie auf **Umbenennen**, und ändern Sie den Namen zu **Extract Sample Currency Data**.  
  
    Es empfiehlt sich, eindeutige Namen für alle Komponenten bereitzustellen, die Sie einer Entwurfsoberfläche hinzufügen. Aus Gründen der Benutzer- und Wartungsfreundlichkeit sollten die Namen die Funktion beschreiben, die jede Komponente ausführt. Das Befolgen dieser Namensrichtlinien ermöglicht die Selbstdokumentierung Ihrer [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakete. Eine andere Möglichkeit zur Dokumentation Ihrer Pakete besteht im Verwenden von Anmerkungen. Weitere Informationen zum Verwenden von Anmerkungen finden Sie unter [Verwenden von Anmerkungen in Paketen](../integration-services/use-annotations-in-packages.md).  
  
4.  Klicken Sie mit der rechten Maustaste auf den Datenflusstask, klicken Sie auf **Eigenschaften**, und prüfen Sie im Eigenschaftenfenster, ob die **LocaleID** -Eigenschaft auf **Englisch (USA)** festgelegt ist.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Schritt 5: Hinzufügen und Konfigurieren der Flatfilequelle](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Datenflusstask](../integration-services/control-flow/data-flow-task.md)  
  
  
  
