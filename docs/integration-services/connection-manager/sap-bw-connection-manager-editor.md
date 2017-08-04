---
title: SAP BW-Verbindungs-Manager-Editor | Microsoft Docs
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
- sql13.dts.designer.sapbwconnectionmanager.f1
ms.assetid: ec970319-e749-4753-8675-9cf76ed99669
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a9f07a79e630550d7d0599026a91ee53f5b05d05
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-connection-manager-editor"></a>SAP BW-Verbindungs-Manager-Editor
  Verwenden Sie den **SAP BW-Verbindungs-Manager-Editor** , um die Eigenschaften festzulegen, mit denen eine Verbindung mit einem SAP NetWeaver BW-System, Version 7, hergestellt werden soll.  
  
 Der SAP BW-Verbindungs-Manager stellt Verbindungen mit einem SAP NetWeaver BW-System (Version 7) her, die von einer SAP BW-Quelle oder einem SAP BW-Ziel verwendet werden. Weitere Informationen zum SAP BW-Verbindungs-Manager von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW finden Sie unter [SAP BW-Verbindungs-Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 **So öffnen Sie den SAP BW-Verbindungs-Manager-Editor**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das den SAP BW-Verbindungs-Manager enthält.  
  
2.  Führen Sie im Bereich Verbindungs-Manager auf der Registerkarte **Ablaufsteuerung** einen der folgenden Schritte aus:  
  
    -   Doppelklicken Sie auf den SAP BW-Verbindungs-Manager.  
  
         – oder –  
  
    -   Klicken Sie mit der rechten Maustaste auf den SAP BW-Verbindungs-Manager, und wählen Sie dann **Bearbeiten**aus.  
  
## <a name="options"></a>enthalten  
  
> [!NOTE]  
>  Wenn Sie nicht alle Werte kennen, die zur Konfiguration des Verbindungs-Managers erforderlich sind, müssen Sie ggf. Ihren SAP-Administrator um Unterstützung bitten.  
  
 **Client**  
 Geben Sie die Clientanzahl des Systems an.  
  
 **Sprache**  
 Geben Sie die Sprache an, die vom System verwendet wird. Geben Sie beispielsweise **EN** für Englisch an.  
  
 **Benutzername**  
 Geben Sie den Benutzernamen an, über den eine Verbindung mit dem System hergestellt wird.  
  
 **Kennwort**  
 Geben Sie das Kennwort an, das mit dem Benutzernamen verwendet wird.  
  
 **Einzelnen Anwendungsserver verwenden**  
 Stellen Sie eine Verbindung mit einem einzelnen Anwendungsserver her.  
  
 Um eine Verbindung mit einer Gruppe von Servern mit Lastenausgleich herzustellen, verwenden Sie stattdessen die Option **Lastenausgleich verwenden** .  
  
 **Host**  
 Wenn Sie eine Verbindung mit einem einzelnen Anwendungsserver herstellen, geben Sie den Hostnamen an.  
  
> [!NOTE]  
>  Diese Option ist nur verfügbar, wenn Sie die Option **Einzelnen Anwendungsserver verwenden** ausgewählt haben.  
  
 **Systemnummer**  
 Wenn Sie eine Verbindung mit einem Einzelanwendungsserver herstellen, geben Sie die Systemnummer an.  
  
> [!NOTE]  
>  Diese Option ist nur verfügbar, wenn Sie die Option **Einzelnen Anwendungsserver verwenden** ausgewählt haben.  
  
 **Lastenausgleich verwenden**  
 Stellen Sie einen Verbindung mit einer Gruppe von Servern mit Lastenausgleich her.  
  
 Um eine Verbindung mit einem Einzelanwendungsserver herzustellen, verwenden Sie stattdessen die Option **Einzelnen Anwendungsserver verwenden** .  
  
 **Nachrichtenserver**  
 Beim Herstellen einer Verbindung mit einer Gruppe von Servern mit Lastenausgleich, geben Sie den Namen des Nachrichtenservers an.  
  
> [!NOTE]  
>  Diese Option ist nur verfügbar, wenn Sie die Option **Lastenausgleich verwenden** ausgewählt haben.  
  
 **Gruppieren**  
 Beim Herstellen einer Verbindung mit einer Gruppe von Servern mit Lastenausgleich geben Sie den Namen der Servergruppe an.  
  
> [!NOTE]  
>  Diese Option ist nur verfügbar, wenn Sie die Option **Lastenausgleich verwenden** ausgewählt haben.  
  
 **SID**  
 Beim Herstellen einer Verbindung mit einer Gruppe von Servern mit Lastenausgleich geben Sie die System-ID für die Verbindung an.  
  
> [!NOTE]  
>  Diese Option ist nur verfügbar, wenn Sie die Option **Lastenausgleich verwenden** ausgewählt haben.  
  
 **Protokollverzeichnis**  
 Aktivieren Sie die Protokollierung für die Komponenten von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW.  
  
 Um die Protokollierung zu aktivieren, geben Sie ein Verzeichnis für die Protokolldateien an, die vor und nach jedem RFC-Funktionsaufruf erstellt werden. (Durch diese Protokollierungsfunktion werden viele Protokolldateien im XML-Format erstellt. Da diese Protokolldateien auch alle übertragenen Datenzeilen enthalten, können sie viel Speicherplatz auf dem Datenträger beanspruchen.)  
  
> [!IMPORTANT]  
>  Wenn die übertragenen Daten vertrauliche Informationen enthalten, sind diese auch in den Protokolldateien enthalten.  
  
 Um das Protokollverzeichnis anzugeben, können Sie entweder den Verzeichnispfad manuell eingeben oder auf **Durchsuchen** klicken und zum Protokollverzeichnis navigieren.  
  
 Wenn Sie kein Protokollverzeichnis auswählen, wird die Protokollierung nicht aktiviert.  
  
 **Durchsuchen**  
 Wechseln Sie zu einem Ordner, der als Protokollverzeichnis verwendet wird.  
  
 **Verbindung testen**  
 Testen Sie die Verbindung mithilfe der Werte, die Sie eingegeben haben. Nachdem Sie auf **Verbindung testen**geklickt haben, wird in einem Meldungsfeld angezeigt, ob die Verbindung erfolgreich war oder nicht.  
  
## <a name="see-also"></a>Siehe auch  
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
