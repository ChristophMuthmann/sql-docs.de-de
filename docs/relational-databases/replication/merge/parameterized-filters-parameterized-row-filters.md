---
title: Parametrisierte Zeilenfilter |Microsoft Dokumentation
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
- publications [SQL Server replication], dynamic filters
- merge replication [SQL Server replication], dynamic filters
- parameterized filters [SQL Server replication]
- filters [SQL Server replication], dynamic
- merge replication parameterized filters [SQL Server replication]
- publications [SQL Server replication], parameterized filters
- parameterized filters [SQL Server replication], about parameterized filters
- filters [SQL Server replication], parameterized
- dynamic filters [SQL Server replication]
ms.assetid: b48a6825-068f-47c8-afdc-c83540da4639
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 334abcb537765b94212fb8a17a5459e85ebb967e
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="parameterized-filters---parameterized-row-filters"></a>Parametrisierte Filter – Parametrisierte Zeilenfilter
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mit parametrisierten Zeilenfiltern können verschiedene Datenpartitionen an verschiedene Abonnenten gesendet werden, ohne dass hierfür mehrere Veröffentlichungen erstellt werden müssen (parametrisierte Filter wurden in früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]als dynamische Filter bezeichnet). Der Begriff Partition bezeichnet nichts weiter als eine Teilmenge der Zeilen in einer Tabelle. Abhängig von den Einstellungen für den parametrisierten Zeilenfilter, die im Zuge der Erstellung des Filters festgelegt werden, kann jede Zeile in einer veröffentlichten Tabelle entweder nur zu einer Partition (nicht überlappende Partitionen) oder aber zu mehreren Partitionen (überlappende Partitionen) gehören.  
  
 Nicht überlappende Partitionen können für mehrere Abonnenten freigegeben werden, oder es kann einschränkend festgelegt werden, dass eine bestimmte Partition einem Abonnement zugewiesen wird. Die Einstellungen, mit denen das Verhalten der Partition gesteuert wird, werden weiter unten unter "Verwenden der richtigen Filteroptionen" erläutert. Mithilfe dieser Einstellungen können Sie die parametrisierten Filter an die jeweiligen Anwendungs- und Leistungsanforderungen anpassen. Allgemein gilt, dass überlappende Partitionen ein höheres Maß an Flexibilität ermöglichen, während nicht überlappende Partitionen, die nur für ein einzelnes Abonnement repliziert werden, eine höhere Leistungsfähigkeit aufweisen.  
  
 Parametrisierte Filter werden in einer einzelnen Tabelle verwendet und in der Regel mit Joinfiltern kombiniert, um auch verknüpfte Tabellen filtern zu können. Weitere Informationen finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
 Informationen zum Definieren oder Ändern eines parametrisierten Zeilenfilters finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
## <a name="how-parameterized-filters-work"></a>Funktionsweise parametrisierter Filter  
 Parametrisierte Zeilenfilter verwenden zum Auswählen der Daten, die veröffentlicht werden sollen, eine WHERE-Klausel. Statt in der Klausel einen Literalwert anzugeben (wie dies bei statischen Zeilenfiltern der Fall wäre), wird mindestens eine der folgenden Systemfunktionen angegeben: SUSER_SNAME() und HOST_NAME(). Darüber hinaus können auch benutzerdefinierte Funktionen verwendet werden, sofern diese in ihrem Hauptteil SUSER_SNAME() oder HOST_NAME() enthalten bzw. eine dieser Systemfunktionen auswerten (wie beispielsweise `MyUDF(SUSER_SNAME()`). Wenn eine benutzerdefinierte Funktion in ihrem Hauptteil SUSER_SNAME() oder HOST_NAME() enthält, können dieser Funktion keine Parameter übergeben werden.  
  
 Die SUSER_SNAME() und HOST_NAME()-Systemfunktionen können auch für andere Zwecke als die Mergereplikation verwendet werden, sie werden von dieser aber für das parametrisierte Filtern verwendet:  
  
