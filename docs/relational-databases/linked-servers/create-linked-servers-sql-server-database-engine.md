---
title: Erstellen von Verbindungsservern (SQL Server-Datenbankmodul) | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/20/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linked-servers
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.linkedserver.properties.general.f1
- sql13.swb.linkedserver.properties.security.f1
- sql13.swb.linkedserver.properties.provider.f1
- sql13.swb.linkedserver.properties.options.f1
helpviewer_keywords: linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7b6d7a92e154f6e517fe3299a952a78a05aa4b7d
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="create-linked-servers-sql-server-database-engine"></a>Erstellen von Verbindungsservern (SQL Server-Datenbankmodul)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [Erstellen von Verbindungsservern (SQL Server-Datenbankmodul)](https://msdn.microsoft.com/en-US/library/ff772782(SQL.120).aspx).

  In diesem Thema wird die Erstellung eines Verbindungsservers und das Zugreifen auf Daten von einem anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]erläutert. Durch Erstellen eines Verbindungsservers können Sie mit Daten aus mehreren Quellen arbeiten. Der Verbindungsserver muss keine weitere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sein, allerdings ist dies ein gängiges Szenario.  
  
##  <a name="Background"></a> Hintergrund  
 Ein Verbindungsserver ermöglicht den Zugriff auf verteilte, heterogene Abfragen für OLE DB-Datenquellen. Nach der Erstellung eines Verbindungsservers können für den Server verteilte Abfragen ausgeführt werden, und Abfragen können Tabellen von mehreren Datenquellen verknüpfen. Wenn der Verbindungsserver als Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]definiert wird, können remote gespeicherte Prozeduren ausgeführt werden.  
  
 Die Funktionen und erforderlichen Argumente des Verbindungsservers können erheblich abweichen. In diesem Thema werden typische Beispiele aufgeführt, allerdings werden nicht alle Optionen beschrieben. Weitere Informationen finden Sie unter [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)erläutert.  
  
##  <a name="Security"></a> Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Wenn Sie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen verwenden, ist die Berechtigung **ALTER ANY LINKED SERVER** auf dem Server oder die Mitgliedschaft in der festen Serverrolle **setupadmin** erforderlich. Wenn Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] verwenden, ist die Berechtigung **CONTROL SERVER** oder die Mitgliedschaft in der festen Serverrolle **sysadmin** erforderlich.  
  
##  <a name="Procedures"></a> So erstellen Sie einen Verbindungsserver  
 Sie können eine der folgenden Anwendungen verwenden:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>So erstellen Sie einen Verbindungsserver für eine andere Instanz von SQL Server anhand von SQL Server Management Studio  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Objekt-Explorer, erweitern Sie **Serverobjekte**, klicken Sie mit der rechten Maustaste auf **Verbindungsserver**, und klicken Sie auf **Neuer Verbindungsserver**.  
  
2.  Geben Sie auf der Seite **Allgemein** im Feld **Verbindungsserver** den Namen der Instanz von **SQL Server** ein, mit der Sie einen Link herstellen möchten.  
  
     **SQL Server**  
     Identifiziert den Verbindungsserver als eine Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn Sie einen Verbindungsserver von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach dieser Methode definieren, muss der im Feld **Verbindungsserver** angegebene Name der Netzwerkname des Servers sein. Außerdem stammen alle vom Server abgerufenen Tabellen aus der Standarddatenbank, die für den Benutzernamen auf dem Verbindungsserver definiert wurde.  
  
     **Andere Datenquelle**  
     Gibt einen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]abweichenden OLE DB-Servertyp an. Durch Klicken auf diese Option werden die darunter aufgeführten Optionen aktiviert.  
  
     **Anbieter**  
     Wählen Sie eine OLE DB-Datenquelle aus dem Listenfeld aus. Der OLE DB-Anbieter ist mit der angegebenen PROGID in der Registrierung registriert.  
  
     **Produktname**  
     Geben Sie den Produktnamen der OLE DB-Datenquelle ein, die als Verbindungsserver hinzugefügt werden soll.  
  
     **Datenquelle**  
     Geben Sie den Namen der Datenquelle ein, wie er durch den OLE DB-Anbieter interpretiert wird. Wenn Sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]herstellen, geben Sie den Instanznamen an.  
  
     **Anbieterzeichenfolge**  
     Geben Sie die ProgID des OLE DB-Anbieters ein, die der Datenquelle entspricht. Beispiele für gültige Anbieterzeichenfolgen finden Sie unter [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)erläutert.  
  
     **Speicherort**  
     Geben Sie den Speicherort der Datenbank ein, wie er durch den OLE DB-Anbieter interpretiert wird.  
  
     **Katalog**  
     Geben Sie den Namen des Katalogs ein, der beim Herstellen einer Verbindung mit dem OLE DB-Anbieter verwendet werden soll.  
  
     Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Verbindungsserver, und klicken Sie anschließend auf **Verbindung testen**, um die Fähigkeit zur Verbindungsherstellung mit einem Verbindungsserver zu testen.  
  
    > [!NOTE]  
    >  Wenn die Instanz von **SQL Server** die Standardinstanz ist, geben Sie den Namen des Computers ein, auf dem die Instanz von **SQL Server**gehostet wird. Wenn der **SQL Server** eine benannte Instanz ist, geben Sie den Namen des Computers und den der Instanz ein, z.B. **Accounting\SQLExpress**.  
  
