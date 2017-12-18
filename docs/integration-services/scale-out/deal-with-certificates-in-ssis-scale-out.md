---
title: Umgang mit Zertifikaten in SQL Server Integration Services Scale Out | Microsoft-Dokumentation
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
ms.openlocfilehash: e09fec1fcf9cf0221dad50d708adef773b297237
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>Umgang mit Zertifikaten in SQL Server Integration Services Scale Out

Zur Sicherung der Kommunikation zwischen dem Scale Out-Master und dem Scale Out-Worker werden zwei Zertifikate in Scale Out verwendet: das Scale Out-Masterzertifikat und das Scale Out-Workerzertifikat. 

## <a name="scale-out-master-certificate"></a>Scale Out-Masterzertifikat

In der Regel wird das Scale Out-Masterzertifikat während der Installation des Scale Out-Masters konfiguriert.

Auf der Seite **Integration Services Scale Out-Konfiguration – Masterknoten** des SQL Server-Installationsassistenten können Sie entweder ein neues selbstsigniertes SSL-Zertifikat erstellen oder ein vorhandenes SSL-Zertifikat verwenden.

![Masterkonfiguration](media/master-config.PNG)

Wenn Sie keine besonderen Anforderungen an Zertifikate haben, können Sie ein neues selbstsigniertes SSL-Zertifikat erstellen. Sie können die allgemeinen Namen in diesem Zertifikat näher bestimmen. Stellen Sie sicher, dass der Hostname des Masterendpunkts, der später vom Scale Out-Worker verwendet wird, in den allgemeinen Namen enthalten ist. Standardmäßig sind der Computername und die IP-Adresse des Masterknotens nicht enthalten. 

Wenn Sie sich dafür entscheiden, ein vorhandenes Zertifikat zu verwenden, klicken Sie auf „Durchsuchen...“, um aus dem **Stammzertifikatspeicher** des lokalen Computers ein SSL-Zertifikat auszuwählen.

### <a name="change-scale-out-master-certificate"></a>Ändern des Scale Out-Masterzertifikats

Möglicherweise möchten Sie das Scale Out-Masterzertifikat ändern, weil z.B. das Zertifikat abgelaufen ist. Führen Sie dafür die folgenden Schritte aus:

#### <a name="1-create-a-ssl-certificate"></a>1. Erstellen Sie ein SSL-Zertifikat.
Erstellen und installieren Sie mithilfe des folgenden Befehls ein SSL-Zertifikat auf dem Masterknoten:
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
Beispiel:
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2. Binden Sie das Zertifikat an den Masterport
Überprüfen Sie mithilfe des folgenden Befehls die ursprüngliche Bindung:
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
Beispiel:
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
Löschen Sie die ursprüngliche Bindung, und richten Sie die neue Bindung mithilfe des folgenden Befehls ein:
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
Beispiel:
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3. Aktualisieren Sie die Konfigurationsdatei des Scale Out Masterdiensts.
Aktualisieren Sie die Konfigurationsdatei des Scale Out Master-Diensts („\<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config“) auf dem Masterknoten. Aktualisieren Sie **SSLCertThumbprint** auf den Fingerabdruck des neuen SSL-Zertifikats.

#### <a name="4-restart-scale-out-master-service"></a>4. Starten Sie den Scale Out Master-Dienst neu.

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5. Stellen Sie erneut eine Verbindung zwischen dem Scale Out-Worker und dem Scale Out-Master her.
Löschen Sie für jeden Scale Out-Worker entweder den Worker, und fügen Sie Ihn erneut mit dem [Scale Out-Manager](integration-services-ssis-scale-out-manager.md) hinzu, oder führen Sie die Schritte 5.1 bis 5.3 aus:

5.1 Installieren Sie das SSL-Clientzertifikat im Stammspeicher des lokalen Computers auf dem Workerknoten.

5.2 Aktualisieren Sie die Konfigurationsdatei des Scale Out Worker-Diensts „\<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config“ auf dem Workerknoten. Aktualisieren Sie **MasterHttpsCertThumbprint** auf den Fingerabdruck des neuen SSL-Zertifikats.

5.3 Starten Sie den Scale Out Worker-Dienst neu.


## <a name="scale-out-worker-certificate"></a>Scale Out Worker-Zertifikat

Das Scale Out Worker-Zertifikat wird automatisch bei der Installation des Scale Out-Workers installiert. 

### <a name="change-scale-out-worker-certificate"></a>Ändern des Scale Out Worker-Zertifikats

Wenn Sie das Scale Out-Workerzertifikat ändern möchten, führen Sie die folgenden Schritte aus.

#### <a name="1-create-a-certificate"></a>1. Erstellen eines Zertifikats
Erstellen und installieren Sie mithilfe des folgenden Befehls ein Zertifikat:
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
Beispiel:
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2. Installieren Sie das Clientzertifikat im Stammspeicher des lokalen Computers auf dem Workerknoten.

#### <a name="3-give-service-access-to-the-certificate"></a>3. Gewähren Sie dem Dienst Zugriff auf das Zertifikat.
Löschen Sie das alte Zertifikat, und gewähren Sie dem Scale Out-Workerdienst über den folgenden Befehl Zugriff auf das Zertifikat:
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
Beispiel:
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4. Aktualisieren Sie die Konfigurationsdatei des Scale Out-Workers
Aktualisieren Sie die Konfigurationsdatei des Scale Out-Workers „\<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config“ auf dem Workerknoten. Aktualisieren Sie **WorkerHttpsCertThumbprint** auf den Fingerabdruck des neuen Zertifikats.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5. Installieren Sie das Clientzertifikat im Stammspeicher des lokalen Computers auf dem Masterknoten.

#### <a name="6-restart-scale-out-worker-service"></a>6. Starten Sie den Scale Out-Workerdienst neu.
