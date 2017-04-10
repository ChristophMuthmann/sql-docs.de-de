---
title: "Kopieren eines Pakets in SQL Server-Datentools | Microsoft Docs"
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
  - "Pakete [Integration Services], kopieren"
  - "Kopieren von Paketen"
  - "Neugenerieren von Paket-GUIDs"
  - "Aktualisieren von Paketeigenschaften"
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Kopieren eines Pakets in SQL Server-Datentools
  In diesem Thema wird beschrieben, wie Sie ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Paket durch Kopieren eines vorhandenen Pakets erstellen und wie Sie die Eigenschaften **Name** und **GUID** des neuen Pakets aktualisieren.  
  
### So kopieren Sie ein Paket  
  
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
  
## Siehe auch  
 [Speichern einer Kopie eines Pakets](../Topic/Save%20a%20Copy%20of%20a%20Package.md)   
 [Erstellen von Paketen in SQL Server-Datentools](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integration Services-Pakete &#40;SSIS&#41;](../integration-services/integration-services-ssis-packages.md)  
  
  