3.  Wählen Sie im Bereich **Servertyp** die Option **SQL Server** aus, um anzugeben, dass der Verbindungsserver eine weitere Instanz von **SQL Server**ist.  
  
4.  Geben Sie auf der Seite **Sicherheit** den Sicherheitskontext an, der beim Herstellen einer Verbindung mit dem Verbindungsserver durch den originalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird. In einer Domänenumgebung, in der Benutzer Verbindungen anhand ihrer Domänenanmeldenamen herstellen, ist die Auswahl der Option **Im aktuellen Sicherheitskontext der Anmeldung verwendet** oft die beste Wahl. Stellen die Benutzer die Verbindung mit dem originalen **SQL Server** anhand eines **SQL Server** -Anmeldenamens her, empfiehlt sich häufig die Auswahl von **In folgendem Sicherheitskontext verwendet**, um anschließend die nötigen Anmeldeinformationen zur Authentifizierung am Verbindungsserver bereitzustellen.  
  
     **Lokale Anmeldung**  
     Gibt die lokale Anmeldung an, mit der eine Verbindung zum Verbindungsserver hergestellt werden kann. Die lokale Anmeldung kann eine Anmeldung sein, die entweder die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung oder eine Windows-authentifizierte Anmeldung verwendet. Verwenden Sie diese Liste, um die Verbindung mit spezifischen Anmeldungen zu beschränken oder einigen Anmeldungen das Herstellen einer Verbindung unter einer anderen Anmeldung zu ermöglichen.  
  
     **Impersonate**  
     Übergibt den Benutzernamen und das Kennwort von der lokalen Anmeldung an den Verbindungsserver. Bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung muss eine Anmeldung mit dem genau gleichen Namen und Kennwort auf dem Remoteserver vorhanden sein. Bei Windows-Anmeldungen muss die Anmeldung eine gültige Anmeldung auf dem Verbindungsserver sein.  
  
     Um Identitätswechsel verwenden zu können, muss die Konfiguration die Anforderungen für die Delegierung erfüllen.  
  
     **Remotebenutzer**  
     Verwendet den Remotebenutzer für die Zuordnung von Benutzern, die nicht in **Lokale Anmeldung**definiert sind. Der **Remotebenutzer** muss ein Anmeldename mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung auf dem Remoteserver sein.  
  
     **Remotekennwort**  
     Gibt das Kennwort des Remotebenutzers an.  
  
     **Hinzufügen**  
     Fügt eine neue lokale Anmeldung hinzu.  
  
     **Entfernen**  
     Entfernt eine vorhandene lokale Anmeldung.  
  
     **Nicht durchgeführt**  
     Gibt an, dass für nicht in der Liste definierte Anmeldungen keine Verbindung hergestellt wird.  
  
     **Nicht in einem Sicherheitskontext verwendet**  
     Gibt an, dass für nicht in der Liste definierte Anmeldungen eine Verbindung ohne Verwendung eines Sicherheitskontexts hergestellt wird.  
  
     **Im aktuellen Sicherheitskontext der Anmeldung verwendet**  
     Gibt an, dass für nicht in der Liste definierte Anmeldungen eine Verbindung mithilfe des aktuellen Sicherheitskontexts der Anmeldung hergestellt wird. Wenn die Verbindung mit dem lokalen Server mithilfe der Windows-Authentifizierung hergestellt wurde, werden zum Herstellen der Verbindung mit dem Remoteserver Ihre Windows-Anmeldeinformationen verwendet. Wenn die Verbindung mit dem lokalen Server mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung hergestellt wurde, werden zum Herstellen der Verbindung mit dem Remoteserver Anmeldename und Kennwort verwendet. In diesem Fall muss eine Anmeldung mit dem genau gleichen Namen und Kennwort auf dem Remoteserver vorhanden sein.  
  
     **In folgendem Sicherheitskontext verwendet**  
     Gibt an, dass eine Verbindung mithilfe der Anmeldung und des Kennworts hergestellt wird, die in den Feldern **Remoteanmeldung** und **Mit Kennwort** für nicht in der Liste definierte Anmeldungen angegeben sind. Die Remoteanmeldung muss eine Anmeldung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung auf dem Remoteserver sein.  
  
