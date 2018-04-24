---
title: Telemetrie-Feedback - Analytics Platform System | Microsoft Docs
description: Senden Sie Telemetriedaten an Microsoft für Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 747274cd03e9cbd5dd2eab4423458700331358dd
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Senden Sie Telemetrie für Analytics Platform System an Microsoft
Analyseplattformsystem ist eine optionale Telemetrie-Funktion, die Verwaltungskonsole Daten an Microsoft zu senden. 
  
> [!NOTE]  
> In dieser Version überwacht Microsoft Telemetriedaten nicht aktiv. Die Daten werden nur zu Analysezwecken gesammelt wird.  
  
## <a name="privacy"></a>Datenschutz  
Um die maximale Datenschutz zu gewährleisten, wird Sie ohne Aktivierung der Telemetrie APS geliefert. Bevor Sie diese Funktion aktivieren, lesen Sie zunächst die [Microsoft Analytics Platform System Privacy Statement](http://go.microsoft.com/fwlink/?LinkId=400902). Um sich zu registrieren, führen Sie das PowerShell-Skript, das im folgenden beschrieben.  
  
## <a name="enable"></a>Aktivieren Sie Telemetrie  
**DNS-Weiterleitung:** Senden von Telemetriedaten an Microsoft Analytics Platform System für die Verbindung mit dem Internet über einen DNS-Weiterleitung erforderlich. Um dieses Feature zu aktivieren, müssen Sie die DNS-Weiterleitung auf allen Hosts und virtuellen aktivieren. Aufrufen der `Enable-RemoteMonitoring` -Befehl mit der `SetupDnsForwarder` Option aus, um ordnungsgemäß konfigurieren Sie die DNS-Weiterleitung, und aktivieren Sie Telemetrie. Aufrufen der `Enable-RemoteMonitoring` Befehl ohne die `SetupDnsForwarder` option, wenn DNS-Weiterleitung bereits konfiguriert ist und Sie nur Taktüberwachung aktivieren möchten.  
  
> [!IMPORTANT]  
> DNS-Weiterleitung aktivieren, wird die Internetverbindung für alle Hosts und virtuellen geöffnet.  
  
#### <a name="to-enable-feedback"></a>Um Feedback zu aktivieren.  
  
1.  Mit einem Administratorkonto der Appliance-Domäne mit dem Steuerungsknoten hergestellt (***Appliance_domain *-CTL01**), und öffnen Sie eine Eingabeaufforderung unter Verwendung von Windows-Administratoranmeldeinformationen.  
  
2.  Navigieren Sie zum folgenden Verzeichnis: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importieren Sie das Modul `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Sie importieren muss zwei Punkte im Befehl verwenden.  
  
    **Beispiel:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Aufrufen der `Enable-RemoteMonitoring` Befehl.  
  
    > [!NOTE]  
    > Das Skript wird davon ausgegangen, dass die Verbindung mit dem Internet ordnungsgemäß funktioniert und die Internet-Verbindung wird nicht überprüft.  
  
    1.  Verwenden Sie folgenden Befehl erstmalig die Telemetrie zu aktivieren, stellen Sie sicher, dass alle DNS-Weiterleitungen ordnungsgemäß konfiguriert sind. Ersetzen Sie in diesem Beispiel wird die DNS-weitergeleitete IP-Adresse `xx.xx.xx.xx` mit der DNS-Weiterleitung IP-Adresse in Ihrer Umgebung.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Bei der DNS-Weiterleitungen bereits Konfiguration wie z. B. Telemetrie Reaktivierung zuvor deaktiviert werden, verwenden Sie den folgenden Befehl, um Telemetrie ohne Konfiguration der DNS-Weiterleitung zu aktivieren.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Sie werden aufgefordert, die zum Lesen und zu bestätigen, dass APS Informationen über die Anwendung gesammelt werden. Es wird ein Link in der APS-datenschutzerklärung diese können Sie kopieren und fügen Sie alle Internet-Browser zur Überprüfung vorhanden sein.  
  
6.  Geben Sie **Y** zu übernehmen und das Feedback zu abonnieren, oder geben **N** nicht zu akzeptieren.  
  
7.  Wenn Sie eingegeben haben **Y** werden eine Reihe von Befehlen, die ausgeführt werden und die Telemetrie (und optional die DNS-Weiterleitung) aktiviert die Funktion auf Ihrer Anwendung. Wenden Sie sich an CSS um Unterstützung zu erhalten, wenn Sie sehen Fehler oder die Informationen, die führt Sie der Meinung sind, dass der Befehl nicht erfolgreich war.  
  
Wenn Sie eingegeben haben **N**keine Befehle durchgeführt werden und die Funktion wird nicht aktiviert werden, und keine weiteren erforderlich.  
  
Es gibt keinen Schaden beim Ausführen der `Enable-RemoteMonitoring` Befehl mehrmals. Wenn die DNS-Weiterleitung bereits festgelegt ist, erhalten Sie eine Warnmeldung zeigt an, dass dies der Fall ist.  
  
## <a name="disable"></a>Deaktivieren der Telemetrie  
Deaktivieren der Telemetrie werden alle Vorgänge beendet, die Informationen über den Status des Geräts auf die APS Überwachungsdienst in der Cloud kommunizieren.  
  
> [!IMPORTANT]  
> Ausführen des Vorgangs wird der DNS-Weiterleitung oder Internetverbindung verwendet, die von weiteren Funktionen in der Einheit u. u. nicht deaktivieren.  
  
#### <a name="to-disable-telemetry"></a>So deaktivieren Sie Telemetrie  
  
1.  Mit einem Administratorkonto der Appliance-Domäne mit dem Steuerungsknoten hergestellt (***Appliance_domain *-CTL01**), und öffnen Sie ein PowerShell-Fenster mit Administratorrechten aus.  
  
2.  Navigieren Sie zum folgenden Verzeichnis: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importieren Sie das Modul `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Sie importieren muss zwei Punkte im Befehl verwenden.  
  
    **Beispiel:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Aufrufen der `Disable-RemoteMonitoring` Befehl ohne Parameter. Mit diesem Befehl wird das Senden von Feedback beendet. (Dies nicht der lokalen Überwachung wirkt.) Der Befehl wird jedoch nicht die DNS-Weiterleitung deaktivieren und/oder alle Internetkonnektivität deaktivieren. Dies muss manuell durchgeführt werden, nach dem Deaktivieren von erfolgreich Feedback.  
  
    **Beispiel:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Wenden Sie sich an CSS um Unterstützung zu erhalten, wenn Sie sehen Fehler oder die Informationen, die führt Sie der Meinung sind, dass der Befehl nicht erfolgreich war.  
  
Es gibt keinen Schaden beim Ausführen der `Disable-RemoteMonitoring` Befehl mehrmals.  
  
## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie in den folgenden Themen:
- [Überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Überwachen Sie die Anwendung mithilfe von Systemsichten &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Überwachen Sie die Anwendung mit System Center Operationsmanager &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Verwenden Sie nicht-Appliance DNS-Namen auflösen eine DNS-Weiterleitung &#40;Analyseplattformsystem&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
