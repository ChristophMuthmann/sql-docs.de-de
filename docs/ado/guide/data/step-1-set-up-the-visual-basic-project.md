---
title: 'Schritt 1: Einrichten von Visual Basic-Projekt | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8bfdee45f81b2b69e0d495b643878f599345edf5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Schritt 1: Einrichten von Visual Basic-Projekt
In diesem Szenario wird davon ausgegangen, dass Sie Microsoft Visual Basic 6.0, ADO 2.5 oder höher und den Microsoft OLE DB-Anbieter für Internet Publishing auf Ihrem System installiert haben. Sie erstellen zunächst ein neues Projekt, und klicken Sie dann einige Steuerelemente hinzufügen, um das Standardformular in das Projekt.  
  
### <a name="to-create-an-ado-project"></a>So erstellen Sie ein ADO-Projekt  
  
1.  Erstellen Sie in Microsoft Visual Basic ein neues Standard-EXE-Projekt.  
  
2.  Wählen Sie im Menü Projekt Verweise ein.  
  
3.  Wählen Sie "Microsoft ActiveX Data Objects 2.5 Library", und klicken Sie auf OK.  
  
### <a name="to-insert-controls-on-the-main-form"></a>So fügen Sie die Steuerelemente im Hauptformular:  
  
1.  Fügen Sie ein ListBox-Steuerelement auf Form1. Legen Sie die Name-Eigenschaft auf **IstMain**.  
  
2.  Fügen Sie ein anderes ListBox-Steuerelement auf Form1. Legen Sie die Name-Eigenschaft auf **LstDetails**.  
  
3.  Fügen Sie in Form1 ein TextBox-Steuerelement hinzu. Legen Sie die Name-Eigenschaft auf **TxtDetails**.  
  
## <a name="see-also"></a>Siehe auch  
 [Internet, die Publishing-Szenario](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Schritt 2: Initialisieren der wichtigsten Listenfelder](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
