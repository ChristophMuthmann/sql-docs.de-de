---
title: "Ziel-Editor für SAP BW (Seite „Verbindungs-Manager“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.sapbwdestination.connection.f1
ms.assetid: 04ae38f8-5287-45a3-826a-8aac5dd15a91
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c63ac10d6cb4726817d8481be70533df8e2014c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sap-bw-destination-editor-connection-manager-page"></a>Ziel-Editor für SAP BW (Seite Verbindungs-Manager)
  Verwenden Sie die Seite **Verbindungs-Manager** im **Ziel-Editor für SAP BW** , um den SAP BW-Verbindungs-Manager auszuwählen, der vom SAP BW-Ziel verwendet wird. Auf dieser Seite wählen Sie außerdem die Parameter aus, die zum Laden der Daten in das SAP NetWeaver BW-System verwendet werden.  
  
 Weitere Informationen zum SAP BW-Ziel von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW finden Sie unter [SAP BW-Ziel](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 **So öffnen Sie die Seite "Verbindungs-Manager"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem das SAP BW-Ziel enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das SAP BW-Ziel.  
  
3.  Klicken Sie im **Ziel-Editor für SAP BW**auf **Verbindungs-Manager** , um die Seite **Verbindungs-Manager** des Editors zu öffnen.  
  
## <a name="options"></a>enthalten  
  
> [!NOTE]  
>  Wenn Sie nicht alle Werte kennen, die zur Konfiguration des Ziels erforderlich sind, müssen Sie ggf. Ihren SAP-Administrator um Unterstützung bitten.  
  
 **SAP BW-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **SAP BW-Verbindungs-Manager** einen neuen Verbindungs-Manager.  
  
 **Testladevorgang**  
 Führen Sie einen Testladevorgang aus, in dem die ausgewählten Einstellungen verwendet und 0 Zeilen geladen werden.  
  
### <a name="infopackageinfosource-options"></a>Optionen für "InfoPackage/InfoSource"  
 Diese Werte müssen nicht im Voraus bekannt sein und eingegeben werden. Verwenden Sie die Schaltfläche **Suchen** , um das entsprechende InfoPackage zu suchen und auszuwählen. Nachdem Sie ein InfoPackage ausgewählt haben, werden die entsprechenden Werte für diese Optionen von der Komponente eingegeben.  
  
 **InfoPackage**  
 Geben Sie den Namen für das InfoPackage ein.  
  
 **InfoSource**  
 Geben Sie den Namen für die InfoSource ein.  
  
 **Typ**  
 Geben Sie das Einzelzeichen ein, durch das der InfoSource-Typ identifiziert wird. In der folgenden Tabelle sind die zulässigen Einzelzeichenwerte aufgeführt.  
  
|Wert|Description|  
|-----------|-----------------|  
|**D**|Transaktionsdaten|  
|**M**|Masterdaten|  
|**T**|Texte|  
|**H**|Hierarchiedaten|  
  
 **Logisches System**  
 Geben Sie den Namen des logischen Systems ein, das dem InfoPackage zugeordnet ist.  
  
 **Suchen**  
 Suchen Sie das InfoPackage mithilfe des Dialogfelds **InfoPackage suchen** . Weitere Informationen zu diesem Dialogfeld finden Sie unter [Look Up InfoPackage](../../integration-services/data-flow/look-up-infopackage.md).  
  
### <a name="rfc-destination-options"></a>Optionen für "RFC-Ziel"  
 Diese Werte müssen nicht im Voraus bekannt sein und eingegeben werden. Verwenden Sie die Schaltfläche **Suchen** , um das entsprechende RFC-Ziel zu suchen und auszuwählen. Nachdem Sie ein RFC-Ziel ausgewählt haben, werden die entsprechenden Werte für diese Optionen von der Komponente eingegeben.  
  
 **Gatewayhost**  
 Geben Sie den Servernamen oder die IP-Adresse des Gatewayhosts ein. Normalerweise ist der Name oder die IP-Adresse identisch mit dem SAP-Anwendungsserver.  
  
 **Gatewaydienst**  
 Geben Sie den Namen des Gatewaydiensts im Format **sapgwNN**ein, wobei **NN** der Systemnummer entspricht.  
  
 **Programm-ID**  
 Geben Sie die Programm-ID ein, die dem RFC-Ziel zugeordnet ist.  
  
 **Suchen**  
 Suchen Sie das RFC-Ziel mithilfe des Dialogfelds **RFC-Ziel suchen** . Weitere Informationen zu diesem Dialogfeld finden Sie unter [Look Up RFC Destination](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
### <a name="create-sap-bw-objects-options"></a>Optionen für "SAP BW-Objekte erstellen"  
 **Objekttyp auswählen**  
 Wählen Sie den Typ des SAP NetWeaver BW-Objekts aus, das Sie erstellen möchten. Wählen Sie einen der folgenden Typen aus:  
  
-   InfoObject  
  
-   InfoCube  
  
-   InfoSource  
  
-   InfoPackage  
  
 **Create**  
 Erstellen Sie den ausgewählten SAP NetWeaver BW-Objekttyp.  
  
|Objekttyp|Ergebnis|  
|-----------------|------------|  
|**InfoObject**|Erstellen Sie ein neues InfoObject mithilfe des Dialogfelds **Neues InfoObject erstellen** . Weitere Informationen zu diesem Dialogfeld finden Sie unter [Create New InfoObject](../../integration-services/data-flow/create-new-infoobject.md).|  
|**InfoCube**|Erstellen Sie einen neuen InfoCube mithilfe des Dialogfelds **InfoCube für Transaktionsdaten erstellen** . Weitere Informationen zu diesem Dialogfeld finden Sie unter [Create InfoCube for Transaction Data](../../integration-services/data-flow/create-infocube-for-transaction-data.md).|  
|**InfoSource**|Erstellen Sie eine neue InfoSource, indem Sie erst das Dialogfeld **InfoSource erstellen** und dann das Dialogfeld **InfoSource für Transaktionsdaten erstellen** oder **InfoSource für Masterdaten erstellen** verwenden. Weitere Informationen zu diesen Dialogfeldern finden Sie unter [Create InfoSource](../../integration-services/data-flow/create-infosource.md), [Create InfoSource for Transaction Data](../../integration-services/data-flow/create-infosource-for-transaction-data.md) und [Create InfoSource for Master Data](../../integration-services/data-flow/create-infosource-for-master-data.md).|  
|**InfoPackage**|Erstellen Sie ein neues InfoPackage mithilfe des Dialogfelds **InfoPackage erstellen** . Weitere Informationen zu diesem Dialogfeld finden Sie unter [Create InfoPackage](../../integration-services/data-flow/create-infopackage.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Ziel-Editor für SAP BW &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)   
 [Ziel-Editor für SAP BW &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [Ziel-Editor für SAP BW &#40;Seite „Erweitert“&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
