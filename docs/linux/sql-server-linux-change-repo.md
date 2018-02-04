---
title: "Registrieren Sie die allgemeine Verfügbarkeit-Repositorys für SQL Server on Linux | Microsoft Docs"
description: "Ändern von Repositorys aus dem Repository für die Vorschau von SQL Server-2017 im Repository der allgemeinen Verfügbarkeit (GA) unter Linux (GA wird manchmal auch bezeichnet als RTM-Version)."
author: annashres
ms.author: anshrest
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
ms.workload: Inactive
ms.openlocfilehash: 28c5668598c5464c893c1bf62c19699282ecf7b3
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="change-repositories-from-the-preview-repository-to-the-ga-repository"></a>Ändern Sie Repositorys aus dem Repository Vorschau in GA-repository

Beim upgrade von SQL Server-2017 von CTP-Version 2.1, RC1 oder RC2 auf die Version der allgemeinen Verfügbarkeit (GA) müssen Sie Repositorys zu wechseln. In den folgenden Abschnitten wird erläutert, die Auswahl des Repositorys und wie die Änderung vor dem Upgrade vornehmen.

## <a name="repository-choices"></a>Repository-Optionen

Es ist wichtig zu beachten, dass es zwei Haupttypen von Repositorys für jede Verteilung gibt:

  > [!IMPORTANT]
  > Eine Version vor der CTP-Version 2.1 muss auf mindestens 2.1 aktualisiert werden, vor dem Upgrade auf GA

- **Kumulative Updates (CU)**: das kumulative Update (CU)-Repository enthält Pakete für die grundlegenden SQL Server-Version sowie alle Programmfehlerbehebungen und Verbesserungen seit diesem Release. Kumulative Updates sind spezifisch für die endgültige Produktversion, z. B. SQL Server-2017. Sie werden in einem regulären Rhythmus veröffentlicht.

- **GDR**: die GDR-Repository enthält Pakete für die grundlegenden SQL Server-Version und nur kritische Updates und Sicherheitsupdates seit diesem Release. Diese Updates werden auch auf die nächste CU-Version hinzugefügt.

Jeder CU und GDR-Version enthält die vollständige SQL Server-Paket und alle vorherigen Updates für das Repository. Aktualisieren von einer GDR-Version für eine CU-Version wird durch Ändern des konfigurierten Repositorys für SQL Server unterstützt. Sie können auch [downgrade](sql-server-linux-setup.md#rollback) auf eine beliebige Version innerhalb der Hauptversion (zum Beispiel: 2017).

> [!NOTE]
> Sie können von einer GDR-Version aktualisieren, um CU jederzeit freigegeben werden, indem ein Repositorys ändern. Aktualisieren von ein CU-Version mit einer GDR-Version wird nicht unterstützt. 

## <a name="change-to-a-ga-repository"></a>Ändern Sie in einem Repository GA

Um in einem Quellrepository (CU oder GDR) aus dem Repository für die Vorschau zu ändern, verwenden Sie die folgenden Schritte aus:

1. Entfernen Sie die zuvor konfigurierten Preview-Repository.

   | Platform | Befehl der Repository-entfernen |
   |-----|-----|
   | RHEL | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | Ubuntu | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |

1. Für **Ubuntu nur**, importieren Sie die öffentlichen Repositorys GPG Schlüssel.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Konfigurieren Sie das neue Repository.

   | Platform | Repository | Befehl |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [Installieren Sie](sql-server-linux-setup.md#platforms) oder [aktualisieren](sql-server-linux-setup.md#upgrade) SQL Server mithilfe der GA-Repository.

   > [!IMPORTANT]
   > An diesem Punkt, falls gewünscht, zum Ausführen einer vollständigen Installation mit den [Schnellstart-Lernprogrammen](#platforms), denken Sie daran, dass Sie das Zielrepository gerade konfiguriert haben. Wiederholen Sie diesen Schritt nicht in den Lernprogrammen. Dies ist insbesondere dann, wenn Sie das Repository GDR konfigurieren, da die Schnellstart-Lernprogrammen CU-Repository verwenden.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Installieren von SQL Server-2017 unter Linux finden Sie unter [-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md).
