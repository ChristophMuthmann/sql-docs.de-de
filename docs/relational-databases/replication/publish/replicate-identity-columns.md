---
title: Replizieren von Identitätsspalten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/04/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- identities [SQL Server replication]
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: eb2f23a8-7ec2-48af-9361-0e3cb87ebaf7
caps.latest.revision: 51
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 605d72412610ec17863e000b9ef3813e4d3fe424
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="replicate-identity-columns"></a>Replizieren von Identitätsspalten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Wenn Sie einer Spalte eine IDENTITY-Eigenschaft zuweisen, generiert [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für neue Zeilen, die in die Tabelle, die die Identitätsspalte enthält, eingefügt werden, automatisch sequenzielle Zahlwerte. Weitere Informationen finden Sie unter [IDENTITY &#40;Eigenschaft&#41; &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql-identity-property.md). Da Identitätsspalten als Teil des Primärschlüssels aufgenommen werden können, ist es wichtig, dass die Identitätsspalten keine doppelten Werte enthalten. Wenn Identitätsspalten in einer Replikationstopologie verwendet werden sollen, die an mehreren Knoten Updates besitzt, muss jeder Knoten in der Replikationstopologie einen anderen Bereich von Identitätswerten verwenden, damit es nicht zu Dopplungen kommt.  
  
 Beispielsweise kann dem Verleger der Bereich 1-100 zugewiesen werden, dem Abonnent A der Bereich 101-200 und dem Abonnent B der Bereich 201-300. Wenn beim Verleger eine Zeile eingefügt wird und der Identitätswert beispielsweise 65 beträgt, wird der Wert für jeden Abonnenten repliziert. Beim Einfügen der Daten auf den einzelnen Abonnenten erhöht die Replikation jedoch nicht den Identitätsspaltenwert in der Abonnententabelle um 1, sondern es wird der Literalwert 65 eingefügt. Eine inkrementelle Erhöhung des Identitätsspaltenwerts erfolgt nur bei Benutzereinfügungen, nicht jedoch bei Einfügungen durch einen Replikations-Agent.  
  
 Die Replikation behandelt die Identitätsspalten in allen Veröffentlichungs- und Abonnementtypen und ermöglicht es Ihnen so, die Spalten entweder selbst manuell zu verwalten oder die Spalten automatisch durch die Replikation verwalten zu lassen.  
  
> [!NOTE]  
>  Das Hinzufügen einer Identitätsspalte zu einer veröffentlichten Tabelle wird nicht unterstützt, da ein solcher Vorgang zu Nichtkonvergenz führen kann, wenn die Spalte auf den Abonnenten repliziert wird. Die Werte in der Identitätsspalte auf dem Verleger richten sich nach der Ordnung, in der die Zeilen für die betreffende Tabelle physisch gespeichert sind. Es ist möglich, dass die Zeilen auf dem Abonnenten anders gespeichert sind, sodass der Wert für die Identitätsspalte für dieselben Zeilen unterschiedlich sein kann.  
  
## <a name="specifying-an-identity-range-management-option"></a>Angeben der Optionen für die Identitätsbereichsverwaltung  
 Die Replikation bietet die folgenden drei Optionen für die Identitätsbereichsverwaltung:  
  
-   Automatisch. Diese Option ist bei Mergereplikationen und Transaktionsreplikationen mit Update auf den Abonnenten zu verwenden. Geben Sie die Größenbereiche für den Verleger und die Abonnenten an. Die Replikation übernimmt dann automatisch die Zuweisung der neuen Bereiche. Die Replikation aktiviert die Option NOT FOR REPLICATION für die Identitätsspalte auf dem Abonnenten, sodass nur Benutzereinfügungen zu einer inkrementellen Erhöhung des Werts auf dem Abonnenten führen.  
  
    > [!NOTE]  
    >  Die Abonnenten müssen mit dem Verleger synchronisiert werden, um die neuen Bereiche zu empfangen. Da den Abonnenten die Identitätsbereiche automatisch zugewiesen werden, ist es für alle Abonnenten möglich, sämtliche Identitätsbereiche auszuschöpfen, wenn wiederholt neue Bereiche angefordert werden.  
  
-   Manuell. Diese Option ist bei Momentaufnahme- und Transaktionsreplikationen ohne Updates auf dem Abonnenten, bei Peer-zu-Peer-Transaktionsreplikationen und in den Fällen zu verwenden, in denen Ihre Anwendung die Identitätsbereiche programmgesteuert kontrollieren muss. Wenn Sie die manuelle Verwaltung angeben, müssen Sie sicherstellen, dass dem Verleger und den einzelnen Abonnenten Bereiche zugewiesen werden und dass neue Bereiche zugeordnet werden, sofern die anfänglichen Bereiche verwendet werden. Die Replikation aktiviert die Option NOT FOR REPLICATION für die Identitätsspalte auf dem Abonnenten.  
  
-   Keine. Diese Option sollte nur für die Rückwärtskompatibilität mit früheren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Versionen verwendet werden. Bei Transaktionsveröffentlichungen ist die Option nur über die gespeicherte Prozedur verfügbar.  
  
 Informationen zum Angeben einer Option für die Identitätsbereichsverwaltung finden Sie unter [Verwalten von Identitätsspalten](../../../relational-databases/replication/publish/manage-identity-columns.md).  
  
## <a name="assigning-identity-ranges"></a>Zuweisen von Identitätsbereichen  
 Bei der Mergereplikation und der Transaktionsreplikation kommen zum Zuweisen von Bereichen unterschiedliche Methoden zum Einsatz. Diese Methoden werden im Folgenden näher beschrieben.  
  
 Beim Replizieren von Identitätsspalten sind die folgenden beiden Bereichstypen zu berücksichtigen: Bereiche, die dem Verleger und den Abonnenten zugewiesen werden, und der Bereich des Datentyps in der Spalte. Die folgende Tabelle enthält eine Übersicht über die für die Datentypen verfügbaren Bereiche, die in der Regel in Identitätsspalten verwendet werden. Der Bereich wird in allen Knoten in einer Topologie verwendet. Wenn Sie z. B. **smallint** beginnend mit 1 und einem Inkrement von 1 verwenden, sind maximal 32.767 Einfügungen für den Verleger und alle Abonnenten zulässig. Die tatsächliche Anzahl der Einfügungen hängt davon ab, ob es in den verwendeten Werten Lücken gibt und ob ein Schwellenwert verwendet wird. Weitere Informationen zu Schwellenwerten finden Sie in den folgenden Abschnitten: "Mergereplikation" und "Transaktionsreplikation mit Abonnements mit verzögertem Update über eine Warteschlange".  
  
 Wenn der Verleger nach einer Einfügung seinen Identitätsbereich ausgeschöpft hat, kann er automatisch einen neuen Bereich zuweisen, wenn die Einfügung von einem Mitglied mit der festen **db_owner** -Datenbankrolle ausgeführt wurde. Wenn die Einfügung von einem Benutzer mit einer anderen Rolle ausgeführt wird, muss der Protokolllese-Agent, der Merge-Agent oder ein Benutzer, der Mitglied der **db_owner**-Rolle ist, [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md) ausführen. Bei Transaktionsveröffentlichungen muss der Protokolllese-Agent ausgeführt werden, damit automatisch ein neuer Bereich zugeordnet wird (der Agent wird standardmäßig ununterbrochen ausgeführt).  
  
> [!WARNING]  
>  Während einer umfangreichen Batcheinfügung wird der Replikationstrigger nur einmal und nicht für jede eingefügte Zeile ausgelöst. Dies kann zu einem Fehler bei der INSERT-Anweisung führen, wenn ein Identitätsbereich während einer umfangreichen Einfügung, z. B. einer **INSERT INTO** -Anweisung, ausgeschöpft ist.  
  
|Datentyp|Bereich|  
|---------------|-----------|  
|**tinyint**|Keine Unterstützung bei automatischer Verwaltung|  
|**smallint**|-2^15 (-32,768) bis 2^15-1 (32,767)|  
|**int**|-2^31 (-2.147.483.648) bis 2^31-1 (2.147.483.647)|  
|**bigint**|-2^63 (-9.223.372.036.854.775.808) bis 2^63-1 (9.223.372.036.854.775.807)|  
|**decimal** und **numeric**|-10^38+1 bis 10^38-1|  
  
> [!NOTE]  
>  Weitere Informationen zu einer automatisch inkrementierten Zahl, die in mehreren Tabellen verwendet oder aus Anwendungen aufgerufen werden kann, ohne dass auf eine Tabelle verwiesen wird, finden Sie unter [Sequenznummern](../../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
### <a name="merge-replication"></a>Mergereplikation  
 Identitätsbereiche werden vom Verleger verwaltet und vom Merge-Agent an die Abonnenten weitergegeben (in einer Wiederveröffentlichungshierarchie werden die Bereiche vom Stammverleger und den Neuverlegern verwaltet). Die Identitätswerte werden auf dem Verleger aus einem Pool zugewiesen. Wenn Sie einen Artikel mit einer Identitätsspalte einer Veröffentlichung im Assistenten für neue Veröffentlichung oder mithilfe von [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) hinzufügen, können Sie Werte für die folgenden Parameter angeben:  
  
-   Mit dem **@identity_range**-Parameter steuern Sie die Größe des Identitätsbereichs, der dem Verleger und den Abonnenten mit Clientabonnements anfänglich zugeordnet wird.  
  
    > [!NOTE]  
    >  Bei Abonnenten, die eine ältere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Version ausführen, steuert dieser Parameter darüber hinaus die Größe des Identitätsbereichs auf den Wiederveröffentlichungsabonnenten (und tritt damit an die Stelle des **@pub_identity_range** -Parameters).  
  
-   Mit dem **@pub_identity_range**-Parameter steuern Sie die Größe des Identitätsbereichs für die Wiederveröffentlichung, der den Abonnenten mit Serverabonnements zugeordnet ist (erforderlich für die Wiederveröffentlichung von Daten). Alle Abonnenten mit Serverabonnenten erhalten einen Bereich zur Wiederveröffentlichung, auch wenn sie gar keine Daten erneut veröffentlichen.  
  
-   Mit dem **@threshold**-Parameter bestimmen Sie, wann ein neuer Identitätsbereich für ein Abonnement von [!INCLUDE[ssEW](../../../includes/ssew-md.md)] oder eine frühere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Version erforderlich ist.  
  
 So könnten Sie z. B. für **@identity_range** 10.000 und für **@pub_identity_range**. Dem Verleger und allen Abonnenten, die [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version ausführen, einschließlich des Abonnenten mit dem Serverabonnement, wird der Primärbereich 10.000 zugewiesen. Dem Abonnenten mit dem Serverabonnement wird zudem der Primärbereich 500.000 zugewiesen, der von den Abonnenten verwendet werden kann, die eine Synchronisierung mit dem Wiederveröffentlichungsabonnenten ausführen (für die Artikel in der Veröffentlichung auf dem Wiederveröffentlichungsabonnenten müssen Sie ebenfalls einen Wert für **@identity_range**, **@pub_identity_range**und **@threshold** angeben).  
  
 Jeder Abonnent, auf dem [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version ausgeführt wird, erhält darüber hinaus einen sekundären Identitätsbereich. Der sekundäre Bereich entspricht in seiner Größe der Größe des Primärbereichs. Wenn der Primärbereich ausgeschöpft ist, wird der sekundäre Bereich verwendet, und der Merge-Agent weist dem Abonnenten einen neuen Bereich zu. Der neue Bereich wird zum sekundären Bereich, und der Prozess wird fortgesetzt.  
  
  
### <a name="transactional-replication-with-queued-updating-subscriptions"></a>Transaktionsreplikation mit Abonnements mit verzögertem Update über eine Warteschlange  
 Die Identitätsbereiche werden vom Verteilungs-Agent auf dem Verteiler verwaltet und an die Abonnenten weitergegeben. Die Identitätswerte werden auf dem Verteiler aus einem Pool zugewiesen. Die Größe des Pools richtet sich nach der Größe des Datentyps und des für die Identitätsspalte verwendeten Inkrements. Wenn Sie einen Artikel mit einer Identitätsspalte einer Veröffentlichung im Assistenten für neue Veröffentlichung oder mithilfe von [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) hinzufügen, können Sie Werte für die folgenden Parameter angeben:  
  
-   Mit dem **@identity_range**-Parameter steuern Sie die Größe des Identitätsbereichs, der allen Abonnenten anfänglich zugeordnet wird.  
  
-   Mit dem **@pub_identity_range**-Parameter steuern Sie die Größe des Identitätsbereichs, der dem Verleger zugeordnet wird.  
  
-   Mit dem **@threshold**-Parameter bestimmen Sie, wann ein neuer Bereich für ein Abonnement erforderlich ist.  
  
 So könnten Sie z. B. für **@pub_identity_range**10.000, für **@identity_range** 1.000 (unter der Annahme einer geringeren Anzahl von Updates auf dem Abonnenten) und für **@threshold**. Nach 800 Einfügungen auf einem Abonnenten (80 Prozent von 1.000) wird einem Abonnenten ein neuer Bereich zugewiesen. Nach 8.000 Einfügungen auf dem Verleger wird dem Verleger ein neuer Bereich zugewiesen. Beim Zuweisen eines neuen Bereichs ergibt sich jedoch eine Lücke in den Identitätsbereichswerten in der Tabelle. Durch Angabe eines höheren Schwellenwerts fallen diese Lücken zwar kleiner aus, das System ist dann aber auch weniger fehlertolerant, d. h., wenn der Verteilungs-Agent aus irgendeinem Grund nicht ausgeführt werden kann, gehen einem Abonnenten möglicherweise schneller die Identitäten aus.  
  
## <a name="assigning-ranges-for-manual-identity-range-management"></a>Zuweisen von Bereichen für die manuelle Identitätsbereichsverwaltung  
 Wenn Sie die manuelle Identitätsbereichsverwaltung angeben, müssen Sie sicherstellen, dass der Verleger und alle Abonnenten verschiedene Identitätsbereiche verwenden. Stellen Sie sich z. B. eine Tabelle auf dem Verleger mit einer als `IDENTITY(1,1)`definierten Identitätsspalte vor: Die Identitätsspalte beginnt mit 1 und erhöht sich bei jeder neu eingefügten Zeile um 1. Wenn die Tabelle auf dem Verleger 5.000 Zeilen besitzt und Sie für den weiteren Entwicklungsverlauf der Anwendung eine gewisse Vergrößerung der Tabelle erwarten, könnte der Verleger den Bereich 1-10.000 verwenden. Bei Vorhandensein von zwei Abonnenten könnte der Abonnent A den Bereich 10.001-20.000 und der Abonnent B den Bereich 20.001-30.000 verwenden.  
  
 Nachdem ein Abonnent mit einer Momentaufnahme oder auf andere Weise initialisiert wurde, führen Sie DBCC CHECKIDENT aus, um dem Abonnenten einen Anfangspunkt für dessen Identitätsbereich zuzuweisen. Auf Abonnent A würden Sie dazu z. B. `DBCC CHECKIDENT('<TableName>','reseed',10001)`ausführen. Auf Abonnent B ist dann `CHECKIDENT('<TableName>','reseed',20001)`auszuführen.  
  
 Zum Zuweisen neuer Bereiche zum Verleger bzw. zu den Abonnenten führen Sie DBCC CHECKIDENT aus, und geben Sie einen neuen Wert als Ausgangswert für die Tabelle an. Auf irgendeine Weise müssen Sie auch bestimmen, wann ein neuer Bereich zugewiesen werden muss. So könnte Ihre Anwendung z. B. einen Mechanismus besitzen, der erkennt, wann ein Knoten seinen Bereich fast ausgeschöpft hat, und mithilfe von DBCC CHECKIDENT einen neuen Bereich zuweisen. Sie können auch eine CHECK-Einschränkung hinzufügen, um sicherzustellen, dass keine Zeile hinzugefügt wird, wenn dies zum Verwenden eines außerhalb des Bereichs liegenden Identitätswerts führen würde.  
  
## <a name="handling-identity-ranges-after-a-database-restore"></a>Umgang mit Identitätsbereichen nach einer Datenbankwiederherstellung  
 Wenn Sie die automatische Identitätsbereichsverwaltung verwenden und ein Abonnent aus einer Sicherung wiederhergestellt wird, fordert dieser Abonnent automatisch einen neuen Bereich von Identitätswerten an. Wenn ein Verleger aus einer Sicherung wiederhergestellt wird, müssen Sie selbst sicherstellen, dass dem Verleger ein entsprechender Bereich zugewiesen wird. Für die Mergereplikation weisen Sie einen neuen Bereich mit [sp_restoremergeidentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-restoremergeidentityrange-transact-sql.md) zu. Bei Transaktionsreplikationen müssen Sie den höchsten Wert bestimmen, der verwendet wurde, und dann den Anfangspunkt für neue Bereiche festlegen. Gehen Sie nach dem Wiederherstellen der Veröffentlichungsdatenbank wie folgt vor:  
  
1.  Beenden Sie alle Aktivitäten auf allen Abonnenten.  
  
2.  Gehen Sie für jede veröffentlichte Tabelle, die eine Identitätsspalte enthält, wie folgt vor:  
  
    1.  Führen Sie in der Abonnementdatenbank auf jedem Abonnenten `IDENT_CURRENT('<TableName>')`aus.  
  
    2.  Notieren Sie sich den höchsten Wert, den Sie bei den Abonnenten gefunden haben.  
  
    3.  Führen Sie in der Veröffentlichungsdatenbank auf dem Verleger `DBCC CHECKIDENT(<TableName>','reseed',<HighestValueFound+1>`) aus.  
  
    4.  Führen Sie in der Veröffentlichungsdatenbank auf dem Verleger `sp_adjustpublisheridentityrange <PublicationName>, <TableName>`aus.  
  
    > [!NOTE]  
    >  Wenn für den Wert in der Identitätsspalte festgelegt wurde, dass er verringert statt vergrößert werden soll, notieren Sie sich den niedrigsten gefundenen Wert, und legen Sie diesen Wert dann als neuen Ausgangswert fest.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENTITY &#40;Eigenschaft&#41; &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md)  
  
  
