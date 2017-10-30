---
title: Debuggen eines Skripts durch Festlegen von Breakpoints in einem Skripttask und Skriptkomponente | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96815b337311c4ba8d16e10c25891c728e7a0c74
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>Debuggen eines Skripts durch Festlegen von Breakpoints in einem Skripttask und einer Skriptkomponente
  In diesem Verfahren wird beschrieben, wie Sie in den Skripts Breakpoints festlegen, die im Skripttask und in der Skriptkomponente verwendet werden.  
  
 Nach dem Festlegen von Breakpoints im Skript, das **Breakpoints festlegen - \<Objektname >** Dialogfeld werden die Breakpoints zusammen mit den integrierten Breakpoints aufgelistet.  
  
> [!IMPORTANT]  
>  In bestimmten Fällen werden Breakpoints im Skripttask und in der Skriptkomponente ignoriert. Weitere Informationen finden Sie unter der **Debuggen des Skripttasks** im Abschnitt [codieren und Debuggen des Skripttasks](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) und **Debuggen der Skriptkomponente** im Abschnitt [codieren und Debuggen der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="to-set-a-breakpoint-in-script"></a>So legen Sie einen Breakpoint im Skript fest  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie auf das Paket mit dem Skript, in dem Sie Breakpoints festlegen möchten.  
  
3.  Um den Skripttask zu öffnen, klicken Sie auf die **Control Flow** Registerkarte, und doppelklicken Sie dann auf den Skripttask angeben.  
  
4.  Um die Skriptkomponente zu öffnen, klicken Sie auf die **Datenfluss** Registerkarte, und doppelklicken Sie dann auf die Skriptkomponente.  
  
5.  Klicken Sie auf **Skript** , und klicken Sie dann auf **Bearbeitungsskript**.  
  
6.  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA), suchen Sie die Zeile des Skripts, die Sie auf einen Haltepunkt festlegen, mit der rechten Maustaste in dieser Zeile, zeigen Sie auf **Haltepunkt**, und klicken Sie dann auf **Haltepunkt einfügen**.  
  
     Das Breakpointsymbol wird in der Codezeile angezeigt.  
  
7.  Klicken Sie im Menü **Datei** auf **Beenden**.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
  

