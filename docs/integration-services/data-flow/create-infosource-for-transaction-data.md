---
title: "InfoSource für Transaktionsdaten erstellen | Microsoft Docs"
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
ms.assetid: ab5f23e2-cd4e-4507-83d9-ac5ef721c171
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aae1b77456b66a00a547fa35f9a253f0199963cc
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="create-infosource-for-transaction-data"></a>InfoSource für Transaktionsdaten erstellen
  Verwenden Sie das Dialogfeld **InfoSource für Transaktionsdaten erstellen** , um eine neue InfoSource für Transaktionsdaten im SAP NetWeaver BW-System zu erstellen.  
  
 Sie können das Dialogfeld **InfoSource für Transaktionsdaten erstellen** im **Ziel-Editor für SAP BW** auf der Seite **Verbindungs-Manager**öffnen. Weitere Informationen zum SAP BW-Ziel finden Sie unter [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 **So öffnen Sie das Dialogfeld "InfoSource für Transaktionsdaten erstellen"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem das SAP BW-Ziel enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das SAP BW-Ziel.  
  
3.  Klicken Sie im **Ziel-Editor für SAP BW**auf **Verbindungs-Manager** , um die Seite **Verbindungs-Manager** des Editors zu öffnen.  
  
4.  Wählen Sie auf der Seite **Verbindungs-Manager** im Gruppenfeld **SAP BW-Objekte erstellen** die Option **InfoSource**aus, und klicken Sie dann auf **Erstellen**.  
  
5.  Wählen Sie im Dialogfeld **InfoSource erstellen** die Option **Transaktionsdaten**aus, und klicken Sie dann auf **OK**.  
  
## <a name="general-options"></a>Allgemeine Optionen  
 **InfoSource-Name**  
 Geben Sie einen Namen für die neue InfoSource ein.  
  
 **Kurze Beschreibung**  
 Geben Sie eine kurze Beschreibung für die neue InfoSource ein.  
  
 **Lange Beschreibung**  
 Geben Sie eine lange Beschreibung für die neue InfoSource ein.  
  
 **Quellsystem**  
 Wählen Sie das Quellsystem aus, das der InfoSource zugeordnet ist.  
  
 **Speichern und aktivieren**  
 Speichern und aktivieren Sie die neue InfoSource.  
  
## <a name="infosource-transfer-structure-options"></a>Optionen für die "InfoSource-Übergangsstruktur"  
 Mithilfe der InfoSource-Übergangsstruktur können Sie InfoSources Datenflussspalten zuordnen.  
  
 **PipelineElement**  
 Zeigt die Spalte in der Ausgabe des Datenflusses an, der mit dem SAP BW-Ziel verbunden ist.  
  
 **PipelineDataType**  
 Zeigt den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentyp der Datenflussspalte an.  
  
 **Iobject - Suchen**  
 Ordnen Sie der Datenflussspalte in der aktuellen Zeile ein vorhandenes InfoObject zu. Um diese Zuordnung zu erstellen, klicken Sie auf **Suchen**und verwenden dann das Dialogfeld **InfoObject suchen** , um das vorhandene InfoObject auszuwählen. Weitere Informationen zu diesem Dialogfeld finden Sie unter [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md).  
  
 Nachdem Sie ein vorhandenes InfoObject ausgewählt haben, werden die Spalten **InfoObject** und **Typ** von der Komponente mit den ausgewählten Werten aufgefüllt.  
  
 **Iobject - Neu**  
 Erstellen Sie ein neues InfoObject, und ordnen Sie dieses neue InfoObject der Datenflussspalte in der aktuellen Zeile zu. Um das neue InfoObject zu erstellen, klicken Sie auf **Neu**und erstellen dann das InfoObject im Dialogfeld **Neues InfoObject erstellen** . Weitere Informationen zu diesem Dialogfeld finden Sie unter [Create New InfoObject](../../integration-services/data-flow/create-new-infoobject.md).  
  
 Nachdem Sie ein neues InfoObject erstellt haben, werden die Spalten **InfoObject** und **Typ** mit den neuen Werten aufgefüllt.  
  
 **Iobject - Entfernen**  
 Heben Sie die Zuordnung zwischen dem InfoObject und der Datenflussspalte für die aktuelle Zeile auf. Um die Zuordnung aufzuheben, klicken Sie auf **Entfernen**.  
  
 **InfoObject**  
 Zeigt den Namen des InfoObject an, das der Datenflussspalte zugeordnet ist.  
  
 **Typ**  
 Zeigt den Typ des InfoObject an, das der Datenflussspalte zugeordnet ist. In der folgenden Tabelle sind die möglichen Werte für den Typ aufgelistet.  
  
|Wert|Description|  
|-----------|-----------------|  
|CHA|Merkmale|  
|UNI|Einheiten|  
|KYF|Kennzahlen|  
|TIM|Zeitmerkmale|  
  
 **Einheitenfeld**  
 Geben Sie die Einheiten an, die vom InfoObject verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [InfoSource erstellen](../../integration-services/data-flow/create-infosource.md)   
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  

