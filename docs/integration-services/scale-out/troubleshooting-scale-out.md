---
title: "Problembehandlung für Scale Out mit SQL Server Integration Services (SSIS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 56d61bc6ba76514ba2291243002a7423ec8e265c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-scale-out"></a>Problembehandlung für Scale Out

SSIS-Scale Out umfasst die Kommunikation zwischen SSISDB, dem Scale Out-Masterdienst und dem Scale Out-Workerdienst. Gelegentlich wird diese Kommunikation u.a. aufgrund von Konfigurationsfehlern und fehlenden Zugriffsberechtigungen unterbrochen. Dieser Artikel soll Sie bei der Behandlung von Problemen mit der Scale Out-Konfiguration unterstützen.

Führen Sie die unten aufgeführten Schritte nacheinander aus, bis Ihr Problem gelöst ist, um den Symptomen, auf die Sie stoßen, auf den Grund zu gehen.

### <a name="symptoms"></a>**Symptome** 
Der Scale Out-Master kann keine Verbindung mit SSISDB herstellen. 

Die Master-Eigenschaften können im Scale Out-Manager nicht angezeigt werden.

Die Mastereigenschaften werden nicht in [SSISDB].[catalog].[master_properties] eingefügt.

### <a name="solution"></a>**Lösung**
Schritt 1: Überprüfen Sie, ob Scale Out aktiviert ist.

Klicken Sie mit der rechten Maustaste im SSMS-Objektexplorer auf den Knoten **SSISDB**, und überprüfen Sie, ob die **Scale Out-Funktion aktiviert ist**.

![Scale Out ist aktiviert](media\isenabled.PNG)

Wenn der Eigenschaftswert FALSE ist, aktivieren Sie Scale Out, indem Sie die gespeicherte Prozedur [SSISDB].[catalog].[enable_scaleout] aufrufen.

Schritt 2: Überprüfen Sie, ob der in der Konfigurationsdatei des Scale Out-Masters angegebene SQL Server-Name richtig ist, und starten Sie den Scale Out-Masterdienst neu.

### <a name="symptoms"></a>**Symptome** 
Der Scale Out-Worker kann keine Verbindung mit dem Scale Out-Master herstellen.

Der Scale Out-Worker wird nicht angezeigt, nachdem er dem Scale Out-Manager hinzugefügt wurde.

Der Scale Out-Worker wird in [SSISDB].[catalog].[worker_agents] nicht angezeigt.

Der Scale Out-Workerdienst wird ausgeführt, obwohl der Scale Out-Worker offline ist.

### <a name="solutions"></a>**Lösungen** 
Überprüfen Sie die Fehlermeldungen im Protokoll des Scale Out-Workerdiensts unter \<Treiber\>:\Users\\*[Konto, das den Worker-Dienst ausführt]*\AppData\Local\SSIS\Cluster\Agent.

**Fall** 

System.ServiceModel.EndpointNotFoundException: Unter https://*[Computername]:[Port]*/ClusterManagement/ wurde keine Überwachung durch einen Endpunkt durchgeführt, der die Meldung annehmen konnte.

Schritt 1: Überprüfen Sie, ob die in der Konfigurationsdatei des Scale Out-Masterdiensts angegebene Portnummer richtig ist, und starten Sie den Scale Out-Masterdienst neu. 

Schritt 2: Überprüfen Sie, ob der in der Konfigurationsdatei des Scale Out-Workerdiensts angegebene Masterendpunkt richtig ist, und starten Sie den Scale Out-Workerdienst neu.

Schritt 3: Überprüfen Sie, ob der Firewallport auf dem Scale Out-Masterknoten geöffnet ist.

Schritt 4: Lösen Sie alle anderen bestehenden Verbindungsprobleme zwischen dem Scale Out-Masterknoten und dem Scale Out-Workerknoten.

**Fall**

