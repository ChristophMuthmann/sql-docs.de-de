---
title: SQLServer Express LocalDB-Header und Versionsinformationen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apilocation: sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1b349093cc92fdfced91476f69bf98b60384e783
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>SQL Server Express LocalDB-Header und Versionsinformationen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Es ist keine separate Headerdatei für die SQL Server Express LocalDB Instanz-API. die LocalDB-Funktionssignaturen und Fehlercodes werden in der SQL Server Native Client-Headerdatei (sqlncli.h) definiert. Zur Verwendung der LocalDB-Instanz-API müssen Sie die Headerdatei sqlncli.h in das Projekt einfügen.  
  
## <a name="localdb-versioning"></a>LocalDB-Versionsverwaltung  
 Die LocalDB-Installation verwendet pro Haupt-SQL Server-Version einen einzelnen Satz Binärdateien. Diese LocalDB-Versionen werden gewartet und unabhängig gepatcht. Das bedeutet, dass der Benutzer angeben muss, welche LocalDB-Baselineversion (also Haupt-SQL Server-Version) er verwendet. Die Version wird angegeben, in dem von .NET Framework definierten Standardversion Format **System.Version** Klasse:  
  
 *[.Revision]]*  
  
 Die ersten beiden Zahlen in der Versionszeichenfolge (*wichtigen* und *kleinere*) müssen angegeben werden. Die letzten zwei Zahlen in der Versionszeichenfolge (*erstellen* und *Revision*) sind optional und standardmäßig auf 0 (null), wenn der Benutzer sie auslässt. Wenn der Benutzer nur "12.2" als LocalDB-Versionsnummer angibt, wird diese behandelt, als ob er "12.2.0.0" angegeben hätte.  
  
 Die Version für die LocalDB-Installation ist im Registrierungsschlüssel MSSQLServer\CurrentVersion unter dem SQL Server-Instanz-Registrierungsschlüssel definiert. Beispiel:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL13E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 Mehrere LocalDB-Versionen auf derselben Arbeitsstation werden gleichzeitig unterstützt. Allerdings Benutzercode verwendet immer die neuesten verfügbaren **SQLUserInstance** DLL auf dem lokalen Computer zur Verbindung mit LocalDB-Instanzen.  
  
## <a name="locating-the-sqluserinstance-dll"></a>Suchen der SQLUserInstance-DLL  
 Suchen der **SQLUserInstance** DLL, verwendet der Clientanbieter den folgenden Registrierungsschlüssel:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 Unter diesem Schlüssel befindet sich eine Liste Schlüssel, einer für jede Version der auf dem Computer installierten LocalDB. Jeder dieser Schlüssel ist mit der LocalDB-Versionsnummer im Format namens  *\<Hauptversion >*. *\<Nebenversion >* (z. B. den Schlüssel für [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] heißt 13.0). Unter jedem Versionsschlüssel dort ist ein `InstanceAPIPath`-Name-Wert-Paar, das den vollständigen Pfad zur mit dieser Version installierten SQLUserInstance.dll-Datei definiert. Das folgende Beispiel zeigt die Registrierungseinträge für einen Computer mit LocalDB-Versionen 11.0 und 13.0 installiert:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 Finden Sie den Clientanbieter muss die neueste Version für alle installierten Versionen und laden die **SQLUserInstance** DLL-Datei aus dem zugeordneten `InstanceAPIPath` Wert.  
  
### <a name="wow64-mode-on-64-bit-windows"></a>WOW64-Modus unter 64-Bit-Windows  
 64-Bit-Installationen von LocalDB weisen einen zusätzlichen Satz Registrierungsschlüssel auf, der 32-Bit-Anwendungen, die im WOW64 (Windows-32-on-Windows-64)-Modus ausgeführt werden, die Verwendung von LocalDB ermöglicht. Insbesondere unter 64-Bit-Windows erstellt LocalDB-MSI die folgenden Registrierungsschlüssel:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 64-Bit-Programme lesen den `Installed Versions` -Schlüssel und sehen Werte, die auf 64-Bit-Versionen der der **SQLUserInstance** DLL, die während der 32-Bit-Programme, die (auf 64-Bit-Windows im WOW64-Modus ausgeführt wird) automatisch umgeleitet werden, ein `Installed Versions` Zertifikatschlüssel befindet sich unter der `Wow6432Node` Hive. Dieser Schlüssel enthält Werte, die auf 32-Bit-Versionen der der **SQLUserInstance** DLL.  
  
## <a name="using-localdbdefineproxyfunctions"></a>Verwenden von LOCALDB_DEFINE_PROXY_FUNCTIONS  
 Die LocalDB Instanz-API definiert eine Konstante, die mit der Bezeichnung LOCALDB_DEFINE_PROXY_FUNCTIONS, die die Ermittlung und Laden von automatisiert die **SqlUserInstance** DLL.  
  
 Der durch diese Konstante aktivierte Abschnitt des Codes stellt eine Implementierung der Proxys für jede der LocalDB-APIs bereit. Die Proxyimplementierungen verwenden eine allgemeine Funktion zum Binden an verschiedenen Punkten in der neuesten installierten **SqlUserInstance** DLL, und klicken Sie dann die Anforderungen weiterzuleiten.  
  
 Die Proxyfunktionen werden nur aktiviert, wenn die Konstante LOCALDB_DEFINE_PROXY_FUNCTIONS vor dem Einfügen der Datei sqlncli.h im Benutzercode definiert wurde. Die Konstante darf in nur einem Quellenmodul (CPP-Datei) definiert werden, da sie externe Funktionsnamen für alle API-Einstiegspunkte definiert. Sie stellt eine Implementierung der Proxys für alle LocalDB-APIs bereit.  
  
 Im folgenden Codebeispiel wird gezeigt, wie das Makro vom systemeigenen C++-Code verwendet wird:  
  
```  
// Define the LOCALDB_DEFINE_PROXY_FUNCTIONS constant to enable the LocalDB proxy functions   
// The #define has to take place BEFORE the API header file (sqlncli.h) is included  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include <sqlncli.h>  
…  
HRESULT hr = S_OK;  
  
// Create LocalDB instance by calling the create API proxy function included by macro  
if (FAILED(hr = LocalDBCreateInstance( L"12.0", L"name", 0)))  
{  
…  
}  
…  
  
```  
  
  
