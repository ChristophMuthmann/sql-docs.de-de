---
title: "InfoSource für Masterdaten erstellen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4caf4c8fde349f6865792d327965a8dea4161f73
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-infosource-for-master-data"></a>InfoSource für Masterdaten erstellen
  Verwenden Sie das Dialogfeld **InfoSource für Masterdaten erstellen** , um eine neue InfoSource für Masterdaten im SAP NetWeaver BW-System zu erstellen.  
  
 Sie können das Dialogfeld **InfoSource für Masterdaten erstellen** im **Ziel-Editor für SAP BW** auf der Seite **Verbindungs-Manager**öffnen. Weitere Informationen zum SAP BW-Ziel finden Sie unter [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 **So öffnen Sie das Dialogfeld "InfoSource für Masterdaten erstellen"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem das SAP BW-Ziel enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das SAP BW-Ziel.  
  
3.  Klicken Sie im **Ziel-Editor für SAP BW**auf **Verbindungs-Manager** , um die Seite **Verbindungs-Manager** des Editors zu öffnen.  
  
4.  Wählen Sie auf der Seite **Verbindungs-Manager** im Gruppenfeld **SAP BW-Objekte erstellen** die Option **InfoSource**aus, und klicken Sie dann auf **Erstellen**.  
  
5.  Wählen Sie im Dialogfeld **InfoSource erstellen** die Option **Masterdaten**aus, und klicken Sie dann auf **OK**.  
  
## <a name="options"></a>Tastatur  
 **InfoObject-Name**  
 Geben Sie den Namen des InfoObject ein, auf dem die neue InfoSource basieren soll.  
  
 **Suchen**  
 Suchen Sie das InfoObject. Mit dieser Option wird das Dialogfeld **InfoObject suchen** geöffnet, in dem Sie das InfoObject auswählen können. Weitere Informationen zu diesem Dialogfeld finden Sie unter [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md).  
  
 Nachdem Sie ein InfoObject ausgewählt haben, wird das Textfeld **InfoObject-Name** mit dem Namen des ausgewählten InfoObject aufgefüllt.  
  
 **Neu**  
 Erstellen Sie ein neues InfoObject. Mit dieser Option wird das Dialogfeld **Neues InfoObject erstellen** geöffnet, in dem Sie das neue InfoObject erstellen können. Weitere Informationen zu diesem Dialogfeld finden Sie unter [Create New InfoObject](../../integration-services/data-flow/create-new-infoobject.md).  
  
 Nachdem Sie ein InfoObject erstellt haben, wird das Textfeld **InfoObject-Name** mit dem Namen des neuen InfoObject aufgefüllt.  
  
 **Kurze Beschreibung**  
 Geben Sie eine kurze Beschreibung für die neue InfoSource ein.  
  
 **Lange Beschreibung**  
 Geben Sie eine lange Beschreibung für die neue InfoSource ein.  
  
 **Quellsystem**  
 Wählen Sie das Quellsystem aus, das der neuen InfoSource zugeordnet werden soll.  
  
 **Application**  
 Geben Sie den Namen der Anwendung ein, die der neuen InfoSource zugeordnet werden soll.  
  
 **Attribute**  
 Gibt an, dass sich die Masterdaten aus Attributen zusammensetzen.  
  
 **Texte**  
 Gibt an, dass sich die Masterdaten aus Attributen zusammensetzen.  
  
 **Speichern und aktivieren**  
 Speichern und aktivieren Sie die neue InfoSource.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [InfoSource erstellen](../../integration-services/data-flow/create-infosource.md)   
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
