---
title: "Überlegungen zum Entwurf und Einschränkungen für Oracle-Verleger | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], design considerations and limitations
ms.assetid: 8d9dcc59-3de8-4d36-a61f-bc3ca96516b6
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41628417abe4662740407c6d86b44d60a1a58a66
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="design-considerations-and-limitations-for-oracle-publishers"></a>Überlegungen zum Entwurf und Einschränkungen für Oracle-Verleger
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das Veröffentlichen aus Oracle-Datenbanken erfolgt nahezu auf die gleiche Weise wie das Veröffentlichen aus [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbanken. Beachten Sie jedoch die folgenden Punkte und Einschränkungen:  
  
-   Die Option Oracle (Gateway) bietet eine bessere Leistung im Vergleich zur Option Oracle (Vollständig), allerdings ist es mit dieser Option nicht möglich, dieselbe Tabelle in mehreren Transaktionsveröffentlichungen zu veröffentlichen. Eine Tabelle kann in höchstens eine Transaktionsveröffentlichung und in beliebig viele Momentaufnahmeveröffentlichungen aufgenommen werden. Wenn Sie dieselbe Tabelle in mehreren Transaktionsveröffentlichungen veröffentlichen müssen, wählen Sie die Option Oracle (Vollständig) aus.  
  
-   Die Replikation unterstützt das Veröffentlichen von Tabellen, Indizes und materialisierten Sichten. Andere Objekte werden nicht repliziert.  
  
-   Es bestehen einige geringfügige Unterschiede zwischen dem Speichern und Verarbeiten von Daten in Oracle- und in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbanken, die sich auf die Replikation auswirken.  
  
-   Zahlreiche Unterschiede bestehen dahingehend, wie Replikationsfunktionen bei der Verwendung eines Oracle-Verlegers unterstützt werden.  
  
## <a name="support-for-publishing-objects-from-oracle"></a>Unterstützung für das Veröffentlichen von Objekten aus Oracle-Datenbanken  
 Das Replizieren der folgenden Objekte aus Oracle-Datenbanken wird von der Replikation unterstützt:  
  
-   Tabellen  
  
-   Durch Indizes organisierte Tabellen  
  
-   Indizes  
  
-   Materialisierte Sichten (als Tabellen repliziert)  
  
 Folgendes kann bei veröffentlichten Tabellen vorhanden sein, wird jedoch nicht repliziert:  
  
-   Domänenbasierte Indizes  
  
-   Funktionsbasierte Indizes  
  
-   Standardwerte  
  
-   Check-Einschränkungen  
  
-   Fremdschlüssel  
  
-   Speicheroptionen (Tabellenbereiche, Cluster usw.)  
  
 Die folgenden Objekte können nicht repliziert werden:  
  
-   Geschachtelte Tabellen  
  
-   Sichten  
  
-   Pakete, Paketkörper, Prozeduren und Trigger  
  
-   Warteschlangen  
  
-   Sequenzen  
  
-   Synonyme  
  
 Informationen zu unterstützten Datentypen finden Sie unter [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
## <a name="differences-between-oracle-and-sql-server"></a>Unterschiede zwischen Oracle und SQL Server  
  
-   Bei Oracle unterscheidet sich die maximal zulässige Größe für einige Objekte. Die Größe der Objekte, die in der Oracle-Veröffentlichungsdatenbank erstellt werden, muss mit der maximal zulässigen Größe der entsprechenden Objekte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]übereinstimmen. Weitere Informationen zu Einschränkungen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] finden Sie unter [Spezifikationen der maximalen Kapazität für SQL Server](../../../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
-   Standardmäßig werden Oracle-Objektnamen in Großbuchstaben erstellt. Stellen Sie sicher, dass beim Veröffentlichen von Oracle-Objekten über einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler die Namen der Objekte Großbuchstaben aufweisen, wenn sie in der Oracle-Datenbank in Großbuchstaben vorliegen. Stimmt die Schreibweise nicht überein, gibt möglicherweise eine Fehlermeldung an, dass das Objekt nicht gefunden werden kann.  
  
-   Der SQL-Dialekt von Oracle und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]unterscheidet sich leicht. Schreiben Sie Zeilenfilter in einer mit Oracle kompatiblen Syntax.  
  
