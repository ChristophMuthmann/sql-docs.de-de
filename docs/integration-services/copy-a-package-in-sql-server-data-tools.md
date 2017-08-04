---
title: Kopieren eines Pakets in SQL Server Datatools | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 59a001e0aa360183e5e393faedc613cfabda0f02
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="copy-a-package-in-sql-server-data-tools"></a>Kopieren eines Pakets in SQL Server-Datentools
  In diesem Thema wird beschrieben, wie Sie ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket durch Kopieren eines vorhandenen Pakets erstellen und wie Sie die Eigenschaften **Name** und **GUID** des neuen Pakets aktualisieren.  
  
### <a name="to-copy-a-package"></a>So kopieren Sie ein Paket  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, das Sie kopieren möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket.  
  
3.  Stellen Sie entweder sicher, dass das zu kopierende Paket im Projektmappen-Explorer ausgewählt ist oder dass die Registerkarte im SSIS-Designer, in dem das Paket enthalten ist, aktiviert ist.  
  
4.  Auf der **Datei** Menü klicken Sie auf **speichern \<Paketname > als**.  
  
    > [!NOTE]  
    >  Das Paket muss im SSIS-Designer geöffnet sein, bevor im Menü **Datei** die Option **Speichern unter** angezeigt wird.  
  
5.  Suchen Sie optional nach einem anderen Ordner.  
  
6.  Aktualisieren Sie den Namen der Paketdatei. Stellen Sie sicher, dass die Dateierweiterung DTSX beibehalten wird.  
  
7.  Klicken Sie auf **Speichern**.  
  
8.  Wählen Sie an der Eingabeaufforderung aus, ob der Name des Paketobjekts zur Übereinstimmung mit dem Dateinamen aktualisiert werden soll. Wenn Sie auf **Ja**klicken, wird die **Name** -Eigenschaft des Pakets aktualisiert. Das neue Paket wird dem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt hinzugefügt und im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer geöffnet.  
  
9. Klicken Sie optional in den Hintergrund der Registerkarte **Ablaufsteuerung** , und klicken Sie auf **Eigenschaften**.  
  
10. Klicken Sie im Fenster Eigenschaften auf den Wert der ID-Eigenschaft, und klicken Sie dann in der Dropdownliste auf  **\<neue ID generieren >**.  
  
11. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das neue Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Speichern einer Kopie eines Pakets](http://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [Erstellen von Paketen in SQL Server Datatools](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integrationsservices &#40; SSIS &#41; Pakete](../integration-services/integration-services-ssis-packages.md)  
  
  
