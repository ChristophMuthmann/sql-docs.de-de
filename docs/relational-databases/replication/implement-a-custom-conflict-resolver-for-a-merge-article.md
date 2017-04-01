---
title: "Implementieren eines benutzerdefinierten Konfliktl&#246;sers f&#252;r einen Mergeartikel | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Mergereplikation Konfliktlösung [SQL Server-Replikation], auf gespeicherten Prozeduren basierende Konfliktlöser"
  - "Artikel [SQL Server-Replikation], Konfliktlösung"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Implementieren eines benutzerdefinierten Konfliktl&#246;sers f&#252;r einen Mergeartikel
  In diesem Thema wird beschrieben, wie zum Implementieren von benutzerdefinierten Konfliktlöser für einen Mergeartikel in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[tsql](../../includes/tsql-md.md)] oder [COM-basierter benutzerdefinierter Konfliktlöser](../../relational-databases/replication/merge/com-based-custom-resolvers.md).  
  
 **In diesem Thema**  
  
-   **So implementieren Sie einen benutzerdefinierten Konfliktlöser für einen Mergeartikel mit:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [COM-basierter Konfliktlöser](#COM)  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können einen eigenen benutzerdefinierten Konfliktlöser als gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozedur in einem Verleger schreiben. Diese gespeicherte Prozedur wird während der Synchronisierung aufgerufen, wenn in einem Artikel, für den der Konfliktlöser registriert wurde, Konflikte erkannt werden. Die Informationen zur Konfliktzeile werden vom Merge-Agent an die erforderlichen Parameter der Prozedur übergeben. Auf gespeicherten Prozeduren basierende benutzerdefinierte Konfliktlöser werden immer auf dem Verleger erstellt.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Konfliktlöser für gespeicherte Prozeduren werden nur aufgerufen, um Zeile änderungsbasierte Konflikte zu behandeln. Sie können nicht zur Behandlung anderer Arten von Konflikten verwendet werden, z.&nbsp;B. von Einfügefehlern, die durch den Verstoß gegen eine PRIMARY&nbsp;KEY-Einschränkung oder einen eindeutigen Index verursacht werden.  
  
#### So erstellen und registrieren Sie einen auf gespeicherten Prozeduren basierenden benutzerdefinierten Konfliktlöser  
  
1.  Erstellen Sie auf dem Verleger entweder in der Veröffentlichungs- oder der **msdb** -Datenbank eine neue gespeicherte Systemprozedur, welche die folgenden erforderlichen Parameter implementiert:  
  
    |Parameter|Datentyp|Beschreibung|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|**sysname**|Name des Besitzers der Tabelle, für die ein Konflikt gelöst wird. Dies ist der Besitzer der Tabelle der Veröffentlichungsdatenbank.|  
    |**@tablename**|**sysname**|Name der Tabelle, für die ein Konflikt gelöst wird.|  
    |**@rowguid**|**uniqueidentifier**|Eindeutiger Bezeichner für die Zeile, die den Konflikt enthält.|  
    |**@subscriber**|**sysname**|Name des Servers, von dem eine konfliktverursachende Änderung weitergegeben wird.|  
    |**@subscriber_db**|**sysname**|Name der Datenbank, von der eine konfliktverursachende Änderung weitergegeben wird.|  
    |**@log_conflict OUTPUT**|**int**|Ob der Mergeprozess einen Konflikt für eine spätere Auflösung protokollieren soll:<br /><br /> **0** = Es wird der Konflikt nicht protokollieren.<br /><br /> **1** = Abonnent verliert den Konflikt.<br /><br /> **2** = Verleger verliert den Konflikt.|  
    |**@conflict_message OUTPUT**|**nvarchar(512)**|Meldung, die über die Auflösung ausgegeben werden soll, wenn der Konflikt protokolliert wird.|  
    |**@destowner**|**sysname**|Der Besitzer der auf dem Abonnenten veröffentlichten Tabelle.|  
  
     Diese gespeicherte Prozedur verwendet die Werte, die vom Merge-Agent für diese Parameter übergeben werden, um die benutzerdefinierte Konfliktlöserlogik zu implementieren. Sie muss ein einzeiliges Resultset zurückgeben, dessen Struktur mit der Struktur der Basistabelle identisch ist, und das die Datenwerte für die gewinnende Version der Zeile enthält.  
  
2.  Gewähren Sie allen Anmeldungen, die von Abonnenten zum Verbindungsaufbau mit dem Verleger verwendet werden, EXECUTE-Berechtigungen für die gespeicherte Prozedur.  
  
#### So verwenden Sie einen benutzerdefinierten Konfliktlöser mit einem neuen Tabellenartikel  
  
1.  Führen Sie [Sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) definieren Sie einen Artikel, die bei Angabe des Werts **Microsoft SQL** **Server Stored Procedure Resolver** für die **@article_resolver** -Parameter und den Namen der gespeicherten Prozedur, der die konfliktlöserlogik implementiert die **@resolver_info** Parameter. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### So verwenden Sie einen benutzerdefinierten Konfliktlöser mit einem vorhandenen Tabellenartikel  
  
1.  Führen Sie [Sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), unter Angabe **@publication**, **@article**, Wert **Article_resolver** für **@property**, und den Wert **MicrosoftSQL** **Server gespeicherten ProcedureResolver** für **@value**.  
  
2.  Führen Sie [Sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), wobei **@publication**, **@article**, ein Wert von **Resolver_info** für **@property**, und den Namen der gespeicherten Prozedur, der die konfliktlöserlogik implementiert **@value**.  
  
##  <a name="COM"></a> Verwenden eines COM-basierten benutzerdefinierten Konfliktlösers  
 Die <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> Namespace implementiert eine Schnittstelle, mit dem Sie komplexe Geschäftslogik zum Verarbeiten von Ereignissen und Lösen von Konflikten, die auftreten, während der Synchronisierung der Mergereplikation zu schreiben. Weitere Informationen finden Sie unter [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md). Sie können auch eine eigene, auf systemeigenem Code basierende benutzerdefinierte Geschäftslogik zur Lösung von Konflikten schreiben. Diese Logik wird mithilfe von Produkten wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ als COM-Komponente konzipiert und in DLLs (Dynamic-Link Libraries) kompiliert. Solcher COM-basierter benutzerdefinierter Konfliktlöser muss Implementieren der **ICustomResolver** -Schnittstelle, die speziell für die Auflösung des Konflikts zwischen entworfen wurde.  
  
#### So erstellen und registrieren Sie einen COM-basierten benutzerdefinierten Konfliktlöser  
  
1.  Fügen Sie in einer COM-kompatiblen Erstellungsumgebung Verweise auf die benutzerdefinierte Konfliktlöserbibliothek hinzu.  
  
2.  Verwenden Sie für ein Visual&nbsp;C++-Projekt die #import-Direktive, um diese Bibliothek in Ihr Projekt zu importieren.  
  
3.  Fügen Sie eine Klasse hinzu, die die **ICustomResolver** -Schnittstelle implementiert.  
  
4.  Implementieren Sie bestimmte Methoden und Eigenschaften.  
  
5.  Erstellen Sie das Projekt, um die benutzerdefinierte Konfliktlöserbibliotheksdatei zu erstellen.  
  
6.  Stellen Sie die Bibliothek in dem Verzeichnis bereit, das die ausführbare Datei des Merge-Agents (normalerweise \Microsoft SQL Server\100\COM) enthält.  
  
    > [!NOTE]  
    >  Ein benutzerdefinierter Konfliktlöser muss bei einem Pullabonnement auf dem Abonnenten, bei einem Pushabonnement auf dem Verteiler oder auf dem mit der Websynchronisierung verwendeten Webserver bereitgestellt werden.  
  
7.  Registrieren Sie die benutzerdefinierte Konfliktlöserbibliothek folgendermaßen mit regsvr32.exe vom Bereitstellungsverzeichnis aus:  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  Führen Sie auf dem Verleger [Sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) Überprüfen Sie, dass die Bibliothek als benutzerdefinierten Konfliktlöser noch nicht registriert ist.  
  
9. Führen Sie zum Registrieren der Bibliotheks als benutzerdefinierten Konfliktlöser [Sp_registercustomresolver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md), auf dem Verteiler. Geben Sie den Anzeigenamen des COM-Objekts für **@article_resolver**, die Bibliotheks ID (CLSID) für **@resolver_clsid**, und der Wert **false** für **@is_dotnet_assembly**.  
  
    > [!NOTE]  
    >  Wenn nicht mehr benötigt wird, kann ein benutzerdefinierten Konfliktlösers mit aufgehoben werden [Sp_unregistercustomresolver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md).  
  
10. (Optional) Wiederholen Sie bei einem Cluster die Schritte 5&nbsp;bis&nbsp;8, um den benutzerdefinierten Konfliktlöser auf allen Knoten des Clusters zu registrieren. Dies ist erforderlich, um sicherzustellen, dass der benutzerdefinierte Konfliktlöser nach einem Failover die Synchronisierung korrekt laden kann.  
  
#### So verwenden Sie einen benutzerdefinierten Konfliktlöser mit einem neuen Tabellenartikel  
  
1.  Führen Sie auf dem Verleger [Sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) und beachten Sie den Anzeigenamen des gewünschten Konfliktlösers.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Um einen Artikel zu definieren. Geben Sie den Anzeigenamen des Artikelkonfliktlösers aus Schritt 1 für **@article_resolver**. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### So verwenden Sie einen benutzerdefinierten Konfliktlöser mit einem vorhandenen Tabellenartikel  
  
1.  Führen Sie auf dem Verleger [Sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) und beachten Sie den Anzeigenamen des gewünschten Konfliktlösers.  
  
2.  Führen Sie [Sp_changemergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), wobei **@publication**, **@article**, ein Wert von **Article_resolver** für **@property**, und den Anzeigenamen des Artikelkonfliktlösers aus Schritt 1 für **@value**.  
  
#### Anzeigen eines Beispiels für einen benutzerdefinierten Konfliktlöser  
  
1.  Ein Beispiel ist in SQL Server 2000-Beispieldateien verfügbar. Laden Sie **sql2000samples.cab** von [Aktualisierte Beispiele für SQL Server 2000 Service Pack 3](http://www.microsoft.com/download/details.aspx?id=8560)herunter. Dadurch werden acht Dateien mit einer Gesamtkapazität von 6,9 MB heruntergeladen.  
  
2.  Extrahieren Sie die Dateien aus der heruntergeladenen komprimierten CAB-Datei.  
  
3.  Führen Sie **setup.exe**aus.  
  
    > [!NOTE]  
    >  Bei der Auswahl der Installationsoptionen müssen Sie nur die Beispiele für die **Replikation** installieren. (Der Standardinstallationspfad lautet **C:\Programme\Microsoft Dateien (x86) \Microsoft SQL Server 2000 Samples\1033\\**)  
  
4.  Wechseln Sie zum Installationsordner. (Der Standardordner ist **C:\Programme\Microsoft Dateien (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**)  
  
5.  Führen Sie die **unzip_sqlreplSP3.exe** Programm.  
  
    > [!NOTE]  
    >  Installieren der Beispiel-com-Konfliktlöser (standardmäßig) auf den **C:\Program Files (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** Ordner.  
  
6.  In der **Subspres** Ordner, suchen Sie alle Vorkommen von **#include sqlres.h** in allen Quelldateien und Ersetzen Sie sie durch **#import "replrec.dll" No_namespace, Raw_interfaces_only**  
  
## Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM-basierte benutzerdefinierte Konfliktlöser](../../relational-databases/replication/merge/com-based-custom-resolvers.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  