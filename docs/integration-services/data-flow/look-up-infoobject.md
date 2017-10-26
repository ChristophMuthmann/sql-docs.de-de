---
title: InfoObject suchen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e7f4c132-a5ec-49d8-a964-45775432731f
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f25c00406ce375a2a7a380859ca0eaa5031b54d3
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="look-up-infoobject"></a>InfoObject suchen
  Verwenden Sie das Dialogfeld **InfoObject suchen** , um ein InfoObject zu suchen, das im SAP NetWeaver BW-System definiert ist. Wenn die Liste der verfügbaren InfoObjects angezeigt wird, wählen Sie das gewünschte InfoObject aus. Daraufhin werden die zugehörigen Optionen vom SAP BW-Ziel mit den erforderlichen Werten aufgefüllt.  
  
 Das SAP BW-Ziel von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW verwendet das Dialogfeld **InfoObject suchen** . Weitere Informationen zum SAP BW-Ziel finden Sie unter [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 **So öffnen Sie das Dialogfeld "InfoObject suchen"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem das SAP BW-Ziel enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das SAP BW-Ziel.  
  
3.  Klicken Sie im **Ziel-Editor für SAP BW**auf **Verbindungs-Manager** , um die Seite **Verbindungs-Manager** des Editors zu öffnen.  
  
4.  Wählen Sie auf der Seite **Verbindungs-Manager** im Gruppenfeld **SAP BW-Objekte erstellen** eine der folgenden Optionen aus:  
  
    1.  Wählen Sie **InfoCube**aus. Klicken Sie dann auf **Erstellen**. Klicken Sie im Dialogfeld **InfoCube für Transaktionsdaten erstellen** in der Spalte **IObject** für eine der Zeilen in der Liste auf **Suchen** . Jede Zeile stellt eine Spalte im Datenfluss des Pakets dar.  
  
    2.  Wählen Sie **InfoSource**aus. Klicken Sie dann auf **Erstellen**. Wählen Sie im Dialogfeld **InfoSource erstellen** die Option **Transaktionsdaten**aus. Klicken Sie im Dialogfeld **InfoSource für Transaktionsdaten erstellen** in der Spalte **IObject** für eine der Zeilen in der Liste auf **Suchen** . Jede Zeile stellt eine Spalte im Datenfluss des Pakets dar.  
  
    3.  Wählen Sie **InfoSource**aus. Klicken Sie dann auf **Erstellen**. Wählen Sie im Dialogfeld **InfoSource erstellen** die Option **Masterdaten**aus. Klicken Sie im Dialogfeld **InfoSource für Masterdaten erstellen** auf **Suchen**.  
  
 Sie können das Dialogfeld **InfoObject suchen** auch öffnen, indem Sie im Abschnitt **Attribute** des Dialogfelds **Neues InfoObject erstellen** auf **Hinzufügen** klicken.  
  
## <a name="lookup-options"></a>Suchoptionen  
 In den Suchtextfeldern können Sie Ergebnisse filtern, indem Sie das Platzhalterzeichen (*) oder eine Teilzeichenfolge in Kombination mit dem Platzhalterzeichen (*) verwenden. Wenn Sie ein Suchfeld jedoch leer lassen, werden beim Suchvorgang nur leere Zeichenfolgen in diesem Feld abgeglichen.  
  
 **Merkmale**  
 Suchen Sie die InfoObjects, die die Eigenschaften darstellen.  
  
 **Einheiten**  
 Suchen Sie die InfoObjects, die die Einheiten darstellen.  
  
 **Kennzahlen**  
 Suchen Sie die InfoObjects, die die Kennzahlen darstellen.  
  
 **Zeitmerkmale**  
 Suchen Sie die InfoObjects, die die Zeitmerkmale darstellen.  
  
 **Name**  
 Geben Sie den Namen des InfoObject ein, das Sie suchen möchten, oder geben Sie einen Teilnamen mit dem Platzhalterzeichen (*) ein. Alternativ können Sie das Platzhalterzeichen (*) alleine verwenden, um alle InfoObjects einzuschließen.  
  
 **Description**  
 Geben Sie die Beschreibung oder eine teilweise Beschreibung mit dem Platzhalterzeichen (*) ein. Alternativ können Sie das Platzhalterzeichen (*) alleine verwenden, um alle InfoObjects unabhängig von der Beschreibung einzuschließen.  
  
 **Suchen**  
 Suchen Sie übereinstimmende InfoObjects, die im SAP NetWeaver BW-System definiert sind.  
  
## <a name="lookup-results"></a>Suchergebnisse  
 Nachdem Sie auf die Schaltfläche Suchen geklickt haben, wird eine Liste der im SAP NetWeaver BW-System enthaltenen InfoObjects in einer Tabelle angezeigt, die über die folgenden Spaltenüberschriften verfügt.  
  
 **InfoObject**  
 Zeigt den Namen des InfoObject an, das im SAP NetWeaver BW-System definiert ist.  
  
 **Text (kurz)**  
 Zeigt den kurzen Text an, der dem InfoObject zugeordnet ist.  
  
 Wenn die Liste der verfügbaren InfoObjects angezeigt wird, wählen Sie das gewünschte InfoObject aus. Daraufhin werden die zugehörigen Optionen vom Ziel mit den erforderlichen Werten aufgefüllt.  
  
## <a name="see-also"></a>Siehe auch  
 [InfoCube für Transaktionsdaten erstellen](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [InfoSource erstellen](../../integration-services/data-flow/create-infosource.md)   
 [InfoSource für Transaktionsdaten erstellen](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [InfoSource für Masterdaten erstellen](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [Neues InfoObject erstellen](../../integration-services/data-flow/create-new-infoobject.md)   
 [Ziel-Editor für SAP BW &#40; Seite Verbindungs-Manager &#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  

