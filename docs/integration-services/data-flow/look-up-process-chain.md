---
title: Prozesskette suchen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f6303ea4-fbbf-4cba-bc60-828df62be8c2
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 331b54b21cd7d19c1c38943f8d6056708cfc52c9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="look-up-process-chain"></a>Prozesskette suchen
  Verwenden Sie das Dialogfeld **Prozesskette suchen** , um eine Prozesskette suchen, die im SAP NetWeaver BW-System definiert ist. Wenn die Liste der verfügbaren Prozessketten angezeigt wird, wählen Sie die gewünschte Kette aus. Daraufhin werden die zugehörigen Optionen von der Quelle mit den erforderlichen Werten aufgefüllt.  
  
 Die SAP BW-Quelle von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW verwendet das Dialogfeld **Prozesskette suchen** . Weitere Informationen zur SAP BW-Quelle finden Sie unter [SAP BW Source](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 **So öffnen Sie das Dialogfeld "Prozesskette suchen"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem die SAP BW-Quelle enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die SAP BW-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für SAP BW**auf **Verbindungs-Manager** , um die Seite **Verbindungs-Manager** des Editors zu öffnen.  
  
4.  Klicken Sie im Gruppenfeld **Prozesskette** auf **Suchen** , um das Dialogfeld **Prozesskette suchen** anzuzeigen.  
  
     Das Gruppenfeld **Prozesskette** wird nur angezeigt, wenn der Wert für **Ausführungsmodus** auf **P - Prozesskette auslösen**festgelegt ist.  
  
## <a name="lookup-options"></a>Suchoptionen  
 In den Suchfeldern können Sie Ergebnisse filtern, indem Sie das Platzhalterzeichen (*) oder eine Teilzeichenfolge in Kombination mit dem Platzhalterzeichen (*) verwenden. Wenn Sie ein Suchfeld leer lassen, werden beim Suchvorgang jedoch nur leere Zeichenfolgen in diesem Feld abgeglichen.  
  
 **Process chain**  
 Geben Sie den Namen der gesuchten Prozesskette oder einen Teilnamen mit dem Platzhalterzeichen (*) ein. Alternativ können Sie das Platzhalterzeichen (*) alleine verwenden, um alle Prozessketten einzuschließen.  
  
 **Suchen**  
 Suchen Sie übereinstimmende Prozessketten, die im SAP NetWeaver BW-System definiert sind.  
  
## <a name="lookup-results"></a>Suchergebnisse  
 Nachdem Sie auf die Schaltfläche Suchen geklickt haben, wird eine Liste der im SAP NetWeaver BW-System enthaltenen Prozessketten in einer Tabelle angezeigt, die über die folgenden Spaltenüberschriften verfügt.  
  
 **Prozesskette**  
 Zeigt den Namen der Prozesskette an, die im SAP NetWeaver BW-System definiert ist.  
  
 **Beschreibung**  
 Zeigt die Beschreibung der Prozesskette an.  
  
 Wenn die Liste der verfügbaren Prozessketten angezeigt wird, wählen Sie die gewünschte Kette aus. Daraufhin werden die zugehörigen Optionen von der Quelle mit den erforderlichen Werten aufgefüllt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Quellen-Editor für SAP BW &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