-   SUSER_SNAME() gibt Anmeldeinformationen für Verbindungen mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zurück. Bei Verwendung in einem parametrisierten Filter wird der Anmeldename zurückgegeben, mit dessen Hilfe der Merge-Agent eine Verbindung mit dem Verleger herstellt (den Anmeldenamen müssen Sie beim Erstellen des Abonnements angeben).  
  
-   HOST_NAME() gibt den Namen des Computers zurück, der mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verbunden ist. Bei Verwendung in einem parametrisierten Filter gibt die Funktion standardmäßig den Namen des Computers zurück, auf dem der Merge-Agent ausgeführt wird. Bei Pullabonnements ist dies der Name des Abonnenten, während bei Pushabonnements der Name des Verteilers zurückgegeben wird.  
  
     Durch Eingabe eines anderen Wertes als den Namen des Abonnenten oder Verteilers kann diese Funktion überschrieben werden. In der Regel überschreiben Anwendungen diese Funktion mit sinnvolleren Werten, z. B. einem Vertriebsmitarbeiternamen oder einer Vertriebsmitarbeiter-ID. Weitere Informationen finden Sie im Abschnitt zu "Überschreiben des HOST_NAME()-Werts" weiter unten in diesem Thema.  
  
 Der Wert, der von der Systemfunktion zurückgegeben wird, wird mit der von Ihnen angegebenen Spalte in der gefilterten Tabelle verglichen. Danach werden die entsprechenden Daten auf den Abonnenten heruntergeladen. Dieser Vergleich erfolgt sowohl bei der Initialisierung des Abonnements (damit in der Anfangsmomentaufnahme nur die relevanten Daten enthalten sind) als auch bei jeder Abonnementsynchronisierung. Wenn eine Änderung auf dem Abonnenten dazu führt, dass eine Zeile aus einer Partition herausgenommen wird, wird diese Zeile standardmäßig auf dem Abonnenten gelöscht. (Dieses Verhalten kann mit dem **@allow_partition_realignment**-Parameter von [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) gesteuert werden.)  
  
> [!NOTE]  
>  Bei Vergleichen für parametrisierte Filter wird in jedem Fall die Datenbanksortierung verwendet. Wenn die Datenbanksortierung z. B. ohne Unterscheidung von Groß- und Kleinschreibung erfolgt, die Tabellen- oder Spaltensortierung dagegen mit, wird beim Vergleich nicht zwischen Groß-/Kleinschreibung unterschieden.  
  
### <a name="filtering-with-susersname"></a>Filtern mit SUSER_SNAME()  
 Sehen Sie sich die **Employee-Tabelle** in der [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] -Beispieldatenbank an. Diese Tabelle enthält die **LoginID**-Spalte, in der Sie die Domäne und den Anmeldenamen (Anmelde-ID) für jeden Mitarbeiter in der Form*domain\login*finden. Wenn Sie diese Tabelle so filtern möchten, dass alle Mitarbeiter nur die Daten erhalten, die für sie jeweils relevant sind, geben Sie folgende Filterklausel an:  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 Nehmen wir z. B. an, der Wert für einen der Mitarbeiter ist 'adventure-works\john5'. Wenn der Merge-Agent eine Verbindung mit dem Verleger herstellt, verwendet dieser den Anmeldenamen, den Sie bei der Erstellung des Abonnements angegeben haben (in diesem Fall 'adventure-works\john5'). Der Merge-Agent vergleicht dann den von SUSER_SNAME() zurückgegebenen Wert mit den Werten in der Tabelle und lädt nur die Zeile herunter, die in der **LoginID** -Spalte den Wert 'adventure-works\john5' enthält.  
  
### <a name="filtering-with-hostname"></a>Filtern mit HOST_NAME()  
 Sehen Sie sich die **HumanResources.Employee** -Tabelle an. Nehmen wir an, diese Tabelle enthält eine **ComputerName** -Spalte, in der die Namen der Computer der einzelnen Mitarbeiter aufgeführt sind. Die Einträge weisen die Form '*name_computertype*' auf. Wenn Sie diese Tabelle so filtern möchten, dass alle Mitarbeiter nur die Daten erhalten, die für sie jeweils relevant sind, geben Sie folgende Filterklausel an:  
  
