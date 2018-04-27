---
title: Hinzufügen oder Löschen eines Tasks oder Containers in einer Ablaufsteuerung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2c9cdee1246cb1df0d3e268ec9ea54fb7cc32ffe
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>Hinzufügen oder Löschen eines Tasks oder Containers in einer Ablaufsteuerung
  Wenn Sie im Ablaufsteuerungs-Designer arbeiten, werden in der Toolbox im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer die Tasks aufgeführt, die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zum Erstellen einer Ablaufsteuerung in einem Paket bereitstellt. Weitere Informationen über die Toolbox finden Sie unter [SSIS Toolbox](../../integration-services/ssis-toolbox.md).  
  
 Ein Paket kann mehrere Instanzen desselben Tasks einschließen. Jede Instanz eines Tasks wird im Paket eindeutig identifiziert, und Sie können jede Instanz unterschiedlich konfigurieren.  
  
 Wenn Sie einen Task löschen, werden die Rangfolgeneinschränkungen, die den Task mit anderen Tasks und Container in der Ablaufsteuerung verbinden, ebenfalls gelöscht.  
  
 Im Folgenden wird beschrieben, wie ein Task oder Container zur Ablaufsteuerung eines Pakets hinzugefügt oder in dieser gelöscht wird.  
  
## <a name="add-a-task-or-a-container-to-a-control-flow"></a>Hinzufügen eines Tasks oder Containers zu einer Ablaufsteuerung  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie im Menü **Ansicht**auf **Toolbox** , um **Toolbox** zu öffnen.  
  
5.  Erweitern Sie **Ablaufsteuerungselemente** und **Wartungstasks**.  
  
6.  Ziehen Sie Tasks und Container aus der **Toolbox** auf die Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** .  
  
7.  Verbinden Sie einen Task oder Container innerhalb der Paketablaufsteuerung, indem Sie dessen Konnektor auf eine andere Komponente in der Ablaufsteuerung ziehen.  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="delete-a-task-or-a-container-from-a-control-flow"></a>Löschen eines Tasks oder Containers aus einer Ablaufsteuerung  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen. Führen Sie eines der folgenden Verfahren aus:  
  
    -   Klicken Sie auf die Registerkarte **Ablaufsteuerung** , klicken Sie mit der rechten Maustaste auf den Task oder Container, den Sie entfernen möchten, und klicken Sie anschließend auf **Löschen**.  
  
    -   Öffnen Sie **Paket-Explorer**. Klicken Sie im Ordner **Ausführbare Dateien** mit der rechten Maustaste auf den Task oder Container, den Sie entfernen möchten, und klicken Sie anschließend auf **Löschen**.  
  
3.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

## <a name="set-the-properties-of-a-task-or-container"></a>Festlegen der Eigenschaften eines Tasks oder Containers
Sie können die meisten Eigenschaften von Tasks und Containern im Fenster **Eigenschaften** festlegen. Eine Ausnahme sind Eigenschaften von Taskauflistungen und Eigenschaften, die zu komplex sind, als dass sie im Fenster **Eigenschaften** festgelegt werden könnten. Beispielsweise können Sie nicht den Enumerator konfigurieren, der vom Foreach-Schleifencontainer im Fenster **Eigenschaften** verwendet wird. Sie müssen einen Task- oder Container-Editor verwenden, um diese komplexen Eigenschaften festzulegen. Die meisten Task- und Container-Editoren weisen mehrere Knoten auf, und jeder Knoten enthält zugehörige Eigenschaften. Der Name des Knotens weist auf die Art der Eigenschaften hin, die der Knoten enthält.  
  
 Im Folgenden wird beschrieben, wie die Eigenschaften eines Tasks oder Containers entweder mit dem Fenster **Eigenschaften** oder dem entsprechenden Task- oder Container-Editor festgelegt werden.  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-properties-window"></a>Festlegen der Eigenschaften eines Tasks oder Containers mithilfe des Eigenschaftenfensters  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** mit der rechten Maustaste auf den Task oder Container, und klicken Sie auf **Eigenschaften**.  
  
5.  Aktualisieren Sie im Fenster **Eigenschaften** den Eigenschaftswert.  
  
    > [!NOTE]  
    >  Die meisten Eigenschaften können durch direktes Eingeben der gewünschten Werte in die jeweiligen Textfelder bzw. Auswählen der Werte aus einer Liste festgelegt werden. Einige Eigenschaften sind jedoch komplexer und verfügen über einen Editor für benutzerdefinierte Eigenschaften. Zum Festlegen der Eigenschaft klicken Sie in das Textfeld und anschließend auf die Schaltfläche zum Erstellen **(...)** . Der benutzerdefinierte Editor wird geöffnet.  
  
6.  Erstellen Sie optional Eigenschaftsausdrücke, um die Eigenschaften des Tasks oder Containers dynamisch zu aktualisieren. Weitere Informationen finden Sie unter [Hinzufügen oder Ändern eines Eigenschaftsausdrucks](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-task-or-container-editor"></a>Festlegen der Eigenschaften eines Tasks oder Containers mithilfe eines Task- oder Container-Editors  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** mit der rechten Maustaste auf den Task oder Container, und klicken Sie auf **Bearbeiten** , um den entsprechenden Task- bzw. Container-Editor zu öffnen.  
  
     Informationen zum Konfigurieren eines For-Schleifencontainers finden Sie unter [Konfigurieren eines For-Schleifencontainers](http://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5).  
  
     Informationen zum Konfigurieren eines Foreach-Schleifencontainers finden Sie unter [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
    > [!NOTE]  
    >  Der Sequenzcontainer weist keinen benutzerdefinierten Editor auf.  
  
5.  Falls der Task- oder Container-Editor mehrere Knoten aufweist, klicken Sie auf den Knoten mit der Eigenschaft, die Sie festlegen möchten.  
  
6.  Klicken Sie optional auf **Ausdrücke** , und erstellen Sie auf der Seite **Ausdrücke** Eigenschaftsausdrücke, um die Eigenschaften des Tasks oder Containers dynamisch zu aktualisieren. Weitere Informationen finden Sie unter [Hinzufügen oder Ändern eines Eigenschaftsausdrucks](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Aktualisieren Sie den Eigenschaftswert.  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services-Container](../../integration-services/control-flow/integration-services-containers.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  
