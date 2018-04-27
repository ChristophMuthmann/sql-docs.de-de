---
title: Hinzufügen oder Löschen einer Komponente im Datenfluss | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- adding components
- components [Integration Services], data flow
ms.assetid: d99124f9-0994-4f40-a48e-fdca6a4383e7
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d909806c8d1f45c546dc19325b647a67d0bced6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="add-or-delete-a-component-in-a-data-flow"></a>Hinzufügen oder Löschen einer Komponente im Datenfluss
  Bei Datenflusskomponenten handelt es sich um Quellen, Ziele und Transformationen in einem Datenfluss. Bevor Sie einem Datenfluss Komponenten hinzufügen können, muss die Ablaufsteuerung im Paket einen Datenflusstask einschließen.  
  
 Im Folgenden wird beschrieben, wie eine Komponente zum Datenfluss eines Pakets hinzugefügt oder in diesem gelöscht wird.  
  
### <a name="to-add-a-component-to-a-data-flow"></a>So fügen Sie einem Datenfluss eine Komponente hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** , und doppelklicken Sie dann auf den Datenflusstask, der den Datenfluss enthält, dem Sie eine Komponente hinzufügen möchten.  
  
4.  Erweitern Sie in der Toolbox **Datenflussquellen**, **Datenflusstransformationen**oder **Datenflussziele**, und ziehen Sie ein Datenflusselement auf die Entwurfsoberfläche der Registerkarte **Datenfluss** .  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
### <a name="to-delete-a-component-from-a-data-flow"></a>So löschen Sie eine Komponente aus einem Datenfluss  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** , und doppelklicken Sie dann auf den Datenflusstask, der den Datenfluss enthält, in dem Sie eine Komponente löschen möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Datenflusskomponente, und klicken Sie dann auf **Löschen**.  
  
5.  Bestätigen Sie den Löschvorgang.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verbinden von Komponenten in einem Datenfluss](../../integration-services/data-flow/connect-components-in-a-data-flow.md)   
 [Debuggen des Datenflusses](../../integration-services/troubleshooting/debugging-data-flow.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  
