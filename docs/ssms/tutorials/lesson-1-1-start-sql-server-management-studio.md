---
title: Starten von Microsoft SQL Server Management Studio | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6fad886d9f1748a671ee206d02df1b9398bd73c3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-1-1---start-sql-server-management-studio"></a>Lektion 1-1: Starten von SQL Server Management Studio
Zu Beginn dieses Lernprogramms geht es hauptsächlich um [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="opening-sql-server-management-studio"></a>Öffnen von SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>So öffnen Sie SQL Server Management Studio  
  
1.  Wie Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] (SSMS) starten, hängt von Ihrem Betriebssystem ab.  
  * Geben Sie für neuere Versionen von Windows mit einer **Startseite** auf der **Startseite** **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]** ein, und das Programm wird angezeigt. Klicken Sie auf das Programm, um SSMS zu öffnen. Möglicherweise möchten Sie auch mit der rechten Maustaste auf das Programm klicken, und es anschließend an die **Startseite**anheften.   
  * Zeigen Sie für ältere Versionen von Windows im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], und klicken Sie anschließend auf **SQL Server Management Studio**. Geben Sie alternativ im Dialogfeld **Ausführen** **SSMS.exe** ein, und klicken Sie anschließend auf **OK**.  
  
    > [!NOTE]  
    >  Wenn SSMS nicht angezeigt wird, haben Sie SSMS möglicherweise nicht richtig installiert. Installieren Sie SSMS aus dem [Download-Center](../download-sql-server-management-studio-ssms.md). SSMS wird nicht automatisch mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 installiert. Verwenden Sie die neueste Version, um auf alle Features zuzugreifen.  
  
2.  Im nächsten Schritt stellen Sie mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Objekt-Explorer **-Komponente von SSMS eine Verbindung mit** her. Wenn der Bereich Objekt-Explorer nicht sichtbar ist, klicken Sie im Menü **Ansicht** auf **Objekt-Explorer**. Klicken Sie im Menü des Objekt-Explorers auf die Schaltfläche **Verbinden** und anschließend auf **Datenbankmodul**. Das Dialogfeld **Verbindung mit Server herstellen** sollte angezeigt werden. (Wenn Sie zuvor SSMS installiert haben, erscheint durch die Benutzereinstellungen das Dialogfeld **Verbindung mit dem Server herstellen** möglicherweise automatisch.)  
  
3.  Schließen Sie im Dialogfeld **Verbindung mit Server herstellen** das Feld **Servername** ab. Sie können mit einem von drei Typen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eine Verbindung herstellen. Jeder Typ hat ein geringfügig anderes Format für das Feld **Servername** . Wählen Sie eines der folgenden Formate aus:  
  -  **Eine Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installieren, können Sie angeben, dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Standardinstanz (unbenannte Instanz) oder eine benannte Instanz sein wird. Wenn Sie eine Verbindung mit einer Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen, geben Sie den Namen des Computers ein. Wenn Sie z.B. SSMS auf einem Computer mit dem Namen „Buchhaltung“ ausführen, und Sie stellen eine Verbindung mit einer Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  her, der auf diesem Computer installiert ist, geben Sie **Buchhaltung** in das Feld **Servername** ein.  
  -  **Eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** Während des Setups von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Sie einen Namen für die Instanz angeben. Auf einem Computer mit dem Namen „Buchhaltung“ können Sie eine benannte Instanz mit dem Namen **Forderungen** angeben. Um eine Verbindung mit einer benannten Instanz herzustellen, geben Sie im Feld **Servername** „Computername Umgekehrter Schrägstrich Instanzname“ein, z.B. **Buchhaltung\Forderungen**.  
  -  **Eine Azure SQL-Datenbank:** Das Format des Servernamens für die SQL-Datenbank ist SQL_Server_name.database.windows.net, z.B. **mydb2.database.windows.net**. Wenn Sie Probleme beim Bestimmen des Servernamens haben, besuchen Sie das Azure-Portal, um Hilfe beim Erstellen einer Verbindungszeichenfolge zu erhalten.  
  
