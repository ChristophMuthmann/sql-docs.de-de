---
title: "Problembehandlung bei der SQL Serverintegration Services (SSIS) für horizontales Skalieren | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 41bb853dd08591596f6f5baa918e174d0c26a6b5
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="troubleshooting-scale-out"></a>Problembehandlung für horizontales Skalieren

Umfasst das SSIS-horizontal skalieren Communtication zwischen SSISDB, Scale-Out-Master-Dienst und Scale-Out-Worker-Dienst. In einigen Fällen ist die Kommunikation unterbrochen, weil eine Konfigurationsfehler, fehlender Zugriffsberechtigungen und andere Gründe vorliegen. Dieses Dokument unterstützt Sie horizontal skalieren Konfigurationsprobleme zu beheben.

Um die Symptome zu forschen, die auftreten, gehen Sie nacheinander, bis das Problem behoben ist.

### <a name="symptoms"></a>**Symptome** 
Scale-Out-Master herstellen nicht SSISDB. 

Haupteigenschaften können nicht in Scale-Out-Manager angezeigt.

Haupteigenschaften werden nicht in [SSISDB] gefüllt. [Catalog]. [Master_properties]

### <a name="solution"></a>**Lösung**
Schritt 1: Überprüfen Sie, ob horizontal skalieren aktiviert ist.

Mit der rechten Maustaste **SSISDB** Knoten im Objekt-Explorer von SSMS und Kontrollkästchen **horizontal skalieren Feature aktiviert**.

![Horizontales Skalieren aktiviert ist](media\isenabled.PNG)

Wenn der Eigenschaftswert auf "false" ist, aktivieren Sie horizontal skalieren, durch Aufrufen der gespeicherten Prozedur [SSISDB]. [Catalog]. [Enable_scaleout].

Schritt 2: Überprüfen Sie, ob in Scale-Out-Master-Konfigurationsdatei angegebenen Sql Server-Name richtig ist und Scale-Out-Master-Dienst neu.

### <a name="symptoms"></a>**Symptome** 
Scale-Out-Worker herstellen nicht Scale-Out-Master.

Scale-Out-Worker wird nicht angezeigt, nach dem im Scale-Out-Manager hinzufügen

Scale-Out-Worker ist nicht in [SSISDB] angezeigt. [Catalog]. [Worker_agents]

Scale-Out-Worker-Dienst ausgeführt wird, während Scale-Out-Worker offline ist,

### <a name="solutions"></a>**Projektmappen** 
Überprüfen Sie die Fehlermeldungen im Protokoll der Scale-Out-Worker-Diensts unter \<Treiber\>: \Users\\*[Account Worker-Dienst ausgeführt]*\AppData\Local\SSIS\Cluster\Agent.

**Fall** 

System.ServiceModel.EndpointNotFoundException: Es wurde kein Endpunkt https:// hört*[Computername]: [Port]*/ClusterManagement/, die die Nachricht akzeptieren konnte.

Schritt 1: Überprüfen Sie, ob in der Dienstkonfigurationsdatei Scale-Out-Master angegebene Portnummer richtig ist und Scale-Out-Master-Dienst neu. 

Schritt 2: Überprüfen Sie, ob der master-Endpunkt in Scale-Out-Worker-Dienstkonfiguration angegebene richtig ist und Scale-Out-Worker-Dienst neu.

Schritt 3: Überprüfen Sie, ob der Firewallport für den Scale-Out-Master-Knoten geöffnet ist.

Schritt 4: Beheben Sie alle anderen Verbindungsprobleme zwischen Scale-Out-Master und Scale-Out-Worker-Knoten.

**Fall**

System.ServiceModel.Security.SecurityNegotiationException: Konnte keine Vertrauensstellung für den sicheren SSL/TLS-Kanal mit den Berechtigungen hergestellt "*[Computername]: [Port]*". ---> System.NET.WebException:: die zugrunde liegende Verbindung wurde geschlossen: konnte keine Vertrauensstellung für den sicheren SSL/TLS-Kanal hergestellt. ---> System.Security.Authentication.AuthenticationException: Das Remotezertifikat ist laut Validierungsverfahren ungültig.

Schritt 1: Install Skalierung Out Master das Zertifikat für den Zertifikatspeicher des lokalen Computers auf Scale-Out-Worker-Knoten Stammzertifizierungsstellen ggf. noch nicht installiert und Scale-Out-Worker-Dienst neu starten.

Schritt 2: Überprüfen Sie, ob der Hostname in der master-Endpunkt im CNs Scale Out Master Zertifikat enthalten ist. Wenn dies nicht der Fall ist, Zurücksetzen des master-Endpunkts in Scale-Out-Worker-Konfigurationsdatei, und Scale-Out-Worker-Dienst neu. 

> [!Note]
> Ist es nicht möglich, den Hostnamen des master-Endpunkt aufgrund von DNS-Einstellungen zu ändern, müssen Sie das Zertifikat Scale-Out-Master zu ändern. Finden Sie unter [Umgang mit Zertifikaten in SSIS horizontal skalieren](deal-with-certificates-in-ssis-scale-out.md).

