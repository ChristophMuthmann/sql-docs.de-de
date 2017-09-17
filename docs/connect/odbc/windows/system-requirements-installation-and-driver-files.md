---
title: Systemanforderungen, Installation und Treiberdateien | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a11d146a889da5af037a154a1f8226e2bcb8ccb2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-installation-and-driver-files"></a>Systemanforderungen, Installation und Treiberdateien
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Der ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unterstützt Verbindungen mit SQL Server 2014, SQL Server 2012 R2, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro_md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]und [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)].  
  
Der ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] on Windows kann auf einem Computer installiert werden, der auch eine oder mehrere Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client besitzt.  
  
Der ODBC Driver 13 und 13.1 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], zusätzlich zu den oben genannten unterstützt SQL Server 2016.  
  
Der Treibername, den Sie in einer Verbindungszeichenfolge angeben lautet `ODBC Driver 11 for SQL Server` oder `ODBC Driver 13 for SQL Server` (bei 13 und 13.1).
  
## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme

Sie können Programme mit dem Treiber auf die folgenden Windows-Betriebssysteme ausführen:  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(nur Odbcdriver 11)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Installieren Microsoft ODBC Driver for SQLServer

Der Treiber ist installiert, wenn Sie ausführen `msodbcsql.msi` aus [Herunterladen der Microsoft ODBC Driver 13.1 for SQL Server unter Windows](https://www.microsoft.com/download/details.aspx?id=53339), [Herunterladen von Microsoft ODBC Driver 13 for SQL Server unter Windows](https://www.microsoft.com/download/details.aspx?id=50420), oder [ Microsoft ODBC Driver 11 for SQLServer on Windows herunterladen](https://www.microsoft.com/download/details.aspx?id=36434). Installierte Seite-an-Seite mit möglich [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client.  

Beim Aufruf `msodbcsql.msi`, werden nur die Clientkomponenten standardmäßig installiert. Den Clientkomponenten handelt es sich um Dateien, die Unterstützung der Ausführung einer Anwendung, die mit dem Treiber entwickelt wurde. Um die SDK-Komponenten zu installieren, geben `ADDLOCAL=ALL` in der Befehlszeile angegeben. Beispiel:  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 Geben Sie `IACCEPTMSODBCSQLLICENSETERMS=YES` zum Akzeptieren der Bestimmungen der Endbenutzerlizenz, bei Verwendung der `/passive`, `/qn`, `/qb`, oder `/qr` Option zur Installation. Diese Option muss vollständig in Großbuchstaben angegeben werden. Beispiel:  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 So führen Sie eine unbeaufsichtigte Deinstallation aus:  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
Wenn eine Anwendung den Treiber verwendet, sollte die Anwendung angeben, abhängig vom Treiber über die Installationsoption `APPGUID`. Dies ermöglicht den Treiber-Installer, abhängige berichtsanwendungen vor der Deinstallation. Um eine Abhängigkeit vom Treiber anzugeben, legen die `APPGUID` Befehlszeilenparameter auf Ihren Produktcode, wenn der Treiber unbeaufsichtigt installieren. (Beim Packen des Setupprogramms für die Anwendung mit Microsoft Installer muss ein Produktcode erstellt werden.) Beispiel:  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Befehlszeilentools: sqlcmd.exe und bcp.exe

Die `bcp.exe` und `sqlcmd.exe` tools für die Verwendung mit dem Treiber heruntergeladen werden kann, auf [Microsoft Befehlszeilenprogramme 11 für SQL Server](http://www.microsoft.com/download/details.aspx?id=36433), [Microsoft über die Befehlszeile Hilfsprogramme 13 für SQL Server](https://www.microsoft.com/download/details.aspx?id=52680), oder [Microsoft Befehlszeilenprogramme 13.1 for SQLServer](https://www.microsoft.com/download/details.aspx?id=53591). Der Treiber ist Voraussetzung für die Installation `sqlcmd.exe` und `bcp.exe`.
  
`bcp.exe`und `sqlcmd.exe` installiert sind, der `110\Tools` Unterordner des `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` für Version 11 und `130\Tools` für 13 und 13.1.

Eine Anwendung, die BCP-Funktionen verwendet, muss den Treiber mit derselben Version das geliefert angeben, mit der Headerdatei und Bibliothek verwendet, um die Anwendung zu kompilieren.  

Beispielsweise wird beim Kompilieren einer ODBC-Anwendung mit `msodbcsql11.lib` und `msodbcsql.h`, verwenden Sie "DRIVER = {Odbcdriver 11 für SQLServer}" in der Verbindungszeichenfolge angegeben.

## <a name="components-of-the-microsoft-odbc-driver-13-and-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Komponenten von Microsoft ODBC Driver 13 und 13.1 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Windows  
 Der ODBC-Treiber für Windows enthält die folgenden Komponenten:  
  
|Komponente|Beschreibung|  
|---------------|-----------------|  
|msodbcsql13.dll|Die DLL-Datei (Dynamic-Link Library, DLL), die die gesamte Funktionalität des Treibers enthält „msodbcsql13.dll“ wird in %SYSTEMROOT%\System32 installiert.|  
|msodbcsqlr13.rll|Die begleitende Ressourcendatei für die Treiberbibliothek. „msodbcsqlr13.rll“ wird in %SYSTEMROOT%\System32\1033 installiert.|  
|s13ch_msodbcsql.chm|Die Hilfedatei des Datenquellen-Assistenten, die zum Erstellen einer Datenquelle für den Treiber dokumentiert. „s13ch_msodbcsql.chm“ wird in %SYSTEMROOT%\System32\1033 installiert.|  
|msodbcsql.h|Die Header-Datei, die alle erforderlichen neuen Definitionen benötigt des Treibers enthält.<br /><br /> **Hinweis:**  Sie können nicht auf „msodbcsql.h“ und „odbcss.h“ im selben Programm verweisen.<br /><br /> "msodbcsql.h" wird in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK installiert.|  
|msodbcsql13.lib|Die Bibliotheksdatei, die zum Aufrufen der **Bcp** Hilfsfunktionen, die Teil des Treibers.<br /><br /> **Hinweis:**  Wenn Sie in Ihrem Programm auf „msodbcsql13.lib“ verweisen, stellen Sie sicher, dass „msodbcsql13.dll“ in Ihrem Systempfad sowie im Systempfad der Dateien, die die Anwendungen verwenden, vorhanden ist.<br /><br /> msodbcsql13.lib wird in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK installiert.|  
  
## <a name="components-of-the-microsoft-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Komponenten von Microsoft ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] on Windows  
 Der ODBC-Treiber für Windows enthält die folgenden Komponenten:  
  
|Komponente|Beschreibung|  
|---------------|-----------------|  
|msodbcsql11.dll|Die DLL-Datei (Dynamic-Link Library, DLL), die die gesamte Funktionalität des Treibers enthält „msodbcsql11.dll“ wird in %SYSTEMROOT%\System32 installiert.|  
|msodbcsqlr11.rll|Die begleitende Ressourcendatei für die Treiberbibliothek. „msodbcsqlr11.rll“ wird in %SYSTEMROOT%\System32\1033 installiert.|  
|s11ch_msodbcsql.chm|Die Hilfedatei des Datenquellen-Assistenten, die zum Erstellen einer Datenquelle für den Treiber dokumentiert. „s11ch_msodbcsql.chm“ wird in %SYSTEMROOT%\System32\1033 installiert.|  
|msodbcsql.h|Die Header-Datei, die alle erforderlichen neuen Definitionen benötigt des Treibers enthält.<br /><br /> **Hinweis:**  Sie können nicht auf „msodbcsql.h“ und „odbcss.h“ im selben Programm verweisen.<br /><br /> „msodbcsql.h“ wird in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK installiert.|  
|msodbcsql11.lib|Die Bibliotheksdatei, die zum Aufrufen der **Bcp** Hilfsfunktionen, die Teil des Treibers.<br /><br /> **Hinweis:**  Wenn Sie in Ihrem Programm auf „msodbcsql11.lib“ verweisen, stellen Sie sicher, dass „msodbcsql11.dll“ in Ihrem Systempfad sowie im Systempfad der Dateien, die die Anwendungen verwenden, vorhanden ist.<br /><br /> „msodbcsql11.lib“ wird in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK installiert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  

