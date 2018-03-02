---
title: Erste Schritte mit SQL Server-2017 in der Cloud | Microsoft Docs
description: "Dieser Schnellstart veranschaulicht, wie der SQL Server-2017 unter Linux in der Cloud Ihrer Wahl ausführen."
author: annashres
ms.author: annashres
manager: craigg
ms.date: 10/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.component: 
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.openlocfilehash: 3966bb71f4112c12d340ab9780586013d8732206
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/24/2018
---
# <a name="quickstart-run-the-sql-server-2017-in-the-cloud"></a>Schnellstart: Führen Sie die SQL Server-2017 in der cloud

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Schnellstart installieren Sie SQL Server-2017 unter Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) oder Ubuntu in der Cloud Ihrer Wahl. Wechseln Sie zu [Bereitstellen eines Linux SQL Server-virtuellen Computers im Azure-Portal](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json) zu SQL Server unter Linux in Azure ausgeführt wird.

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>Amazon Web Services
1.  Erstellen Sie eine Linux AMI mit mindestens 2 GB Arbeitsspeicher aus dem marketplace 
    * [RHEL 7.3+](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Herstellen einer Verbindung mit der AMI mit ssh
1.  Führen Sie den Schnellstart für die Linux-Distribution, die Sie ausgewählt haben: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Für Remoteverbindungen zu konfigurieren: 
    * Öffnen der [EC2 Amazon-Konsole]( https://console.aws.amazon.com/ec2/)
    * Wählen Sie im Navigationsbereich **Sicherheitsgruppen**. 
    * Wählen Sie **eingehend, bearbeiten, Regel hinzufügen**
    * Fügen Sie eine eingehende Regel zum Zulassen von Datenverkehr an den Port auf dem SQL Server (standardmäßig TCP-Port 1433) lauscht hinzu

    
## <a name="digital-ocean"></a>Digitale "Ozean"
1. Melden Sie sich auf die [Systemsteuerung](https://cloud.digitalocean.com/login) und klicken Sie auf ein Droplet erstellen
1. Wählen Sie eine Ubuntu 16.04 Droplet mit mindestens 2 GB Arbeitsspeicher
1. Herstellen einer Verbindung mit der Droplet mit ssh
1. Führen Sie die [Ubuntu-Schnellstart](quickstart-install-connect-ubuntu.md)
1. Für Remoteverbindungen zu konfigurieren:
    * Am oberen Rand der Systemsteuerung, befolgen Sie die **Networking** verknüpfen, und wählen Sie dann **Firewalls**
    * Fügen Sie eine eingehende Regel zum Zulassen von Datenverkehr an den Port auf dem SQL Server (standardmäßig TCP-Port 1433) lauscht hinzu
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  Erstellen Sie eine Linux-Image mit mindestens 2 GB Arbeitsspeicher aus dem Cloud-Startprogramm 
    * [RHEL 7.3+](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Herstellen einer Verbindung mit dem Image mit ssh
1.  Führen Sie den Schnellstart für die Linux-Distribution, die Sie ausgewählt haben: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Für Remoteverbindungen zu konfigurieren: 
    * Wechseln Sie zu der [Firewall-Regeln](https://console.cloud.google.com/networking/firewalls)
    * Fügen Sie eine eingehende Regel zum Zulassen von Datenverkehr am Port auf dem SQL Server lauscht (standardmäßig Tcp: 1433)
