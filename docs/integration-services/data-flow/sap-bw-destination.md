---
title: SAP BW-Ziel | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a612ed91-b89b-4173-a0b1-0bce381e1e28
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 28d86db3fac9d5230fa554369bccd7a23304d63c
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-destination"></a>SAP BW-Ziel
  Das SAP BW-Ziel ist die Zielkomponente von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Folglich lädt das SAP BW-Ziel Daten aus dem Datenfluss in ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket im SAP NetWeaver BW-System, Version 7.  
  
 Das Ziel weist eine Eingabe und eine Fehlerausgabe auf.  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 Führen Sie die folgenden Aufgaben aus, um das SAP BW-Ziel zu verwenden:  
  
-   [Vorbereiten der SAP NetWeaver BW-Objekte](#bkmk_Prepare_Objects)  
  
-   [Verbinden mit dem SAP NetWeaver BW-System](#bkmk_Connect_Database)  
  
-   [Konfigurieren des SAP BW-Ziels](#bkmk_Configure_Destination)  
  
##  <a name="bkmk_Prepare_Objects"></a> Vorbereiten der SAP NetWeaver BW-Objekte, die für das Ziel erforderlich sind  
 Das SAP BW-Ziel erfordert, dass sich bestimmte Objekte im SAP NetWeaver BW-System befinden, damit das Ziel funktionsfähig ist. Wenn diese Objekte noch nicht vorhanden sind, müssen Sie diese Schritte ausführen, um die Objekte im SAP NetWeaver BW-System zu erstellen und zu konfigurieren.  
  
> [!NOTE]  
>  Zusätzliche Informationen zu diesen Objekten und die Konfigurationsschritte finden Sie in der SAP NetWeaver BW-Dokumentation.  
  
1.  Erstellen Sie ein neues Quellsystem:  
  
    1.  Wählen Sie den Typ **Third Party/Staging BAPIs**(Drittanbieter/Staging BAPIs) aus.  
  
    2.  Wählen Sie für **Communication Type with Target System**(Kommunikationstyp mit Zielsystem) die Option **Non-Unicode (Inactive MDMP Settings)**(Nicht-Unicode (inaktive MDMP-Einstellungen)) aus.  
  
    3.  Weisen Sie eine entsprechende Programm-ID zu.  
  
2.  Weisen Sie einer InfoSource das Quellsystem zu.  
  
3.  Erstellen Sie ein InfoPackage.  
  
     Das InfoPackage ist das wichtigste Objekt, das vom SAP BW-Ziel benötigt wird.  
  
 Sie können zusätzliche InfoObjects, InfoCubes, InfoSources und InfoPackages erstellen, die erforderlich sind, um den Ladevorgang der Daten in das SAP NetWeaver BW-System zu unterstützen.  
  
##  <a name="bkmk_Connect_Database"></a> Herstellen einer Verbindung mit dem SAP NetWeaver BW-System  
 Um eine Verbindung mit dem SAP NetWeaver BW-System, Version 7, herzustellen, verwendet das SQL BW-Ziel den SAP BW-Verbindungs-Manager, der im Lieferumfang des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW-Pakets enthalten ist. Der SAP BW-Verbindungs-Manager ist der einzige [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Verbindungs-Manager, der vom SAP BW-Ziel verwendet werden kann.  
  
 Weitere Informationen zum SAP BW-Verbindungs-Manager finden Sie unter [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
##  <a name="bkmk_Configure_Destination"></a> Konfigurieren des SAP BW-Ziels  
 Es gibt folgende Möglichkeiten, um das SAP BW-Ziel zu konfigurieren:  
  
-   Suchen Sie das InfoPackage, das zum Laden von Daten verwendet werden soll, und wählen Sie es aus.  
  
-   Ordnen Sie jede Spalte im Datenfluss dem entsprechenden InfoObject im InfoPackage zu.  
  
-   Geben Sie an, wie viele Datenzeilen auf einmal übertragen werden, indem Sie die **PackageSize** -Eigenschaft konfigurieren.  
  
-   Warten Sie, bis das SAP NetWeaver BW-System den Datenladevorgang vollständig abgeschlossen hat.  
  
-   Lösen Sie das InfoPackage nicht aus, sondern warten Sie auf die Benachrichtigung, dass das SAP NetWeaver BW-System den Datenladevorgang gestartet hat.  
  
-   Optional können Sie eine weitere Prozesskette auslösen, nachdem der Datenladevorgang abgeschlossen wurde.  
  
-   Optional können Sie die SAP NetWeaver BW-Objekte erstellen, die vom Ziel benötigt werden. Dazu gehören InfoObjects, InfoCubes, InfoSources und InfoPackages.  
  
-   Testen Sie den Datenladevorgang anhand der ausgewählten Optionen.  
  
 Sie können auch die Protokollierung von RFC-Funktionsaufrufen durch das Ziel aktivieren. (Diese Protokollierung wird separat von der optionalen Protokollierung ausgeführt, die Sie für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete aktivieren können.) Sie aktivieren die Protokollierung von RFC-Funktionsaufrufen bei der Konfiguration des SAP BW-Verbindungs-Managers, der vom Ziel verwendet wird. Weitere Informationen zur Konfiguration des SAP BW-Verbindungs-Managers finden Sie unter [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
 Wenn Sie nicht alle Werte kennen, die zur Konfiguration des Ziels erforderlich sind, müssen Sie ggf. Ihren SAP-Administrator um Unterstützung bitten.  
  
 Eine exemplarische Vorgehensweise, die zeigt, wie der SAP BW-Verbindungs-Manager sowie die zugehörige Quelle und das zugehörige Ziel konfiguriert und verwendet werden, finden Sie im Whitepaper [Verwenden von SQL Server 2008 Integration Services und SAP BI 7.0](http://go.microsoft.com/fwlink/?LinkID=137090). In diesem Whitepaper wird auch erläutert, wie die erforderlichen Objekte in SAP BW konfiguriert werden.  
  
### <a name="using-the-ssis-designer-to-configure-the-destination"></a>Konfigurieren des Ziels mit dem SSIS-Designer  
 Um weitere Informationen zu den Eigenschaften des SAP BW-Ziels zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können, klicken Sie auf eines der folgenden Themen:  
  
-   [Ziel-Editor für SAP BW &#40; Seite Verbindungs-Manager &#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)  
  
-   [Ziel-Editor für SAP BW &#40; Seite "Zuordnungen" &#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)  
  
-   [Ziel-Editor für SAP BW &#40; Seite "Fehlerausgabe" Fehler &#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)  
  
-   [Ziel-Editor für SAP BW &#40; Seite "Erweitert" &#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)  
  
 Während Sie das SAP BW-Ziel konfigurieren, können Sie auch verschiedene Dialogfelder verwenden, um SAP NetWeaver BW-Objekte zu suchen oder zu erstellen. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu diesen Dialogfeldern zu erhalten:  
  
-   [Infopackage suchen](../../integration-services/data-flow/look-up-infopackage.md)  
  
-   [Neues InfoObject erstellen](../../integration-services/data-flow/create-new-infoobject.md)  
  
-   [InfoCube für Transaktionsdaten erstellen](../../integration-services/data-flow/create-infocube-for-transaction-data.md)  
  
-   [InfoObject suchen](../../integration-services/data-flow/look-up-infoobject.md)  
  
-   [InfoSource erstellen](../../integration-services/data-flow/create-infosource.md)  
  
-   [InfoSource für Transaktionsdaten erstellen](../../integration-services/data-flow/create-infosource-for-transaction-data.md)  
  
-   [InfoSource für Masterdaten erstellen](../../integration-services/data-flow/create-infosource-for-master-data.md)  
  
-   [InfoPackage erstellen](../../integration-services/data-flow/create-infopackage.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Connector for SAP BW Components](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
