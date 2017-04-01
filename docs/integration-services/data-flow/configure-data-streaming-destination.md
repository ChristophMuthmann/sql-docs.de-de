---
title: "Konfigurieren des Datenstreamingziels | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1"
ms.assetid: bcdbb833-20c8-47ff-a641-bb517f9a1af3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Konfigurieren des Datenstreamingziels
  Konfigurieren Sie das Datenstreamingziel mithilfe des Dialogfelds **Erweiterter Editor für das Datenstreamingziel** . Öffnen Sie das Dialogfeld, indem Sie auf die Komponente doppelklicken oder indem Sie im Datenfluss-Designer mit der rechten Maustaste auf die Komponente und anschließend auf **Bearbeiten** klicken.  
  
 Dieses Dialogfeld enthält drei Registerkarten: **Komponenteneigenschaften**, **Eingabespalten**und **Eingabe- und Ausgabeeigenschaften**.  
  
## Registerkarte „Komponenteneigenschaften“  
 Auf dieser Registerkarte können die folgenden Elemente bearbeitet werden:  
  
|Feld|Description|  
|-----------|-----------------|  
|Name|Name der Datenstreamingziel-Komponente im Paket.|  
|ValidateExternalMetadata|Gibt an, ob die Komponente zur Entwurfszeit mit externen Datenquellen überprüft wird. Ist diese Option auf „false“ festgelegt, wird die Überprüfung anhand externer Datenquellen bis zur Laufzeit verzögert.|  
|IDColumnName|Die vom Assistenten für das Veröffentlichen von Datenfeeds generierte Ansicht umfasst diese zusätzliche ID-Spalte. Die ID-Spalte dient als EntityKey für die Ausgabedaten aus dem Datenfluss, wenn die Daten als OData-Feed von einer anderen Anwendung genutzt werden.<br /><br /> Der Standardname für diese Spalte lautet „_ID“. Sie können einen anderen Namen für die ID-Spalte angeben.|  
  
## Registerkarte „Eingabespalten“  
 Im oberen Bereich dieser Registerkarte sind alle verfügbaren Eingabespalten aufgeführt. Wählen Sie die Spalten, die in der Ausgabe dieser Komponente enthalten sein sollen. Die ausgewählten Spalten werden in einer Liste im unteren Bereich angezeigt. Sie können den Namen der Ausgabespalte ändern, indem Sie den neuen Namen für das Feld **Ausgabealias** in der Liste eingeben.  
  
## Registerkarte „Eingabe- und Ausgabeeigenschaften“  
 Ähnlich wie bei der Registerkarte „Eingabespalten“ können Sie auf dieser Registerkarte die Namen von Ausgabespalten ändern. Erweitern Sie in der Strukturansicht auf der linken Seite den Eintrag **Eingabe des Datenstreamingziels** , und erweitern Sie dann **Eingabespalten**. Klicken Sie auf den Namen der Eingabespalte, und ändern Sie im rechten Bereich den Namen der Ausgabespalte.  
  
## Siehe auch  
 [Konfigurieren des Datenstreamingziels](../../integration-services/data-flow/data-streaming-destination.md)   
 [Exemplarische Vorgehensweise: Veröffentlichen eines SSIS-Pakets als eine SQL-Ansicht](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
  