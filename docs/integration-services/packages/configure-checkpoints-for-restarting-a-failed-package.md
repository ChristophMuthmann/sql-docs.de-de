---
title: "Konfigurieren von Pr&#252;fpunkten zum erneuten Starten eines fehlerhaften Pakets | Microsoft Docs"
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
  - "Prüfpunkte [Integration Services]"
  - "Neustarten von Paketen"
  - "Starten von Paketen"
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Konfigurieren von Pr&#252;fpunkten zum erneuten Starten eines fehlerhaften Pakets
  Sie können ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket so konfigurieren, dass nicht das gesamte Paket erneut ausgeführt wird, sondern ab dem Punkt, an dem ein Fehler auftrat. Hierzu legen Sie die Eigenschaften fest, die für Prüfpunkte gelten.  
  
### So konfigurieren Sie den Neustart eines Pakets  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, das Sie konfigurieren möchten.  
  
2.  Doppelklicken Sie im **Projektmappen-Explorer** auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie mit der rechten Maustaste an einer beliebigen Stelle im Hintergrund der Entwurfsoberfläche der Ablaufsteuerung, und klicken Sie anschließend auf **Eigenschaften**.  
  
5.  Legen Sie die SaveCheckpoints-Eigenschaft auf **TRUE** fest.  
  
6.  Geben Sie den Namen der Prüfpunktdatei in die CheckpointFileName-Eigenschaft ein.  
  
7.  Legen Sie die CheckpointUsage-Eigenschaft auf einen der beiden Werte fest:  
  
    -   Wählen Sie **Always** aus, damit das Paket immer am Prüfpunkt neu gestartet wird.  
  
        > [!IMPORTANT]  
        >  Falls die Prüfpunktdatei nicht verfügbar ist, tritt ein Fehler auf.  
  
    -   Wählen Sie **IfExists** aus, damit das Paket nur neu gestartet wird, wenn die Prüfpunktdatei verfügbar ist.  
  
8.  Konfigurieren Sie die Tasks und Container, von denen das Paket neu gestartet werden kann.  
  
    -   Klicken Sie mit der rechten Maustaste auf einen Task oder Container, und klicken Sie anschließend auf **Eigenschaften**.  
  
    -   Legen Sie die FailPackageOnFailure-Eigenschaft auf **TRUE** für alle ausgewählten Tasks und Container fest.  
  
## Siehe auch  
 [Neustarten von Paketen mit Prüfpunkten](../../integration-services/packages/restart-packages-by-using-checkpoints.md)  
  
  