```  
ComputerName = HOST_NAME()  
```  
  
 Nehmen wir z. B. an, der Wert für einen der Mitarbeiter ist 'john5_laptop'. Wenn der Merge-Agent eine Verbindung mit dem Verleger hergestellt hat, vergleicht er den von HOST_NAME() zurückgegebenen Wert mit den Werten in der Tabelle und lädt nur die Zeile herunter, die in der **ComputerName** -Spalte den Wert 'john5_laptop' enthält.  
  
 Die beiden Funktionen können zu Filterzwecken auch kombiniert werden. Wenn Sie beispielsweise sicherstellen möchten, dass ein Mitarbeiter nur dann Daten erhält, wenn er sich mit seinem Anmeldenamen auf seinem Computer angemeldet hat, könnte folgende Filterklausel eingerichtet werden:  
  
```  
LoginID = SUSER_SNAME() AND ComputerName = HOST_NAME()  
```  
  
 Sofern Sie nicht den HOST_NAME()-Wert überschreiben, wird das Filtern mit HOST_NAME() in der Regel nur bei Pullabonnements verwendet. Die Funktion gibt den Namen des Computers zurück, auf dem der Merge-Agent ausgeführt wird. Bei Pullabonnements ist dieser Wert für jedes Abonnement anders. Im Falle der Pushabonnements bleibt der Wert jedoch immer gleich, weil bei diesem Abonnementtyp alle Merge-Agents auf dem Verteiler ausgeführt werden.  
  
> [!IMPORTANT]  
>  Der Wert für die HOST_NAME()-Funktion kann überschrieben werden. Daher können Filter, die HOST_NAME() enthalten, nicht für die Steuerung des Zugriffs auf Datenpartitionen verwendet werden. Für die Steuerung des Zugriffs auf Datenpartitionen sollten Sie daher SUSER_SNAME(), SUSER_SNAME() in Kombination mit HOST_NAME() oder statische Zeilenfilter verwenden.  
  
#### <a name="overriding-the-hostname-value"></a>Überschreiben des HOST_NAME()-Wertes  
 Wie bereits erwähnt, gibt HOST_NAME() den Namen des Computers zurück, der eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]herstellt. Bei der Verwendung parametrisierter Filter wird dieser Wert häufig überschrieben, indem bei der Abonnementerstellung ein anderer Wert angegeben wird. Daraufhin wird durch die HOST_NAME()-Funktion nicht der Name des Computers, sondern der von Ihnen angegebene Wert zurückgegeben.  
  
> [!NOTE]  
>  Wenn Sie HOST_NAME() überschreiben, wird für sämtliche Aufrufe der HOST_NAME()-Funktion der von Ihnen angegebene Wert zurückgegeben. Stellen Sie sicher, dass keine andere Anwendung darauf angewiesen ist, dass HOST_NAME() den Computernamen zurückgibt.  
  
 Sehen Sie sich die **HumanResources.Employee** -Tabelle an. Diese Tabelle enthält die **EmployeeID**-Spalte. Wenn Sie diese Tabelle so filtern möchten, dass jeder Mitarbeiter nur die Daten erhält, die für ihn relevant sind, geben Sie folgende Filterklausel an:  
  
 `EmployeeID = CONVERT(int,HOST_NAME())`  
  
 Der Mitarbeiterin Pamela Ansman-Wolfe wurde z. B. eine Mitarbeiter-ID von 280 zugewiesen. Geben Sie bei der Erstellung eines Abonnements für diese Mitarbeiterin als Wert für HOST-NAME() die Mitarbeiternummer (hier: 280) an. Wenn der Merge-Agent eine Verbindung mit dem Verleger hergestellt hat, vergleicht er den von HOST_NAME() zurückgegebenen Wert mit den Werten in der Tabelle und lädt nur die Zeile herunter, bei der der Wert 280 in der **EmployeeID** -Spalte enthalten ist.  
  
