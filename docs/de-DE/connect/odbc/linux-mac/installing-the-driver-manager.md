---
title: Installieren des Treiber-Managers (Odbcdriver for SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
caps.latest.revision: 59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e465c3fa67375316be9cfbe614dfd5bfa62b7823
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="installing-the-driver-manager"></a>Installieren des Treiber-Managers
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Dieser Artikel enthält Anweisungen zur Installation des UnixODBC Treiber-Manager für die Verwendung mit allen Versionen von Microsoft ODBC Driver für SQL Server unter Linux und MacOS.  

> [!IMPORTANT]  
> Löschen Sie alle Treiber-Manager-Pakete, die auf Ihrem Computer installiert sind, bevor Sie den unixODBC Treiber-Manager installieren. Die Installation des unixODBC Treiber-Managers kann einen Fehler eines vorhandenen Treiber-Managers verursachen.  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>Installieren des Treiber-Managers für Microsoft ODBC Driver 13 13.1 und 17
Die Abhängigkeit der Treiber-Manager wird durch die paketverwaltungssystem automatisch aufgelöst, bei der Installation von Microsoft Odbcdriver 13, 13.1 oder 17 für SQL Server unter Linux oder MacOS, anhand der Anweisungen in [Installieren des Microsoft ODBC Driver für SQL Server unter Linux oder MacOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Installieren des Treiber-Managers für Microsoft ODBC Driver 11 (Preview) for SQL Server.  

(SUSE und Red Hat Linux nur.)

**Verwenden des Installationsskripts**  
  
> [!IMPORTANT]  
> Diese Anleitung bezieht sich auf `msodbcsql-11.0.2270.0.tar.gz`, also die Installationsdatei für Red Hat Linux. Wenn Sie die Vorschau für SUSE Linux installieren, wird der Dateiname `msodbcsql-11.0.2260.0.tar.gz`.  

Installieren des Treiber-Managers:  
  
1.  Stellen Sie sicher, dass Sie die Root-Berechtigung besitzen.  
  
2.  Wechseln Sie zu dem Verzeichnis, in dem die [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ODBC-Treiber-Download platziert hat die Datei mit dem Namen `msodbcsql-11.0.2270.0.tar.gz`. Stellen Sie sicher, dass Sie die zu Ihrer Linux-Version passende Datei „ \*.tar.g“ besitzen. Um die Dateien zu extrahieren, führen Sie den folgenden Befehl: **Xvzf "Msodbcsql-11.0.2270.0.TAR.gz" tar**.  

3.  Ändern Sie in der `msodbcsql-11.0.2270.0` Verzeichnis, und es wird eine Datei namens angezeigt `build_dm.sh`. Sie können ausführen `build_dm.sh` UnixODBC Treiber-Manager installieren.

4.  Um eine Liste der verfügbaren Optionen zu erhalten, führen Sie den folgenden Befehl: **./build_dm.sh – Hilfe**.  
  
5.  Wenn Sie zur Installation bereit sind, und Ihr Computer eine externe Website über FTP zugreifen kann, führen Sie den folgenden Befehl: **./build_dm.sh**.

Wenn Ihr Computer eine externe Website über FTP zugreifen kann, erhalten `unixODBC-2.3.0.tar.gz`. Sie erhalten `unixODBC-2.3.0.tar.gz` aus [ http://www.unixodbc.org ](http://www.unixodbc.org/). Klicken Sie auf die **herunterladen** Link auf der linken Seite der Seite, um zur Downloadseite zu wechseln. Klicken Sie dann auf den entsprechenden Link, um unixODBC-2.3.0 (nicht unixODBC-2.3.1) herunterzuladen. UnixODBC-2.3.1 wird nicht unterstützt, mit dieser Version von den [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Führen Sie den folgenden Befehl aus, um den UnixODBC Treiber-Manager-Installation zu beginnen: **./build_dm.sh – Download-Url = file://unixODBC-2.3.0.tar.gz**.  

6.  Typ **Ja** zu fortfahren mit dem Entpacken der Dateien. In diesem Teil des Prozesses kann bis zu fünf Minuten in Anspruch nehmen.  

7.  Nachdem das Skript beendet ist, befolgen Sie die Anweisungen auf dem Bildschirm, um den unixODBC Treiber-Manager zu installieren.

Sie können nun den Treiber installieren. Weitere Informationen finden Sie unter [Installieren von Microsoft ODBC Driver für SQL Server unter Linux und MacOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  

**Manuelle Installation**

Wenn das Skript für die Installation nicht abgeschlossen werden konnte, konfigurieren und erstellen Sie selbst den richtigen Treiber-Manager.

1.  Entfernen Sie alle älteren installierten Versionen von unixODBC (z. B. unixODBC 2.2.11). Führen Sie den folgenden Befehl auf Red Hat Enterprise Linux 5 oder 6: **Yum entfernen UnixODBC**. Auf SUSE Linux Enterprise: **Zypper entfernen UnixODBC**.  
  
2.  Klicken Sie auf [ http://www.unixodbc.org ](http://www.unixodbc.org/). Klicken Sie auf die **herunterladen** Link auf der linken Seite der Seite, um zur Downloadseite zu wechseln. Klicken Sie dann auf den entsprechenden Link, um die Datei „unixodbc-2.3.0.tar.gz“ auf Ihrem Computer zu speichern. UnixODBC-2.3.1 wird nicht unterstützt, mit dieser Version von den [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
3.  Führen Sie den Befehl auf dem Linux-Computer: **tar Xvzf UnixODBC-2.3.0.tar.gz**.  
  
4.  Wechseln Sie zum Verzeichnis „unixODBC-2.3.0“.  
  
5.  Führen Sie an einer Eingabeaufforderung den Befehl: **CPPFLAGS = "-DSIZEOF_LONG_INT = 8"**.  
  
6.  Führen Sie an einer Eingabeaufforderung den Befehl: **CPPFLAGS exportieren**.  
  
7.  Führen Sie an einer Eingabeaufforderung den Befehl: **". / konfigurieren – prefix = / Usr--Libdir = / Usr/lib64--Sysconfdir = / usw. – Enable-gui = Nein – Enable-Treiber = Nein – Enable-Iconv--mit-Iconv-Char-Enc UTF8--mit-Iconv-Ucode-Enc = UTF16LE ="**.  
  
8.  Führen Sie den Befehl an einer Eingabeaufforderung (angemeldet als Root): **stellen**.  
  
9. Führen Sie den Befehl an einer Eingabeaufforderung (angemeldet als Root): **stellen installieren**.  

Sie können nun den Treiber installieren. Weitere Informationen finden Sie unter [Installieren von Microsoft ODBC Driver für SQL Server unter Linux und MacOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  
  
## <a name="see-also"></a>Siehe auch
[Installieren von Microsoft ODBC Driver für SQL Server unter Linux und macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[Bekannte Probleme in dieser Version des Treibers](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Anmerkungen zu dieser Version](../../../connect/odbc/linux-mac/release-notes.md)
