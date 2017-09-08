---
title: Migration von einer SQL Server-Datenbank von Windows, Linux | Microsoft Docs
description: Dieses Thema veranschaulicht das Erstellen einer Sicherung einer SQL Server-Datenbank auf Windows und auf einem Linux-Computer mit SQL Server 2017 RC2 wiederherstellen.
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/16/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.translationtype: MT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: 0405f6faad62b9dbaf32cb9730ac1450da2b2f48
ms.contentlocale: de-de
ms.lasthandoff: 08/16/2017

---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migration von einer SQL Server-Datenbank von Windows, Linux mit Sicherung und Wiederherstellung

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server die Sicherung und die Wiederherstellungsfunktion ist die empfohlene Methode zum Migrieren einer Datenbank von SQL Server unter Windows auf SQL Server 2017 RC2 unter Linux. In diesem Lernprogramm führt Sie durch die erforderlichen Schritte zum Verschieben einer Datenbank auf Linux mit Sicherung und Wiederherstellung von Techniken.

> [!div class="checklist"]
> * Erstellen Sie eine Sicherungsdatei auf Windows mit SSMS
> * Installieren von Bash-Shell unter Windows
> * Verschieben Sie die Sicherungsdatei auf Linux von Bash-shell
> * Stellt die Sicherungsdatei unter Linux mit Transact-SQL
> * Führen Sie eine Abfrage zum Überprüfen der migration

## <a name="prerequisites"></a>Erforderliche Komponenten

Die folgenden Voraussetzungen sind erforderlich, um dieses Lernprogramm abzuschließen:

* Windows-Computer mit den folgenden:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) installiert.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) installiert.
  * Die Zieldatenbank zu migrieren.

* Linux-Computer mit Folgendes installiert:
  * SQL Server 2017 RC2. Finden Sie unter der Installations-Schnellstarts für [RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), oder [Ubuntu](quickstart-install-connect-ubuntu.md).
  * SQL Server 2017 RC2 [Befehlszeilentools](sql-server-linux-setup-tools.md).

## <a name="create-a-backup-on-windows"></a>Erstellen Sie eine Sicherung in Windows

Es gibt mehrere Möglichkeiten, erstellen eine Sicherungsdatei mit einer Datenbank auf Windows aus. Verwenden Sie SQL Server Management Studio (SSMS) die folgenden Schritte aus.

1. Starten Sie **SQL Server Management Studio** auf dem Windows-Computer.

1. Geben Sie im Verbindungsdialogfeld **"localhost"**.

1. Erweitern Sie im Objekt-Explorer **Datenbanken**.

