---
title: "Hinzuf&#252;gen oder L&#246;schen einer Komponente im Datenfluss | Microsoft Docs"
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
  - "Hinzufügen von Komponenten"
  - "Komponenten [Integration Services], Datenfluss"
ms.assetid: d99124f9-0994-4f40-a48e-fdca6a4383e7
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# Hinzuf&#252;gen oder L&#246;schen einer Komponente im Datenfluss
  Bei Datenflusskomponenten handelt es sich um Quellen, Ziele und Transformationen in einem Datenfluss. Bevor Sie einem Datenfluss Komponenten hinzufügen können, muss die Ablaufsteuerung im Paket einen Datenflusstask einschließen.  
  
 Im Folgenden wird beschrieben, wie eine Komponente zum Datenfluss eines Pakets hinzugefügt oder in diesem gelöscht wird.  
  
### So fügen Sie einem Datenfluss eine Komponente hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung**, und doppelklicken Sie dann auf den Datenflusstask, der den Datenfluss enthält, dem Sie eine Komponente hinzufügen möchten.  
  
4.  Erweitern Sie in der Toolbox **Datenflussquellen**, **Datenflusstransformationen**oder **Datenflussziele**, und ziehen Sie ein Datenflusselement auf die Entwurfsoberfläche der Registerkarte **Datenfluss** .  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
### So löschen Sie eine Komponente aus einem Datenfluss  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung**, und doppelklicken Sie dann auf den Datenflusstask, der den Datenfluss enthält, in dem Sie eine Komponente löschen möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Datenflusskomponente, und klicken Sie dann auf **Löschen**.  
  
5.  Bestätigen Sie den Löschvorgang.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## Siehe auch  
 [Verbinden von Komponenten in einem Datenfluss](../../integration-services/data-flow/connect-components-in-a-data-flow.md)   
 [Konfigurieren einer Fehlerausgabe in einer Datenflusskomponente](../../integration-services/troubleshooting/configure-an-error-output-in-a-data-flow-component.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  