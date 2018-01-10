---
title: SQL Server 2016 Express LocalDB | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 8e9500bdeffd9c7e9e9480f30a87e1678074cc57
ms.sourcegitcommit: 6e016a4ffd28b09456008f40ff88aef3d911c7ba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="sql-server-2016-express-localdb"></a>SQL Server 2016 Express LocalDB
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [SQL Server 2014 Express LocalDB](https://msdn.microsoft.com/en-US/library/hh510202(SQL.120).aspx).

Microsoft SQL Server 2016 Express **LocalDB** ist ein Feature von [SQL Server Express](https://msdn.microsoft.com/library/ms144275(SQL.130).aspx) , das speziell für Entwickler konzipiert wurde. Es ist in SQL Server 2016 Express mit Advanced Services verfügbar.  

 **Die LocalDB** -Installation kopiert einen minimalen Satz von Dateien, der für den Start von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]erforderlich ist. Sobald LocalDB installiert ist, können Sie mithilfe einer speziellen Verbindungszeichenfolge eine Verbindung herstellen. Wenn eine Verbindung hergestellt wird, wird die erforderliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Infrastruktur automatisch erstellt und gestartet. Sie ermöglicht der Anwendung, die Datenbank zu verwenden, und zwar ohne komplexe Konfigurationstasks. Mit Developer Tools können Entwickler [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] bereitstellen, womit sie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code schreiben und testen können, und zwar ohne dabei eine vollständige Serverinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwalten zu müssen. 
 
 
 ## <a name="try-it-out"></a>Probieren Sie es aus. 
  
-   Um SQL Server 2016 Express herunterzuladen und zu installieren, navigieren Sie zu der Seite **[SQL Server Downloads](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)**. LocalDB ist eine Funktion, die Sie während der Installation auswählen. Sie ist verfügbar, wenn Sie die Medien herunterladen. Wenn Sie die Medien herunterladen, wählen Sie **Express Advanced** oder das **LocalDB** Paket aus. 
  
-   Sie haben ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** , um einen virtuellen Computer zu starten, auf dem [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bereits installiert ist.  
  
## <a name="install-localdb"></a>Installieren von LocalDB  
 Installieren Sie **LocalDB** über den Installations-Assistenten oder mithilfe des SqlLocalDB.msi-Programms. **LocalDB** ist eine Option bei der Installation von [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]. 
 
Wählen Sie während der Installation **LocalDB** auf der Seite **Funktionsauswahl/Freigegebene Funktionen** aus. Es darf nur eine Installation der **LocalDB** -Binärdateien für eine [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Hauptversion vorhanden sein. Mehrere [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Prozesse können gestartet werden und verwenden dann die gleichen Binärdateien. Für eine Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], die als **LocalDB** gestartet wurde, gelten die gleichen Einschränkungen wie für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  

 Eine Instanz von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** wird mit dem Hilfsprogramm **SqlLocalDB.exe** verwaltet. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** sollte anstelle des veralteten [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] -Benutzerinstanzfeatures verwendet werden. 
  
## <a name="description"></a>Description  
 Das **LocalDB** -Setupprogramm installiert mithilfe des SqlLocalDB.msi-Programms die notwendigen Dateien auf dem Computer. Nach der Installation ist **LocalDB** eine Instanz von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken erstellt und geöffnet werden können. Die Systemdatenbankdateien für die Datenbank werden im lokalen AppData-Pfad des Benutzers gespeichert. Dieser Pfad ist normalerweise verborgen. Beispiel: **C:\Users\\<Benutzer\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**. Benutzerdatenbankdateien werden an dem vom Benutzer angegebenen Speicherort gespeichert, in der Regel im Ordner **C:\Users\\<Benutzer\>\Documents\\**.  
  
 Weitere Informationen zum Einbeziehen von **LocalDB** in eine Anwendung finden Sie in der [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]-Dokumentation [Übersicht über lokale Daten](http://msdn.microsoft.com/library/ms233817\(VS.110\).aspx) unter [Exemplarische Vorgehensweise: Erstellen einer SQL Server-LocalDB-Datenbank](http://msdn.microsoft.com/library/ms233763\(VS.110\).aspx) und unter [Exemplarische Vorgehensweise: Herstellen einer Verbindung zu Daten in einer SQL Server-LocalDB-Datenbank (Windows Forms)](http://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Weitere Informationen zur **LocalDB** -API finden Sie unter [SQL Server Express LocalDB Instanz-API-Referenz](http://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) und [LocalDBStartInstance-Funktion](http://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 Das Hilfsprogramm SqlLocalDb kann neue Instanzen von **LocalDB**erstellen, eine Instanz von **LocalDB**starten und beenden und enthält Optionen zur Verwaltung von **LocalDB**.  Weitere Informationen zum Hilfsprogramm von SqlLocalDb finden Sie unter [SqlLocalDB-Hilfsprogramm](../../tools/sqllocaldb-utility.md).  
  
 Die Instanzsortierung für **LocalDB** wird auf SQL_Latin1_General_CP1_CI_AS festgelegt und kann nicht geändert werden. Auf Datenbankebene, Spaltenebene und Ausdrucksebene werden Sortierungen normal unterstützt. Eigenständige Datenbanken basieren auf den Metadaten- und tempdb-Sortierungsregeln unter [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restrictions  
 **LocalDB** kann nicht als Abonnent für die Mergereplikation hinzugefügt werden.  
  
 FILESTREAM wird von**LocalDB** nicht unterstützt.  
  
 **LocalDB** lässt nur lokale Warteschlangen für Service Broker zu.  
  
 Eine Instanz von **LocalDB** , die den integrierten Konten gehört, wie z.B. NT AUTHORITY\SYSTEM, kann aufgrund der Windows-Dateisystemumleitung Verwaltbarkeitsprobleme aufweisen. Verwenden Sie stattdessen ein normales Windows-Benutzerkonto als Besitzer.  
  
### <a name="automatic-and-named-instances"></a>Automatisch und benannte Instanzen  
 **LocalDB** unterstützt zwei Arten von Instanzen: Automatische Instanzen und benannte Instanzen.  
  
-   Automatische Instanzen von **LocalDB** sind öffentlich. Sie werden erstellt und automatisch für den Benutzer verwaltet. Sie können von allen Anwendungen verwendet werden. Eine automatische Instanz von **LocalDB** ist für jede Version von **LocalDB** vorhanden, die auf dem Computer des Benutzers installiert ist. Automatische Instanzen von **LocalDB** stellen die nahtlose Instanzverwaltung bereit. Es ist nicht nötig, eine Instanz zu stellen, da es auch so funktioniert. Dies ermöglicht einfache Anwendungsinstallationen und eine Migration zu einem anderen Computer. Wenn auf dem Zielcomputer die angegebene Version von **LocalDB** installiert ist, ist die automatische Instanz von **LocalDB** für diese Version auch auf dem Zielcomputer verfügbar. Automatische Instanzen von **LocalDB** haben ein besonderes Muster für den Instanznamen, der zu einem reservierten Namespace gehört. Dies verhindert Namenskonflikte mit benannten **LocalDB**-Instanzen. Der Name der automatischen Instanz ist **MSSQLLocalDB**.  
  
-   Benannte Instanzen von **LocalDB** sind privat. Diese gehören einer Einzelanwendung, die für das Erstellen und Verwalten der Instanz zuständig ist. Benannte Instanzen sind zum Teil von anderen Instanzen isoliert und können durch die Reduzierung von Ressourcenkonflikten, die mit anderen Datenbankbenutzern auftreten können, die Leistung verbessern. Der Benutzer muss benannte Instanzen explizit über die **LocalDB** -Verwaltungs-API oder implizit für eine verwaltete Anwendung (auch wenn die verwaltete Anwendung auch bei Bedarf die API verwenden kann) über die Datei „app.config“ erstellen. Jede benannte Instanz von **LocalDB** verfügt über eine zugeordnete Version von **LocalDB** , die auf einen angegebenen Satz **LocalDB** -Binärdateien verweist. Ein Instanzname von **LocalDB** ist ein **sysname** -Datentyp und kann bis zu 128 Zeichen aufweisen. (Dies unterscheidet sich von regulären benannten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die Namen auf reguläre NetBIOS-Namen von 16 ASCII-Zeichen beschränken.) Der Name einer Instanz von **LocalDB** kann alle Unicode-Zeichen enthalten, die für den Dateinamen gültig sind.  Eine benannte Instanz, die einen automatischen Instanznamen verwendet, wird eine automatische Instanz.  
  
 Unterschiedliche Benutzer eines Computers können über Instanzen mit dem gleichen Namen verfügen. Jede Instanz ist ein anderer Prozess, der als ein anderer Benutzer ausgeführt wird.  
  
## <a name="shared-instances-of-localdb"></a>Freigegebene Instanzen von LocalDB  
 Von **LocalDB**wird das Freigeben von Instanzen unterstützt, um Szenarien zu unterstützen, in denen mehrere Benutzer eines Computer sich mit einer einzelnen Instanz von **LocalDB** verbinden müssen. Ein Instanzbesitzer kann auswählen, anderen Benutzern auf dem Computer zu ermöglichen, eine Verbindung mit seiner Instanz herzustellen. Sowohl die automatische als auch die benannten Instanzen von **LocalDB** können freigegeben werden. Zum Freigeben einer Instanz von **LocalDB** müssen Benutzer einen freigegebenen Namen (Alias) dafür auswählen. Da der freigegebene Name für Benutzer des Computers sichtbar ist, muss dieser freigegebene Name auf dem Computer eindeutig sein. Der freigegebene Name für eine Instanz von **LocalDB** verfügt über das gleiche Format wie die benannte Instanz von **LocalDB**.  
  
 Nur ein Administrator auf dem Computer kann eine freigegebene Instanz von **LocalDB**erstellen. Die Freigabe einer freigegebenen Instanz von **LocalDB** kann von einem Administrator oder dem Besitzer der freigegebenen Instanz von **LocalDB**entfernt werden Verwenden Sie zum Freigeben oder zum Entfernen der Freigabe einer Instanz von **LocalDB**die `LocalDBShareInstance` und `LocalDBUnShareInstance` -Methoden der **LocalDB** -API oder die Optionen zum Freigeben oder zum Entfernen einer Freigabe des SqlLocalDb-Hilfsprogramms.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Starten von LocalDB und Herstellen einer Verbindung zu LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Herstellen einer Verbindung zur automatischen Instanz  
 Die einfachste Möglichkeit zur Verwendung von **LocalDB** besteht darin, mit der Verbindungszeichenfolge **"Server=(localdb)\MSSQLLocalDB;Integrated Security=true"**eine Verbindung mit der automatischen Instanz herzustellen, deren Besitzer der aktuelle Benutzer ist. Verwenden Sie eine Verbindungszeichenfolge ähnlich **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**, um eine Verbindung mit einer bestimmten Datenbank mit dem Dateinamen herzustellen.  
  
> [!NOTE]  
>  Wenn ein Benutzer zum ersten Mal auf einem Computer versucht, eine Verbindung mit **LocalDB**herzustellen, muss die automatische Instanz sowohl erstellt als auch gestartet werden. Die zusätzliche Zeit, die für das Erstellen der Instanz benötigt wird, kann dazu führen, dass der Verbindungsversuch abgebrochen und eine Timeoutmeldung ausgegeben wird. Warten Sie in diesem Fall einige Sekunden, bis der Erstellungsvorgang vollständig abgeschlossen ist, und stellen Sie dann erneut eine Verbindung her.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Erstellen einer benannten Instanz und Herstellen einer Verbindung  
 Zusätzlich zur automatischen Instanz unterstützt **LocalDB** auch benannte Instanzen. Mit dem Programm SqlLocalDB.exe können Sie eine benannte Instanz von **LocalDB**erstellen, starten und beenden. Weitere Informationen zu SqlLocalDB.exe finden Sie unter [SqlLocalDB-Hilfsprogramm](../../tools/sqllocaldb-utility.md).  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 Die letzte Zeile oben gibt Informationen ähnlich der folgenden zurück.  
  
|||  
|-|-|  
|Name|"LocalDBApp1"|  
|Versionsoptionen|\<aktuelle Version>|  
|Freigegebener Name|""|  
|Besitzer|„\<Ihr Windows-Benutzerkonto>“|  
|Automatisch erstellen|nein|  
|Status|Ausführen|  
|Letzte Startzeit|\<Datum und Uhrzeit>|  
|Instanz-Pipename|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Wenn Ihre Anwendung eine Version vor .NET 4.0.2 verwendet, müssen Sie eine direkte Verbindung mit der Named Pipe von **LocalDB**herstellen. Der Wert für Instanz-Pipename ist die Named Pipe, welche die Instanz von **LocalDB** überwacht. Der Teil des Instanzpipenamens nach LOCALDB # ändert sich jedes Mal, wenn die Instanz von **LocalDB** gestartet wird. Sie stellen eine Verbindung zur Instanz von **LocalDB** mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] her, indem Sie den Namen der Instanzpipe im Feld **Servername** des Dialogfeldes **Verbindung herstellen mit [!INCLUDE[ssDE](../../includes/ssde-md.md)]** eingeben. Von Ihrem benutzerdefinierten Programm aus können Sie mit einer Verbindungszeichenfolge ähnlich **Die LocalDB** eine Verbindung mit der Instanz von LocalDB `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Herstellen einer Verbindung mit einer freigegebenen Instanz von LocalDB  
 Fügen Sie zum Herstellen einer Verbindung mit einer freigegebenen Instanz von **LocalDB** der Verbindungszeichenfolge **erforderlich ist.\\** (Punkt + umgekehrter Schrägstrich) hinzu, um einen Verweis auf den für die freigegebenen Instanzen reservierten Namespace zu erstellen. Verwenden Sie beispielsweise eine Verbindungszeichenfolge wie als Teil der Verbindungszeichenfolge, um eine Verbindung mit einer freigegeben Instanz von **LocalDB** `AppData` namens `(localdb)\.\AppData` herzustellen. Benutzer, die eine Verbindung mit einer freigegebenen Instanz von **LocalDB** herstellen, die sie nicht besitzen, müssen über eine Windows-Authentifizierung oder über einen Anmeldenamen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verfügen.  
  
## <a name="troubleshooting"></a>Problembehandlung  
 Informationen zur Problembehandlung für **LocalDB**finden Sie unter [Problembehandlung SQL Server 2012 Express LocalDB](http://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Berechtigungen  
 Eine Instanz von [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]**LocalDB** ist eine von einem Benutzer zur eigenen Verwendung erstellte Instanz. Jeder Benutzer auf dem Computer kann eine Datenbank mithilfe einer **LocalDB**-Instanz erstellen, Dateien unter seinem Benutzerprofil speichern und die gemäß der Anmeldeinformationen erlaubten Prozesse ausführen. Der Zugriff auf die **LocalDB** -Instanz ist standardmäßig auf den Besitzer beschränkt. Die in **LocalDB** enthaltenen Daten sind per Dateisystemzugriff auf die Datenbankdateien geschützt. Wenn die Datenbankdateien eines Benutzers an einem freigegebenen Speicherort gespeichert werden, kann die Datenbank von jedem Benutzer mit Dateisystemzugriff auf diesen Speicherort geöffnet werden, und zwar über die jeweils eigene Instanz von **LocalDB** . Wenn die Datenbankdateien sich an einem geschützten Speicherort befinden, z. B. dem Datenordner des Benutzers, können nur dieser Benutzer und Administratoren mit Zugriffsrechten für diesen Ordner die Datenbank öffnen. Die **LocalDB** -Dateien können jeweils nur von einer **LocalDB** -Instanz geöffnet werden.  
  
> [!NOTE]  
>  **LocalDB** wird immer im Sicherheitskontext des Benutzers ausgeführt, d. h., **LocalDB** wird nie mit den Anmeldeinformationen der Gruppe lokaler Administratoren ausgeführt. Das bedeutet, dass der Zugriff auf alle von einer **LocalDB** -Instanz verwendeten Datenbankdateien über das eigene Windows-Konto des Benutzers möglich sein muss, unabhängig von der Mitgliedschaft in der Gruppe lokaler Administratoren.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SqlLocalDB-Hilfsprogramm](../../tools/sqllocaldb-utility.md)  
  
  
