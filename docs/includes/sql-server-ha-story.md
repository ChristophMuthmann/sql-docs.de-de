Dieser Artikel bietet eine Übersicht über Lösungen für Geschäftskontinuität für Hochverfügbarkeit und Notfallwiederherstellung in SQL Server. 

Eine allgemeine Aufgabe, die jeder berücksichtigen sollte, der SQL Server bereitstellt, ist das Sicherstellen der Verfügbarkeit aller unternehmenskritischen SQL Server-Instanzen und der darin enthaltenen Datenbanken, wenn das Unternehmen oder die Benutzer diese benötigen, ob von 9 bis 17 Uhr oder rund um die Uhr. Das Ziel ist, das Unternehmen mit minimaler oder ohne Unterbrechung aufrechtzuerhalten. Dieses Konzept wird auch als Geschäftskontinuität bezeichnet.

In SQL Server 2017 werden viele neue Funktionen oder Erweiterungen für vorhandene eingeführt, einige davon sind für die Verfügbarkeit. Die wichtigste Erweiterung für SQL Server 2017 ist die Unterstützung für SQL Server auf Linux-Verteilungen. Eine vollständige Liste der neuen Funktionen in SQL Server 2017 finden Sie unter [Neues in SQL Server 2017](http://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017).

Dieser Artikel konzentriert sich auf die Verfügbarkeitsszenarios sowie auf die neuen und erweiterten Verfügbarkeitsfunktionen in SQL Server 2017. Dabei sind auch hybride Szenarios enthalten, durch die SQL Server-Bereitstellungen Windows Server und Linux umfassen können sowie Szenarios, die die Anzahl von lesbaren Kopien einer Datenbank erhöhen können. Dieser Artikel behandelt keine Verfügbarkeitsoptionen außerhalb von SQL Server, z.B. solche, die durch die Virtualisierung bereitgestellt werden. Sämtliche Erläuterungen beziehen sich auf Installationen von SQL Server innerhalb eines virtuellen Gastcomputers, der sich entweder in der öffentlichen Cloud befindet oder von einem lokalen Hypervisorserver gehostet wird.

## <a name="sql-server-2017-scenarios-using-the-availability-features"></a>SQL Server 2017-Szenarios, die Verfügbarkeitsfunktionen verwenden

Verfügbarkeitsgruppen, FCIs und der Protokollversand können auf verschiedene Arten verwendet werden und nicht nur aus Gründen der Verfügbarkeit. Verfügbarkeitsfunktionen können auf vier verschiedene Arten verwendet werden:

* Hohe Verfügbarkeit
* Notfallwiederherstellung
* Migrationen und Upgrades
* Horizontales Hochskalieren von lesbaren Kopien von einer oder mehreren Datenbanken

In jedem Abschnitt werden die relevanten Funktionen erläutert, die für ein bestimmtes Szenario verwendet werden können. Die einzige Funktion, die nicht behandelt wird, ist die [SQL Server-Replikation](http://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication). Diese ist nicht offiziell als Verfügbarkeitsfunktion von Always On festgelegt, sie wird jedoch häufig verwendet, um Daten in bestimmten Szenarios überflüssig zu machen. Die Replikation wird in einer zukünftigen Version zu SQL Server unter Linux hinzugefügt.

> [!IMPORTANT] 
> Die SQL Server-Verfügbarkeitsfunktionen ersetzen keine stabile, gut getestete Sicherungs- und Wiederherstellungsstrategie, bei der es sich um den grundlegendsten Baustein jeder Verfügbarkeitslösung handelt.

### <a name="high-availability"></a>Hohe Verfügbarkeit

Es ist wichtig, sicherzustellen, dass SQL Server-Instanzen oder -Datenbanken im Fall eines lokalen Problems eines Rechenzentrums oder einer einzelnen Region in der Cloudregion verfügbar sind. Dieser Abschnitt erläutert, wie die SQL Server-Verfügbarkeitsfunktionen Sie bei dieser Aufgabe unterstützen können. Alle beschriebenen Funktionen sind für Windows Server und Linux verfügbar. 

#### <a name="always-on-availability-groups"></a>Always On-Verfügbarkeitsgruppen

Die in SQL Server 2012 eingeführten Always On-Verfügbarkeitsgruppen (Verfügbarkeitsgruppen) stellen Schutz auf Datenbankebene bereit, indem sie jede Transaktion einer Datenbank zu einer anderen Instanz (auch als Replikat bezeichnet) senden, die eine Kopie dieser Datenbank in einem speziellen Zustand enthält. Eine Verfügbarkeitsgruppe kann auf der Standard Edition oder Enterprise Edition bereitgestellt werden.  Die Instanzen, die in einer Verfügbarkeitsgruppe enthalten sind, können eigenständig oder Always On-Failoverclusterinstanzen (FCIs, im nächsten Abschnitt beschrieben) sein. Da die Transaktionen direkt an ein Replikat gesendet werden, werden Verfügbarkeitsgruppen empfohlen, wenn Anforderungen für niedrigere Ziele bei Wiederherstellungspunkten und der Wiederherstellungszeit bestehen. Das Verschieben von Daten zwischen Replikaten kann synchron oder asynchron erfolgen. Die Enterprise Edition unterstützt bis zu drei synchrone Replikate, einschließlich des primären Replikats. Eine Verfügbarkeitsgruppe enthält eine vollständige Lese-/Schreibkopie der Datenbank, die sich auf dem primären Replikat befindet. Sekundäre Replikate können keine Transaktionen direkt von Benutzern oder Anwendungen erhalten. 

> [!NOTE] 
> Always On ist ein Überbegriff für die Verfügbarkeitsfunktionen in SQL Server und schließt Verfügbarkeitsgruppen und FCIs ein. Always On ist nicht der Name der Verfügbarkeitsgruppenfunktion.

Da Verfügbarkeitsgruppen nur Schutz auf Datenbankebene bereitstellen, nicht auf Instanzebene, muss alles, was nicht im Transaktionsprotokoll erfasst oder in der Datenbank konfiguriert ist, für jedes sekundäre Replikat manuell synchronisiert werden. Einige Beispiele für Objekte, die manuell synchronisiert werden müssen, sind Anmeldungen auf Instanzebene, Verbindungsserver und SQL Server-Agent-Aufträge.

Eine Verfügbarkeitsgruppe besitzt eine weitere Komponente, die als Listener bezeichnet wird. Durch diesen können Anwendungen und Benutzer eine Verbindung herstellen, ohne zu wissen, welche Instanz von SQL Server das primäre Replikat hostet. Jede Verfügbarkeitsgruppe muss ihren eigenen Listener besitzen. Während die Implementierungen des Listeners sich geringfügig zwischen Windows Server und Linux unterscheiden, sind die bereitgestellte Funktionalität und die Verwendung identisch. Die untenstehende Abbildung zeigt eine Windows Server-basierte Verfügbarkeitsgruppe, die ein Windows Server-Failovercluster (WSFC) verwendet. Ein zugrunde liegender Cluster auf OS-Ebene ist für die Verfügbarkeit auf Linux oder Windows Server erforderlich. Dieses Beispiel zeigt eine einfache Konfiguration für zwei Server oder Knoten, bei der ein WSFC den zugrunde liegenden Cluster darstellt. 

![Einfache Verfügbarkeitsgruppe][SimpleAG]
 
Bei Replikaten besitzen die Standard Edition und die Enterprise Edition unterschiedliche Höchstwerte. Eine Verfügbarkeitsgruppe in der Standard Edition, die als Basis-Verfügbarkeitsgruppe bezeichnet wird, unterstützt zwei Replikate (ein primäres und ein sekundäres) mit nur einer einzigen Datenbank in der Verfügbarkeitsgruppe. In der Enterprise Edition können nicht nur mehrere Datenbanken für eine einzige Verfügbarkeitsgruppe konfiguriert werden, sondern es können auch bis zu neun Replikate (ein primäres, acht sekundäre) vorhanden sein. Die Enterprise Edition bietet weitere optionale Vorteile, z.B. lesbare sekundäre Replikate, das Erstellen von Sicherungen aus einem sekundären Replikat usw.

>[!NOTE]
> Die Datenbankspiegelung, die seit SQL Server 2012 veraltet ist, ist nicht für die Linux-Version von SQL Server verfügbar und wird nicht hinzugefügt. Kunden, die die Datenbankspiegelung immer noch verwenden, sollten die Migration zu Verfügbarkeitsgruppen planen, die den Ersatz für die Datenbankspiegelung darstellen.

Verfügbarkeitsgruppen stellen für die Verfügbarkeit entweder automatische oder manuelle Failover bereit. Automatische Failover können auftreten, wenn die synchrone Datenverschiebung konfiguriert ist und die Datenbank auf dem primären und sekundären Replikat sich in einem synchronisierten Zustand befindet. Solange der Listener verwendet wird und die Datenbank eine höhere Version von .NET (3.5 mit einem Update oder 4.0 und höher) verwendet, sollte das Failover mit minimaler oder ohne Auswirkungen für den Benutzer behandelt werden. Ein Failover, das ein sekundäres Replikat zum neuen primären Replikat macht, kann als automatisch oder manuell konfiguriert werden und wird im Allgemeinen in Sekunden gemessen.

Die folgende Liste hebt einige Unterschiede von Verfügbarkeitsgruppen zwischen Windows Server und Linux hervor:
* Da die zugrunde liegenden Cluster unterschiedlich unter Linux und Windows Server funktionieren, werden alle Failover (manuell oder automatisch) von Verfügbarkeitsgruppen über den Cluster unter Linux ausgeführt. Bei Bereitstellungen von Windows Server-basierten Verfügbarkeitsgruppen müssen manuelle Failover über SQL Server ausgeführt werden. Automatische Failover werden unter Windows Server und Linux von den zugrunde liegenden Clustern behandelt. 
* Die empfohlene Konfiguration für Verfügbarkeitsgruppen in SQL Server 2017 unter Linux umfasst mindestens drei Replikate. Der Grund dafür liegt in der Funktionsweise des zugrunde liegenden Clusterings. Eine verbesserte Lösung für die Konfiguration mit zwei Replikaten wird nach der Veröffentlichung bereitgestellt.
* Unter Linux wird der allgemeine Name, der von jedem Listener verwendet wird, im DNS und nicht wie unter Windows Server im Cluster definiert.

In SQL Server 2017 gibt es einige neue Funktionen und Erweiterungen für Verfügbarkeitsgruppen:

* Clustertypen
* REQUIRED_SECONDARIES_TO_COMMIT
* Erweiterte MS DTC-Unterstützung (Microsoft Distributed Transaction Coordinator) für Windows Server-basierte Konfigurationen
* Zusätzliche Szenarios für horizontales Hochskalieren von schreibgeschützten Datenbanken (später in diesem Artikel beschrieben)

##### <a name="always-on-availability-group-cluster-types"></a>Clustertypen von Always On-Verfügbarkeitsgruppen

Das integrierte Verfügbarkeitsformular des Clusterings in Windows Server wird über eine Funktion namens Failoverclustering aktiviert. Dadurch kann ein WSFC erstellt werden, das mit einer Verfügbarkeitsgruppe oder einer FCI verwendet werden kann. Die Integration von Verfügbarkeitsgruppen und FCIs wird über clusterfähige Ressourcen-DLLs bereitgestellt, die in SQL Server enthalten sind. 

Jede unterstützte Linux-Verteilung enthält ihre eigene Version der Pacemaker-Clusterlösung. SQL Server 2017 unter Linux unterstützt die Verwendung von Pacemaker. Bei Pacemaker handelt es sich um eine Open Stack-Lösung, in die sich jede Verteilung mit ihrem Stapel integrieren kann. Obwohl die Verteilungen Pacemaker enthalten, ist es nicht so integriert wie die Failoverclusteringfunktion unter Windows Server.

Zwischen WSFC und Pacemaker liegen mehr Gemeinsamkeiten als Unterschiede vor. Beide ermöglichen das Kombinieren von einzelnen Servern in einer Konfiguration, um die Verfügbarkeit zu gewährleisten und enthalten Konzepte für Ressourcen, Einschränken (die jedoch unterschiedlich implementiert sind), Failover usw. Microsoft stellt für das Bereitstellen von Pacemaker für Verfügbarkeitsgruppen- und FCI-Konfigurationen, einschließlich des automatischen Failovers, das Paket „mssql-server-ha package“ bereit, das der Ressourcen-DLL in einem WSFC ähnelt, aber nicht identisch mit diesem ist. Einer der Unterschiede zwischen einem WSFC und Pacemaker ist, dass es keine Netzwerknamenressource in Pacemaker gibt. Diese Komponente unterstützt Sie beim Abstrahieren des Namens des Listeners (oder des Namens der FCI) auf einem WSFC. DNS stellt diese Namensauflösung unter Linux bereit.

Aufgrund der Unterschiede im Clusterstapel müssen einige Änderungen für Verfügbarkeitsgruppen vorgenommen werden, da SQL Server einige der Metadaten behandeln muss, die nativ von einem WSFC behandelt werden. Die wichtigste [!IMPORTANT] Änderung ist die Einführung eines Clustertyps für Verfügbarkeitsgruppen. Dieser wird in „sys.availability_groups“ in den Spalten „cluster_type“ und „cluster_type_desc“ gespeichert. Es gibt drei Clustertypen:

* WSFC 
* Extern
* Keine

Alle Verfügbarkeitsgruppen, die Verfügbarkeit erfordern, müssen einen zugrunde liegenden Cluster verwenden. Dies ist im Fall von SQL Server 2017 ein WSFC oder Pacemaker. Für Windows Server-basierte Verfügbarkeitsgruppen, die einen zugrunde liegenden WSFC verwenden, ist der Standardclustertyp WSFC und muss nicht festgelegt werden. Für Linux-basierte Verfügbarkeitsgruppen muss der Clustertyp beim Erstellen der Verfügbarkeitsgruppe auf „Extern“ festgelegt werden. Die Integration mit Pacemaker wird nach der Erstellung der Verfügbarkeitsgruppe konfiguriert, während dies bei einem WSFC während der Erstellungszeit geschieht.

Der Clustertyp „Keiner“ kann für Windows Server- und Linux-Verfügbarkeitsgruppen verwendet werden. Das Festlegen des Clustertyps auf „Keiner“ bedeutet, dass die Verfügbarkeitsgruppe keinen zugrunde liegenden Cluster erfordert. Das bedeutet, dass es sich bei SQL Server 2017 um die erste Version von SQL Server handelt, die Verfügbarkeitsgruppen ohne einen Cluster unterstützen. Der Nachteil hierbei ist jedoch, dass diese Konfiguration nicht als Hochverfügbarkeitslösung unterstützt wird. 

> [!IMPORTANT] 
> SQL Server 2017 lässt die Änderung des Clustertyps einer Verfügbarkeitsgruppe nicht zu, nachdem diese erstellt ist. Das bedeutet, dass eine Verfügbarkeitsgruppe nicht von „Keiner“ zu „Extern“ oder „WSFC“ (oder umgekehrt) umgeschaltet werden kann. 

Für diejenigen, die nur eine zusätzliche schreibgeschützte Kopie einer Datenbank hinzufügen oder festlegen möchten, welche Optionen eine Verfügbarkeitsgruppe für die Migration/Upgrades bereitstellt, aber nicht an die zusätzliche Komplexität eines zugrunde liegenden Clusters oder der Replikation gebunden sein möchten, ist eine Verfügbarkeitsgruppe mit dem Clustertyp „Keiner“ eine ideale Lösung. Weitere Informationen finden Sie in den Abschnitten [Migrations and Upgrades (Migrationen und Upgrades)](#Migrations) und [Read Scale-out (Schreibgeschützte horizontale Skalierung)](#ReadScaleOut). 

Der folgende Screenshot zeigt die Unterstützung für die verschiedenen Arten von Clustertypen in SSMS. Sie müssen Version 17.1 oder höher ausführen. Der folgende Screenshot stammt aus Version 17.2.

![SSMS AG-Optionen][SSMSAGOptions]
 
##### <a name="requiredsynchronizedsecondariestocommit"></a>REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT

In SQL Server 2016 wurde die Unterstützung für die Anzahl von synchronen Replikaten in der Enterprise Edition von zwei auf drei erhöht. Wenn jedoch ein sekundäres Replikat synchronisiert wurde und bei einem anderen ein Problem auftrat, konnte das Verhalten nicht gesteuert werden, um dem primären Replikat mitzuteilen, entweder auf das sich falsch verhaltende Replikat zu warten oder fortzufahren. Dadurch erhält das primäre Replikat ab einem bestimmten Punkt weiterhin Schreibdatenverkehr, obwohl das sekundäre Replikat sich nicht in einem synchronisierten Zustand befindet. Dies bedeutet, dass es zu Datenverlust auf dem sekundären Replikat kommt.
In SQL Server 2017 gibt es nun eine Option, um das Verhalten zu steuern, das auftritt, wenn es synchronisierte Replikate namens REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT gibt. Diese Optionen funktionieren folgendermaßen:
* Es gibt drei mögliche Werte: 0, 1 und 2.
* Der Wert entspricht der Anzahl von sekundären Replikaten, die synchronisiert werden müssen, und hat Auswirkungen auf den Datenverlust, die Verfügbarkeit von Verfügbarkeitsgruppen und auf Failover.
* Für WSFCs und den Clustertyp „Keiner“ ist der Standardwert 0 und kann manuell auf 1 oder 2 festgelegt werden.
* Für den Clustertyp „Extern“ wird dies standardmäßig durch den Clustermechanismus festgelegt und kann manuell überschrieben werden. Bei drei synchronen Replikaten ist der Standardwert 1.
Unter Linux wird der Wert für REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT auf der Verfügbarkeitsgruppenressource im Cluster konfiguriert. Unter Windows wird dieser über Transact-SQL festgelegt.

Ein Wert, der größer als 0 ist, gewährleistet einen höheren Datenschutz, denn wenn die erforderliche Anzahl von sekundären Replikaten nicht verfügbar ist, ist auch das primäre Replikat nicht verfügbar, bis dies gelöst ist. REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT wirkt sich auch auf das Failoververhalten aus, da ein automatisches Failover nicht auftreten kann, wenn sich nicht die richtige Anzahl von sekundären Replikaten im korrekten Zustand befindet. Unter Linux lässt ein Wert von 0 keine automatischen Failover zu. Wenn Sie unter Linux also synchrone Replikate mit automatischem Failover verwenden, muss der Wert größer als 0 festgelegt werden, um ein automatisches Failover zu erzielen. Unter Windows Server stellt 0 das Verhalten von SQL Server 2016 und früher dar.

##### <a name="enhanced-microsoft-distributed-transaction-coordinator-support"></a>Erweiterte Microsoft Distributed Transaction Coordinator-Unterstützung

Vor SQL Server 2016 war die einzige Möglichkeit das Bereitstellen von FCIs, um Verfügbarkeit für Anwendungen in SQL Server bereitzustellen, die verteilte Transaktionen erfordern, die DTC im Hintergrund verwenden. Eine verteilte Transaktion kann auf zwei Arten erfolgen:
* Eine Transaktion, die mehr als eine Datenbank auf derselben Instanz von SQL Server umfasst
* Eine Transaktion, die mehr als eine Instanz von SQL Server oder möglicherweise eine Nicht-SQL Server-Datenquelle umfasst

In SQL Server 2016 wurde eine Teilunterstützung für DTC mit Verfügbarkeitsgruppen eingeführt, die das zweite Szenario abdecken. SQL Server 2017 unterstützt dann beide Szenarios mit DTC.

Eine andere Erweiterung für die DTC-Unterstützung für Verfügbarkeitsgruppen betrifft die Tatsache, dass in SQL Server 2016 die DTC-Unterstützung für eine Verfügbarkeitsgruppe nur hinzugefügt werden konnte, wenn die Verfügbarkeitsgruppe erstellt wurde. Sie konnte später nicht hinzugefügt werden. In SQL Server 2017 kann die DTC-Unterstützung auch nach der Erstellung zu einer Verfügbarkeitsgruppe hinzugefügt werden.

>[!NOTE]
> Die DTC-Unterstützung kann nur für Datenbanken in Windows Server-basierten SQL Server-Instanzen konfiguriert werden. Wenn DTC eine Voraussetzung für Ihre Anwendung ist, müssen Sie Windows Server als Betriebssystem für Ihre SQL Server-Bereitstellung verwenden. Linux kann nicht verwendet werden. 

#### <a name="always-on-failover-cluster-instances"></a>Always On-Failoverclusterinstanzen
Gruppierte Installationen sind eine Funktion von SQL Server seit Version 6.5. FCIs sind eine bewährte Methode zum Gewährleisten der Verfügbarkeit für die gesamte Installation von SQL Server, die als Instanz bezeichnet wird. Das bedeutet, dass alle Elemente in der Instanz, einschließlich Datenbanken, SQL Server-Agent-Aufträge, Verbindungsserver auf einen anderen Server verschoben werden, wenn auf dem zugrunde liegenden Server ein Problem auftritt. Alle FCIs erfordern freigegebenen Speicher, auch wenn dieser über ein Netzwerk bereitgestellt wird. Die Ressourcen der FCIs können jeweils nur von einem Knoten gleichzeitig ausgeführt und besessen werden. In der folgenden Abbildung besitzt der erste Knoten des Clusters die FCI. Das bedeutet, dass dieser auch die freigegebenen Speicherressourcen besitzt, die ihm zugewiesen sind. Dies ist durch die durchgezogene Linie zum Speicher gekennzeichnet.

![Failoverclusterinstanz][BasicFCI]
 
Wie in der folgenden Abbildung dargestellt ändert sich der Besitzer nach einem Failover.

![Nach einem Failover][PostFailoverFCI]
 
Mit einer FCI gibt es keinen Datenverlust, aber der zugrunde liegende freigegebene Speicher ist eine einzelne Fehlerquelle, da eine Kopie der Daten vorhanden ist. FCIs werden häufig mit anderen Verfügbarkeitsmethoden kombiniert, z.B. Verfügbarkeitsgruppen und Protokollversand, damit redundante Kopien der Datenbank verfügbar sind. Die zusätzlich bereitgestellte Methode sollte einen anderen physischen Speicher als die FCI verwenden. Wenn die FCI ein Failover auf einen anderen Knoten ausführt, hält diese im Gegensatz zu einem Server, der ein- und ausgeschaltet wird, auf einem Knoten an und fährt auf einem anderen fort. Eine FCI durchläuft den normalen Wiederherstellungsprozess. Das bedeutet, dass alle Transaktionen ein Rollforward ausgeführt wird, die einen benötigen, und für alle unvollständigen Transaktionen wird ein Rollback ausgeführt. Daher ist eine Datenbank von einem Datenpunkt aus bis zum Zeitpunkt des Fehlers oder des manuellen Failovers konsistent und es kommt nicht zu Datenverlust. Datenbank sind erst verfügbar, wenn die Wiederherstellung abgeschlossen ist. Die Wiederherstellungszeit hängt also von mehreren Faktoren ab und ist im Allgemeinen länger als das Ausführen eines Failovers für eine Verfügbarkeitsgruppe dauert. Der Nachteil besteht darin, dass beim Ausführen eines Failovers für eine Verfügbarkeitsgruppe zusätzliche Aufgaben erforderlich sein können, damit die Datenbank verwendet werden kann, z.B. das Aktivieren von SQL Server-Agent-Aufträgen.

FCIs abstrahieren genau wie Verfügbarkeitsgruppen, auf welchem Knoten des zugrunde liegenden Clusters diese gehostet werden. Eine FCI behält immer denselben Namen bei. Anwendungen und Benutzer verbinden sich nie mit den Knoten, sondern der eindeutige Name, der der FCI zugewiesen ist, wird verwendet. Eine FCI kann in einer Verfügbarkeitsgruppe als eine der Instanzen enthalten sein, die entweder ein primäres oder ein sekundäres Replikat hosten.

Die folgende Liste hebt einige Unterschiede von FCIs zwischen Windows Server und Linux hervor:

* Unter Windows Server ist FCI ein Teil des Installationsvorgangs. Unter Linux wird eine FCI nach der Installation von SQL Server konfiguriert.
* Linux unterstützt nur eine einzige Installation von SQL Server pro Host, sodass alle FCIs eine Standardinstanz darstellen. Windows Server unterstützt bis zu 25 FCIs pro WSFC.
* Der allgemeine Name, der von FCIs unter Linux verwendet wird, wird in DNS definiert und sollte mit dem der Ressource identisch sein, die für die FCI erstellt wurde.

#### <a name="log-shipping"></a>Protokollversand
Wenn die Ziele für den Wiederherstellungspunkt und die Wiederherstellungszeit flexibler sind, oder Datenbanken nicht als hoch unternehmenskritisch betrachtet werden, ist der Protokollversand eine weitere bewährte Verfügbarkeitsfunktion in SQL Server. Basierend auf den nativen Sicherungen von SQL Server generiert der Prozess für den Protokollversand automatisch Transaktionsprotokollsicherungen, kopiert diese auf eine oder mehrere Instanzen, die als betriebsbereit bekannt sind und wendet sie auf diese Standbyinstanzen an. Der Protokollversand verwendet SQL Server-Agent-Aufträge, um den Sicherungs- und Kopiervorgang sowie den Anwendungsvorgang der Transaktionsprotokollsicherungen zu automatisieren. 
> [!IMPORTANT] 
> Unter Linux sind SQL Server-Agent-Aufträge nicht als Teil der Installation von SQL Server enthalten. Stattdessen sind diese im Paket „package mssql-server-Agent jobs“ verfügbar, das ebenfalls für das Verwenden des Protokollversands installiert werden muss.

![Protokollversand][LogShipping]
 
Der größte Vorteil der Verwendung des Protokollversands in gewissem Umfang ist der, dass menschliche Fehler erfasst werden. Die Anwendung der Transaktionsprotokolle kann verzögert werden. Wenn jemand also z.B. ein Update ohne eine WHERE-Klausel ausführt, verfügt die Standbyinstanz dadurch nicht über die Änderung, sodass Sie zu dieser wechseln können, während Sie das primäre System reparieren. Während der Protokollversand einfach zu konfigurieren ist, ist das Wechseln von der primären zur betriebsbereiten Standbyinstanz, auch als Rollenänderung bezeichnet, immer ein manueller Vorgang. Eine Rollenänderung wird über Transact-SQL initiiert, und alle Objekte, die nicht im Transaktionsprotokoll erfasst sind, müssen wie bei Verfügbarkeitsgruppen manuell synchronisiert werden. Der Protokollversand muss pro Datenbank konfiguriert werden, während einzelne Verfügbarkeitsgruppen mehrere Datenbanken enthalten können. Im Gegensatz zu Verfügbarkeitsgruppen oder FCIs verfügt der Protokollversand nicht über Abstraktionen für eine Rollenänderung. Anwendungen müssen damit umgehen können. Techniken wie ein DNS-Alias (CNAME) können eingesetzt werden, es gibt jedoch Vor- und Nachteile, z.B. die Zeit, die ein DNS nach dem Wechsel zum Aktualisieren benötigt.

## <a name="disaster-recovery"></a>Notfallwiederherstellung

Wenn Ihr primärer Verfügbarkeitsstandort einer Katastrophe wie einem Erdbeben oder einer Überschwemmung ausgesetzt ist, muss das Unternehmen darauf vorbereitet sein, die Systeme an anderer Stelle online schalten zu können. Dieser Abschnitt erläutert, wie die SQL Server-Verfügbarkeitsfunktionen Sie bei der Geschäftskontinuität unterstützen können.

### <a name="always-on-availability-groups"></a>Always On-Verfügbarkeitsgruppen

Einer der Vorteile von Verfügbarkeitsgruppen ist, dass Hohe Verfügbarkeit und Notfallwiederherstellung mithilfe einer einzigen Funktion konfiguriert werden können. Ohne die Anforderung, dass die Hochverfügbarkeit des freigegebenen Speichers sichergestellt werden muss, ist es deutlich einfacher, lokale Replikate für die Hochverfügbarkeit in einem Rechenzentrum und Remotereplikate mit jeweils separatem Speicher für die Notfallwiederherstellung in anderen Rechenzentren zu besitzen. Das Vorhandensein von zusätzlichen Kopien der Datenbank ist der Nachteil der Gewährleistung von Redundanz. Nachfolgend finden Sie ein Beispiel für eine Verfügbarkeitsgruppe, die mehrere Rechenzentren umfasst. Ein primäres Replikat ist dafür verantwortlich, alle sekundären Replikate zu synchronisieren.

![Verfügbarkeitsgruppe][AG]
 
Außerhalb einer Verfügbarkeitsgruppe mit dem Clustertyp „Keiner“ erfordert eine Verfügbarkeitsgruppe, dass alle Replikate Teil desselben zugrunde liegenden Clusters (WSFC oder Pacemaker) sind. Das bedeutet, dass WSFC in der obigen Abbildung gestreckt wird, um in zwei verschiedenen Rechenzentren zu arbeiten, wodurch die Komplexität unabhängig von der Plattform (Windows Server oder Linux) erhöht wird. Das Strecken von Clustern über Entfernungen erhöht die Komplexität. In SQL Server 2016 wurde eingeführt, dass eine verteilte Verfügbarkeitsgruppe es einer Verfügbarkeitsgruppe ermöglichen kann, Verfügbarkeitsgruppen zu umfassen, die auf verschiedenen Clustern konfiguriert wurden. Dies entkoppelt die Anforderung, dass alle Knoten im selben Cluster enthalten sein müssen. Dadurch wird das Konfigurieren der Notfallwiederherstellung wesentlich einfacher. Weitere Informationen zu verteilten Verfügbarkeitsgruppen finden Sie unter [Verteilte Verfügbarkeitsgruppen](http://docs.microsoft.com/sql/database-engine/availability-groups/windows/distributed-availability-groups).

![Verteilte Verfügbarkeitsgruppen][DAG]
 
### <a name="always-on-failover-cluster-instances"></a>Always On-Failoverclusterinstanzen

FCIs können für die Notfallwiederherstellung verwendet werden. Wie bei einer normalen Verfügbarkeitsgruppe muss der zugrunde liegende Clustermechanismus auf alle Standorte erweitert werden. Dadurch wird die Komplexität erhöht. Zusätzlich muss für FCIs der freigegebene Speicher berücksichtigt werden. Dieselben Datenträger müssen für die primären und sekundären Standorte verfügbar sein. Eine externe Methode ist erforderlich, z.B. die Funktionalität, die vom Speicheranbieter auf Hardwareebene oder durch das Verwenden von Speicherreplikaten unter Windows Server bereitgestellt wird, um sicherzustellen, dass die von der FCI verwendeten Datenträger an anderer Stelle vorhanden sind. 

![Always On-FCI][AlwaysOnFCI]
 
### <a name="log-shipping"></a>Protokollversand
Der Protokollversand ist eine der ältesten Methoden für die Bereitstellung der Notfallwiederherstellung für SQL Server-Datenbanken. Der Protokollversand wird häufig zusammen mit Verfügbarkeitsgruppen und FCIs verwendet, um eine kosteneffektive und einfachere Notfallwiederherstellung bereitzustellen, wenn andere Optionen wegen der Umgebung, der administrativen Fähigkeiten oder des Budgets zu anspruchsvoll sind. Ähnlich wie bei der Hochverfügbarkeit für den Protokollverstand wird bei vielen Umgebungen das Laden eines Transaktionsprotokolls verzögert, um menschliche Fehler zu erfassen.

## <a name = "Migrations"></a> Migrationen und Upgrades

Beim Bereitstellen neuer Instanzen oder beim Aktualisieren von alten kann ein Unternehmen keinen langen Ausfall tolerieren. In diesem Abschnitt wird erläutert, wie die Verfügbarkeitsfunktionen von SQL Server verwendet werden können, um die Ausfallzeit bei einem geplanten Architekturwechsel, einem Serverwechsel, einer Plattformänderung (z.B. Windows Server zu Linux oder umgekehrt) oder während des Patchens zu minimieren.

> [!NOTE]
> Andere Methoden, z.B. das Verwenden von Sicherungen und deren Wiederherstellung an anderer Stelle, können ebenfalls für Migrationen und Upgrades verwendet werden. Diese werden in diesem Dokument nicht erläutert. 

### <a name="always-on-availability-groups"></a>Always On-Verfügbarkeitsgruppen

Eine vorhandene Instanz mit einer oder mehreren Verfügbarkeitsgruppen kann auf SQL Server 2017 aktualisiert werden. Dies erfordert gewisse Ausfallzeiten, die jedoch durch die richtige Planung minimiert werden können. 

Wenn es das Ziel ist, zu neuen Servern zu migrieren, ohne die Konfiguration zu ändern (einschließlich des Betriebssystems oder der SQL Server-Version), können diese Server als Knoten zum vorhandenen zugrunde liegenden Cluster und zur Verfügbarkeitsgruppe hinzugefügt werden. Sobald das Replikat oder die Replikate sich im richtigen Zustand befinden, kann ein manuelles Failover auf einen neuen Server ausgeführt werden. Die alten können dann aus der Verfügbarkeitsgruppe entfernt und letztendlich außer Betrieb genommen werden. 

Verteilte Verfügbarkeitsgruppen stellen eine weitere Methode zum Migrieren zu einer neuen Konfiguration oder zum Aktualisieren von SQL Server dar. Da eine verteilte Verfügbarkeitsgruppe verschiedene zugrunde liegende Verfügbarkeitsgruppen auf verschiedenen Architekturen unterstützt, können Sie z.B. von SQL Server 2016 unter Windows Server 2012 R2 auf SQL Server 2017 unter Windows Server 2016 wechseln. 

![Verteilte Verfügbarkeitsgruppen][image10]

Schließlich können Verfügbarkeitsgruppen mit dem Clustertyp „Keiner“ auch für Migrationen und Upgrades verwendet werden. Sie können Clustertypen in einer typischen Konfiguration von Verfügbarkeitsgruppen nicht mischen und anpassen, darum müssen alle Replikate den Typ „Keiner“ aufweisen. Eine verteilte Verfügbarkeitsgruppe kann verwendet werden, um Verfügbarkeitsgruppen zu umfassen, die mit verschiedenen Clustertypen konfiguriert wurden. Diese Methode wird auf den verschiedenen Betriebssystemplattformen unterstützt.

Alle Varianten von Verfügbarkeitsgruppen für Migrationen und Upgrades ermöglichen das Erledigen der Datensynchronisierung, die den aufwendigsten Teil der Arbeit darstellt, im Lauf der Zeit. Wenn der Wechsel zur neuen Konfiguration initiiert werden soll, verursacht die Umstellung einen kurzen Ausfall im Gegensatz zu einer langen Ausfallzeit, in der die gesamte Arbeit, einschließlich der Datensynchronisierung, abgeschlossen werden muss. 

Verfügbarkeitsgruppen können eine minimale Ausfallzeit während des Patchens des zugrunde liegenden Betriebssystems bereitstellen, indem manuell ein Failover vom primären zu einem sekundären Replikat ausgeführt wird, während der Patchvorgang abgeschlossen wird. Aus der Sicht des Betriebssystems wird dieser Vorgang unter Windows Server häufiger ausgeführt, da die Wartung des zugrunde liegenden Betriebssystems oft, aber nicht immer, einen Neustart erfordert. Das Patchen von Linux erfordert manchmal einen Neustart, dies ist jedoch selten der Fall. 

[Das Patchen von SQL Server-Instanzen, die in einer Verfügbarkeitsgruppe enthalten sind](http://docs.microsoft.com/sql/database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances), kann abhängig von der Architektur der Verfügbarkeitsgruppe ebenfalls die Ausfallzeiten minimieren. Bevor die Server gepatcht werden, die in einer Verfügbarkeitsgruppe enthalten sind, wird zunächst das sekundäre Replikat gepatcht. Sobald die richtige Anzahl von Replikaten gepatcht wurde, wird ein manuelles Failover des primären Replikats auf einen anderen Knoten ausgeführt, um das Upgrade durchzuführen. Alle zu diesem Zeitpunkt verbleibenden sekundären Replikate können ebenfalls aktualisiert werden. 

### <a name="always-on-failover-cluster-instances"></a>Always On-Failoverclusterinstanzen

FCIs allein können traditionelle Migrationen und Upgrades nicht unterstützen. Eine Verfügbarkeitsgruppe oder ein Protokollversand muss für die Datenbanken im FCI und alle anderen berücksichtigten Objekte konfiguriert werden. FCIs unter Windows Server sind jedoch weiterhin eine beliebte Option, wenn die zugrunde liegenden Windows-Server gepatcht werden müssen. Ein manuelles Failover kann initiiert werden, was einen kurzen Ausfall bedeutet, statt dass die Instanz für die gesamte Zeit nicht verfügbar ist, in der Windows Server gepatcht wird.
Eine FCI kann auf SQL Server 2017 aktualisiert werden. Weitere Informationen finden Sie unter [Aktualisieren einer SQL Server-Failoverclusterinstanz](http://docs.microsoft.com/sql/sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance).

### <a name="log-shipping"></a>Protokollversand

Der Protokollversand ist immer noch eine beliebte Option zum Migrieren und Aktualisieren von Datenbanken. Ähnlich wie bei Verfügbarkeitsgruppen kann die Datenweitergabe vor dem Serverwechsel gestartet werden, dieses Mal wird jedoch das Transaktionsprotokoll als Synchronisierungsmethode verwendet. Zum Zweitpunkt des Wechsels, wenn der gesamte Datenverkehr an der Quelle beendet wurde, muss ein letztes Transaktionsprotokoll ausgeführt, kopiert und auf die neue Konfiguration angewendet werden. An diesem Punkt kann die Datenbank online geschaltet werden. Der Protokollversand ist häufig toleranter gegenüber langsameren Netzwerken. Während der Wechsel etwas länger als beim Verwenden einer Verfügbarkeitsgruppe oder einer verteilten Verfügbarkeitsgruppe dauern kann, wird dieser üblicherweise in Minuten gemessen, nicht in Stunden, Tagen oder Wochen.

Ähnlich wie bei Verfügbarkeitsgruppen kann der Protokollversand eine Möglichkeit bereitstellen, um während des Patchens auf einen anderen Server zu wechseln.

### <a name="other-sql-server-deployment-methods-and-availability"></a>Andere SQL Server-Bereitstellungsmethoden und Verfügbarkeit

Es gibt zwei Bereitstellungsmethoden für SQL Server unter Linux: Container und das Verwenden von Azure (oder einem anderen öffentlichen Cloudanbieter). Die allgemeine Notwendigkeit der Verfügbarkeit, die in diesem Dokument erläutert wird, besteht unabhängig von der Bereitstellungsmethode von SQL Server. Beide Methoden weisen Besonderheiten auf, wenn SQL Server hoch verfügbar gemacht werden soll.

[Container, die Docker verwenden](http://docs.microsoft.com/sql/linux/quickstart-install-connect-docker) sind eine neue Möglichkeit für das Bereitstellen von SQL Server unter Windows Server oder Linux. Ein Container ist ein vollständiges Image von SQL Server, das für die Ausführung bereit ist. Es gibt jedoch derzeit keine native Unterstützung für das Clustering und dadurch auch nicht für die direkte Hochverfügbarkeit oder die Notfallwiederherstellung. Die derzeitigen Optionen, um SQL Server-Datenbanken mithilfe von Containern verfügbar zu machen, sind der Protokollversand sowie die Sicherung und Wiederherstellung. Obwohl eine Verfügbarkeitsgruppe mit dem Clustertyp „Keiner“ wie bereits erwähnt konfiguriert werden kann, wird dies nicht als echte Konfiguration für Verfügbarkeitsgruppen betrachtet. Microsoft arbeitet an Möglichkeiten, um Verfügbarkeitsgruppen oder FCIs beim Verwenden von Containern zu aktivieren. 

Wenn Sie Container verwenden und der Container verloren geht, kann er, abhängig von der Containerplattform, erneut bereitgestellt und an den freigegebenen Speicher angefügt werden, der verwendet wurde. Einige dieser Mechanismen werden vom Containerorchestrator bereitgestellt. Obwohl dadurch Stabilität bereitgestellt wird, kann es zu Ausfällen im Zusammenhang mit der Datenbankwiederherstellung kommen und die Hochverfügbarkeit wird nicht genauso wie bei Verwendung einer Verfügbarkeitsgruppe oder FCI gewährleistet. 

Virtuelle IaaS-Computer mit Linux können mithilfe von Azure mit einer Installation von SQL Server bereitgestellt werden. Bei lokalen Installationen erfordert eine unterstützte Installation die Verwendung von STONITH (Shoot the Other Node in the Head), das sich außerhalb von Pacemaker befindet. STONITH wird über Agents für das Umgrenzen der Verfügbarkeit bereitgestellt. In einigen Verteilungen sind diese als Teil der Plattform enthalten, andere basieren auf externer Hardware und Softwareanbietern. Überprüfen Sie für Ihre bevorzugte Linux-Verteilung, um festzustellen, welche Arten von STONITH bereitgestellt werden, damit eine unterstützte Lösung in der öffentlichen Cloud bereitgestellt werden kann.

## <a name="cross-platform-and-linux-distribution-interoperability"></a>Interoperabilität – plattformübergreifend und für Linux-Verteilungen

Da SQL Server nun unter Windows Server und Linux unterstützt wird, deckt dieser Abschnitt die Szenarios ab, wie diese zusätzlich zu anderen Zwecken für die Verfügbarkeit zusammenarbeiten können sowie die Lösungen, durch die mehr als eine Linux-Verteilung integriert werden kann.

Bevor die plattformübergreifenden Szenarios und die für die Interoperabilität abgedeckt werden, müssen zwei Fakten festgehalten werden:

* Es gibt keine Szenarios, in denen eine WSFC-basierte FCI oder Verfügbarkeitsgruppe direkt mit einer Linux-basierten FCI oder Verfügbarkeitsgruppe zusammenarbeitet. Ein WSFC kann nicht durch einen Pacemaker-Knoten erweitert werden und umgekehrt. 
* Das Mischen von Linux-Verteilungen wird von FCIs oder Verfügbarkeitsgruppen mit dem Clustertyp „Extern“ nicht unterstützt. Alle Replikate von Verfügbarkeitsgruppen in diesem Szenario müssen nicht nur für die gleiche Linux-Verteilung, sondern auch für die gleiche Version konfiguriert werden. Die zwei unterstützten Methoden, durch die SQL Server auf beiden Plattformen oder auf mehreren Verteilungen von Linux arbeiten können, sind Verfügbarkeitsgruppen und der Protokollversand.

## <a name="distributed-availability-groups"></a>Verteilte Verfügbarkeitsgruppen 

Verteilte Verfügbarkeitsgruppen wurden dafür entwickelt, mehrere Konfigurationen für Verfügbarkeitsgruppen zu umfassen, unabhängig davon, ob die zwei zugrunde liegenden Cluster der Verfügbarkeitsgruppen zwei verschiedene WSFCs oder Linux-Verteilungen sind oder ob einer sich auf einem WSFC und der andere auf Linux befindet. Eine verteilte Verfügbarkeitsgruppe ist die primäre Methode für plattformübergreifende Lösungen. Eine verteilte Verfügbarkeitsgruppe ist außerdem die primäre Lösung für Migrationen, z.B. für das Konvertieren von einer Windows Server-basierten SQL Server-Infrastruktur zu einer Linux-basierten, wenn Ihr Unternehmen dies durchführen möchte. Wie bereits erwähnt minimieren Verfügbarkeitsgruppen, insbesondere verteilte Verfügbarkeitsgruppen, die Zeit, die eine Anwendung nicht für die Verwendung verfügbar ist. Im Folgenden wird ein Beispiel für eine verteilte Verfügbarkeitsgruppe dargestellt, die einen WSFC und Pacemaker umfasst.

![Verteilte Verfügbarkeitsgruppen][BasicDAG]
 
Wenn eine Verfügbarkeitsgruppe mit dem Clustertyp „Keiner“ konfiguriert ist, kann diese Windows Server und Linux umfassen sowie mehrere Linux-Verteilungen. Da es sich dabei nicht um eine echte Konfiguration für die Hochverfügbarkeit handelt, sollte diese nicht für unternehmenskritische Bereitstellungen verwendet werden, sondern für schreibgeschützte Szenarios sowie für Migrations- und Upgradeszenarios.

## <a name="log-shipping"></a>Protokollversand

Da der Protokollversand nur auf Sicherung und Wiederherstellung basiert, gibt es keine Unterschiede zwischen den Datenbanken, Dateistrukturen usw. für SQL Server unter Windows Server oder Linux. Dies bedeutet, dass der Protokollversand zwischen einer Windows Server-basierten Installation von SQL Server und einer Linux-basierten konfiguriert werden kann und ebenfalls zwischen Linux-Verteilungen. Alles andere bleibt unverändert. Es muss allerdings berücksichtigt werden, dass der Protokollversand, genau wie eine Verfügbarkeitsgruppe, nicht funktioniert, wenn die Quelle sich auf einer höheren Hauptversion von SQL Server befindet als das Ziel, das sich auf einer früheren Version von SQL Server befindet. 

## <a name = "ReadScaleOut"></a> Schreibgeschützte horizontale Skalierung

Seit sekundäre Replikate in SQL Server 2012 eingeführt wurden, können diese für schreibgeschützte Abfragen verwendet werden. Es gibt zwei Möglichkeiten, wie dies mit einer Verfügbarkeitsgruppe erzielt werden kann: Indem direkter Zugriff auf das sekundäre Replikat gewährt wird oder indem das [schreibgeschützte Routing konfiguriert wird](http://docs.microsoft.com/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server), wofür die Verwendung eines Listeners erforderlich ist.  In SQL Server 2016 wurde die Möglichkeit eingeführt, einen Lastenausgleich für schreibgeschützte Verbindungen über den Listener vorzunehmen, indem ein Roundrobin-Algorithmus verwendet wird. Dadurch können schreibgeschützte Anforderungen über alle lesbaren Replikate verteilt werden. 

> [!NOTE] 
Lesbare sekundäre Replikate sind eine Funktion, die nur in der Enterprise Edition enthalten ist. Jede Instanz, die ein lesbares Replikat hostet, erfordert eine SQL Server-Lizenz.

Die Skalierung von lesbaren Kopien einer Datenbank über Verfügbarkeitsgruppen wurde erstmals mit den verteilten Verfügbarkeitsgruppen in SQL Server 2016 eingeführt. Dadurch können Unternehmen schreibgeschützte Kopien der Datenbank nicht nur lokal besitzen, sondern auch regional und global mit minimalem Konfigurationsaufwand. Außerdem werden durch lokal ausgeführte Abfragen der Netzwerkdatenverkehr und die Latenz reduziert. Jedes primäre Replikat einer Verfügbarkeitsgruppe kann für zwei andere Verfügbarkeitsgruppen ein Seeding ausführen, selbst wenn es sich nicht um eine vollständige Lese-/Schreibkopie handelt. Somit kann jede verteilte Verfügbarkeitsgruppe bis zu 27 lesbare Kopien einer Datei unterstützen. 

![Verteilte Verfügbarkeitsgruppen][DAG]

Ab SQL Server 2017 ist es möglich, eine schreibgeschützte Lösung mit Verfügbarkeitsgruppen mit dem Clustertyp „Keiner“ nahezu in Echtzeit zu erstellen. Wenn es das Ziel ist, Verfügbarkeitsgruppen für lesbare sekundäre Replikate und nicht für die Verfügbarkeit zu verwenden, wird dadurch die Komplexität der Verwendung eines WSFC oder von Pacemaker entfernt, außerdem erhalten die lesbaren Replikate die Vorteile einer Verfügbarkeitsgruppe in einer einfacheren Bereitstellungsmethode. 

Dabei muss allerdings berücksichtigt werden, dass kein Cluster mit dem Clustertyp „Keiner“ vorhanden ist und das Konfigurieren des schreibgeschützten Routings sich dadurch geringfügig unterscheidet. Aus der Sicht von SQL Server ist immer noch ein Listener erforderlich, um die Anforderungen weiterzuleiten, obwohl kein Cluster vorhanden ist. Anstatt einen traditionellen Listener zu konfigurieren, wird die IP-Adresse oder der Name des primären Replikats verwendet. Das primäre Replikat wird dann verwendet, um die schreibgeschützten Anforderungen weiterzuleiten.

Ein betriebsbereiter Protokollversand kann technisch gesehen für die Lesbarkeit konfiguriert werden, indem die Datenbank mit der WITH STANDBY-Klausel wiederherstellen. Da die Transaktionsprotokolle jedoch die exklusive Verwendung der Datenbank für die Wiederherstellung benötigen, können Benutzer währenddessen nicht auf die Datenbank zugreifen. Dadurch ist der Protokollversand keine ideale Lösung, besonders wenn Daten nahezu in Echtzeit erforderlich sind. 

Bei allen Szenarios für die schreibgeschützte horizontale Skalierung mit Verfügbarkeitsgruppen sollte beachtet werden, dass anders als bei der Transaktionsreplikation, bei der Livedaten verwendet werden, die sekundären Replikate sich nicht in einem Zustand befinden, in dem eindeutige Indizes angewendet werden können und das Replikat eine exakte Kopie des primären Replikats ist. Wenn die erforderlichen Indizes für die Berichterstellung oder die Daten bearbeitet werden müssen, bedeutet das, dass dies auf den Datenbanken auf dem primären Replikat erfolgen muss. Wenn Sie Flexibilität benötigen, ist die Replikation die bessere Lösung für lesbare Daten.

## <a name="summary"></a>Zusammenfassung

Instanzen und Datenbanken von SQL Server 2017 können hoch verfügbar gemacht werden, indem die gleichen Funktionen unter Windows Server und Linux verwendet werden. Neben den Standardszenarios für die lokale Hochverfügbarkeit und die Verfügbarkeit der Notfallwiederherstellung kann die Ausfallzeit bei Upgrades und Migrationen durch die Verfügbarkeitsfunktionen in SQL Server minimiert werden. Verfügbarkeitsgruppen können ebenfalls zusätzliche Kopien einer Datenbank als Teil derselben Architektur für schreibgeschützte hochskalierte Kopien bereitstellen. Ob Sie eine neue Lösung mithilfe von SQL Server 2017 bereitstellen möchten oder ein Upgrade erwägen: SQL Server 2017 bietet Ihnen die Verfügbarkeit und Zuverlässigkeit, die Sie benötigen.
 
[SimpleAG]:media\sql-server-ha-story\image1.png
[SSMSAGOptions]:media\sql-server-ha-story\image2.png
[BasicFCI]:media\sql-server-ha-story\image3.png
[PostFailoverFCI]:media\sql-server-ha-story\image4.png
[LogShipping]:media\sql-server-ha-story\image5.png
[AG]:media\sql-server-ha-story\image6.png
[DAG]:media\sql-server-ha-story\image7.png
[AlwaysOnFCI]:media\sql-server-ha-story\image8.png
[BasicDAG]:media\sql-server-ha-story\image9.png
[image10]:media\sql-server-ha-story\image10.png
[DAG]:media\sql-server-ha-story\image11.png