### <a name="considerations-for-large-objects"></a>Überlegungen zu großen Objekten  
 Daten großer Objekte (LOB, Large OBjects) werden in der Artikelprotokolltabelle gespeichert. Updates an LOB-Daten werden stets direkt aus der veröffentlichten Tabelle abgerufen. Eine Replikation von Updates erfolgt bei Transaktionsveröffentlichungen nur dann, wenn der Vorgang, der das LOB betrifft, den Replikationstrigger für die replizierte Tabelle auslöst. Oracle-Trigger werden beim Einfügen oder Löschen von Zeilen ausgelöst, die LOBs enthalten; Updates an LOB-Spalten lösen jedoch keine Trigger aus. Das Update einer LOB-Spalte wird nur dann sofort repliziert, wenn in derselben Zeile eine Spalte, die sich nicht auf ein LOB bezieht, mit derselben Oracle-Transaktion ebenfalls aktualisiert wird. Anderenfalls wird die LOB-Spalte nicht auf dem Abonnenten aktualisiert, wenn das nächste Update an einer Spalte, die sich nicht auf ein LOB bezieht, in derselben Zeile stattfindet. Stellen Sie sicher, dass dieses Verhalten bei Ihrer Anwendung toleriert werden kann.  
  
 Um Updates an LOB-Spalten in Transaktionsveröffentlichungen zu replizieren, berücksichtigen Sie beim Schreiben der Anwendung eine der folgenden Strategien:  
  
-   Führen Sie innerhalb einer Transaktion ein Löschen und erneutes Einfügen der Zeile aus, statt die Zeile zu aktualisieren: Geben Sie das neue LOB an, wenn Sie die Zeile erneut einfügen. Da beim Löschen und auch beim Einfügen Trigger ausgelöst werden, wird die Zeile repliziert.  
  
