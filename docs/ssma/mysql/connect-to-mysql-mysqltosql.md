---
title: Herstellen einer Verbindung mit MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b0a3565b466d132f829000d519195d2fedb27dc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-mysql-mysqltosql"></a>Herstellen einer Verbindung mit MySQL (MySQLToSQL)
Verwenden der **Herstellen einer Verbindung mit MySQL** Dialogfeld Verbindung mit der MySQL-Datenbank, die Sie migrieren möchten.  
  
Zum Zugriff auf dieses Dialogfeld, in dem **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit MySQL**. Wenn Sie zuvor eine Verbindung hergestellt haben, wird der Befehl ist **eine erneute Verbindung mit MySQL**.  
  
## <a name="options"></a>enthalten  
**Provider**  
  
MySQL-Anbieter verfügbar ist, MySQL 5.1 Odbcdriver (vertrauenswürdigen).  
  
**Mode**  
  
Der Standardmodus ist Modus "Standard". Im Modus "Standard" eingeben oder wählen Sie Werte für die MySQL, Servername, Server-Port, Benutzername und Kennwort.  
  
**Servername**  
  
Geben Sie den Namen der MySQL-Server aus. Dies ist ein Modus "Standard"-Option.  
  
**Serverport**  
  
Geben Sie den Server-Port. Der Server-Standardport ist 3306. Dies ist ein Modus "Standard"-Option.  
  
**Benutzername**  
  
Geben Sie den Benutzernamen, den SSMA für die Verbindung zur MySQL-Datenbank verwenden.  
  
**Kennwort**  
  
Geben Sie das Kennwort für den Benutzernamen ein.  
  
**SSL**  
  
Wenn Sie eine sichere Verbindung mit MySQL möchten, stellen Sie durch Überprüfung des Secure Socket Layer (SSL) verwenden die **SSL** Kontrollkästchen.  
  
**Konfigurieren**  
  
Es bietet eine Option aus, um die Verbindung mit MySQL über Secure Socket Layer (SSL) konfigurieren.  
  
> [!NOTE]  
> So aktivieren Sie **konfigurieren**, SSL muss festgelegt werden, um **"true"**.  
  
Auf der Schaltfläche "Konfigurieren", ein Dialogfeld wird angezeigt. Definiert [Privacy Enhanced Mail-Zertifikate (PEM)], Verschlüsselung zu verwenden, beim Herstellen einer Verbindung mit MySQL-Datenbank, Pfad, um die folgenden drei Dateien in das Dialogfeld vorhanden sein muss:  
  
-   **SSL-Zertifizierungsstelle:** gibt den Pfad zu einer Datei mit einer Liste von vertrauenswürdigen Zertifizierungsstellen SSL an.  
  
-   **SSL-Zertifikat:** gibt den Namen des SSL-Zertifikatdatei zum Herstellen einer sicheren Verbindung verwendet werden soll.  
  
-   **SSL-Schlüssel:** gibt den Namen der SSL-Schlüsseldatei zum Herstellen einer sicheren Verbindung verwendet werden soll.  
  
> [!NOTE]  
> -   Die **OK** Schaltfläche ist aktiviert, wenn die erforderliche Informationen angegeben wurden. Wenn die Dateipfade ungültig sind, bleiben die Schaltfläche "OK" wird deaktiviert.  
> -   Die **"Abbrechen"** Schaltfläche wird das Dialogfeld geschlossen und **deaktiviert** die Option "SSL" aus der Verbindung Hauptformular.  
  
