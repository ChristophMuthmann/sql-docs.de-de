---
title: Umgang mit Zertifikaten in Sql Server Integration Services horizontal skalieren | Microsoft Docs
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
ms.openlocfilehash: 2970b2b2cc7cf30c18a203ebbb92b5418bfc9be5
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>Umgang mit Zertifikaten in SQL Server Integration Services horizontal skalieren

Zum Sichern der Kommunikation zwischen Scale-Out-Master "und" Scale-Out-Worker sind zwei Zertifikate in horizontal skalieren, d. h. Scale-Out-Master-Zertifikat und Scale-Out-Worker-Zertifikat verwendet. 

## <a name="scale-out-master-certificate"></a>Scale-Out-Master-Zertifikat

In den meisten Fällen ist die Scale-Out-Master Zertifikat während der Installation des Scale-Out-Master konfiguriert.

In der **Scale Out Konfiguration von Integration Services - Master Knoten** Seite des SQL Server-Installations-Assistenten können Sie auswählen, erstellen ein neues selbstsigniertes SSL-Zertifikat oder ein vorhandenes SSL-Zertifikat verwenden.

![Master-Konfigurationsdatei](media/master-config.PNG)

Wenn Sie keine spezielle Anforderungen für Zertifikate haben, können Sie auswählen, um ein neues selbstsigniertes SSL-Zertifikat zu erstellen. Sie können weitere den allgemeinen Namen des Zertifikats angeben. Stellen Sie sicher, dass der Hostname des master Endpunkts verwendeten Scale-Out-Worker weiter unten in den allgemeinen Namen enthalten ist. Standardmäßig sind die Computernamen und IP-Adresse der master-Knoten enthalten. 

Wenn Sie ein vorhandenes Zertifikat verwenden möchten, klicken Sie auf "Durchsuchen…" zum Auswählen eines SSL-Zertifikats aus **Root** Zertifikatspeicher des lokalen Computers.

### <a name="change-scale-out-master-certificate"></a>Scale-Out-Master-Zertifikat ändern

Möglicherweise möchten Ihr Zertifikat Scale-Out-Master aufgrund der Ablauf des Zertifikats oder aus anderen Gründen ändern. Führen Sie die folgenden Schritte aus:

#### <a name="1-create-a-ssl-certificate"></a>1. Erstellen Sie ein SSL-Zertifikat.
Erstellen und installieren Sie ein SSL-Zertifikat auf der Masterseite Knoten mit den folgenden Befehl aus:
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
Beispiel:
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2. Binden des Zertifikats an Master Port
Überprüfen Sie die ursprüngliche Bindung mit dem Befehl ein:
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
Beispiel:
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
Löschen Sie die ursprüngliche Bindung, und richten Sie die neue Bindung mit den folgenden Befehlen:
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
Beispiel:
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3. Aktualisieren der Dienstkonfigurationsdatei Scale-Out-Master
Update Scale-Out-Master Dienstkonfigurationsdatei \<Treiber\>: \Programme\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config, auf der Masterseite Knoten. Update **SSLCertThumbprint** auf den Fingerabdruck des neuen SSL-Zertifikats.

#### <a name="4-restart-scale-out-master-service"></a>4. Scale-Out-Master-Dienst neu starten

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5. Dezentrales Skalieren Worker to Scale Out Master verbinden
Für jeden Arbeitnehmer Scale-Out den Arbeitsthread löschen und erneut hinzufügen mit [Scale-Out-Manager](integration-services-ssis-scale-out-manager.md) oder führen Sie die Schritte 5.1 auf 5.3:

5.1 installieren Sie das Client-SSL-Zertifikat im Stammspeicher des lokalen Computers auf dem Knoten Worker für

5.2 Aktualisieren der Skalierung, Worker-Dienst Konfiguration Datei Update Scale Out Worker Dienstkonfigurationsdatei \<Treiber\>: \Programme\Microsoft SQL-Server\140\DTS\Binn\WorkerSettings.config auf Worker-Knoten. Update **MasterHttpsCertThumbprint** auf den Fingerabdruck des neuen SSL-Zertifikats.

5.3 Skalierung, Worker-Dienst starten


## <a name="scale-out-worker-certificate"></a>Scale-Out-Worker-Zertifikat

Scale-Out-Worker-Zertifikat wird automatisch während der Installation des Scale-Out-Worker generiert. 

### <a name="change-scale-out-worker-certificate"></a>Scale-Out-Worker-Zertifikat ändern

Führen Sie in Fällen, die Skalierung, workerzertifikat ändern möchten die folgenden Schritte aus.

#### <a name="1-create-a-certificate"></a>1. Erstellen Sie ein Zertifikat
Erstellen Sie und installieren Sie ein Zertifikat mit dem folgenden Befehl:
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
Beispiel:
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2. Installieren Sie das Clientzertifikat im Stammspeicher des lokalen Computers auf Worker-Knoten für

#### <a name="3-give-service-access-to-the-certificate"></a>3. Erteilen des Zugriffs auf das Zertifikat
Löschen Sie das alte Zertifikat, und gewähren Sie Scale-Out-Worker-Dienstzugriff auf das neue Zertifikat mit dem Befehl:
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
Beispiel:
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4. Scale-Out-Worker-Konfigurationsdatei aktualisieren
Update Scale-Out-Worker-Dienst-Konfigurationsdatei \<Treiber\>: \Programme\Microsoft SQL-Server\140\DTS\Binn\WorkerSettings.config auf Worker-Knoten. Update **WorkerHttpsCertThumbprint** auf den Fingerabdruck des neuen Zertifikats.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5. Installieren des Clientzertifikats im Stammspeicher des lokalen Computers auf der Masterseite für Knoten

#### <a name="6-restart-scale-out-worker-service"></a>6. Scale-Out-Worker-Dienst neu starten
