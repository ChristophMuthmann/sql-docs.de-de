---
title: Ssms-Hilfsprogramm | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 6dccaff93a6c8b2374a1fad069b2f597898802fc
ms.openlocfilehash: 84b9b39b9a7ae03244dd3703cc303d1cf7f4380b
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="ssms-utility"></a>Ssms-Hilfsprogramm
  Mit dem **Ssms**-Hilfsprogramm wird [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]geöffnet. Bei entsprechender Angabe stellt **Ssms** zudem eine Verbindung mit einem Server her und öffnet Abfragen, Skripts, Dateien, Projekte und Lösungen.  
  
 Sie können Dateien angeben, die Abfragen, Projekte oder Lösungen enthalten. Für Dateien, die Abfragen enthalten, wird automatisch eine Verbindung mit einem Server hergestellt, wenn Verbindungsinformationen bereitgestellt werden und der Dateityp diesem Servertyp zugeordnet ist. So wird z. B. für SQL-Dateien ein SQL-Abfrage-Editorfenster in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]und für MDX-Dateien ein MDX-Abfrage-Editorfenster in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]geöffnet. **SQL Server-Lösungen und -Projekte** werden in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]geöffnet.  
  
> [!NOTE]  
>  Das Hilfsprogramm **Ssms** führt keine Abfragen aus. Zum Ausführen von Abfragen in der Befehlszeile verwenden Sie das **sqlcmd** -Hilfsprogramm.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Ssms  
    [scriptfile] [projectfile] [solutionfile]  
    [-S servername] [-d databasename] [-U username] [-P password]   
    [-E] [-nosplash] [-log [filename]?] [-?]  
