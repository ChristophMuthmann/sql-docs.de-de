---
title: Initialisieren eines Berichtsservers (SSRS-Konfigurations-Manager) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], initializing
- initialization process [Reporting Services]
- checking report server initializations
- scale-out deployments [Reporting Services]
- initializing report servers [Reporting Services]
- verifying report server initializations
ms.assetid: 861d4ec4-1085-412c-9a82-68869a77bd55
caps.latest.revision: "10"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 1f915a96de6567369146030cefa4f126e74a53f4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="ssrs-encryption-keys---initialize-a-report-server"></a>SSRS-Verschlüsselungsschlüssel: Initialisieren eines Berichtsservers
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]kann ein initialisierter Server Daten in einer Berichtsserver-Datenbank verschlüsseln und entschlüsseln. Die Initialisierung ist die Voraussetzung für Berichtsservervorgänge. Die Initialisierung wird ausgeführt, wenn der Berichtsserverdienst zum ersten Mal gestartet wird. Sie wird ebenfalls ausgeführt, wenn Sie den Berichtsserver mit vorhandenen Bereitstellung verknüpfen, oder wenn Sie die Schlüssel manuell, als Teil des Wiederherstellungsprozesses neu erstellen. Weitere Informationen dazu, wie und warum Verschlüsselungsschlüssel verwendet werden, finden Sie unter [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md) und [Speichern verschlüsselter Berichtsserverdaten (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md).  
  
 Verschlüsselungsschlüssel basieren teilweise auf den Profilinformationen des Berichtsserverdiensts. Wenn Sie die Benutzeridentität ändern, mit der Sie den Berichtsserverdienst ausführen, müssen Sie die Schlüssel entsprechend aktualisieren. Wenn Sie das Reporting Services-Konfigurationstool verwenden, um Ihre Identität zu ändern, wird dieser Schritt automatisch für Sie erledigt.  
  
 Falls die Initialisierung fehlschlägt, sendet der Berichtsserver einen **RSReportServerNotActivated** -Fehler als Antwort auf Benutzer- und Dienstanforderungen zurück. In diesem Fall müssen Sie möglicherweise die Problembehandlung für das System oder die Serverkonfiguration ausführen. Weitere Informationen finden Sie unter [SSRS: Beheben von Problemen und Fehlern bei Reporting Services](http://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) in Technet Wiki.  
  
## <a name="overview-of-the-initialization-process"></a>Übersicht über den Initialisierungsprozess  
 Der Initialisierungsprozess erstellt und speichert einen symmetrischen Schlüssel, der zur Verschlüsselung verwendet wird. Der symmetrische Schlüssel wird von den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Kryptografiediensten erstellt und anschließend vom Berichtsserverdienst verwendet, um Daten zu ver- und entschlüsseln. Der symmetrische Schlüssel selbst wird mit einem asymmetrischen Schlüssel verschlüsselt.  
  
 Die folgenden Schritte beschreiben den Initialisierungsprozess:  
  
1.  Beim ersten Start liest der Berichtsserverdienst die Datei RSReportServer.config, um die Installations-ID und die Datenbank-Verbindungsinformationen abzurufen.  
  
2.  Der Berichtsserverdienst fordert einen öffentlichen Schlüssel von den Kryptografiediensten an. Windows erstellt einen privaten und öffentlichen Schlüssel und sendet den öffentlichen Schlüssel an den Berichtsserverdienst.  
  
3.  Der Berichtsserverdienst stellt eine Verbindung zur Berichtsserver-Datenbank her und speichert die Werte der Installations-ID und des öffentlichen Schlüssels.  
  
4.  Der Berichtsserverdienst ruft die Kryptografiedienste erneut auf und fordert diesmal einen symmetrischen Schlüssel an. Windows erstellt den symmetrischen Schlüssel.  
  
5.  Der Berichtsserverdienst stellt erneut eine Verbindung zur Berichtsserver-Datenbank her und fügt den symmetrischen Schlüssel zu den Werten des öffentlichen Schlüssels und der Installations-ID hinzu, die in Schritt 3 gespeichert wurden. Bevor der Berichtsserverdienst seinen öffentlichen Schlüssel speichert, verwendet er ihn zum Verschlüsseln des symmetrischen Schlüssels. Sobald der symmetrische Schlüssel gespeichert ist, gilt der Berichtsserver als initialisiert und verfügbar.  
  
## <a name="initializing-a-report-server-for-scale-out-deployment"></a>Initialisieren eines Berichtsservers für die Bereitstellung für horizontales Skalieren  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt ein Bereitstellungsmodell für horizontales Skalieren, bei dem eine einzelne Berichtsserver-Datenbank für mehrere Berichtsserverinstanzen verwendet wird. Um an einer Bereitstellung für horizontales Skalieren teilzunehmen, muss ein Berichtsserver seine Kopie des symmetrischen Schlüssels in der freigegebenen Datenbank erstellen und speichern. Obwohl ein einzelner symmetrischer Schlüssel von Servern verwendet wird, die die Datenbank verwenden, verfügt jeder Berichtsserver über eine Kopie des Schlüssels. Jede Kopie variiert hinsichtlich ihrer eindeutigen Verschlüsselung des öffentlichen Schlüssels, deren Besitzer sie ist.  
  
 Die ersten Schritte zum Initialisieren eines Berichtsservers zur Bereitstellung für horizontales Skalieren stimmen mit den ersten drei Schritten überein, die die Initialisierung einer Kombination aus einem einzelnen Server und einer Datenbank beschreiben.  
  
 Der Initialisierungsprozess für eine Bereitstellung für horizontales Skalieren unterscheidet sich darin, wie der Berichtsserver den symmetrischen Schlüssel abruft. Wenn der erste Server initialisiert ist, ruft er von Windows den symmetrischen Schlüssel ab. Wenn der zweite Server während der Konfiguration der Bereitstellung für horizontales Skalieren initialisiert wird, ruft er den symmetrischen Schlüssel vom Berichtsserverdienst ab, der bereits initialisiert ist. Die erste Berichtsserverinstanz verwendet den öffentlichen Schlüssel der zweiten Instanz, um eine verschlüsselte Kopie des symmetrischen Schlüssels für die zweite Berichtsserverinstanz zu erstellen. Der symmetrische Schlüssel wird an keinem Punkt dieses Prozesses als Nur-Text offen gelegt  
  
## <a name="how-to-initialize-a-report-server"></a>Initialisieren eines Berichtsservers  
  
-   Verwenden Sie das Reporting Services-Konfigurationstool, um den Berichtsserver zu initialisieren. Die Initialisierung findet automatisch beim Erstellen und Konfigurieren der Berichtsserver-Datenbank statt. Weitere Informationen finden Sie unter [Konfigurieren einer Verbindung mit der Berichtsserver-Datenbank &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
-   Um einen Berichtsserver für die Bereitstellung für horizontales Skalieren zu initialisieren, verwenden Sie die Initialisierungsseite im Reporting Services-Konfigurationstool oder das Hilfsprogramm **RSKeymgmt**. Detaillierte Anleitungen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
> [!NOTE]  
>  **RSKeymgmt** ist eine Konsolenanwendung, die Sie über eine Befehlszeile auf einem Computer ausführen, der eine Berichtsserverinstanz hostet, die bereits Teil einer Bereitstellung für horizontales Skalieren ist. Wenn Sie das Hilfsprogramm ausführen, geben Sie Argumente zum Auswählen einer Remote-Berichtsserverinstanz an, die Sie initialisieren möchten.  
  
 Ein Berichtsserver wird nur initialisiert, wenn eine Übereinstimmung zwischen der Installations-ID und dem öffentlichen Schlüssel vorliegt. Bei einer Übereinstimmung wird ein symmetrischer Schlüssel erstellt, der die umkehrbare Verschlüsselung ermöglicht. Wenn die Übereinstimmung fehlschlägt, wird der Berichtsserver deaktiviert. In diesem Fall werden Sie möglicherweise aufgefordert, einen Sicherungsschlüssel anzuwenden oder die verschlüsselten Daten zu löschen, wenn ein Sicherungsschlüssel nicht verfügbar oder ungültig ist. Weitere Informationen zu Verschlüsselungsschlüsseln, die von einem Berichtsserver verwendet werden, finden Sie unter [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).  
  
> [!NOTE]  
>  Sie können auch den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -WMI-Anbieter (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation) verwenden, um einen Berichtsserver programmgesteuert zu initialisieren. Weitere Informationen finden Sie unter [Zugreifen auf den Reporting Services-WMI-Anbieter](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="how-to-confirm-a-report-server-initialization"></a>Bestätigen der Initialisierung eines Berichtsservers  
 Um die Initialisierung des Berichtsservers zu bestätigen, pingen Sie den Berichtsserver-Webdienst, indem Sie **http://<Servername\</reportserver** in das Befehlsfenster eingeben. Wenn der **RSReportServerNotActivated** -Fehler auftritt, ist die Initialisierung fehlgeschlagen.  
  
## <a name="see-also"></a>Siehe auch
[Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)
  
  
