---
title: Installieren von SQL Server Integrationsservices unter Linux | Microsoft Docs
description: Dieses Thema beschreibt, wie SQL Server Integration Services unter Linux zu installieren.
author: leolimsft
ms.author: lle
manager: craigg
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c3943870ec10b8430ac4819398908c5459a8b03c
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Installieren von SQL Server Integration Services (SSIS) unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Führen Sie die Schritte in diesem Artikel, um die Installation von SQL Server Integration Services (`mssql-server-is`) unter Linux. Weitere Informationen zu den Features, die in dieser Version der Integrationsdienste für Linux unterstützt, finden Sie unter der [Release Notes](sql-server-linux-release-notes.md).

Installieren Sie SQL Server-Integration-Server für Ihre Plattform aus:

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)



## <a name="ubuntu"></a>Installieren Sie SSIS für Ubuntu
So installieren Sie die `mssql-server-is` Paket auf Ubuntu, gehen Sie folgendermaßen vor:


1.  Importieren Sie die öffentlichen Repositorys GPG Schlüssel.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```


2.  Registrieren Sie die Microsoft SQL Server-Ubuntu-Repositorys.

    ```bash
    curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list | sudo tee /etc/apt/sources.list.d/mssql-server.list
    ```


3.  Führen Sie die folgenden Befehle zum Installieren von SQL Server Integration Services.

    ```bash
    sudo apt-get update
    sudo apt-get install -y mssql-server-is
    ```


4.  Führen Sie nach dem Installieren von Integration Services, `ssis-conf`.

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


5.  Nachdem die Konfiguration abgeschlossen ist, legen Sie den Pfad an.

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


Falls Sie noch `mssql-server-is` installiert haben, können Sie auf die neueste Version mit dem folgenden Befehl aktualisieren:

```bash
sudo apt-get install mssql-server-is
```


So entfernen Sie `mssql-server-is`, können Sie folgenden Befehl ausführen:
```bash
sudo apt-get remove msssql-server-is
```



## <a name="RHEL"></a>Installieren Sie SSIS auf RHEL
So installieren Sie die `mssql-server-is` Paket auf RHEL, gehen Sie folgendermaßen vor:


1.  Geben Sie ein Superuser-Modus.

    ```bash
    sudo su
    ```


2.  Herunterladen der Konfigurationsdatei für Microsoft SQL Server-Red Hat-Repository.

    ```bash
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
    ```


3.  Exit-Superuser-Modus.

    ```bash
    exit
    ```


4.  Führen Sie die folgenden Befehle zum Installieren von SQL Server Integration Services.

    ```bash
    sudo yum install -y mssql-server-is
    ```


5.  Führen Sie nach der Installation `ssis-conf`.

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


6.  Sobald die Konfiguration abgeschlossen ist, legen Sie Pfad ein.

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


Falls Sie noch `mssql-server-is` installiert haben, können Sie auf die neueste Version mit dem folgenden Befehl aktualisieren:

```bash
sudo yum update mssql-server-is
```


So entfernen Sie `mssql-server-is`, können Sie folgenden Befehl ausführen:
```bash
sudo yum remove msssql-server-is
```




## <a name="run-a-package"></a>Ausführen eines Pakets
Kopieren Sie das SSIS-Paket auf dem Linux-Computer. Verwenden Sie dann den folgenden Befehl zum Ausführen des Pakets an.

```bash
dtexec /F <package name> /DE <protection password>
```



## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Verwendung von SSIS unter Linux zu extrahieren, Transformieren und Laden von Daten finden Sie unter [extrahieren, Transformieren und Laden von Daten für SQL Server on Linux mit SSIS](sql-server-linux-migrate-ssis.md).
