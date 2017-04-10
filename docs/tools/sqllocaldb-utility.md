---
title: "SqlLocalDB-Hilfsprogramm | Microsoft Docs"
ms.custom: ""
ms.date: "08/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SqlLocalDB-Hilfsprogramm [SQL Server]"
  - "Hilfsprogramm für Laufzeit der lokalen Datenbank"
  - "LocalDB, SqlLocalDB-Hilfsprogramm"
ms.assetid: d785cdb7-1ea0-4871-bde9-1ae7881190f5
caps.latest.revision: 19
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 19
---
# SqlLocalDB-Hilfsprogramm
  Verwenden Sie das Hilfsprogramm **SqlLocalDB**, um eine Instanz von [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssExpCurrent](../includes/ssexpcurrent-md.md)]**LocalDB** zu erstellen. Das Hilfsprogramm **SqlLocalDB** (SqlLocalDB.exe) ist ein einfaches Befehlszeilentool, mit dem Benutzer und Entwickler eine Instanz von [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** erstellen und verwalten können. Informationen zum Verwenden von **LocalDB** finden Sie unter [SQL Server 2016 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md).  
  
## Syntax  
  
```  
SqlLocalDB.exe   
{  
      [ create   | c ] <instance-name>  <instance-version> [-s ]  
    | [ delete   | d ] <instance-name>  
    | [ start    | s ] <instance-name>  
    | [ stop     | p ] <instance-name>  [ -i ] [ -k ]  
    | [ share    | h ] [" <user_SID> " | " <user_account> " ] " <private-name> " " <shared-name> "  
    | [ unshare  | u ] " <shared-name> "  
    | [ info     | i ] <instance-name>  
    | [ versions | v ]  
    | [ trace    | t ] [ on | off ]  
    | [ help     | -? ]  
}  
```  
  
## Argumente  
 [ **create** | **c** ] *<Instanzname>* *<Instanzversion>* [**-s** ]  
 Erstellt eine neue Instanz von [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. **SqlLocalDB** verwendet die Version der mit dem *<Instanzversion>*-Argument angegebenen [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]-Binärdateien. Die Versionsnummer wird im numerischen Format mit mindestens einer Dezimalzahl angegeben. Die Nebenversionsnummern (Service Packs) sind optional. Beispielsweise werden die folgenden zwei Versionsnummern akzeptiert: 11.0 oder 11.0.1186. Die angegebene Version muss auf dem Computer installiert sein. Wenn die Versionsnummer nicht angegeben ist, wird standardmäßig die Version des Hilfsprogramms **SqlLocalDB** verwendet. Durch Hinzufügen von **-s** wird die neue Instanz von **LocalDB** gestartet.  
  
 [ **share** | **h** ]  
 Gibt die angegebene private Instanz von **LocalDB** mithilfe des angegebenen freigegebenen Namens frei. Wenn die Benutzer-SID oder der Kontoname weggelassen wird, wird standardmäßig der aktuelle Benutzer verwendet.  
  
 [ **unshared** | **u** ]  
 Beendet die Freigabe der angegebenen freigegebenen Instanz von **LocalDB**.  
  
 [ **delete** | **d** ] *<Instanzname>*  
 Löscht die angegebene Instanz von [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**.  
  
 [ **start** | **s** ] "*<Instanzname>*"  
 Startet die angegebene Instanz von [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. Bei Erfolg gibt die Anweisung die Named Pipe-Adresse von **LocalDB** zurück.  
  
 [ **stop** | **p** ] *<Instanzname>* [**-i** ] [**-k** ]  
 Beendet die angegebene Instanz von [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. Durch Hinzufügen von **-i** wird das Herunterfahren der Instanz mit der **NOWAIT**-Option angefordert. Durch Hinzufügen von **-k** wird der Instanzprozess ohne Kontaktieren abgebrochen.  
  
 [ **info** | **i** ] [ *<Instanzname>* ]  
 Listet alle Instanzen von [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** auf, die im Besitz des aktuellen Benutzers sind.  
  
 *<Instanzname>* gibt Name, Version, Status („Wird ausgeführt“ oder „Beendet“) und die letzte Startzeit für die angegebene Instanz von [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** und den lokalen Pipenamen von **LocalDB** zurück.  
  
 [ **trace** | **t** ] **on** | **off**  
 **trace on** aktiviert die Ablaufverfolgung für die **SqlLocalDB**-API-Aufrufe für den aktuellen Benutzer. **trace off** deaktiviert die Ablaufverfolgung.  
  
 **-?**  
 Gibt eine kurze Beschreibungen jeder **SqlLocalDB**-Option zurück.  
  
## Hinweise  
 Für das *instance name*-Argument müssen die Regeln für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Bezeichner befolgt werden, oder das Argument muss in doppelte Anführungszeichen eingeschlossen werden.  
  
 Bei der Ausführung von „SqlLocalDB“ ohne Argumente wird der Hilfetext zurückgegeben.  
  
 Vorgänge, die keine Startvorgänge sind, können nur für eine Instanz ausgeführt werden, die zum derzeit angemeldeten Benutzer gehört. Wenn eine SQLLOCALDB-Instanz freigegeben wird, kann sie nur vom Besitzer der Instanz gestartet und beendet werden.  
  
## Beispiele  
  
### A. Erstellen einer Instanz von LocalDB  
 Im folgenden Beispiel wird mithilfe der [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Binärdateien eine Instanz von [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** namens `DEPARTMENT` erstellt und die Instanz gestartet.  
  
```  
SqlLocalDB.exe create "DEPARTMENT" 12.0 -s  
```  
  
### B. Verwenden einer freigegebenen Instanz von LocalDB  
 Öffnen Sie eine Eingabeaufforderung unter Administratorberechtigungen.  
  
```  
SqlLocalDB.exe create "DeptLocalDB"  
SqlLocalDB.exe share "DeptLocalDB" "DeptSharedLocalDB"  
SqlLocalDB.exe start "DeptLocalDB"  
SqlLocalDB.exe info "DeptLocalDB"  
REM The previous statement outputs the Instance pipe name for the next step  
sqlcmd –S np:\\.\pipe\LOCALDB#<use your pipe name>\tsql\query  
CREATE LOGIN NewLogin WITH PASSWORD = 'Passw0rd!!@52';   
GO  
CREATE USER NewLogin;  
GO  
EXIT  
```  
  
 Führen Sie den folgenden Code aus, um unter Verwendung des `NewLogin`-Anmeldenamens eine Verbindung zur freigegebenen **LocalDB**-Instanz herzustellen.  
  
```  
sqlcmd –S (localdb)\.\DeptSharedLocalDB -U NewLogin -P Passw0rd!!@52  
```  
  
## Siehe auch  
 [SQL Server 2016 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
[Verwaltungstool für Befehlszeilen: SqlLocalDB.exe](Command-Line%20Management%20Tool:%20SqlLocalDB.exe.md)  
  