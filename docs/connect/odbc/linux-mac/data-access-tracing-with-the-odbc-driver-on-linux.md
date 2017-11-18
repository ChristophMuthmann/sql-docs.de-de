---
title: Data Access Tracing, mit der ODBC-Treiber unter Linux und MacOS | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ae175bfa033ba445d9a8235706a2f6fe55690ac
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Data Access Tracing, mit dem ODBC-Treiber unter Linux und Mac OS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Der UnixODBC-Treiber-Manager unter Mac OS und Linux unterstützt die Verfolgung von ODBC-API-Aufrufeintrag, und Beenden des ODBC-Treibers für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].

Um die Anwendung ODBC-Verhalten zu verfolgen, bearbeiten Sie die `odbcinst.ini` Datei `[ODBC]` Abschnitt zum Festlegen der Werte `Trace=Yes` und `TraceFile` auf den Pfad der Datei, die in der Ablaufverfolgungsausgabe; enthalten z. B.:

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(Sie können auch `/dev/stdout` oder den Namen eines anderen Geräts Ablaufverfolgungsausgabe es anstelle des in einer persistenten Datei senden.) Mit den oben genannten Einstellungen jedes Mal, wenn eine Anwendung den UnixODBC Treiber-Managers, lädt zeichnet er alle ODBC-API-Aufrufe die es in die Ausgabedatei ausgeführt.

Nachdem Sie die Ablaufverfolgung Ihrer Anwendung abgeschlossen haben, entfernen `Trace=Yes` aus der `odbcinst.ini` -Datei, um Leistungseinbußen während der Ablaufverfolgung zu vermeiden und sicherzustellen, dass unnötigen Ablaufverfolgungsdateien werden entfernt.
  
Die Ablaufverfolgung gilt für alle Anwendungen mit dem Treiber `odbcinst.ini`. Um alle Anwendungen (z. B. verhindern, dass benutzerbezogene vertrauliche Informationen weitergegeben) nicht verfolgen zu können, können Sie eine einzelne Anwendungsinstanz verfolgen, unter Angabe den Speicherort einer privaten `odbcinst.ini`unter Verwendung der `ODBCSYSINI` -Umgebungsvariablen angegeben. Beispiel:  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
In diesem Fall können Sie hinzufügen `Trace=Yes` auf die `[ODBC Driver 13 for SQL Server]` Abschnitt `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Bestimmen, welche odbc.ini Datei der Treiber verwendet wird

Die ODBC-Treiber für Linux und MacOS führen Sie nicht wissen, welche `odbc.ini` wird verwendet, oder den Pfad zu der `odbc.ini` Datei. Allerdings Informationen dazu, welche `odbc.ini` Datei befindet sich in Verwendung ist über die UnixODBC-Tools verfügbar `odbc_config` und `odbcinst`, und von den UnixODBC Treiber-Manager-Dokumentation.  
  
Beispielsweise wird mit der folgende Befehl ausgibt (u. a.) für den Speicherort der System- und `odbc.ini` Dateien, die System- und Benutzer-DSN enthalten:

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

Die [UnixODBC-Dokumentation](http://www.unixodbc.org/doc/UserManual/) erläutert den Unterschied zwischen Benutzer und System-DSNs. Zusammenfassung:  

- Benutzer-DSNs---Hierbei handelt es sich um DSNs nur mit einem bestimmten Benutzer zur Verfügung stehen. Benutzer können Verbindung mit herstellen, hinzufügen, ändern oder entfernen eigene Benutzer-DSNs. Benutzer-DSNs werden in einer Datei im Basisverzeichnis des Benutzers oder auf einem Unterverzeichnis gespeichert.
  
- System-DSNs---diese DSNs stehen für alle Benutzer des Systems für die verbindungsherstellung, jedoch können nur hinzugefügt, geändert, und entfernt werden von einem Systemadministrator. Wenn ein Benutzer einen Benutzer-DSN mit dem gleichen Namen wie ein System-DSN hat, wird der Benutzer-DSN bei Verbindungen von diesem Benutzer verwendet werden.

## <a name="see-also"></a>Siehe auch
[Programmierrichtlinien](../../../connect/odbc/linux-mac/programming-guidelines.md)

