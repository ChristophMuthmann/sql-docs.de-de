---
title: Fehler- und Ereignisreferenz (Reporting Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- messages [Reporting Services]
- errors [Reporting Services]
- Reporting Services, errors and events
- troubleshooting [Reporting Services], errors
- events [Reporting Services]
ms.assetid: 818b4cc1-e65d-4f1a-bf7d-fe269e6dd739
caps.latest.revision: "42"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 0c5111a2b0e1ff5472ae57cf2e8c07834709d628
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="errors-and-events-reference-reporting-services"></a>Fehler- und Ereignisreferenz (Reporting Services)
  Dieses Thema enthält Informationen zu Fehlern und Ereignissen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Protokolldateien enthalten ebenfalls Fehlerinformationen. Weitere Informationen zu den verfügbaren Arten von Protokolldateien und zum Anzeigen der Protokolle finden Sie unter [Reporting Services-Protokolldateien und -Quellen](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Ursachen und Lösungen für Reporting Services-Fehlermeldungen  
 Für die häufig auf [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Websites gesuchten Fehlermeldungen sind Informationen zu Ursachen und Lösungen verfügbar. Weitere Informationen finden Sie unter [Cause and Resolution of Reporting Services Errors](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md).  
  
## <a name="report-server-events"></a>Berichtsserverereignisse  
 Die folgenden Berichtsserverereignisse werden im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anwendungsprotokoll aufgezeichnet.  
  
|Ereignis-ID|Typ|Kategorie|Quelle|Description|  
|--------------|----------|--------------|------------|-----------------|  
|106|Fehler|Zeitplanung|Berichtsserver|Zum Definieren geplanter Operationen (beispielsweise Berichtsabonnierung und -übermittlung) muss SQL Server-Agent ausgeführt werden.|  
|[107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)|Fehler|Start/Herunterfahren|Berichtsserver<br /><br /> Prozessor für Zeitplanung und Übermittlung|*\<Quelle>* kann keine Verbindung mit der Berichtsserver-Datenbank herstellen. Weitere Informationen finden Sie unter [Report Server-Windows-Dienst &#40;MSSQLServer&#41; 107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md).|  
|108|Fehler|Erweiterung|Berichtsserver<br /><br /> Berichts-Manager|*\<Quelle>* kann keine Übermittlungs-, Datenverarbeitungs- oder Renderingerweiterung laden.<br /><br /> Dies ist wahrscheinlich auf eine unvollständige Bereitstellung oder das Entfernen einer Erweiterung zurückzuführen. Weitere Informationen finden Sie unter [Deploying a Data Processing Extension](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md) und [Deploying a Delivery Extension](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md).|  
|109|Informationen|Verwaltung|Berichtsserver<br /><br /> Berichts-Manager|Die Konfigurationsdatei wurde geändert. Weitere Informationen finden Sie unter [Reporting Services Configuration Files](../../reporting-services/report-server/reporting-services-configuration-files.md).|  
|110|Warnung|Verwaltung|Berichtsserver<br /><br /> Berichts-Manager|Eine Einstellung in einer der Konfigurationsdateien wurde geändert und ist daher nicht mehr gültig. Stattdessen wird der Standardwert verwendet. Weitere Informationen finden Sie unter [Reporting Services Configuration Files](../../reporting-services/report-server/reporting-services-configuration-files.md).|  
|111|Fehler|Protokollierung|Berichtsserver<br /><br /> Berichts-Manager|*\<Quelle>* kann das Ablaufverfolgungsprotokoll nicht erstellen. Weitere Informationen finden Sie unter [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).|  
|112|Warnung|Security|Berichtsserver|Der Berichtsserver hat einen möglichen Denial-of-Service-Angriff (DoS) entdeckt. Weitere Informationen finden Sie unter [Sicherheit und Schutz für Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md).|  
|113|Fehler|Protokollierung|Berichtsserver|Der Berichtsserver kann einen Leistungsindikator nicht erstellen.|  
|114|Fehler|Start/Herunterfahren|Berichts-Manager|Der Berichts-Manager kann keine Verbindung mit dem Berichtsserverdienst herstellen.|  
|115|Warnung|Zeitplanung|Prozessor für Zeitplanung und Übermittlung|Eine geplante Aufgabe in der SQL Server-Agent-Warteschlange wurde geändert oder gelöscht.|  
|116|Fehler|Intern|Berichtsserver<br /><br /> Berichts-Manager<br /><br /> Prozessor für Zeitplanung und Übermittlung|Interner Fehler.|  
|117|Fehler|Start/Herunterfahren|Berichtsserver|Die Version der Berichtsserver-Datenbank ist ungültig.|  
|118|Warnung|Protokollierung|Berichtsserver<br /><br /> Berichts-Manager|Das Ablaufverfolgungsprotokoll befindet sich nicht an der erwarteten Verzeichnisposition. Ein neues Ablaufverfolgungsprotokoll wird im Standardverzeichnis erstellt. Weitere Informationen finden Sie unter [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).|  
|119|Fehler|Aktivierung|Berichtsserver<br /><br /> Prozessor für Zeitplanung und Übermittlung|*\<Quelle>* wurde kein Zugriff auf den Inhalt der Berichtsserver-Datenbank gewährt.|  
|120|Fehler|Aktivierung|Berichtsserver|Der symmetrische Schlüssel kann nicht entschlüsselt werden. Wahrscheinlichste Ursache ist eine Änderung des Kontos, unter dem der Dienst ausgeführt wird. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|121|Fehler|Start/Herunterfahren|Berichtsserver|Fehler beim Starten des Remoteprozeduraufruf-Diensts.|  
|122|Warnung|Delivery|Prozessor für Zeitplanung und Übermittlung|Der Prozessor für Zeitplanung und Übermittlung konnte keine Verbindung zum SMTP-Server herstellen, der für die Übermittlung von E-Mail verwendet wird. Weitere Informationen zu SMTP-Serververbindungen finden Sie unter [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).|  
|123|Warnung|Protokollierung|Berichtsserver<br /><br /> Berichts-Manager|Der Berichtsserver konnte das Ablaufverfolgungsprotokoll nicht schreiben. Weitere Informationen zu Ablaufverfolgungsprotokollen finden Sie unter [Berichtsserverdienst-Ablaufverfolgungsprotokoll](../../reporting-services/report-server/report-server-service-trace-log.md).|  
|124|Informationen|Aktivierung|Berichtsserver|Der Berichtsserverdienst wurde initialisiert. Weitere Informationen finden Sie unter [Initialisieren eines Berichtsservers (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).|  
|125|Informationen|Aktivierung|Berichtsserver|Der Schlüssel für die Datenverschlüsselung wurde erfolgreich extrahiert. Weitere Informationen zu Schlüsseln finden Sie unter [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|126|Informationen|Aktivierung|Berichtsserver|Der Schlüssel für die Datenverschlüsselung wurde erfolgreich angewandt. Weitere Informationen zu Schlüsseln finden Sie unter [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|127|Informationen|Aktivierung|Berichtsserver|Der verschlüsselte Inhalt wurde erfolgreich aus der Berichtsserver-Datenbank entfernt. Weitere Informationen zum Löschen von nicht wiederherstellbaren verschlüsselten Daten finden Sie unter [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|128|Fehler|Aktivierung|Berichtsserver|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Komponenten aus verschiedenen Versionen können nicht zusammen verwendet werden.|  
|129|Fehler|Verwaltung|Berichtsserver<br /><br /> Prozessor für Zeitplanung und Übermittlung|Ein verschlüsselter Wert der Konfigurationseinstellung kann nicht entschlüsselt werden.|  
|130|Fehler|Verwaltung|Berichtsserver<br /><br /> Prozessor für Zeitplanung und Übermittlung|*\<Quelle>* kann die Konfigurationsdatei nicht finden. Konfigurationsdateien sind für den Berichtsserver erforderlich.|  
|131|Fehler|Security|Berichtsserver<br /><br /> Prozessor für Zeitplanung und Übermittlung|Ein verschlüsselter Benutzerdatenwert konnte nicht entschlüsselt werden.|  
|132|Fehler|Security|Berichtsserver|Fehler beim Verschlüsseln von Benutzerdaten. Der Wert kann nicht gespeichert werden.|  
|133|Fehler|Verwaltung|Berichtsserver<br /><br /> Berichts-Manager<br /><br /> Prozessor für Zeitplanung und Übermittlung|Fehler beim Laden der Konfigurationsdatei. Dieser Fehler kann auftreten, wenn XML ungültig ist.|  
|134|Fehler|Verwaltung|Berichtsserver|Der Berichtsserver konnte Werte für eine Einstellung in einer Konfigurationsdatei nicht verschlüsseln.|  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen von Reporting Services-Abonnements](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)   
 [Reporting Services Log Files and Sources (Reporting Services-Protokolldateien und -Quellen)](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]