-   Nehmen Sie zusammen mit der LOB-Spalte eine Spalte auf, die sich nicht auf ein LOB bezieht, oder aktualisieren Sie eine solche Spalte im Rahmen derselben Oracle-Transaktion. In beiden Fällen stellt das Aktualisieren der Spalte, die sich nicht auf ein LOB bezieht, das Auslösen des Triggers sicher.  
  
 Weitere Informationen zu LOBs finden Sie unter [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
### <a name="unique-indexes-and-constraints"></a>Eindeutige Indizes und Einschränkungen  
 Bei der Momentaufnahme- und der Transaktionsreplikation unterliegen Spalten, die in eindeutigen Indizes und Einschränkungen (einschließlich PRIMARY KEY-Einschränkungen) enthalten sind, bestimmten Bedingungen. Werden diese Bedingungen nicht erfüllt, wird die Einschränkung oder der Index nicht repliziert.  
  
-   Die maximale Zahl zulässiger Spalten in einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Index beträgt 16.  
  
-   Alle in UNIQUE-Einschränkungen aufgenommene Spalten müssen unterstützte Datentypen aufweisen. Weitere Informationen zu Datentypen finden Sie unter [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
-   Alle in UNIQUE-Einschränkungen aufgenommene Spalten müssen veröffentlicht werden (sie können nicht gefiltert werden).  
  
-   Für Spalten, die von UNIQUE-Einschränkungen betroffen sind, muss ein Wert ungleich NULL angegeben sein.  
  
 Berücksichtigen Sie außerdem die folgenden Punkte:  
  
-   Oracle und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verarbeiten NULL-Werte unterschiedlich: Oracle lässt mehrere Zeilen mit NULL-Werten für Spalten zu, bei denen NULL-Werte zulässig sind und die in UNIQUE-Einschränkungen oder -Indizes eingeschlossen sind. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erzwingt die Eindeutigkeit, indem nur eine einzige Zeile mit einem NULL-Wert für die gleiche Spalte zulässig ist. UNIQUE-Einschränkungen oder -Indizes, die NULL zulassen, können nicht veröffentlicht werden. Anderenfalls würde eine Einschränkungsverletzung auf dem Abonnenten eintreten, wenn die veröffentlichte Tabelle für eine der im Index oder der Einschränkung enthaltenen Spalten mehrere Zeilen mit NULL-Werten enthält.  
  
-   Beim Testen der Eindeutigkeit ignoriert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nachfolgende Leerzeichen in einem Feld, nicht jedoch Oracle.  
  
 Tabellen in Oracle-Transaktionsveröffentlichungen erfordern wie bei der Transaktionsreplikation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] einen Primärschlüssel und müssen gemäß den oben stehenden Regeln eindeutig sein. Wenn der Primärschlüssel nicht den oben beschriebenen Regeln folgt, kann die Tabelle nicht für die Transaktionsreplikation veröffentlicht werden.  
  
## <a name="differences-between-oracle-publishing-and-standard-transactional-replication"></a>Unterschiede zwischen dem Veröffentlichen mit Oracle und der Standardtransaktionsreplikation  
  
-   Oracle-Verleger können nicht den gleichen Namen aufweisen, wie deren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler, einer der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verleger, die den Verteiler verwenden, oder einer der Abonnenten, die die Veröffentlichung erhalten. Von demselben Verteiler bediente Veröffentlichungen müssen jeweils einen eindeutigen Namen haben.  
  
-   Eine in einer Oracle-Veröffentlichung veröffentlichte Tabelle kann keine replizierten Daten erhalten. Daher unterstützen Oracle-Veröffentlichungen Folgendes nicht: Veröffentlichungen mit Abonnements mit sofortigem Update und mit verzögertem Update über eine Warteschlange oder Topologien, in denen Veröffentlichungstabellen auch als Abonnementtabellen dienen, z. B. bei der Peer-zu-Peer- und bidirektionalen Replikation.  
  
-   Primärschlüssel/Fremdschlüssel-Beziehungen in der Oracle-Datenbank werden nicht auf die Abonnenten repliziert. Die Beziehungen bleiben jedoch in den Daten erhalten, wenn Änderungen übermittelt werden.  
  
-   Transaktionsveröffentlichungen unterstützen standardmäßig Tabellen mit bis zu 1000 Spalten. Oracle-Transaktionsveröffentlichungen unterstützen 995 Spalten (bei der Replikation werden jeder veröffentlichten Tabelle fünf Spalten hinzugefügt).  
  
-   Sortierklauseln werden den CREATE TABLE-Anweisungen hinzugefügt, damit Groß- und Kleinbuchstaben bei Vergleichen berücksichtigt werden, was bei Primärschlüsseln und UNIQUE-Einschränkungen eine wichtige Rolle spielt. Dieses Verhalten wird durch die Schemaoption 0x1000 gesteuert, die mit dem **@schema_option**-Parameter von [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) angegeben wird.  
  
-   Wenn Sie zur Konfiguration oder Verwaltung eines Oracle-Verlegers gespeicherte Prozeduren verwenden, nehmen Sie die Prozeduren nicht innerhalb einer expliziten Transaktion auf. Dies wird über den Verbindungsserver nicht unterstützt, mit dem die Verbindung mit dem Oracle-Verleger hergestellt wird.  
  
-   Wenn Sie ein Pullabonnement für eine Oracle-Veröffentlichung mithilfe eines Assistenten erstellen, müssen Sie den Assistent für neue Abonnements verwenden, der mit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und höheren Versionen bereitgestellt wird. Bei früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]können Sie jedoch die gespeicherte Prozedur und SQL-DOM-Schnittstellen verwenden, um Pullabonnements Oracle-Veröffentlichungen einzurichten.  
  
-   Bei der Weitergabe von Änderungen mithilfe gespeicherter Prozeduren an Abonnenten (Standardverfahren) wird die MCALL-Syntax zwar unterstützt, weist jedoch ein anderes Verhalten auf, wenn die Veröffentlichung von einem Oracle-Verleger stammt. In der Regel stellt MCAL ein Bitmuster bereit, das die auf dem Verleger aktualisierten Spalten zeigt. Bei einer Oracle-Veröffentlichung zeigt das Bitmuster immer, dass alle Spalten aktualisiert wurden. Weitere Informationen zur Verwendung gespeicherter Prozeduren finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
### <a name="transactional-replication-feature-support"></a>Unterstützte Funktionen der Transaktionsreplikation  
  
