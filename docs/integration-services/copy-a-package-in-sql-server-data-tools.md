---
title: Kopieren eines Pakets in SQL Server Data Tools | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5fa5c5a4783c2573500932b7c5838aa6af96abd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>Kopieren eines Pakets in SQL Server-Datentools
  In diesem Thema wird beschrieben, wie Sie ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket durch Kopieren eines vorhandenen Pakets erstellen und wie Sie die Eigenschaften **Name** und **GUID** des neuen Pakets aktualisieren.  
  
### <a name="to-copy-a-package"></a>So kopieren Sie ein Paket  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, das Sie kopieren möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket.  
  
3.  Stellen Sie entweder sicher, dass das zu kopierende Paket im Projektmappen-Explorer ausgewählt ist oder dass die Registerkarte im SSIS-Designer, in dem das Paket enthalten ist, aktiviert ist.  
  
4.  Klicken Sie im Menü **Datei** auf **\<Paketname> speichern unter**.  
  
    > [!NOTE]  
    >  Das Paket muss im SSIS-Designer geöffnet sein, bevor im Menü **Datei** die Option **Speichern unter** angezeigt wird.  
  
5.  Suchen Sie optional nach einem anderen Ordner.  
  
6.  Aktualisieren Sie den Namen der Paketdatei. Stellen Sie sicher, dass die Dateierweiterung DTSX beibehalten wird.  
  
7.  Klicken Sie auf **Speichern**.  
  
8.  Wählen Sie an der Eingabeaufforderung aus, ob der Name des Paketobjekts zur Übereinstimmung mit dem Dateinamen aktualisiert werden soll. Wenn Sie auf **Ja**klicken, wird die **Name** -Eigenschaft des Pakets aktualisiert. Das neue Paket wird dem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt hinzugefügt und im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer geöffnet.  
  
9. Klicken Sie optional in den Hintergrund der Registerkarte **Ablaufsteuerung** , und klicken Sie auf **Eigenschaften**.  
  
10. Klicken Sie im Eigenschaftenfenster auf den Wert der ID-Eigenschaft, und klicken Sie anschließend in der Dropdownliste auf **\<Neue ID generieren>**.  
  
11. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das neue Paket zu speichern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Speichern einer Kopie eines Pakets](http://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [Erstellen von Paketen in SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40;SSIS&#41; Packages](../integration-services/integration-services-ssis-packages.md) (Integration Services-Pakete [SSIS])  
  
  
