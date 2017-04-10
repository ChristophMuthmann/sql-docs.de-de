---
title: "Hinzuf&#252;gen oder L&#246;schen eines Tasks oder Containers in einer Ablaufsteuerung | Microsoft Docs"
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
  - "Container [Integration Services], hinzufügen"
  - "Hinzufügen von Tasks"
  - "Hinzufügen von Containern"
  - "Aufgaben [Integration Services], hinzufügen"
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# Hinzuf&#252;gen oder L&#246;schen eines Tasks oder Containers in einer Ablaufsteuerung
  Wenn Sie im Ablaufsteuerungs-Designer arbeiten, werden in der Toolbox im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer die Tasks aufgeführt, die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zum Erstellen einer Ablaufsteuerung in einem Paket bereitstellt. Weitere Informationen über die Toolbox finden Sie unter [SSIS Toolbox](../../integration-services/ssis-toolbox.md).  
  
 Ein Paket kann mehrere Instanzen desselben Tasks einschließen. Jede Instanz eines Tasks wird im Paket eindeutig identifiziert, und Sie können jede Instanz unterschiedlich konfigurieren.  
  
 Wenn Sie einen Task löschen, werden die Rangfolgeneinschränkungen, die den Task mit anderen Tasks und Container in der Ablaufsteuerung verbinden, ebenfalls gelöscht.  
  
 Im Folgenden wird beschrieben, wie ein Task oder Container zur Ablaufsteuerung eines Pakets hinzugefügt oder in dieser gelöscht wird.  
  
### So fügen Sie einer Ablaufsteuerung einen Task oder Container hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie im Menü **Ansicht**auf **Toolbox** , um **Toolbox** zu öffnen.  
  
5.  Erweitern Sie **Ablaufsteuerungselemente** und **Wartungstasks**.  
  
6.  Ziehen Sie Tasks und Container aus der **Toolbox** auf die Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** .  
  
7.  Verbinden Sie einen Task oder Container innerhalb der Paketablaufsteuerung, indem Sie dessen Konnektor auf eine andere Komponente in der Ablaufsteuerung ziehen.  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
### So löschen Sie einen Task oder Container aus einer Ablaufsteuerung  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen. Führen Sie eines der folgenden Verfahren aus:  
  
    -   Klicken Sie auf die Registerkarte **Ablaufsteuerung**, klicken Sie mit der rechten Maustaste auf den Task oder Container, den Sie entfernen möchten, und klicken Sie anschließend auf **Löschen**.  
  
    -   Öffnen Sie **Paket-Explorer**. Klicken Sie im Ordner **Ausführbare Dateien** mit der rechten Maustaste auf den Task oder Container, den Sie entfernen möchten, und klicken Sie anschließend auf **Löschen**.  
  
3.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [SQL Server Integration Services-Container](../../integration-services/control-flow/integration-services-containers.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  