System.ServiceModel.Security.SecurityNegotiationException: Es konnte keine Vertrauensstellung für den sicheren SSL/TLS-Kanal mit Autorität „*[Computername]:[Port]*“ eingerichtet werden. ---> System.Net.WebException: Die zugrunde liegende Verbindung wurde geschlossen: Für den geschützten SSL/TLS-Kanal konnte keine Vertrauensstellung hergestellt werden. ---> System.Security.Authentication.AuthenticationException: Das Remotezertifikat ist laut Validierungsverfahren ungültig.

Schritt 1: Installieren Sie das Scale Out-Masterzertifikat auf dem Scale Out-Workerknoten im Stammzertifikatspeicher des lokalen Computers, falls noch nicht geschehen, und starten Sie den Scale Out-Workerdienst neu.

Schritt 2: Überprüfen Sie, ob der Hostname im Masterendpunkt im allgemeinen Namen des Scale Out-Masterzertifikats enthalten ist. Falls dies nicht der Fall ist, setzen Sie den Masterendpunkt in der Konfigurationsdatei des Scale Out-Workers zurück, und starten Sie den Scale Out-Workerdienst neu. 

> [!Note]
> Wenn Sie den Hostnamen des Masterendpunkts aufgrund von DNS-Einstellungen nicht ändern können, müssen Sie das Scale Out-Masterzertifikat ändern. Informationen dazu finden Sie unter [Deal with certificates in SSIS Scale Out (Umgang mit Zertifikaten in SSIS Scale Out)](deal-with-certificates-in-ssis-scale-out.md).

Schritt 3: Überprüfen Sie, ob der Fingerabdruck des Masters, der in der Konfiguration des Scale Out-Workers angegeben wird, mit dem Fingerabdruck des Zertifikats des Scale Out-Masters übereinstimmt. 

**Fall**

System.ServiceModel.Security.SecurityNegotiationException: Es konnte kein sicherer Kanal für SSL/TLS mit der Stelle „*[Computername]:[Port]*“ eingerichtet werden. ---> System.Net.WebException: Die Anforderung wurde abgebrochen: Es konnte kein sicherer SSL/TLS-Kanal erstellt werden.

Schritt 1: Überprüfen Sie mithilfe des folgenden Befehls, ob das Konto, das den Scale Out-Workerdienst ausführt, Zugriff auf das Zertifikat des Scale Out-Workers hat.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

Wenn das Konto keinen Zugriff hat, erteilen Sie Ihm diesen mithilfe des folgenden Befehls, und starten Sie den Scale Out-Workerdienst neu.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**Fall**

System.ServiceModel.Security.MessageSecurityException: Die HTTP-Anforderung wurde mit Clientauthentifizierungsschema „Anonym“ nicht zugelassen. ---> System.Net.WebException: Der Remoteserver hat einen Fehler zurückgegeben: 403 Verboten.

Schritt 1: Installieren Sie das Zertifikat des Scale Out-Workers auf dem Scale Out-Masterknoten im Stammzertifikatspeicher des lokalen Computers, falls noch nicht geschehen, und starten Sie den Scale Out-Workerdienst neu.

Schritt 2: Bereinigen Sie unnötige Zertifikate auf dem Scale Out-Masterknoten im Stammzertifikatspeicher des lokalen Computers.

Schritt 3: Konfigurieren Sie Schannel (sicherer Kanal), damit dieser keine Liste von vertrauenswürdigen Stammzertifizierungsstellen mehr während des TLS/SSL-Handshakevorgangs sendet, indem Sie den Registrierungseintrag unterhalb des Scale Out-Masterknotens hinzufügen.

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Wertname: SendTrustedIssuerList 

Werttyp: REG_DWORD 

Wertdaten: 0 (FALSE)

**Fall**