1. Mit der rechten Maustaste in die Zieldatenbank, wählen Sie **Aufgaben**, und klicken Sie dann auf **sichern...** .

   ![Verwenden Sie SSMS, um eine Sicherungsdatei erstellen](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. In der **Sicherung Datenbank** Dialogfeld, überprüfen Sie, ob **Sicherungstyp** ist **vollständige** und **Sichern auf** ist **Datenträger**. Beachten Sie, Name und Speicherort der Datei. Angenommen, eine Datenbank namens **YourDB** für SQL Server 2016 verfügt der Standardsicherungspfad `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`.

1. Klicken Sie auf **OK** zum Sichern der Datenbank.

> [!NOTE]
> Eine weitere Option ist beim Ausführen einer Transact-SQL-Abfrage zum Erstellen der Sicherungsdatei. Die folgende Transact-SQL-Befehl führt die gleichen Aktionen wie in den vorherigen Schritten für eine Datenbank namens **YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Installieren von Bash-Shell unter Windows

Um die Datenbank wiederherzustellen, müssen Sie zuerst die Sicherungsdatei aus dem Windows-Computer auf den Linux-Zielcomputer übertragen. In diesem Lernprogramm wird die Datei verschieben Linux aus einer Bash-Shell (terminal-Fenster) unter Windows.

1. Installieren von Bash-Shell auf dem Windows-Computer, die unterstützt die **scp** (sichere kopieren) und **SSH-** (remote Login)-Befehle. Zwei Beispiele:

   * Die [Windows-Subsystem für Linux](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * Das Git-Bash-Shell ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Öffnen Sie eine Bash-Sitzung unter Windows.

## <a id="scp"></a>Kopieren Sie die Sicherungsdatei auf Linux

1. Navigieren Sie in der Bash-Sitzung auf das Verzeichnis, das die Sicherungsdatei enthält. Beispiel:

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. Verwenden der **scp** Befehl aus, um die Datei auf dem Ziel-Linux-Computer übertragen. Das folgende Beispiel Übertragungen **YourDB.bak** auf das Stammverzeichnis des *"user1"* auf dem Linux-Server mit der IP-Adresse *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![SCP-Befehl](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> Es gibt Alternativen zur Verwendung der scp für die Übertragung von Dateien. Eine ist die Verwendung [Samba](https://help.ubuntu.com/community/Samba) so konfigurieren Sie eine SMB-Netzwerkfreigabe zwischen Windows- und Linux. Eine exemplarische Vorgehensweise für Ubuntu finden Sie unter [zum Erstellen einer Netzwerk-Dateifreigabe über Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Sobald eingerichtet, können Sie darauf zugreifen, als eine Netzwerkdatei Freigeben von Windows, z. B.  **\\ \\Machinenameorip\\freigeben**.

## <a name="move-the-backup-file-before-restoring"></a>Verschieben Sie die Sicherungsdatei vor dem Wiederherstellen

An diesem Punkt wird die Sicherungsdatei auf dem Linux-Server im Basisverzeichnis des Benutzers ein. Vor dem Wiederherstellen der Datenbank mit SQL Server müssen Sie die Sicherung in einem Unterverzeichnis des anordnen **/var/opt/mssql**.

1. In der gleichen Windows Bash Sitzung eine Remoteverbindung mit dem Ziel Linux-Computer mit **ssh**. Im folgenden Beispiel wird eine Verbindung mit dem Linux-Computer **192.0.2.9** als Benutzer **"user1"**.

   ```bash
   ssh user1@192.0.2.9
   ```

   Befehle werden jetzt auf dem Linux-Remoteserver ausgeführt werden.

1. Geben Sie die Administrator-Modus.

   ```bash
   sudo su
   ```

1. Erstellen Sie ein neues Verzeichnis für die Sicherung. Der Parameter-p wird keine Aktion ausgeführt, wenn das Verzeichnis bereits vorhanden ist.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. Verschieben Sie die Sicherungsdatei auf dieses Verzeichnis. Im folgenden Beispiel wird die Sicherungsdatei im home-Verzeichnis befindet *"user1"*. Ändern Sie den Befehl aus, um den Speicherort und Dateinamen der Sicherungsdatei übereinstimmen.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. Exit-super User-Modus.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Wiederherstellen der Datenbank unter Linux

Um die datenbanksicherung wiederherzustellen, können Sie die **RESTORE DATABASE** (TQL)-Transact-SQL-Befehl.

> [!NOTE]
> Die folgenden Schritte verwenden den **Sqlcmd** Tool. Wenn Sie die Installation noch nicht SQL Server-Tools finden Sie unter [Installieren von SQL Server-Befehlszeilentools unter Linux](sql-server-linux-setup-tools.md).

1. Starten Sie in der gleichen Terminaldienste **Sqlcmd**. Im folgenden Beispiel wird eine Verbindung mit der lokalen SQL Server-Instanz mit der **SA** Benutzer. Geben Sie das Kennwort ein, oder geben Sie das Kennwort durch Hinzufügen der **-P** Parameter.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. Bei der `>1` dazu aufgefordert werden, geben Sie den folgenden **RESTORE DATABASE** Befehl ein, Drücken der EINGABETASTE nach jeder Zeile (Sie können nicht kopieren und Einfügen den gesamten mehrzeilige-Befehl auf einmal). Ersetzen Sie alle Vorkommen von `YourDB` mit dem Namen der Datenbank.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   Sie sollten eine Meldung erhalten, die die Datenbank erfolgreich wiederhergestellt wurde.

1. Überprüfen Sie die Wiederherstellung durch das Auflisten aller Datenbanken auf dem Server ein. Die wiederhergestellte Datenbank sollte aufgeführt sein.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. Führen Sie andere Abfragen auf die migrierte Datenbank ein. Der folgende Befehl einen Kontextwechsel auf die **YourDB** Datenbank und wählt die Zeilen aus einer Tabelle.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. Wenn Sie fertig sind mit **Sqlcmd**, Typ `exit`.

1. Wenn Sie fertig sind in der Remote arbeiten **SSH-** Geben Sie die Sitzung `exit` erneut aus.

## <a name="next-steps"></a>Nächste Schritte

In diesem Lernprogramm haben Sie gelernt, wie Sichern einer Datenbank auf Windows und verschieben Sie sie für einen Linux-Server, die mit SQL Server 2017 RC2. Sie haben gelernt, wie auf:
> [!div class="checklist"]
> * Verwenden von SSMS und Transact-SQL zum Erstellen einer Sicherungsdatei unter Windows
> * Installieren von Bash-Shell unter Windows
> * Verwendung **scp** Sicherungsdateien von Windows, Linux zu verschieben.
> * Verwendung **ssh** eine Remoteverbindung mit dem Linux-Computer herstellen
> * Verschieben Sie die Sicherungsdatei zur Vorbereitung der Wiederherstellung
> * Verwendung **Sqlcmd** auszuführende Transact-SQL-Befehle
> * Wiederherstellen der datenbanksicherung durch die **RESTORE DATABASE** Befehl 

Untersuchen Sie anschließend andere Migrationsszenarien für SQL Server unter Linux. 

> [!div class="nextstepaction"]
>[Migrieren von Datenbanken zu SQL Server on Linux](sql-server-linux-migrate-overview.md)

