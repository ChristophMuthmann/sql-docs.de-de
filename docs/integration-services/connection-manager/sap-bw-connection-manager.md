---
title: SAP BW-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 665bb24c9ccf53ccbe5b5789c2a2014a4770a547
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-connection-manager"></a>SAP BW-Verbindungs-Manager
  Der SAP BW-Verbindungs-Manager ist die Verbindungs-Manager-Komponente von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Daher stellt der SAP BW-Verbindungs-Manager die Konnektivität mit einem SAP NetWeaver BW-System, Version 7, bereit, das für die Quell- und Zielkomponenten von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW erforderlich ist. (SAP BW-Quelle und -Ziel, die Teil des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW-Pakets sind, sind die einzigen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten, die den SAP BW-Verbindungs-Manager verwenden.)  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 Wenn Sie einem Paket einen SAP BW-Verbindungs-Manager hinzufügen, wird die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers auf **SAPBI**festgelegt.  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>Konfigurieren des SAP BW-Verbindungs-Managers  
 Es gibt folgende Möglichkeiten, um den SAP BW-Verbindungs-Manager zu konfigurieren:  
  
-   Geben Sie Client, Benutzernamen, Kennwort und Sprache für die Verbindung an.  
  
-   Wählen Sie aus, ob eine Verbindung mit einem Einzelanwendungsserver oder einer Gruppe von Servern mit Lastenausgleich hergestellt werden soll.  
  
-   Geben Sie die Host- und Systemnummer für einen Einzelanwendungsserver oder Nachrichtenserver, Gruppe und SID für eine Gruppe von Servern mit Lastenausgleich an.  
  
-   Aktivieren Sie die benutzerdefinierte Protokollierung von RFC-Funktionsaufrufen für Komponenten von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. (Diese Protokollierung wird separat von der optionalen Protokollierung ausgeführt, die Sie für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete aktivieren können.) Um die Protokollierung von RFC-Funktionsaufrufen zu aktivieren, geben Sie ein Verzeichnis an, in dem Sie die Protokolldateien speichern, die vor und nach jedem RFC-Funktionsaufruf erstellt werden. (Durch diese Protokollierungsfunktion werden viele Protokolldateien im XML-Format erstellt. Da diese Protokolldateien auch alle übertragenen Datenzeilen enthalten, können sie viel Speicherplatz auf dem Datenträger beanspruchen.) Wenn Sie kein Protokollverzeichnis auswählen, wird die Protokollierung nicht aktiviert.  
  
    > [!IMPORTANT]  
    >  Wenn die übertragenen Daten vertrauliche Informationen enthalten, sind diese auch in den Protokolldateien enthalten.  
  
-   Testen Sie die Verbindung anhand der eingegebenen Werte.  
  
 Wenn Sie nicht alle Werte kennen, die zur Konfiguration des Verbindungs-Managers erforderlich sind, müssen Sie ggf. Ihren SAP-Administrator um Unterstützung bitten.  
  
 Eine exemplarische Vorgehensweise, die zeigt, wie der SAP BW-Verbindungs-Manager sowie die zugehörige Quelle und das zugehörige Ziel konfiguriert und verwendet werden, finden Sie im Whitepaper [Verwenden von SQL Server 2008 Integration Services und SAP BI 7.0](http://go.microsoft.com/fwlink/?LinkID=137090). In diesem Whitepaper wird auch erläutert, wie die erforderlichen Objekte in SAP BW konfiguriert werden.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Konfigurieren der Quelle mit dem SSIS-Designer  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften des SAP BW-Verbindungs-Managers zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [SAP BW-Verbindungs-Manager-Editor](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Connector for SAP BW Components](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