> [!IMPORTANT]  
>  Die HOST_NAME()-Funktion gibt einen **nchar** -Wert zurück, sodass Sie CONVERT verwenden müssen, wenn es sich bei der Spalte in der Filterklausel um eine numerische Spalte handelt (wie im Beispiel oben). Zur Verbesserung der Leistung sollten Funktionen nicht auf Spaltennamen in Klauseln für parametrisierte Zeilenfilter (wie `CONVERT(nchar,EmployeeID) = HOST_NAME()`) angewendet werden. Gehen Sie stattdessen wie im folgenden Beispiel vor: `EmployeeID = CONVERT(int,HOST_NAME())`. Diese Klausel kann zwar für den **@subset_filterclause** -Parameter von [@subset_filterclause](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)verwendet werden, in der Regel aber nicht im Assistenten für neue Veröffentlichung. (Der Assistent führt die Filterklausel aus, um sie zu überprüfen, erhält dabei aber ein negatives Ergebnis, weil der Computername nicht in einen **int**als dynamische Filter bezeichnet). Wenn Sie mit dem Assistenten für neue Veröffentlichung arbeiten, sollten Sie vor dem Erstellen einer Momentaufnahme für die Veröffentlichung `CONVERT(nchar,EmployeeID) = HOST_NAME()` im Assistenten angeben und dann [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) verwenden, um die Klausel in `EmployeeID = CONVERT(int,HOST_NAME())` zu ändern.  
  
 **So überschreiben Sie den HOST_NAME()-Wert**  
  
 Verwenden Sie zum Überschreiben des Wertes für HOST_NAME() eine der folgenden Methoden:  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: Geben Sie auf der Seite **HOST\_NAME\(\)-Werte** des Assistenten für neue Abonnements einen Wert an. Weitere Informationen zum Erstellen von Abonnements finden Sie unter [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Replikationsprogrammierung mit [!INCLUDE[tsql](../../../includes/tsql-md.md)]: Geben Sie für den **@hostname**-Parameter von [sp_addmergesubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) (bei Pushabonnements) oder von [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (bei Pullabonnements) einen Wert an.  
  
-   Merge-Agent: Geben Sie in der Befehlszeile oder per Agent-Profil einen Wert für den Parameter **-Hostname** an. Weitere Informationen zum Merge-Agent finden Sie unter [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md). Weitere Informationen zu Agentprofilen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="initializing-a-subscription-to-a-publication-with-parameterized-filters"></a>Initialisieren von Veröffentlichungsabonnements mit parametrisierten Filtern  
 Wenn parametrisierte Zeilenfilter in Mergeveröffentlichungen verwendet werden, wird jedes Abonnement bei der Replikation mit einer zweiteiligen Momentaufnahme initialisiert. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## <a name="using-the-appropriate-filtering-options"></a>Verwenden der richtigen Filteroptionen  
 Bei der Verwendung von parametrisierten Filtern können Sie die folgenden beiden Schlüsselbereiche steuern:  
  
-   Sie können festlegen, wie die Filter durch die Mergereplikation verarbeitet werden. Dazu stehen zwei Veröffentlichungseinstellungen zur Verfügung: **use partition groups** und **keep partition changes**.  
  
-   Sie können steuern, wie die Daten auf die einzelnen Abonnenten aufgeteilt werden. Dies muss sich in der Artikeleinstellung **partition options**widerspiegeln.  
  
 Informationen zum Festlegen von Filteroptionen finden Sie unter [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md).  
  
### <a name="setting-use-partition-groups-and-keep-partition-changes"></a>Festlegen von 'use partition groups' und 'keep partition changes'  
 Die Optionen **use partition groups** und **keep partition changes** verbessern bei Veröffentlichungen mit gefilterten Artikeln die Synchronisierungsleistung, da in der Veröffentlichungsdatenbank zusätzliche Metadaten gespeichert werden. Da die Option **use partition groups** auf vorausberechnete Partitionen zurückgreift, bietet sie das größere Potenzial für eine Leistungserhöhung. Diese Option ist standardmäßig auf **true** festgelegt, wenn die Artikel in Ihrer Veröffentlichung einem Satz von Anforderungen entsprechen. Weitere Informationen zu diesen Anforderungen finden Sie unter [Optimieren der Leistung parametrisierter Filter mithilfe vorausberechneter Partitionen](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md). Wenn die Anforderungen für die Verwendung vorausberechneter Partitionen von Ihren Artikeln nicht erfüllt werden, wird die Option **keep partition changes** auf **true**festgelegt.  
  
### <a name="setting-partition-options"></a>Festlegen von 'partition options'  
 Der Wert für die **partition options** -Eigenschaft wird angegeben, wenn Sie einen Artikel erstellen. Ausschlaggebend für den Wert ist dabei die Art und Weise, wie die Daten in der gefilterten Tabelle für mehrere Abonnenten freigegeben werden. Die Eigenschaft kann mithilfe von [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)und dem Dialogfeld **Artikeleigenschaften** auf einen von vier Werten festgelegt werden. Wird das Dialogfeld **Filter hinzufügen** oder **Filter bearbeiten** verwendet, kann aus zwei Werten ausgewählt werden. Diese beiden Dialogfelder stehen über den Assistenten für neue Veröffentlichung und das Dialogfeld **Veröffentlichungseigenschaften** zur Verfügung. Die folgende Tabelle gibt einen Überblick über die verfügbaren Werte für diese Eigenschaft:  
  
|Description|Wert in Filter hinzufügen und Filter bearbeiten|Wert in Artikeleigenschaften|Wert in gespeicherten Prozeduren|  
|-----------------|-----------------------------------------|---------------------------------|--------------------------------|  
|Daten in den Partitionen überlappen sich. Der Abonnent kann die Spalten, auf die im parametrisierten Filter verwiesen wird, aktualisieren.|**Eine Zeile aus dieser Tabelle wird an mehrere Abonnements gesendet**|**Überlappend**|**0**|  
|Daten in den Partitionen überlappen sich. Der Abonnent kann die Spalten, auf die in parametrisierten Filtern verwiesen wird, nicht aktualisieren.|Nicht zutreffend*|**Überlappend, Datenänderungen außerhalb der Partition nicht zulassen**|**1**|  
|Daten in den Partitionen überlappen sich nicht. Die Daten werden für die Abonnements freigegeben. Der Abonnent kann Spalten, auf die in einem parametrisierten Filter verwiesen wird, nicht aktualisieren.|Nicht zutreffend*|**Nicht überlappend, für mehrere Abonnements freigegeben**|**2**|  
|Daten in den Partitionen überlappen sich nicht. Jeder Partition ist genau ein Abonnement zugewiesen. Der Abonnent kann Spalten, auf die in einem parametrisierten Filter verwiesen wird, nicht aktualisieren.**|**Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**|**Nicht überlappend, ein Abonnement**|**3**|  
  
 \*Wenn die zugrunde liegende Filteroption auf den Wert **0**, **1** oder **2** festgelegt ist, wird in den Dialogfeldern **Filter hinzufügen** und **Filter bearbeiten** die Meldung **Eine Zeile aus dieser Tabelle wird an mehrere Abonnements gesendet** angezeigt.  
  
 **Wenn Sie diese Option angeben, gibt es für jede Datenpartition im Artikel genau ein Abonnement. Wird ein zweites Abonnement erstellt, in dem das Filterkriterium des neuen Abonnements die gleiche Partition ergibt wie das vorhandene Abonnement, wird das vorhandene Abonnement gelöscht.  
  
> [!IMPORTANT]  
>  Der Wert für **partition options** muss sich danach richten, wie die Daten für mehrere Abonnenten freigegeben werden. Wenn Sie beispielsweise für eine Partition angeben, dass sie nicht überlappend und nur einem spezifischen Abonnenten zugewiesen sein soll, die Daten dann aber von einem anderen Abonnenten aktualisiert werden, kann dies zu einem Fehlschlagen der Synchronisierung des Merge-Agents und zu einer Nichtkonvergenz führen.  
  
#### <a name="selecting-the-appropriate-partition-option"></a>Auswählen der richtigen Partitionsoption  
 Nicht überlappende Partitionen arbeiten mit vorausberechneten Partitionen zusammen, um dort, wo einige funktionale Einschränkungen akzeptabel sind, die Leistung zu verbessern. Die vorausberechneten Partitionen beschleunigen Downloads auf Abonnenten, verlangsamen aber Uploads. Nicht überlappende Partitionen minimieren die bei vorausberechneten Partitionen entstehenden Uploadkosten. Die Leistungsvorteile nicht überlappender Partitionen treten deutlicher hervor, wenn die verwendeten parametrisierten Filter und Joinfilter komplexer sind.  
  
 Die folgenden Szenarien sollen veranschaulichen, welche Partitionsoptionen in einer Veröffentlichung ausgewählt werden sollten.  
  
-   [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] unterhält einen mobilen Außendienst, wobei die Vertreter jeweils für einen bestimmten Postleitzahlenbereich zuständig sind. Die Anwendung soll in der Lage sein, bei Umzügen von Kunden von einem Postleitzahlenbereich in einen anderen die Kundenpostleitzahl so zu aktualisieren, dass der Kunde einem anderen Vertreter zugewiesen wird. Der parametrisierte Filter basiert auf der Postleitzahl des Kunden. Das Update führt dazu, dass die Postleitzahl aus der Partition des früheren Vertreters entfernt und in die Partition des neuen Vertreters eingefügt wird. Dafür sind überlappende Partitionen mit der Möglichkeit erforderlich, Spalten zu aktualisieren, auf die im parametrisierten Filter verwiesen wird. Diese Option bietet ein Höchstmaß an Flexibilität, führt aber im Vergleich zu nicht überlappenden Partitionen zu Einbußen bei der Leistung.  
  
-   Eine Arbeitsvermittlung verfügt über Daten, die an die untergeordneten Behörden in den einzelnen Landkreisen verteilt werden sollen. Die Daten sind nicht überlappend, d. h., jede Zeile in der Tabelle in der Landeszentrale gehört nur zu einer Partition, diese Partition wird aber an mehrere Außenstellen im selben Landkreis gesendet. In diesem Fall empfiehlt sich die Verwendung von nicht überlappenden Partitionen, die für mehrere Abonnements freigegeben werden. Dies ermöglicht eine höhere Leistung als bei überlappenden Partitionen, ohne dass dabei Abstriche an der Erfüllung der Anwendungsanforderungen gemacht werden müssen.  
  
-   Wenn Sie nicht überlappende Partitionen haben und nur ein Abonnent die Daten in der Partition empfängt und aktualisiert, lassen sich weitere Leistungsverbesserungen erzielen. Dieses Szenario ist beispielsweise für Point-of-Sale-Systeme und Außendienstanwendungen typisch, in denen Daten vor allem auf dem Abonnenten erfasst und zum Verleger hochgeladen werden. Angenommen, in einer Außendienstanwendung ist eine **Package** -Tabelle vorhanden: Jedes Mal, wenn ein Paket auf einen LKW verladen wird, wird der Status des Pakets in der **Package** -Tabelle entsprechend geändert, und die Änderung wird an die Zentrale zurückrepliziert. Da der Status ein und desselben Pakets nicht auf zwei unterschiedlichen LKWs aktualisiert werden wird, eignet sich die **Package** -Tabelle hervorragend für eine nicht überlappende Partition mit einem Abonnenten pro Partition.  
  
#### <a name="considerations-for-nonoverlapping-partitions"></a>Überlegungen zu nicht überlappenden Partitionen  
 Beachten Sie bei der Verwendung von nicht überlappenden Partitionen Folgendes:  
  
##### <a name="general-considerations"></a>Allgemeine Überlegungen  
  
-   Die Veröffentlichung muss vorausberechnete Partitionen verwenden.  
  
-   Jede Zeile darf nur zu einer einzigen Partition gehören.  
  
-   Artikel dürfen nicht Teil logischer Datensätze sein.  
  
-   Alternative Synchronisierungspartner werden nicht unterstützt (diese Funktion ist als veraltet markiert).  
  
-   Der Abonnent kann Spalten, auf die in einem parametrisierten Filter verwiesen wird, nicht aktualisieren.  
  
-   Wenn eine Einfügung bei einem Abonnenten nicht zur Partition gehört, wird sie nicht gelöscht. Sie wird aber auch nicht auf die anderen Abonnenten repliziert.  
  
-   In einigen Fällen kann es bei überlappenden Partitionen passieren, dass Identitätsbereiche angepasst werden, wenn der Merge-Agent Daten einfügt. Bei nicht überlappenden Partitionen können Bereiche nur während des Einfügens durch einen Benutzer angepasst werden, der zur Anpassung von Identitätsbereichen in der Abonnementdatenbank berechtigt ist. Der Benutzer muss die Tabelle besitzen oder Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrolle **db_owner** oder **db_ddladmin** sein.  
  
##### <a name="additional-considerations-for-nonoverlapping-partitions-with-a-single-subscription-per-partition"></a>Zusätzliche Überlegungen für nicht überlappende Partitionen mit einem Abonnenten pro Partition  
  
-   Artikel können immer nur in einer Veröffentlichung vorhanden sein. Ein erneutes Veröffentlichen ist nicht möglich.  
  
-   Die Veröffentlichung muss das Initiieren des Momentaufnahmeprozesses durch Abonnenten zulassen. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
##### <a name="additional-considerations-for-join-filters"></a>Zusätzliche Überlegungen zu Joinfiltern  
  
-   Artikel mit einer überlappenden Partition dürfen in Joinfilterhierarchien nicht oberhalb von Artikeln mit einer nicht überlappenden Partition angezeigt werden. Anders ausgedrückt: Ein übergeordneter Artikel muss nicht überlappende Partitionen verwenden, wenn dies für den untergeordneten Artikel zutrifft. Informationen zu Joinfiltern finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Bei Joinfiltern, in denen die nicht überlappende Partition untergeordnet ist, muss für die **join unique key** -Eigenschaft der Wert 1 festgelegt sein. Weitere Informationen finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Der Artikel sollte nur einen einzigen parametrisierten Filter bzw. Joinfilter aufweisen. Ein Artikel darf einen parametrisierten Filter aufweisen und gleichzeitig in einem Joinfilter übergeordnet sein. Hingegen ist es nicht möglich, dass ein Artikel einen parametrisierten Filter aufweist und gleichzeitig in einem Joinfilter untergeordnet ist. Darüber hinaus darf der Artikel nicht über mehrere Joinfilter verfügen.  
  
-   Wenn zwei Tabellen auf dem Abonnenten über eine Joinfilterbeziehung verfügen und die untergeordnete Tabelle Zeilen enthält, für die es in der übergeordneten Tabelle keine entsprechende Zeile gibt, führt das Einfügen der fehlenden übergeordneten Zeile nicht dazu, dass die zugehörigen Zeilen auf den Abonnenten heruntergeladen werden (bei überlappenden Partitionen würde ein Download erfolgen). Wenn z. B. die **SalesOrderDetail** -Tabelle über Zeilen ohne zugehörige Zeile in der **SalesOrderHeader** -Tabelle verfügt und Sie die fehlende Zeile in **SalesOrderHeader**einfügen, wird zwar die Zeile auf dem Abonnenten heruntergeladen, nicht aber die zugehörigen Zeilen in **SalesOrderDetail** .  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Bewährte Methoden für zeitbasierte Zeilenfilter](../../../relational-databases/replication/merge/best-practices-for-time-based-row-filters.md)   
 [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtern veröffentlichter Daten für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
