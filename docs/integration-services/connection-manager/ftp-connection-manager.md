---
title: FTP-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 051dc7db2ef8aa475fa8739b097edd93d8286524
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="ftp-connection-manager"></a>FTP-Verbindungs-Manager
  Mit einem FTP-Verbindungs-Manager kann ein Paket eine Verbindung mit einem FTP-Server (File Transfer Protocol) herstellen. Der FTP-Task von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet diesen Verbindungs-Manager.  
  
 Wenn Sie einem Paket einen FTP-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit als FTP-Verbindung aufgelöst werden kann, die Eigenschaften des Verbindungs-Managers festlegt und der **Connections** -Sammlung im Paket den Verbindungs-Manager hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **FTP**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um den FTP-Verbindungs-Manager zu konfigurieren:  
  
-   Geben Sie einen Servernamen und einen Serverport an.  
  
-   Geben Sie den anonymen Zugriff an, oder stellen Sie einen Benutzernamen und ein Kennwort für die Standardauthentifizierung bereit.  
  
    > [!IMPORTANT]  
    >  Der FTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
-   Legen Sie das Timeout, die Wiederholungsversuche und die jeweils zu kopierende Datenmenge fest.  
  
-   Geben Sie an, ob der FTP-Verbindungs-Manager den passiven oder aktiven Modus verwendet.  
  
 Sie müssen u. U. die folgenden Standardwerte des Verbindungs-Managers ändern, je nach Konfiguration der FTP-Site, zu der der FTP-Verbindungs-Manager eine Verbindung herstellt:  
  
-   Der Serverport wird auf 21 festgelegt. Sie sollten den Port angeben, an dem von der FTP-Site gelauscht wird.  
  
-   Der Benutzername ist auf "anonym" festgelegt. Sie sollten die für die FTP-Site erforderlichen Anmeldeinformationen bereitstellen.  
  
## <a name="activepassive-modes"></a>Aktiver/passiver Modus  
 Ein FTP-Verbindungs-Manager kann Dateien mithilfe des aktiven oder passiven Modus senden und empfangen. Im aktiven Modus wird die Datenverbindung vom Server initiiert, im passiven Modus wird sie vom Client initiiert.  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>Konfiguration des FTP-Verbindungs-Managers  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können, finden Sie unter [FTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/ftp-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
## <a name="ftp-connection-manager-editor"></a>FTP-Verbindungs-Manager-Editor
  Mithilfe des Dialogfelds **FTP-Verbindungs-Manager-Editor** können Sie Eigenschaften für Verbindungen mit einem FTP-Server angeben.  
  
> [!IMPORTANT]  
>  Der FTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 Weitere Informationen zum FTP-Verbindungs-Manager finden Sie unter [FTP Connection Manager](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
### <a name="options"></a>enthalten  
 **Servername**  
 Geben Sie den Namen des FTP-Servers an.  
  
 **Serverport**  
 Geben Sie die Portnummer des FTP-Servers an, der für die Verbindung verwendet werden soll. Der Standardwert dieser Eigenschaft ist **21**.  
  
 **Benutzername**  
 Geben Sie einen Benutzernamen für den Zugriff auf den FTP-Server an. Der Standardwert dieser Eigenschaft ist **anonymous**.  
  
 **Kennwort**  
 Geben Sie das Kennwort für den Zugriff auf den FTP-Server an.  
  
 **Timeout (in Sekunden)**  
 Geben Sie die Dauer in Sekunden an, bevor ein Timeout für den Task eintritt. Der Wert **0** gibt einen unbegrenzten Zeitraum an. Der Standardwert dieser Eigenschaft ist **60**.  
  
 **Passivmodus verwenden**  
 Geben Sie an, ob die Verbindung durch den Server oder durch den Client initiiert wird. Die Initiierung der Verbindung durch den Server erfolgt im Aktivmodus; der Client aktiviert die Verbindung im Passivmodus. Der Standardwert dieser Eigenschaft ist der **Aktivmodus**.  
  
 **Wiederholungen**  
 Geben Sie die Häufigkeit an, mit der der Task versucht, eine Verbindung herzustellen. Der Wert **0** gibt eine unbegrenzte Anzahl von Versuchen an.  
  
 **Segmentgröße (in KB)**  
 Geben Sie eine Segmentgröße in KB für das Übertragen von Daten an.  
  
 **Verbindung testen**  
 Nachdem die Konfiguration des FTP-Verbindungs-Managers abgeschlossen ist, bestätigen Sie die Gültigkeit der Verbindung, indem Sie auf **Verbindung testen**klicken.  
  
## <a name="see-also"></a>Siehe auch  
 [FTP-Task](../../integration-services/control-flow/ftp-task.md)   
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