-   Oracle-Veröffentlichungen unterstützen nicht alle Schemaoptionen, die von SQL Server-Veröffentlichungen unterstützt werden. Weitere Informationen zu Schemaoptionen finden Sie unter [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Abonnenten von Oracle-Veröffentlichungen können keine Abonnements mit sofortigem Update oder Abonnements mit verzögertem Update über eine Warteschlange verwenden und keine Knoten in einer Peer-zu-Peer- oder bidirektionalen Topologie sein.  
  
-   Abonnenten von Oracle-Veröffentlichungen können nicht automatisch von einer Sicherung initialisiert werden.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt zwei Überprüfungstypen: binär und Zeilenanzahl. Oracle-Verleger unterstützen die Zeilenanzahlüberprüfung. Weitere Informationen finden Sie unter [Überprüfen von replizierten Daten](../../../relational-databases/replication/validate-replicated-data.md).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stellt zwei Momentaufnahmeformate bereit: systemeigener BCP-Modus und Zeichenmodus. Oracle-Verleger unterstützen Momentaufnahmen im Zeichenmodus.  
  
-   Schemaänderungen an veröffentlichten Oracle-Tabellen werden nicht unterstützt. Wenn Sie das Schema ändern möchten, löschen Sie zuerst die Veröffentlichung, nehmen Sie die Änderungen vor, und erstellen Sie dann die Veröffentlichung und alle Abonnements neu.  
  
    > [!NOTE]  
    >  Wenn die Schemaänderungen und das anschließende Löschen sowie Neuerstellen der Veröffentlichung und Abonnements dann vorgenommen werden, wenn keine Aktivität an den veröffentlichten Tabellen stattfindet, können Sie die Option 'Nur Replikationsunterstützung' für die Abonnements angeben. Die Abonnements werden dann synchronisiert, ohne dass eine Momentaufnahme auf jeden Abonnenten kopiert werden muss. Weitere Informationen finden Sie unter [Initialisieren eines Transaktionsabonnements ohne Momentaufnahme](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="replication-security-model"></a>Replikationssicherheitsmodell  
 Das Sicherheitsmodell für das Veröffentlichen mit Oracle ist mit dem der Standardtransaktionsreplikation identisch. Ausnahmen:  
  
-   Das Konto, unter dem der Momentaufnahme-Agent und der Protokolllese-Agent Verbindungen vom Verteiler zum Verleger herstellen, wird mit einer der folgenden Methoden angegeben:  
  
    -   Die **@security_mode**-Parameter von [sp_adddistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md) (Sie geben auch Werte für **@login** und **@password** bei Oracle-Authentifizierung an)  
  
    -   Im Dialogfeld **Verbindung mit Server herstellen** in SQL Server Management Studio (Sie verwenden das Dialogfeld zum Konfigurieren des Oracle-Verlegers auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler).  
  
     Das Konto wird bei der standardmäßigen Transaktionsreplikation mit [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) und [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) angegeben.  
  
-   Das Konto, unter dem der Momentaufnahmeagent und der Protokollleseagent Verbindungen herstellen, kann nicht mithilfe von [sp_changedistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) oder einem Eigenschaftenblatt geändert werden. Das Kennwort können Sie jedoch ändern.  
  
-   Wenn Sie den Wert 1 (integrierte Windows-Authentifizierung) für den **@security_mode**-Parameter von [sp_adddistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md) angeben:  
  
    -   Das Prozesskonto und das Kennwort für den Momentaufnahmeagent und den Protokollleseagenten (die **@job_login**- und **@job_password**-Parameter von [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) und [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)) müssen identisch mit dem Konto und dem Kennwort für die Verbindung mit dem Oracle-Verleger sein.  
  
    -   Sie können den **@job_login**-Parameter nicht über [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) oder [sp_changelogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md) angeben, das Kennwort kann jedoch geändert werden.  
  
 Weitere Informationen zur Replikationssicherheit finden Sie unter [Sicherheit und Schutz &#40;Replikation&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überlegungen zu administrativen Aufgaben bei Oracle-Verlegern](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