Schritt 3: Überprüfen Sie, ob der Hauptschlüssel Fingerabdruck in Scale-Out-Worker-Konfiguration angegebenen den Fingerabdruck des Zertifikats Scale-Out-Master übereinstimmt. 

**Fall**

System.ServiceModel.Security.SecurityNegotiationException: Konnte keine sicheren Kanal für SSL/TLS-Verbindungen herstellen, mit den Berechtigungen "*[Computername]: [Port]*". ---> System.NET.WebException:: die Anforderung wurde abgebrochen: sicheren SSL/TLS-Kanal konnte nicht erstellt werden.

Schritt 1: Überprüfen Sie, ob das Scale-Out-Worker-Dienst-Konto Zugriff auf Scale-Out-Worker-Zertifikat von den folgenden Befehl hat.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

Wenn das Konto keinen Zugriff hat, erteilen, indem Sie den Befehl unten, und Scale-Out-Worker-Dienst neu.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**Fall**

System.ServiceModel.Security.MessageSecurityException: Die HTTP-Anforderung wurde mit Client-Authentifizierungsschema "Anonymous" ist unzulässig. ---> System.NET.WebException:: der Remoteserver hat einen Fehler zurückgegeben: (403) unzulässig.

Schritt 1: Scale Out Worker installieren das Zertifikat für den Zertifikatspeicher des lokalen Computers auf Scale-Out-Master Knoten Stammzertifizierungsstellen ggf. noch installiert wurde und Scale-Out-Worker-Dienst neu.

Schritt 2: Bereinigen von nutzlos Zertifikate in den Stammzertifikatspeicher des lokalen Computers auf Scale-Out-Master-Knoten ab.

Schritt 3: Konfigurieren der Schannel, um die Liste der vertrauenswürdigen Stammzertifizierungsstellen nicht mehr während des TLS/SSL-Handshake-Prozesses zu senden, indem Sie den Registrierungseintrag unten verwenden, auf Scale-Out-Master-Knoten.

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Wertname: SendTrustedIssuerList 

Typ: REG_DWORD 

Wert: 0 (False)

**Fall**

System.ServiceModel.CommunicationException: Fehler beim Ausführen der HTTP-Anforderung zu https://*[Computername]: [Port]*  /ClusterManagement /. Dies ist möglicherweise darauf zurückzuführen, dass das Serverzertifikat mit HTTP nicht ordnungsgemäß konfiguriert ist. SYS im Fall HTTPS. Dies kann auch durch ein Konflikt zwischen der Bindung zwischen dem Client und dem Server verursacht werden. 

Schritt 1: Überprüfen Sie, ob Scale-Out-Master-Zertifikat an den Port in der master-Endpunkt, ordnungsgemäß auf die master-Knoten mit dem folgenden Befehl gebunden ist. Überprüfen Sie, ob die Zertifikat-Hash angezeigt mit Zertifikatfingerabdruck Skala Out Master verglichen wird.

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

Wenn die Bindung nicht richtig ist, mit der folgenden Befehle zurückgesetzt, und Scale-Out-Worker-Dienst neu.

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**Symptome**
Ausführung in horizontal skalieren wird nicht gestartet.

### <a name="solution"></a>**Lösung**

Überprüfen Sie den Status der Computer, die Sie zum Ausführen des Pakets in [SSISDB] ausgewählt. [Catalog]. [Worker_agents]. Mindestens ein Arbeitsprozess muss online und aktiviert sein.

### <a name="symptoms"></a>**Symptome** 
Pakete erfolgreich ausgeführt, aber es ist keine Nachricht protokolliert.

### <a name="solution"></a>**Lösung**

Überprüfen Sie, ob SQL Server-Authentifizierung von Sql Server zugelassen wird SSISDB hosten.

> [!Note]  
> Wenn Sie das Konto für horizontales Skalieren Protokollierung geändert haben, finden Sie unter [ändern Sie das Konto für die Skalierung, Protokollierung](change-logdb-account.md) und überprüfen Sie die Verbindungszeichenfolge für die Protokollierung verwendet.

### <a name="symptoms"></a>**Symptome**
Die Fehlermeldungen im Paket Ausführung Bericht sind nicht genügend Informationen zur Problembehandlung.

### <a name="solution"></a>**Lösung**
Weitere ausführungsprotokolle finden Sie unter TasksRootFolder in WorkerSettings.config konfiguriert. Standardmäßig ist es \<Treiber\>: \Users\\*[Account]*\AppData\Local\SSIS\ScaleOut\Tasks. Die *[Account]* ist das Konto, das Scale-Out-Worker-Dienst hat den Standardwert SSISScaleOutWorker140 ausgeführt.

Suchen Sie das Protokoll für die Ausführung des Pakets mit *[ausführungs-Id]*, führen Sie den T-SQL-Befehl unten zum Abrufen der *[Task-Id]*. Suchen Sie anschließend den Unterordner mit *[Task-Id]* unter TasksRootFolder.<sup> 1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> diese Abfrage ist für die Problembehandlung Zweck öffnen, und Sie nur ändern, wenn die Protokollierung/Diagnose-Szenario für den Scale-Out-Worker in der Zukunft verbessert wird. 
