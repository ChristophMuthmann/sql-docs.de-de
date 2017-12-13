---
title: Installieren von SQL Server Integrationsservices unter Linux | Microsoft Docs
description: Dieser Artikel beschreibt, wie SQL Server Integration Services (SSIS) unter Linux zu installieren.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 13bd5bde7e4e4ec63bb7e3bd7d8959440f499672
ms.sourcegitcommit: 05e2814fac4d308196b84f1f0fbac6755e8ef876
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Installieren von SQL Server Integration Services (SSIS) unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Führen Sie die Schritte in diesem Artikel, um die Installation von SQL Server Integration Services (`mssql-server-is`) unter Linux. Weitere Informationen zu den Features, die in dieser Version der Integrationsdienste für Linux unterstützt, finden Sie unter der [Release Notes](sql-server-linux-release-notes.md).

Installieren Sie SQL Server-Integration-Server für Ihre Plattform aus:

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a>Installieren Sie SSIS für Ubuntu
So installieren Sie die `mssql-server-is` Paket auf Ubuntu, gehen Sie folgendermaßen vor:

1. Importieren Sie die öffentlichen Repositorys GPG Schlüssel.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrieren Sie die Microsoft SQL Server-Ubuntu-Repositorys.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. Führen Sie die folgenden Befehle zum Installieren von SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Führen Sie nach dem Installieren von Integration Services, `ssis-conf`. Weitere Informationen finden Sie unter [konfigurieren SSIS unter Linux mit Ssis-Conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. Nachdem die Konfiguration abgeschlossen ist, legen Sie den Pfad an.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Aktualisieren von SSIS
Falls Sie noch `mssql-server-is` installiert haben, können Sie auf die neueste Version mit dem folgenden Befehl aktualisieren:

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>Entfernen von SSIS
So entfernen Sie `mssql-server-is`, können Sie folgenden Befehl ausführen:
```bash
sudo apt-get remove msssql-server-is
```

## <a name="RHEL"></a>Installieren Sie SSIS auf RHEL
So installieren Sie die `mssql-server-is` Paket auf RHEL, gehen Sie folgendermaßen vor:

1. Herunterladen der Konfigurationsdatei für Microsoft SQL Server-Red Hat-Repository.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. Führen Sie die folgenden Befehle zum Installieren von SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. Nach der Installation auszuführenden `ssis-conf`. Weitere Informationen finden Sie unter [konfigurieren SSIS unter Linux mit Ssis-Conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Sobald die Konfiguration abgeschlossen ist, legen Sie Pfad ein.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Aktualisieren von SSIS
Falls Sie noch `mssql-server-is` installiert haben, können Sie auf die neueste Version mit dem folgenden Befehl aktualisieren:

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>Entfernen von SSIS
So entfernen Sie `mssql-server-is`, können Sie folgenden Befehl ausführen:
```bash
sudo yum remove mssql-server-is
```

## <a name="next-steps"></a>Nächste Schritte

Zum Ausführen von SSIS-Pakete auf Linux finden Sie unter [extrahieren, Transformieren und Laden von Daten für SQL Server on Linux mit SSIS](sql-server-linux-migrate-ssis.md).

Konfigurieren zusätzliche Einstellungen der SSIS unter Linux finden Sie [konfigurieren Sie SQL Server Integration Services unter Linux mit Ssis-Conf](sql-server-linux-configure-ssis.md).