System.ServiceModel.CommunicationException: Ein Fehler ist beim Ausführen der HTTP-Anforderung von „https://*[Compuername]:[Port]*/ClusterManagement/“ aufgetreten. Dies könnte daran liegen, dass das Serverzertifikat nicht richtig mit „HTTP.SYS“ im HTTPS-Fall konfiguriert wurde. Ein weiterer Grund könnte ein Konflikt mit der Sicherheitsbindung zwischen Client und Server sein. 

Schritt 1: Überprüfen Sie mithilfe des folgenden Befehls, ob das Zertifikat des Scale Out-Masters auf dem Masterknoten richtig an den Port im Masterendpunkt gebunden ist. Überprüfen Sie, ob der angezeigte Zertifikathash mit dem Zertifikatfingerabdruck des Scale Out-Masters übereinstimmt.

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

Wenn die Bindung nicht korrekt durchgeführt wurde, setzen Sie den Vorgang mithilfe des folgenden Befehls zurück, und starten Sie den Scale Out-Workerdienst neu.

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**Symptome**
Die Validierung ist bei der Herstellung einer Verbindungen zwischen dem Scale Out-Worker und dem Scale Out-Master im Scale Out-Manager fehlgeschlagen, und es wird folgende Fehlermeldung angezeigt: „Der Zertifikatspeicher auf dem Computer konnte nicht geöffnet werden.“

### <a name="solution"></a>**Lösung**

Schritt 1: Führen Sie den Scale Out-Manager als Administrator aus. Wenn Sie Ihn über SSMS öffnen, müssen Sie als Administrator angemeldet sein.

Schritt 2: Starten Sie den Remoteregistrierungsdienst auf dem Computer, falls dieser nicht ausgeführt wird.

### <a name="symptoms"></a>**Symptome**
Die Ausführung in Scale Out startet nicht.

### <a name="solution"></a>**Lösung**

Überprüfen Sie den Status der Computer, die Sie zum Ausführen der Pakete in [SSISDB].[catalog].[worker_agents] ausgewählt haben. Es muss mindestens ein Worker online und aktiviert sein.

### <a name="symptoms"></a>**Symptome** 
Die Pakete werden erfolgreich ausgeführt, allerdings wird keine Meldung protokolliert.

### <a name="solution"></a>**Lösung**

Überprüfen Sie, ob die SQL Server-Authentifizierung zulässig für SQL Server ist, der SSISDB hostet.

> [!Note]  
> Wenn Sie das Konto für die Scale Out-Protokollierung geändert haben, prüfen Sie die Seite [Change the Account for Scale Out Logging (Ändern des Kontos für die Scale Out-Protokollierung)](change-logdb-account.md), und überprüfen Sie die für die Protokollierung verwendete Verbindungszeichenfolge.

### <a name="symptoms"></a>**Symptome**
Die Fehlermeldungen in dem Paketausführungsbericht reichen für die Problembehandlung nicht aus.

### <a name="solution"></a>**Lösung**
Weitere Ausführungsprotokolle finden Sie unter „TasksRootFolder“, der in „WorkerSettings.config“ konfiguriert ist. Standardmäßig lautet der Pfad wie folgt: \<Treiber\>:\Users\\*[Konto]*\AppData\Local\SSIS\ScaleOut\Tasks. Es handelt sich um das *[Konto]*, das den Scale Out-Workerdienst mit dem Standardwert „SSISScaleOutWorker140“ ausführt.

Führen Sie den folgenden T-SQL-Befehl aus, um das Protokoll für die Paketausführung mit der *[Ausführungs-ID]* zu suchen, sodass die *[Task-ID]* zurückgegeben wird. Suchen sie anschließend den mit der *[Task-ID]* benannten Unterordner unter „TasksRootFolder“.<sup>1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> Diese Abfrage soll ausschließlich der Problembehandlung dienen und kann verändert werden, wenn die Vorgänge zur Protokollierung bzw. Diagnose für den Scale Out-Worker zukünftig verbessert wird. 
