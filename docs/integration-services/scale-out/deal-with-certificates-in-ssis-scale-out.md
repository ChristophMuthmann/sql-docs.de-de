---
title: "Verwalten von Zertifikaten für SQL Server Integration Services Scale Out | Microsoft-Dokumentation"
ms.custom: This article describes how to manage certificates to secure communications between SSIS Scale Out Master and Scale Out Workers.
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cda61336badec20e15cf0d0142e592ef63431254
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="manage-certificates-for-sql-server-integration-services-scale-out"></a>Verwalten von Zertifikaten für SQL Server Integration Services Scale Out

SSIS Scale Out verwendet zwei Zertifikate, um die Kommunikation zwischen dem Scale Out-Master und den Scale Out-Workern sicherzustellen: eins für den Master und eins für die Worker. 

## <a name="scale-out-master-certificate"></a>Scale Out-Masterzertifikat

In der Regel wird das Scale Out-Masterzertifikat während der Installation des Scale Out-Masters konfiguriert.

Auf der Seite **Integration Services Scale Out-Konfiguration – Masterknoten** des SQL Server-Installationsassistenten können Sie entweder ein neues selbstsigniertes SSL-Zertifikat erstellen oder ein vorhandenes SSL-Zertifikat verwenden.

![Masterkonfiguration](media/master-config.PNG)

**Neues Zertifikat.** Wenn Sie keine besonderen Anforderungen an Zertifikate haben, können Sie ein neues selbstsigniertes SSL-Zertifikat erstellen. Sie können die allgemeinen Namen in diesem Zertifikat näher bestimmen. Stellen Sie sicher, dass der Hostname des Masterendpunkts, der später vom Scale Out-Worker verwendet werden soll, in den allgemeinen Namen enthalten ist. Standardmäßig sind der Computername und die IP-Adresse des Masterknotens darin enthalten. 

**Vorhandenes Zertifikat.** Wenn Sie sich dafür entscheiden, ein vorhandenes Zertifikat zu verwenden, klicken Sie auf **Durchsuchen**, um aus dem **Stammzertifikatspeicher** des lokalen Computers ein SSL-Zertifikat auszuwählen.

### <a name="change-the-scale-out-master-certificate"></a>Ändern des Scale Out-Masterzertifikats

Sie sollten das Scale Out-Masterzertifikat ändern, weil es abgelaufen sein kann. Führen Sie die folgende Schritte aus, um das Scale Out-Masterzertifikat zu ändern:

#### <a name="1-create-an-ssl-certificate"></a>1. Erstellen Sie ein SSL-Zertifikat.
Erstellen und installieren Sie mithilfe des folgenden Befehls ein neues SSL-Zertifikat auf dem Masterknoten:

```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
Zum Beispiel:

```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-the-master-port"></a>2. Binden Sie das Zertifikat an den Masterport
Überprüfen Sie mithilfe des folgenden Befehls die ursprüngliche Bindung:

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

Zum Beispiel:

```dos
netsh http show sslcert ipport=0.0.0.0:8391
```

Löschen Sie die ursprüngliche Bindung, und richten Sie die neue Bindung mithilfe des folgenden Befehls ein:

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```

Zum Beispiel:

```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```

#### <a name="3-update-the-scale-out-master-service-configuration-file"></a>3. Aktualisieren Sie die Konfigurationsdatei des Scale Out-Masterdiensts
Aktualisieren Sie die Konfigurationsdatei des Scale Out Masterdiensts (`\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`) auf dem Masterknoten. Aktualisieren Sie **SSLCertThumbprint** auf den Fingerabdruck des neuen SSL-Zertifikats.

#### <a name="4-restart-the-scale-out-master-service"></a>4. Starten Sie den Scale Out-Masterdienst neu.

#### <a name="5-reconnect-scale-out-workers-to-scale-out-master"></a>5. Stellen Sie erneut eine Verbindung zwischen den Scale Out-Workern und dem Scale Out-Master her.
Löschen Sie für jeden Scale Out-Worker entweder den Worker, und fügen Sie Ihn erneut mit dem [Scale Out-Manager](integration-services-ssis-scale-out-manager.md) hinzu, oder führen Sie die folgenden Schritte aus:

A.  Installieren Sie das SSL-Clientzertifikat im Stammspeicher des lokalen Computers auf dem Workerknoten.

B.  Aktualisieren Sie die Konfigurationsdatei des Scale Out-Workerdiensts.

    Update the Scale Out Worker service configuration file, `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`, on the Worker node. Update **MasterHttpsCertThumbprint** to the thumbprint of the new SSL certificate.

c.  Starten Sie den Scale Out-Workerdienst neu.

## <a name="scale-out-worker-certificate"></a>Scale Out Worker-Zertifikat

Das Scale Out Worker-Zertifikat wird automatisch bei der Installation des Scale Out-Workers installiert. 

### <a name="change-the-scale-out-worker-certificate"></a>Ändern des Scale Out-Workerzertifikats

Wenn Sie das Scale Out-Workerzertifikat ändern möchten, führen Sie die folgenden Schritte aus:

#### <a name="1-create-a-certificate"></a>1. Erstellen eines Zertifikats
Erstellen und installieren Sie mithilfe des folgenden Befehls ein Zertifikat:

```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

Zum Beispiel:

```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

#### <a name="2-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-worker-node"></a>2. Installieren Sie das Clientzertifikat im Stammspeicher des lokalen Computers auf dem Workerknoten.

#### <a name="3-grant-service-access-to-the-certificate"></a>3. Gewähren Sie dem Dienst Zugriff auf das Zertifikat.
Löschen Sie das alte Zertifikat, und gewähren Sie dem Scale Out-Workerdienst über den folgenden Befehl Zugriff auf das Zertifikat:

```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```

Zum Beispiel:

```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```

#### <a name="4-update-the-scale-out-worker-service-configuration-file"></a>4. Aktualisieren Sie die Konfigurationsdatei des Scale Out-Workerdiensts
Aktualisieren Sie die Konfigurationsdatei des Scale Out-Workerdiensts (`\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`) auf dem Workerknoten. Aktualisieren Sie **WorkerHttpsCertThumbprint** auf den Fingerabdruck des neuen Zertifikats.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-worker-node"></a>5. Installieren Sie das Clientzertifikat im Stammspeicher des lokalen Computers auf dem Workerknoten.

#### <a name="6-restart-the-scale-out-worker-service"></a>6. Starten Sie den Scale Out-Workerdienst neu

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie in den folgenden Artikeln:
-   [Scale Out-Master von Integration Services (SSIS)](integration-services-ssis-scale-out-master.md)
-   [Scale Out-Worker von Integration Services (SSIS)](integration-services-ssis-scale-out-worker.md)