---
title: "SAP BW-Quelle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 749afb64-3567-4dc9-8431-783d650c25db
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# SAP BW-Quelle
  Die SAP BW-Quelle ist die Quellkomponente von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Daher extrahiert die SAP BW-Quelle Daten aus einem SAP NetWeaver BW-System, Version 7, und macht diese Daten im Datenfluss in einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket verfügbar.  
  
 Diese Quelle weist eine Ausgabe und eine Fehlerausgabe auf.  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
> [!IMPORTANT]  
>  Das Extrahieren von Daten aus SAP NetWeaver BW erfordert zusätzliche SAP-Lizenzen. Stimmen Sie diese Anforderungen mit SAP ab.  
  
 Führen Sie die folgenden Aufgaben aus, um die SAP BW-Quelle zu verwenden:  
  
-   [Vorbereiten der SAP NetWeaver BW-Objekte](#bkmk_Prepare_Objects)  
  
-   [Verbinden mit dem SAP NetWeaver BW-System](#bkmk_Connect_Database)  
  
-   [Konfigurieren der SAP BW-Quelle](#bkmk_Configure_Source)  
  
##  <a name="bkmk_Prepare_Objects"></a> Vorbereiten der SAP NetWeaver BW-Objekte, die für die Quelle erforderlich sind  
 Die SAP BW-Quelle erfordert, dass sich bestimmte Objekte im SAP NetWeaver BW-System befinden, damit die Quelle funktionsfähig ist. Wenn diese Objekte noch nicht vorhanden sind, müssen Sie diese Schritte ausführen, um die Objekte im SAP NetWeaver BW-System zu erstellen und zu konfigurieren.  
  
> [!NOTE]  
>  Zusätzliche Informationen zu diesen Objekten und die Konfigurationsschritte finden Sie in der SAP NetWeaver BW-Dokumentation.  
  
1.  Melden Sie sich über die SAP GUI bei SAP NetWeaver BW an, geben Sie den Transaktionscode SM59 ein, und erstellen Sie ein RFC-Ziel:  
  
    1.  Wählen Sie für **Verbindungstyp** die Option **TCP/IP** aus.  
  
    2.  Wählen Sie für **Activation Type**(Aktivierungstyp) die Option **Registered Server Program**(Registriertes Serverprogramm) aus.  
  
    3.  Wählen Sie für **Communication Type with Target System** (Kommunikationstyp mit Zielsystem) die Option **Non-Unicode (Inactive MDMP Settings)** (Nicht-Unicode (inaktive MDMP-Einstellungen)) aus.  
  
    4.  Weisen Sie eine entsprechende Programm-ID zu.  
  
2.  Erstellen Sie ein Open Hub-Ziel:  
  
    1.  Wechseln Sie zur Administrator-Workbench (Transaktionscode RSA1), und wählen Sie im linken Bereich die Option **Open Hub Destination** (Open Hub-Ziel) aus.  
  
    2.  Klicken Sie im mittleren Bereich mit der rechten Maustaste auf eine InfoArea, und wählen Sie anschließend **Create Open Hub Destination** (Open Hub-Ziel erstellen) aus.  
  
    3.  Wählen Sie für **Destination Type**(Zieltyp) die Option **Third Party Tool**(Drittanbietertool) aus, und geben Sie das zuvor erstellte RFC-Ziel ein.  
  
    4.  Speichern und aktivieren Sie das neue Open Hub-Ziel.  
  
3.  Erstellen Sie einen Datenübertragungsprozess (DTP):  
  
    1.  Klicken Sie im mittleren Bereich der InfoArea mit der rechten Maustaste auf das zuvor erstellte Ziel, und wählen Sie anschließend **Create data transfer process** (Datenübertragungsprozess erstellen) aus.  
  
    2.  Konfigurieren, speichern, und aktivieren Sie den Datenübertragungsprozess.  
  
    3.  Klicken Sie im Menü auf **Goto**(Gehe zu) und dann auf **Settings for Batch Manager**(Einstellungen für Batch-Manager).  
  
    4.  Aktualisieren Sie den Wert für **Number of processes** (Anzahl von Prozessen) für die serielle Verarbeitung auf 1.  
  
4.  Erstellen Sie eine Prozesskette:  
  
    1.  Wählen Sie bei der Konfiguration der Prozesskette die Option **Start Using Metadata Chain or API** (Metadatenkette oder API verwenden) als **Scheduling Options** (Planungsoptionen) für **Start Process**(Prozess starten) aus, und fügen Sie dann den zuvor erstellten Datenübertragungsprozess als nachfolgenden Knoten hinzu.  
  
    2.  Speichern und aktivieren Sie die Prozesskette.  
  
     Die SAP BW-Quelle kann die Prozesskette aufrufen, um den Datenübertragungsprozess zu aktivieren.  
  
##  <a name="bkmk_Connect_Database"></a> Herstellen einer Verbindung mit dem SAP NetWeaver BW-System  
 Um eine Verbindung mit dem SAP NetWeaver BW-System, Version 7, herzustellen, verwendet die SQL BW-Quelle den SAP BW-Verbindungs-Manager, der im Lieferumfang des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW-Pakets enthalten ist. Der SAP BW-Verbindungs-Manager ist der einzige [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Verbindungs-Manager, der von der SAP BW-Quelle verwendet werden kann.  
  
 Weitere Informationen zum SAP BW-Verbindungs-Manager finden Sie unter [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
##  <a name="bkmk_Configure_Source"></a> Konfigurieren der SAP BW-Quelle  
 Es gibt folgende Möglichkeiten, um die SAP BW-Quelle zu konfigurieren:  
  
-   Suchen Sie das OHS (Open Hub Service)-Ziel, das zum Extrahieren von Daten verwendet werden soll, und wählen Sie es aus.  
  
-   Wählen Sie eine der folgenden Methoden zum Extrahieren von Daten aus:  
  
    -   Lösen Sie eine Prozesskette aus. In diesem Fall wird der Extrahierungsprozess vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket gestartet.  
  
    -   Warten Sie auf die Benachrichtigung vom SAP NetWeaver BW-System, um mit der Extrahierung zu beginnen. In diesem Fall wird der Extrahierungsprozess vom SAP NetWeaver BW-System gestartet.  
  
    -   Rufen Sie die Daten ab, die einer bestimmten Anforderungs-ID zugeordnet sind. In diesem Fall hat das SAP NetWeaver BW-System die Daten bereits in eine interne Tabelle extrahiert, und die Daten werden gerade vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket gelesen.  
  
-   Je nach der Methode, die Sie zum Extrahieren von Daten ausgewählt haben, stellen Sie die folgenden zusätzlichen Informationen bereit:  
  
    -   Geben Sie für die Option **P – Prozesskette auslösen** den Host- und den Dienstnamen des Gateways, die Programm-ID für das RFC-Ziel und den Namen der Prozesskette an.  
  
    -   Geben Sie für die Option **W – Benachrichtigung abwarten** den Host- und den Servernamen des Gateways sowie die Programm-ID für das RFC-Ziel an. Sie können auch das Timeout (in Sekunden) angeben. Das Timeout ist die maximale Zeit, die die Quelle auf eine Benachrichtigung wartet.  
  
    -   Geben Sie für die Option **E – Nur extrahieren** die Anforderungs-ID an.  
  
-   Geben Sie Regeln für die Zeichenfolgenkonvertierung an. (Konvertieren Sie beispielsweise alle Zeichenfolgen abhängig davon, ob das SAP NetWeaver BW-System ein Unicode-System ist oder nicht, oder konvertieren Sie alle Zeichenfolgen in **varchar** oder **nvarchar**.)  
  
-   Verwenden Sie die ausgewählten Optionen, um die zu extrahierenden Daten in der Vorschau anzuzeigen.  
  
 Sie können auch die Protokollierung von RFC-Funktionsaufrufen durch die Quelle aktivieren. (Diese Protokollierung wird separat von der optionalen Protokollierung ausgeführt, die Sie für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete aktivieren können.) Sie aktivieren die Protokollierung von RFC-Funktionsaufrufen bei der Konfiguration des SAP BW-Verbindungs-Managers, der von der Quelle verwendet wird. Weitere Informationen zur Konfiguration des SAP BW-Verbindungs-Managers finden Sie unter [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
 Wenn Sie nicht alle Werte kennen, die zur Konfiguration der Quelle erforderlich sind, müssen Sie ggf. Ihren SAP-Administrator um Unterstützung bitten.  
  
 Eine exemplarische Vorgehensweise, die zeigt, wie der SAP BW-Verbindungs-Manager sowie die zugehörige Quelle und das zugehörige Ziel konfiguriert und verwendet werden, finden Sie im Whitepaper [Verwenden von SQL Server 2008 Integration Services und SAP BI 7.0](http://go.microsoft.com/fwlink/?LinkID=137090). In diesem Whitepaper wird auch erläutert, wie die erforderlichen Objekte in SAP BW konfiguriert werden.  
  
### Konfigurieren der Quelle mit dem SSIS-Designer  
 Um weitere Informationen zu den Eigenschaften der SAP BW-Quelle zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können, klicken Sie auf eines der folgenden Themen:  
  
-   [Quellen-Editor für SAP BW &#40;Seite Verbindungs-Manager&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)  
  
-   [Quellen-Editor für SAP BW &#40;Seite Spalten&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)  
  
-   [Quellen-Editor für SAP BW &#40;Seite Fehlerausgabe&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)  
  
-   [Quellen-Editor für SAP BW &#40;Seite Erweitert&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)  
  
 Während Sie die SAP BW-Quelle konfigurieren, können Sie auch verschiedene Dialogfelder verwenden, um SAP NetWeaver BW-Objekte zu suchen oder die Quelldaten in der Vorschau anzuzeigen. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu diesen Dialogfeldern zu erhalten:  
  
-   [RFC-Ziel suchen](../../integration-services/data-flow/look-up-rfc-destination.md)  
  
-   [Prozesskette suchen](../../integration-services/data-flow/look-up-process-chain.md)  
  
-   [Anforderungsprotokoll](../../integration-services/data-flow/request-log.md)  
  
-   [Vorschau](../../integration-services/data-flow/preview.md)  
  
## Siehe auch  
 [Microsoft Connector for SAP BW Components](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  