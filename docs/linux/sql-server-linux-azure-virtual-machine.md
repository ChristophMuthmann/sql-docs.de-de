---
title: Bereitstellen einen Linux-SQL-Server-Computers in Azure | Microsoft Docs
description: Dieses Lernprogramm zeigt, wie eine Linux SQL Server 2017 virtuelle Maschine in Azure zu erstellen.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 222e23b2-51e7-429b-b8e5-61e0ebe7df9b
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 0470622b0fe5a8835213617a4fc2e8c74f674873
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-linux-sql-server-2017-virtual-machine-with-the-azure-portal"></a>Erstellen Sie eine virtuelle Maschine von Linux, SQL Server-2017 mit Azure-portal

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Azure bietet eine Linux-VM-Images, die SQL Server 2017 RC2 installiert haben. Dieses Thema enthält eine kurze exemplarische Vorgehensweise zur Verwendung von Azure-Portal zum Erstellen eines virtuellen Computers Linux SQL Server. 

## <a name="create-a-linux-vm-with-sql-server-installed"></a>Erstellen Sie eine Linux-VM mit SQL Server installiert

Öffnen der [Azure-Portal](https://portal.azure.com/).

1. Klicken Sie auf **neu** auf der linken Seite.

1. In der **neu** Blatt, klicken Sie auf **berechnen**.

1. Klicken Sie auf **finden Sie unter allen** neben der **Funktionsumfang Apps** Überschrift.

   ![Finden Sie unter alle VM-images](./media/sql-server-linux-azure-virtual-machine/azure-compute-blade.png)

1. Geben Sie in das Suchfeld **SQL Server-2017**, und drücken Sie die **EINGABETASTE** mit der Suche begonnen.

    ![Suchfilter für SQL Server 2017 VM-images](./media/sql-server-linux-azure-virtual-machine/searchfilter.png)

    > [!TIP]
    > Dieser Filter zeigt die verfügbaren Linux VM wurde für SQL Server-2017. Im Laufe der Zeit werden 2017 von SQL Server-Images für die anderen unterstützten Linux-Distributionen aufgeführt. Sie können dies auch klicken [Link](https://ms.portal.azure.com/#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/sql%20server%202017) , direkt in den Suchergebnissen für SQL Server-2017 aufzurufen. 

1. Wählen Sie ein Image von SQL Server-2017 in den Suchergebnissen.

1. Klicken Sie auf **Erstellen**.

1. Auf der **Grundlagen** Blatt, füllen Sie die Details für Ihre Linux-VM. 

    ![Blatt "Grundlagen"](./media/sql-server-linux-azure-virtual-machine/basics.png)

    > [!Note]
    > Sie haben die Wahl von einer öffentlichen SSH-Schlüssel oder ein Kennwort für die Authentifizierung verwenden. SSH ist sicherer. Anweisungen zum Generieren eines SSH-Schlüssels, finden Sie unter [erstellen SSH-Schlüssel für Linux und Macintosh für virtuelle Linux-Computer in Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-mac-create-ssh-keys). 

1. Klicken Sie auf **OK**.

1. Auf der **Größe** Blatt, wählen Sie eine Größe des Computers. Für Entwicklungs- und Funktionstests, empfehlen wir eine VM-Größe **dq2** oder höher. Verwenden Sie zum Testen von Leistung **DS13** oder höher.

    ![Wählen Sie eine VM-Größe](./media/sql-server-linux-azure-virtual-machine/vmsizes.png)

    Wählen Sie zum Anzeigen von anderen Größen **alle anzeigen**. Weitere Informationen zu Größen der VM-Computer finden Sie unter [Linux VM-Größen](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes).

1. Klicken Sie auf **Auswählen**.

1. Auf der **Einstellungen** Blatt können Sie nehmen Änderungen an den Einstellungen oder behalten Sie die Standardeinstellungen.

1. Klicken Sie auf **OK**.

1. Auf der **Zusammenfassung** auf **OK** Erstellen des virtuellen Computers.

> [!NOTE]
> Die Azure-VM vorkonfiguriert die Firewall so, dass der SQL Server-Port 1433 für Remoteverbindungen zu öffnen. Jedoch um eine Remoteverbindung herstellen, müssen Sie auch eine Netzwerksicherheits-Gruppenregel hinzufügen, wie im nächsten Abschnitt beschrieben.

## <a id="remote"></a>Konfigurieren für Remoteverbindungen

Um eine Remoteverbindung mit SQL Server auf einem virtuellen Azure-Computer herstellen können, müssen Sie eine eingehende Regel für die Netzwerksicherheitsgruppe konfigurieren. Die Regel den Datenverkehr auf dem Port auf dem SQL Server (standardmäßig 1433) lauscht erlaubt. Die folgenden Schritte zeigen, wie das Azure Portal für diesen Schritt verwenden. 

1. Wählen Sie im Portal **VMs**, und wählen Sie dann Ihre SQL Server-VM.

1. Wählen Sie in der Liste der Eigenschaften, **Netzwerkschnittstellen**.

1. Wählen Sie dann die Netzwerkschnittstelle für Ihren virtuellen Computer an.

    ![Netzwerkschnittstellen](./media/sql-server-linux-azure-virtual-machine/networkinterfaces.png)

1. Klicken Sie auf den Link "Sicherheit Gruppe" Netzwerk.

    ![Netzwerksicherheitsgruppe](./media/sql-server-linux-azure-virtual-machine/networksecuritygroup.png)

1. In den Eigenschaften der Netzwerksicherheitsgruppe wählen **eingehende Sicherheitsregeln**.

1. Klicken Sie auf die **+ Add** Schaltfläche.

1. Geben Sie einen Namen von "SQLServerRemoteConnections".

1. In der **Service** Liste **MS SQL**.

    ![MS-SQL-Regel](./media/sql-server-linux-azure-virtual-machine/sqlnsgrule.png)

1. Klicken Sie auf **OK** um die Regel für Ihren virtuellen Computer zu speichern.

## <a id="connect"></a>Herstellen einer Verbindung mit dem virtuellen Linux-Computer

Wenn Sie bereits eine BASH-Shell verwenden, Verbinden mit virtuellen Azure-Computer die **ssh** Befehl. Ersetzen Sie in den folgenden Befehl ein den VM-Benutzernamen und IP-Adresse, eine Verbindung mit Ihrem Linux-VM.

```bash
ssh -l AzureAdmin 100.55.555.555
```

Sie können die IP-Adresse Ihres virtuellen Computers im Azure-Portal finden.

![IP-Adresse im Azure-portal](./media/sql-server-linux-azure-virtual-machine/vmproperties.png)

Wenn Sie auf dem Windows ausgeführt werden und verfügen nicht über eine BASH-Shell, können Sie einen SSH-Client wie PuTTY installieren.

1. [Herunterladen und installieren Sie PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Führen Sie PuTTY.

1. Geben Sie auf dem Bildschirm PuTTY-Konfiguration des virtuellen Computers öffentliche IP-Adresse ein.

1. Klicken Sie auf Öffnen, und geben Sie Ihren Benutzernamen und Kennwort dazu aufgefordert werden.

Weitere Informationen zum Verbinden mit virtuelle Linux-Computer finden Sie unter [erstellen Sie eine Linux-VM in Azure mithilfe des Portals](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-portal#ssh-to-the-vm).

## <a name="configure-sql-server"></a>Konfigurieren von SQLServer

1. Öffnen Sie nach dem Herstellen einer Verbindung zu Ihrer Linux-VM, einen neuen Befehl terminal ein.

1. Richten Sie SQL Server mit dem folgenden Befehl aus.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup 
   ```

   Akzeptieren Sie die lizenzveREINBARUNG und geben Sie ein Kennwort für das Konto des System-Administrator. Starten Sie den Server aus, wenn Sie aufgefordert werden.

1. Optional, [installieren Sie SQL Server-Tools](sql-server-linux-setup-tools.md).

## <a name="next-steps"></a>Nächste Schritte

Nun, dass Sie einen SQL Server-2017 virtuellen Computer in Azure hat, Sie können eine Verbindung herstellen lokal mit **Sqlcmd** zum Ausführen von Transact-SQL-Abfragen.

Wenn Sie die Azure-VM für Remoteverbindungen für SQL Server konfiguriert haben, sollten Sie auch eine Remoteverbindung herstellen können. Ein Beispiel für die von einem remote-Windows-Computer eine Verbindung zum SQL Server on Linux, finden Sie unter [Verwenden von SSMS unter Windows zur Verbindung mit SQL Server on Linux](sql-server-linux-develop-use-ssms.md).

Weitere allgemeine Informationen über virtuelle Linux-Computer in Azure finden Sie unter der [Linux VM Dokumentation](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/).