5.  Klicken Sie optional auf die Seite **Serveroptionen**  , um Serveroptionen anzuzeigen oder zu bestimmen.  
  
     **Kompatibel mit Sortierung**  
     Betrifft die Ausführung verteilter Abfragen für Verbindungsserver. Wenn diese Option auf "true" festgelegt ist, wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorausgesetzt, dass alle Zeichen auf dem Verbindungsserver bezüglich Zeichensatz und Sortierreihenfolge mit dem lokalen Server kompatibel sind. Dies ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Vergleiche für Zeichenspalten an den Provider zu senden. Wird diese Option nicht festgelegt, werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Vergleiche für Zeichenspalten immer lokal ausgewertet.  
  
     Diese Option sollte nur festgelegt werden, wenn sicher ist, dass die Datenquelle, die dem Verbindungsserver entspricht, den gleichen Zeichensatz und die gleiche Sortierreihenfolge wie der lokale Server verwendet.  
  
     **Datenzugriff**  
     Aktiviert und deaktiviert den Zugriff auf verteilte Abfragen für Verbindungsserver.  
  
     **RPC**  
     Aktiviert RPC (Remote Procedure Call, Remoteprozeduraufruf) von dem angegebenen Server.  
  
     **RPC Out**  
     Aktiviert RPC zu dem angegebenen Server.  
  
     **Remotesortierung verwenden**  
     Bestimmt, ob die Sortierung einer Remotespalte oder eines lokalen Servers verwendet wird.  
  
     Wenn True angegeben ist, wird für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquellen die Sortierung der Remotespalten und für Datenquellen, die keine[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquellen sind, die im Sortierungsnamen angegebene Sortierung verwendet.  
  
     Wenn False angegeben ist, verwenden verteilte Abfragen immer die Standardsortierung des lokalen Servers, während der Sortierungsname und die Sortierung von Remotespalten ignoriert werden. Der Standardwert ist false.  
  
     **Sortierungsname**  
     Gibt den Namen der von der Remotedatenquelle verwendeten Sortierung an, wenn für die Option zum Verwenden der Remotesortierung der Wert True festgelegt ist und es sich bei der Datenquelle nicht um eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle handelt. Der Name muss eine von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützte Sortierung sein.  
  
     Verwenden Sie diese Option, wenn auf eine OLE DB-Datenquelle zugegriffen wird, die keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenquelle ist, deren Sortierung jedoch mit einer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sortierungen übereinstimmt.  
  
     Der Verbindungsserver muss eine einzige Sortierung unterstützen, die für alle Spalten in diesem Server verwendet wird. Legen Sie diese Option nicht fest, wenn der Verbindungsserver mehrere Sortierungen in einer einzelnen Datenquelle unterstützt oder wenn festgestellt wird, dass die Sortierung des Verbindungsservers nicht mit einer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sortierungen übereinstimmt.  
  
     **Verbindungstimeout**  
     Timeoutwert in Sekunden für das Herstellen einer Verbindung mit einem Verbindungsserver.  
  
     Wenn der Wert 0 beträgt, verwenden Sie den Standardwert von **sp_configure** für die Option [remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) .  
  
     **Abfragetimeout**  
     Timeoutwert in Sekunden für Abfragen auf einem Verbindungsserver.  
  
     Wenn der Wert 0 beträgt, verwenden Sie den Standardwert von **sp_configure** für die Option [Timeout für Remoteabfragen](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) .  
  
     **Höherstufung von verteilten Transaktionen aktivieren**  
     Verwenden Sie diese Option, um die Aktionen einer Server-zu-Server-Prozedur durch eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator-Transaktion (MS DTC) zu schützen. Wenn diese Option auf TRUE festgelegt ist und eine remote gespeicherte Prozedur aufgerufen wird, wird eine verteilte Transaktion gestartet und bei MS DTC eingetragen. Weitere Informationen finden Sie unter [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)erläutert.  
  
6.  Klicken Sie auf **OK**.  
  
##### <a name="to-view-the-provider-options"></a>So zeigen Sie die Anbieteroptionen an  
  
-   Um die Optionen anzuzeigen, die der Anbieter zur Verfügung stellt, klicken Sie auf die Seite für die **Anbieteroptionen**.  
  
     Nicht alle Anbieter verfügen über die gleichen Optionen. Bei einigen Typen von Daten sind z. B. Indizes verfügbar, für einige nicht. Mittels dieses Dialogfelds kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Funktionen des Anbieters verstehen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert einige allgemeine Datenanbieter; wenn das Produkt, das die Daten bereitstellt, jedoch geändert wird, unterstützt der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installierte Anbieter möglicherweise nicht alle neuesten Funktionen. Die beste Informationsquelle zu den Funktionen des Produkts, das die Daten bereitstellt, ist die Dokumentation für dieses Produkt.  
  
     **Dynamischer Parameter**  
     Zeigt an, dass der Anbieter die Parametermarkierungssyntax '?' für parametrisierte Abfragen zulässt. Legen Sie diese Option nur dann fest, wenn der Anbieter die **ICommandWithParameters** -Schnittstelle und ein Fragezeichen (?) als Parametermarkierung unterstützt. Durch diese Option kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametrisierte Abfragen für den Anbieter ausführen. Die Fähigkeit zur Ausführung parametrisierter Abfragen für den Anbieter kann bei bestimmten Abfragen zu einer verbesserten Leistung führen.  
  
     **Geschachtelte Abfragen**  
     Zeigt an, dass der Anbieter geschachtelte `SELECT` -Anweisungen in der FROM-Klausel zulässt. Das Festlegen dieser Option ermöglicht es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , bestimmte Abfragen, die das Schachteln von SELECT-Anweisungen in der FROM-Klausel erfordern, an den Anbieter zu delegieren.  
  
     **Nur Ebene Null**  
     Es werden nur OLE DB-Schnittstellen der Ebene 0 mit diesem Anbieter aufgerufen.  
  
     **InProcess zulassen**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht, dass der Anbieter als In-Process-Server instanziiert wird. Wenn diese Option nicht festgelegt ist, wird der Anbieter standardmäßig außerhalb des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozesses instanziiert. Durch Instanziieren des Anbieters außerhalb des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozesses wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess vor Fehlern beim Anbieter geschützt. Wenn der Anbieter außerhalb des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozesses instanziiert wird, sind Updates oder Einfügungen nicht zulässig, die auf lange Spalten verweisen (**text**, **ntext**oder **image**).  
  
     **Nicht durchgeführte Updates**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lässt Updates zu, selbst wenn **ITransactionLocal** nicht zur Verfügung steht. Wenn diese Option aktiviert ist, sind Updates für den Anbieter nicht wiederherstellbar, da der Anbieter keine Transaktionen unterstützt.  
  
     **Index als Zugriffsmethode**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht, Indizes des Anbieters zum Abrufen von Daten zu verwenden. Standardmäßig werden Indizes nur für Metadaten verwendet und nicht geöffnet.  
  
     **Ad-hoc-Zugriffe nicht zulassen**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erlaubt keinen Ad-hoc-Zugriff über die Funktionen OPENROWSET und OPENDATASOURCE auf den OLE DB-Anbieter. Wenn diese Option nicht festgelegt ist, lässt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ebenfalls keinen Ad-hoc-Zugriff zu.  
  
     **Unterstützt 'Like'-Operator**  
     Gibt an, dass der Anbieter Anfragen unterstützt, die das LIKE-Schlüsselwort verwenden.  
  
###  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Verwenden Sie zum Erstellen eines Verbindungsservers mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)] die Anweisungen [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md) und [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md) .  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>So erstellen Sie einen Verbindungsserver für eine andere Instanz von SQL Server anhand von Transact-SQL  
  
1.  Geben Sie im Abfrage-Editor folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl ein, um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit dem Namen `SRVR002\ACCTG`zu verknüpfen:  
  
    ```sql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  Führen Sie folgenden Code aus, um den Verbindungsserver zur Verwendung der Domänenanmeldeinformationen des Anmeldenamens zu konfigurieren, der den Verbindungsserver verwendet.  
  
    ```sql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach der Erstellung eines Verbindungsservers zu unternehmende Schritte  
  
#### <a name="to-test-the-linked-server"></a>So testen Sie den Verbindungsserver  
  
-   Führen Sie folgenden Code aus, um die Verbindung mit dem Verbindungsserver zu testen. Das Beispiel gibt die Namen der Datenbanken auf dem Verbindungsserver zurück.  
  
    ```sql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>Schreiben einer Abfrage, von der Tabellen von einem Verbindungsserver verknüpft werden  
  
-   Verwenden Sie vierteilige Namen, um auf ein Objekt auf einem Verbindungsserver zu verweisen. Führen Sie folgenden Code aus, um eine Liste aller Anmeldenamen auf dem lokalen Server und die entsprechenden Anmeldenamen auf dem Verbindungsserver zurückzugeben.  
  
    ```sql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     Wenn für den Anmeldenamen vom Verbindungsserver NULL zurückgegeben wird, zeigt dies an, dass der Anmeldename auf dem Verbindungsserver nicht vorhanden ist. Von diesen Anmeldenamen kann der Verbindungsserver erst verwendet werden, wenn der Verbindungsserver so konfiguriert wird, dass ein anderer Sicherheitskontext weitergegeben wird oder der Verbindungsserver anonyme Verbindungen akzeptiert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