```  
  
## <a name="arguments"></a>Argumente  
 *scriptfile*  
 Gibt eine oder mehrere zu öffnende Skriptdateien an. Der Parameter muss den vollständigen Pfad zu den Dateien enthalten.  
  
 *projectfile*  
 Gibt ein zu öffnendes Skriptprojekt an. Der Parameter muss den vollständigen Pfad zur Skriptprojektdatei enthalten.  
  
 *solutionfile*  
 Gibt eine zu öffnende Lösung an. Der Parameter muss den vollständigen Pfad zur Lösungsdatei enthalten.  
  
 [**-S** *servername*]  
 Servername  
  
 [**-d** *databasename*]  
 Datenbankname  
  
 [**-U** *username*]  
 Benutzername, wenn die Verbindung mithilfe der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung hergestellt wird.  
  
 [**-P** *password*]  
 Kennwort, wenn die Verbindung mithilfe der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung hergestellt wird.  
  
 [**-E**]  
 Verbindung mithilfe der Windows-Authentifizierung herstellen  
  
 [**-nosplash**]  
 Verhindert, dass [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] beim Öffnen den Begrüßungsbildschirm anzeigt. Verwenden Sie diese Option, wenn Sie eine Verbindung zum Computer mit [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] herstellen und hierfür Terminaldienste über eine Verbindung mit begrenzter Bandbreite einsetzen. Bei diesem Argument wird die Groß- und Kleinschreibung nicht beachtet. Es kann vor oder nach anderen Argumenten angegeben werden.  
  
 [**-log***[filename]?*]  
 Protokolliert die [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] -Aktivität zur Problembehandlung in der angegebenen Datei.  
  
 [**-?**]  
 Zeigt die Hilfe zur Befehlszeile an.  
  
## <a name="remarks"></a>Hinweise  
 Alle Schalter sind optional und werden durch Leerzeichen voneinander getrennt. Eine Ausnahme hiervon bilden Dateien, die durch Kommas getrennt werden. Wenn Sie keine Schalter angeben, wird **Ssms** Ssms [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] so geöffnet, wie es in den Einstellungen unter **Optionen** im Menü **Extras** angegeben ist. Wenn z.B. auf der Seite **Umgebung/Allgemein** unter **Beim Start** die Option **Neues Abfragefenster öffnen**angegeben ist, öffnet **Ssms** ein leeres Abfrage-Editor-Fenster.  
  
 Der **-log** -Schalter muss am Ende der Befehlszeile nach allen anderen Schaltern angegeben werden. Das filename-Argument ist optional. Wenn ein Dateiname angegeben wird und die Datei nicht vorhanden ist, wird sie erstellt. Wenn die Datei beispielsweise aufgrund unzureichender Schreibberechtigungen nicht erstellt werden kann, wird die Datei stattdessen in den Ordner für nicht lokalisierte Anwendungsdaten (APPDATA) geschrieben (siehe unten). Wenn das filename-Argument nicht angegeben wird, werden zwei Dateien in den Ordner für nicht lokalisierte Anwendungsdaten des aktuellen Benutzers geschrieben. Der Ordner für nicht lokalisierte Anwendungsdaten in SQL Server kann anhand der APPDATA-Umgebungsvariablen ermittelt werden. Für SQL Server 2012 lautet der Ordner beispielsweise \<Systemlaufwerk>:\Users\\<Benutzername\>\AppData\Roaming\Microsoft\AppEnv\10.0\\. Die beiden Dateien erhalten standardmäßig den Namen ActivityLog.xml und ActivityLog.xsl. Die erste Datei enthält die Aktivitätsprotokolldaten, und die zweite Datei ist ein XML-Stylesheet, mit dem die XML-Datei auf bequeme Weise angezeigt werden kann. Führen Sie die folgenden Schritte aus, um die Protokolldatei in einem standardmäßigen XML-Viewer wie Internet Explorer anzuzeigen: Klicken Sie auf „Start“ und auf „Ausführen“. Geben Sie dann \<Systemlaufwerk>:\Users\\<Benutzername\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml in das angezeigte Feld ein, und drücken Sie die EINGABETASTE.  
  
 Dateien, die Abfragen enthalten, fordern eine Verbindung mit einem Server an, wenn Verbindungsinformationen bereitgestellt werden und der Dateityp diesem Servertyp zugeordnet ist. So wird z. B. für SQL-Dateien ein SQL-Abfrage-Editorfenster in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]und für MDX-Dateien ein MDX-Abfrage-Editorfenster in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]geöffnet. **SQL Server-Lösungen und -Projekte** werden in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]geöffnet.  
  
 In der folgenden Tabelle werden Servertypen zu Dateierweiterungen zugeordnet.  
  
|Servertyp|Erweiterung|  
|-----------------|---------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|SQL|  
|SQL Server Analysis Services|MDX<br /><br /> XMLA|  
  
## <a name="examples"></a>Beispiele  
 Mit dem folgenden Skript wird [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] mit den Standardeinstellungen von der Eingabeaufforderung aus geöffnet.  
  
```  
Ssms  
  
```  
  
 Mit dem folgenden Skript wird [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] von der Eingabeaufforderung aus geöffnet. Es wird die Windows-Authentifizierung verwendet, im Code-Editor wird der Server `ACCTG and the database AdventureWorks2012,` ausgewählt, und der Begrüßungsbildschirm wird nicht angezeigt:  
  
```  
Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash  
  
```  
  
 Mit dem folgenden Skript wird [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] von der Eingabeaufforderung aus geöffnet. Anschließend wird das Skript MonthEndQuery geöffnet.  
  
```  
Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"  
  
```  
  
 Mit dem folgenden Skript wird [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] von der Eingabeaufforderung aus geöffnet. Anschließend wird das Projekt NewReportsProject auf dem Computer `developer`geöffnet:  
  
```  
Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"  
  
```  
  
 Mit dem folgenden Skript wird [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] von der Eingabeaufforderung aus geöffnet. Anschließend wird die Lösung MonthlyReports geöffnet:  
  
```  
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
  
  
