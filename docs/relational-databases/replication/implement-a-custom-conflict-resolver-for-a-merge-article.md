---
title: "Implementieren eines benutzerdefinierten Konfliktlösers für einen Mergeartikel | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
caps.latest.revision: "45"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66a0716665f2f8df2be0df258392aeb8ea4531dc
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>Implementieren eines benutzerdefinierten Konfliktlösers für einen Mergeartikel
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie ein benutzerdefinierter Konfliktlöser für einen Mergeartikel mit [!INCLUDE[tsql](../../includes/tsql-md.md)] oder einem [COM-basierten benutzerdefinierten Konfliktlöser](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md) in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] implementiert wird.  
  
 **In diesem Thema**  
  
-   **So implementieren Sie einen benutzerdefinierten Konfliktlöser für einen Mergeartikel mit:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [COM-basierter Konfliktlöser](#COM)  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können einen eigenen benutzerdefinierten Konfliktlöser als gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozedur in einem Verleger schreiben. Diese gespeicherte Prozedur wird während der Synchronisierung aufgerufen, wenn in einem Artikel, für den der Konfliktlöser registriert wurde, Konflikte erkannt werden. Die Informationen zur Konfliktzeile werden vom Merge-Agent an die erforderlichen Parameter der Prozedur übergeben. Auf gespeicherten Prozeduren basierende benutzerdefinierte Konfliktlöser werden immer auf dem Verleger erstellt.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfliktlöser für gespeicherte Prozeduren werden nur zur Behandlung änderungsbasierter Konflikte auf Zeilenebene aufgerufen. Sie können nicht zur Behandlung anderer Arten von Konflikten verwendet werden, z.&nbsp;B. von Einfügefehlern, die durch den Verstoß gegen eine PRIMARY&nbsp;KEY-Einschränkung oder einen eindeutigen Index verursacht werden.  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>So erstellen und registrieren Sie einen auf gespeicherten Prozeduren basierenden benutzerdefinierten Konfliktlöser  
  
1.  Erstellen Sie auf dem Verleger entweder in der Veröffentlichungs- oder der **msdb** -Datenbank eine neue gespeicherte Systemprozedur, welche die folgenden erforderlichen Parameter implementiert:  
  
    |Parameter|Datentyp|Description|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|**sysname**|Name des Besitzers der Tabelle, für die ein Konflikt gelöst wird. Dies ist der Besitzer der Tabelle der Veröffentlichungsdatenbank.|  
    |**@tablename**|**sysname**|Name der Tabelle, für die ein Konflikt gelöst wird.|  
    |**@rowguid**|**uniqueidentifier**|Eindeutiger Bezeichner für die Zeile, die den Konflikt enthält.|  
    |**@subscriber**|**sysname**|Name des Servers, von dem eine konfliktverursachende Änderung weitergegeben wird.|  
    |**@subscriber_db**|**sysname**|Name der Datenbank, von der eine konfliktverursachende Änderung weitergegeben wird.|  
    |**@log_conflict AUSGABE**|**int**|Ob der Mergeprozess einen Konflikt für eine spätere Auflösung protokollieren soll:<br /><br /> **0** = Den Konflikt nicht protokollieren.<br /><br /> **1** = Der Abonnent verliert den Konflikt.<br /><br /> **2** = Der Verleger verliert den Konflikt.|  
    |**@conflict_message AUSGABE**|**nvarchar(512)**|Meldung, die über die Auflösung ausgegeben werden soll, wenn der Konflikt protokolliert wird.|  
    |**@destowner**|**sysname**|Der Besitzer der auf dem Abonnenten veröffentlichten Tabelle.|  
  
     Diese gespeicherte Prozedur verwendet die Werte, die vom Merge-Agent für diese Parameter übergeben werden, um die benutzerdefinierte Konfliktlöserlogik zu implementieren. Sie muss ein einzeiliges Resultset zurückgeben, dessen Struktur mit der Struktur der Basistabelle identisch ist, und das die Datenwerte für die gewinnende Version der Zeile enthält.  
  
2.  Gewähren Sie allen Anmeldungen, die von Abonnenten zum Verbindungsaufbau mit dem Verleger verwendet werden, EXECUTE-Berechtigungen für die gespeicherte Prozedur.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>So verwenden Sie einen benutzerdefinierten Konfliktlöser mit einem neuen Tabellenartikel  
  
1.  Führen Sie [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) zur Definition eines Artikels unter Angabe eines Werts des **MicrosoftSQL**-**Konfliktlösers für gespeicherte Prozeduren** für den **@article_resolver**-Parameter und den Namen der gespeicherten Prozedur, mit der die Konfliktlöserlogik implementiert wird, für den Parameter **@resolver_info** aus. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>So verwenden Sie einen benutzerdefinierten Konfliktlöser mit einem vorhandenen Tabellenartikel  
  
1.  Führen Sie [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) aus, wobei Sie **@publication**,**@article**, den Wert **article_resolver** für **@property** und einen Wert des **MicrosoftSQL** **Konfliktlösers für gespeicherte Prozeduren** für **@value** angeben.  
  
2.  Führen Sie [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)aus, wobei Sie **@publication**, **@article**, den Wert **resolver_info** für **@property**und den Namen der gespeicherten Prozedur, mit der die Konfliktlöserlogik implementiert wird, für **@value**implementiert wird.  
  
##  <a name="COM"></a> Verwenden eines COM-basierten benutzerdefinierten Konfliktlösers  
 Der <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> -Namespace implementiert eine Schnittstelle, mit der Sie eine komplexe Geschäftslogik zum Verarbeiten von Ereignissen und zur Lösung von Konflikten schreiben können, die während der Synchronisierung der Mergereplikation eintreten. Weitere Informationen finden Sie unter [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md). Sie können auch eine eigene, auf systemeigenem Code basierende benutzerdefinierte Geschäftslogik zur Lösung von Konflikten schreiben. Diese Logik wird mithilfe von Produkten wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ als COM-Komponente konzipiert und in DLLs (Dynamic-Link Libraries) kompiliert. Ein solcher COM-basierter benutzerdefinierter Konfliktlöser muss die **ICustomResolver** -Schnittstelle implementieren, die speziell für die Konfliktlösung entworfen wurde.  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>So erstellen und registrieren Sie einen COM-basierten benutzerdefinierten Konfliktlöser  
  
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
  
8.  Führen Sie auf dem Verleger [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) aus, um zu prüfen, ob die Bibliothek noch nicht als benutzerdefinierter Konfliktlöser registriert wurde.  
  
9. Um die Bibliothek als benutzerdefinierten Konfliktlöser zu registrieren, führen Sie auf dem Verteiler [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) aus. Geben Sie den Anzeigenamen des COM-Objekts für **@article_resolver**, die Bibliotheks-ID (CLSID) für **@resolver_clsid**und den Wert **false** für **@is_dotnet_assembly**implementiert wird.  
  
    > [!NOTE]  
    >  Wenn er nicht mehr benötigt wird, kann die Registrierung eines benutzerdefinierten Konfliktlösers mit [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) aufgehoben werden.  
  
10. (Optional) Wiederholen Sie bei einem Cluster die Schritte 5&nbsp;bis&nbsp;8, um den benutzerdefinierten Konfliktlöser auf allen Knoten des Clusters zu registrieren. Dies ist erforderlich, um sicherzustellen, dass der benutzerdefinierte Konfliktlöser nach einem Failover die Synchronisierung korrekt laden kann.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>So verwenden Sie einen benutzerdefinierten Konfliktlöser mit einem neuen Tabellenartikel  
  
1.  Führen Sie auf dem Verleger [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) aus, und achten Sie auf den Anzeigenamen des gewünschten Konfliktlösers.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) zur Definition eines Artikels aus. Geben Sie den Anzeigenamen des Artikelkonfliktlösers aus Schritt&nbsp;1 für **@article_resolver**implementiert wird. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>So verwenden Sie einen benutzerdefinierten Konfliktlöser mit einem vorhandenen Tabellenartikel  
  
1.  Führen Sie auf dem Verleger [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) aus, und achten Sie auf den Anzeigenamen des gewünschten Konfliktlösers.  
  
2.  Führen Sie [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) aus. Geben Sie dabei **@publication** ,**@article**, den Wert **article_resolver** für **@property** und den Anzeigenamen des Artikelkonfliktlösers aus Schritt 1 für **@value** an.  
  

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM-Based Custom Resolvers](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
