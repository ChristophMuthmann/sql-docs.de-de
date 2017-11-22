---
title: 'Lektion 1: Herstellen einer Verbindung mit dem Datenbankmodul | Microsoft-Dokumentation'
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d029887fd0610748381a4c1512ae74c451769aab
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>Lektion 1: Herstellen einer Verbindung mit dem Datenbankmodul
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [Lektion 1: Herstellen einer Verbindung mit dem Datenbankmodul](https://msdn.microsoft.com/en-US/library/ms345332(SQL.120).aspx).

<a name="when-you-install-the-includessdenoversionincludesssdenoversion-mdmd-the-tools-that-are-installed-depend-upon-the-edition-and-your-setup-choices-this-lesson-reviews-the-principal-tools-and-shows-you-how-to-connect-and-perform-a-basic-function-authorizing-more-users"></a>Welche Tools beim Installieren von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]installiert werden, hängt von der Edition und den von Ihnen ausgewählten Installationsoptionen ab. In dieser Lektion werden die Haupttools vorgestellt, und Sie erfahren, wie Sie Verbindungen herstellen und eine einfache Funktion (Autorisieren zusätzlicher Benutzer) ausführen.  
 -  
 <a name="-this-lesson-contains-the-following-tasks"></a>– Diese Lektion beinhaltet die folgenden Aufgaben:  
 -  
 <a name="-----tools-for-getting-startedtools"></a>-- [Tools für die ersten Schritte](#tools)  
 -  
 <a name="-----connecting-with-management-studioconnect"></a>-- [Herstellen einer Verbindung mit Management Studio](#connect)  
 -  
 <a name="-----authorizing-additional-connectionsadditional"></a>-- [Autorisieren zusätzlicher Verbindungen](#additional)  
 -  
 -## <a name="tools"></a>Tools für die ersten Schritte  
 – Im Lieferumfang von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] sind eine Vielzahl von Tools enthalten. In diesem Thema wird beschrieben, welche Tools Sie zuerst benötigen und wie das richtige Tool für den Auftrag ausgewählt wird. Auf alle Tools kann über das Menü **Start** zugegriffen werden. Einige Tools wie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]werden nicht standardmäßig installiert. Die Tools müssen als Teil der Clientkomponenten während der Ausführung des Setupprogramms installiert werden. Eine vollständige Beschreibung der unten aufgeführten Tools finden Sie, indem Sie in der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Onlinedokumentation danach suchen. [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] enthält nur eine Teilmenge der Tools.  
 -  
 – ### Haupttools  
 -  
 --   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) ist das Haupttool zum Verwalten der [!INCLUDE[ssDE](../includes/ssde-md.md)] und Schreiben von [!INCLUDE[tsql](../includes/tsql-md.md)]-Code. Es wird in der [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] -Shell gehostet. SSMS steht im [Microsoft Download Center](https://msdn.microsoft.com/library/mt238290.aspx)zum Herunterladen zur Verfügung. Die neueste Version kann mit älteren Versionen des [!INCLUDE[ssDE_md](../includes/ssde-md.md)]verwendet werden.  
 -  
 --   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager wird sowohl mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] als auch mit den Clienttools installiert. Sie können damit Serverprotokolle aktivieren, Protokolloptionen wie z. B. TCP-Ports konfigurieren, Serverdienste so konfigurieren, dass sie automatisch gestartet werden, und Clientcomputer so konfigurieren, dass sie mit dem von Ihnen bevorzugten Verfahren gestartet werden. Mit diesem Tool können erweiterte Konnektivitätselemente konfiguriert, aber keine Funktionen aktiviert werden.  
 -  
 – ### Beispieldatenbank  
 – Die Beispieldatenbanken und Beispiele sind nicht standardmäßig in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] enthalten. Die meisten Beispiele, die in der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Onlinedokumentation beschrieben werden, basieren auf der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Beispieldatenbank.  
 -  
 – ##### So starten Sie SQL Server Management Studio  
 -  
 – Geben Sie in aktuellen Versionen von Windows auf der **Startseite** SSMS ein, und klicken Sie anschließend auf **Microsoft SQL Server Management Studio**.  
 – Wenn Sie eine ältere Version von Windows verwenden, zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], und klicken Sie anschließend auf **SQL Server Management Studio**.  
 -  
 – ##### So starten Sie den SQL Server-Konfigurations-Manager  
 -  
 – Geben Sie in aktuellen Versionen von Windows auf der **Startseite** **Configuration Manager** ein, und klicken Sie anschließend auf **SQL Server *Version* Configuration Manager**.   
 – Wenn Sie eine ältere Version von Windows verwenden, zeigen Sie im **Startmenü** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie anschließend auf **SQL Server-Konfigurations-Manager**.  
 -  
 -## <a name="connect"></a>Herstellen einer Verbindung mit Management Studio  
 – Es ist sehr einfach, mithilfe von Tools, die auf demselben Computer ausgeführt werden, eine Verbindung mit [!INCLUDE[ssDE](../includes/ssde-md.md)] herzustellen, wenn Sie den Namen der Instanz kennen und wenn Sie die Verbindung als Mitglied der lokalen Administratorengruppe auf dem Computer herstellen. Die folgenden Vorgänge müssen auf dem Computer ausgeführt werden, der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]hostet.  
 -  
 -> [!NOTE]  
 -> In diesem Thema wird das Herstellen einer Verbindung mit einem lokalen SQL Server beschrieben. Informationen zum Herstellen einer Verbindung mit der Azure SQL-Datenbank finden Sie unter [Herstellen einer Verbindung mit einer SQL-Datenbank mit SQL Server Management Studio und Ausführen einer T-SQL-Beispielabfrage](https://azure.microsoft.com/documentation/articles/sql-database-connect-query-ssms/).  
 -  
 – ##### So bestimmen Sie den Namen der Instanz des Datenbankmoduls  
 -  
 – 1.  Melden Sie sich bei Windows als Mitglied der Administratorgruppe an, und öffnen Sie [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
 -  
 – 2.  Klicken Sie im Dialogfeld **Verbindung mit Server herstellen** auf **Abbrechen**.  
 -  
 – 3.  Wenn Registrierte Server nicht angezeigt wird, klicken Sie im Menü **Ansicht** auf **Registrierte Server**.  
 -  
 – 4.  Wählen Sie in der Symbolleiste „Registrierte Server“ die Option **Datenbankmodul** aus, erweitern Sie **Datenbankmodul**, klicken Sie mit der rechten Maustaste auf **Lokale Servergruppen**, zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Lokale Server registrieren**. Es werden alle auf dem Computer installierten Instanzen von [!INCLUDE[ssDE](../includes/ssde-md.md)] angezeigt. Die Standardinstanz hat keinen Namen und wird mit dem Computernamen angezeigt. Eine benannte Instanz wird als der Computername, gefolgt von einem umgekehrten Schrägstrich (\\) und dem Namen der Instanz, angezeigt. Für [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] hat die Instanz den Namen *<Computername>*\sqlexpress, es sei denn, der Name wurde während des Setups geändert.  
 -  
 – ##### So überprüfen Sie, ob das Datenbankmodul ausgeführt wird  
 -  
 – 1.  Wenn in Registrierte Server neben dem Namen Ihrer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ein grüner Punkt mit einem weißen Pfeil angezeigt wird, bedeutet dies, dass [!INCLUDE[ssDE](../includes/ssde-md.md)] ausgeführt wird und keine weiteren Aktionen erforderlich sind.  
 -  
 – 2.  Wenn neben dem Name Ihrer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ein roter Punkt mit einem weißen Quadrat angezeigt wird, wurde [!INCLUDE[ssDE](../includes/ssde-md.md)] beendet. Klicken Sie mit der rechten Maustaste auf den [!INCLUDE[ssDE](../includes/ssde-md.md)]-Namen, und klicken Sie auf **Dienstkontrolle**und anschließend auf **Starten**. Nachdem ein Bestätigungsdialogfeld angezeigt wurde, sollte das [!INCLUDE[ssDE](../includes/ssde-md.md)] gestartet werden und ein grüner Kreis mit einem weißen Pfeil angezeigt werden.  
 -  
 – ##### So stellen Sie eine Verbindung mit dem Datenbankmodul her  
 -
 – Mindestens ein Administratorkonto wurde ausgewählt, als [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] installiert wurde. Führen Sie den folgenden Schritt aus, während Sie bei Windows als Administrator angemeldet sind.
 -  
 – 1.  Klicken Sie in [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]im Menü **Datei** auf **Objekt-Explorer verbinden**.  
 -  
 -    Das Dialogfeld **Verbindung mit Server herstellen** wird geöffnet. Im Feld **Servertyp** wird der zuletzt verwendete Typ der Komponente angezeigt.  
 -  
 – 2.  Wählen Sie **Datenbankmodul**aus.  
 -
 -    ![Objekt-Explorer](../relational-databases/media/object-explorer.png)
 -  
 – 3.  Geben Sie im Feld **Servername** den Namen der Instanz von [!INCLUDE[ssDE](../includes/ssde-md.md)]ein. Bei der Standardinstanz von SQL Server ist der Servername der Name des Computers. Bei einer benannten Instanz von SQL Server ist der Servername *<computer_name>***\\***<instance_name>,*, wie z.B. **ACCTG_SRVR\SQLEXPRESS**. Der folgende Screenshot zeigt das Herstellen einer Verbindung mit der (unbenannten) Standardinstanz von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] auf einem Computer namens „PracticeComputer“. Der Benutzer, der bei Windows angemeldet ist, ist Mary aus der Domain „Contoso“. Bei Verwendung der Windows-Authentifizierung können Sie den Benutzernamen nicht ändern. 
 -
 -    ![Verbindung-mit-Server-herstellen](../relational-databases/media/connect-to-server.png)
 -  
 – 4.  Klicken Sie auf **Verbinden**.  
 -
 -> [!NOTE]
 -> In diesem Tutorial wird davon ausgegangen, dass Sie noch keine Vorkenntnisse zu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] besitzen und keine besonderen Probleme beim Herstellen einer Verbindung haben. Dies sollte für die meisten Benutzer ausreichen, und so wird das Tutorial einfach gehalten. Detaillierte Schritte zur Fehlerbehebung finden Sie unter [Beheben von Verbindungsfehlern mit dem SQL Server-Datenbankmodul](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md). 
 -  
 -## <a name="additional"></a>Autorisieren zusätzlicher Verbindungen  
 – Nachdem Sie eine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] als Administrator hergestellt haben, besteht eine Ihrer ersten Aufgaben darin, Verbindungen für andere Benutzer zu autorisieren. Dazu erstellen Sie eine Anmeldung und erteilen dieser Anmeldung die Berechtigung, als Benutzer auf eine Datenbank zuzugreifen. Eine Anmeldung kann entweder eine Anmeldung mit Windows-Authentifizierung sein, die Windows-Anmeldeinformationen verwendet, oder eine Anmeldung mit SQL Server-Authentifizierung, die die Authentifizierungsinformationen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] speichert und von Ihren Windows-Anmeldeinformationen unabhängig ist. Verwenden Sie nach Möglichkeit immer Windows-Authentifizierung.
 -
 -> [!TIP]
 -> Die meisten Organisationen verfügen über Domänenbenutzer und verwenden die Windows-Authentifizierung. Sie können selbst herumexperimentieren, indem Sie zusätzliche lokale Benutzer auf Ihrem Computer erstellen. Lokale Benutzer werden von Ihrem Computer authentifiziert, also ist die Domäne der Computername. Wenn Ihr Computer beispielsweise `MyComputer` heißt, und Sie einen Benutzer namens `Test`erstellen, dann lautet die Windows-Beschreibung des Benutzers `Mycomputer\Test`.  
 -  
 – ##### So erstellen Sie einen Benutzernamen für die Windows-Authentifizierung  
 -  
 – 1.  In der vorhergehenden Aufgabe haben Sie eine Verbindung mit [!INCLUDE[ssDE](../includes/ssde-md.md)] mithilfe von [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]hergestellt. Erweitern Sie im Objekt-Explorer Ihre Serverinstanz, erweitern Sie **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und klicken Sie anschließend auf **Neue Anmeldung**.  
 -  
 -    Das Dialogfeld **Anmeldung – Neu** wird angezeigt.  
 -  
 – 2.  Geben Sie auf der Seite **Allgemein** im Feld **Anmeldename** eine Windows-Anmeldung in folgendem Format ein: `<domain>\\<login>`
 -  
 -    ![Neue-Anmeldung](../relational-databases/media/new-login.png)
 -  
 – 3.  Wählen Sie (sofern verfügbar) **im Feld** Standarddatenbank [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] aus. Wählen Sie andernfalls **master**aus.  
 -  
 – 4.  Wenn die neue Anmeldung ein Administrator sein soll, klicken Sie auf der Seite **Serverrollen** auf **sysadmin**, andernfalls lassen Sie sie leer.  
 -  
 – 5.  Wählen Sie auf der Seite **Benutzerzuordnung** die Option **Zuordnen** für die [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank aus, sofern diese verfügbar ist. Wählen Sie andernfalls **master**aus. Beachten Sie, dass das Feld **Benutzer** mit der Anmeldung aufgefüllt wird. Wenn das Dialogfeld geschlossen wird, erstellt es diesen Benutzer in der Datenbank.  
 -  
 – 6.  Geben Sie im Feld **Standardschema** den Schemanamen **dbo** ein, um die Anmeldung dem Schema für Datenbankbesitzer zuzuordnen.  
 -  
 – 7.  Akzeptieren Sie die Standardeinstellungen für die Felder **Sicherungsfähige Elemente** und **Status** , und klicken Sie auf **OK** , um die Anmeldung zu erstellen.  
 -  
 -> [!IMPORTANT]  
 -> Diese grundlegenden Informationen sollen Ihnen den Einstieg erleichtern. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] stellt eine umfassende Sicherheitsumgebung bereit, da das Thema Sicherheit offensichtlich einen wichtigen Aspekt des Datenbankbetriebs darstellt.  
 -  
 – ## Nächste Lektion  
 -[Lektion 2: Herstellen einer Verbindung von einem anderen Computer](../relational-databases/lesson-2-connecting-from-another-computer.md)    
  
  