4. Wählen Sie im Bereich **Authentifizierung** eine Authentifizierungsmethode aus.  
  - Wenn Sie der Administrator des Computers sind und soeben SQL Server installiert haben, testen Sie die **Windows-Authentifizierung**.  Dies funktioniert auch, wenn Sie als Domänenbenutzer konfiguriert sind, der Zugriff auf den SQL-Server hat. Da bei dem Anmeldeversuch die Anmeldeinformationen verwendet werden, mit denen Sie sich bei Windows anmelden, sind die Felder **Benutzername** und **Kennwort** abgeblendet. 
  -  Wenn Sie den Namen und das Kennwort eines Benutzerkontos kennen, wählen Sie **SQL Server-Authentifizierung** aus, und stellen Sie dann den **Benutzernamen** und das **Kennwort** bereit.
  - Wenn Sie die neueste Version von SSMS haben, stehen Ihnen drei weitere Optionen zur Verfügung, beginnend mit der **Active Directory-Authentifizierung**. Informationen zu diesen erweiterten Optionen finden Sie unter [Universelle Authentifizierung bei SQL-Datenbank und SQL Data Warehouse (SSMS-Unterstützung für MFA)](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-ssms-mfa-authentication).  
  
## <a name="management-studio-components"></a>Management Studio-Komponenten  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] stellt seine Informationen in Fenstern bereit, die für die jeweils spezielle Art von Informationen vorgesehen sind. Datenbankinformationen werden im Fenster Objekt-Explorer sowie im Fenster für Dokumente angezeigt.  
  
-   Der Objekt-Explorer enthält eine Strukturansicht aller Datenbankobjekte eines Servers. Diese kann die Datenbanken von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]und [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]umfassen. Der Objekt-Explorer umfasst Informationen zu allen Servern, mit denen eine Verbindung besteht. Wenn Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]öffnen, werden Sie aufgefordert, den Objekt-Explorer mit den zuletzt verwendeten Einstellungen zu verbinden. Zum Herstellen einer Verbindung können Sie auf jeden beliebigen Server in der Komponente Registrierte Server doppelklicken. Sie brauchen keinen Server zu registrieren, um eine Verbindung herzustellen.  
  
-   Das Dokumentfenster ist der größte Bestandteil von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Es kann Abfrage-Editoren und Browserfenster umfassen. Standardmäßig wird die Seite Zusammenfassung angezeigt, die mit der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf dem aktuellen Computer verbunden ist.  
  
## <a name="showing-additional-windows"></a>Anzeigen zusätzlicher Fenster  
  
#### <a name="to-show-the-registered-servers-window"></a>So zeigen Sie das Fenster "Registrierte Server" an  
  
1.  Klicken Sie im Menü **Ansicht** auf **Registrierte Server**.  
  
    Das Fenster „Registrierte Server“ wird über oder neben dem Objekt-Explorer angezeigt. Sie können es verschieben und an verschiedenen Orte andocken. In der Liste „Registrierte Server“ werden die Server aufgelistet, die Sie häufig verwalten. In dieser Liste können Sie Server hinzufügen und entfernen. Als einzige Server werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen auf dem Computer aufgelistet, auf dem [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ausgeführt wird.  
  
2.  Wird Ihr Server nicht angezeigt, klicken Sie in der Liste der registrierten Server mit der rechten Maustaste auf **Datenbankmodul**, dann auf **Tasks**und anschließend auf **Lokale Serverregistrierung aktualisieren**. Um zusätzliche SQL-Server auf einer SQL-Datenbank hinzuzufügen, klicken Sie mit der rechten Maustaste auf einen Speicherort unter Registrierte Server, und klicken Sie anschließend auf **Neue Serverregistrierung**. Tragen Sie im Bereich **Anmeldename** die Informationen ein, die Sie auch im Dialogfeld **Verbindung mit Server herstellen** eingetragen haben.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Herstellen einer Verbindung mit registrierten Servern und dem Objekt-Explorer](../../tools/sql-server-management-studio/lesson-1-2-connect-with-registered-servers-and-object-explorer.md)  

  
