---
title: Hohe Verfügbarkeit und Skalierbarkeit in Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3eb3d358f22c22472185c61baebc4197792f6353
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="high-availability-and-scalability-in-analysis-services"></a>Hohe Verfügbarkeit und Skalierbarkeit in Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In diesem Artikel werden die am häufigsten verwendeten Techniken beschrieben, um Analysis Services-Datenbanken hoch verfügbar und skalierbar zu machen. Zwar lassen sich diese beiden Ziele separat behandeln, praktisch gehen sie jedoch oftmals Hand in Hand: Für eine skalierbaren Bereitstellung für umfangreiche Abfrage- oder Verarbeitungsauslastungen wird typischerweise auch Hochverfügbarkeit gefordert.  
  
 Der umgekehrte Fall trifft jedoch nicht immer zu. Hohe Verfügbarkeit ohne Skalierbarkeit kann das einzige Ziel sein, wenn bindende Vereinbarungen zum Service Level für unternehmenswichtige, aber mäßige Abfrageauslastungen getroffen wurden.  
  
 Techniken, mit denen Analysis Services hoch verfügbar und skalierbar gestaltet werden, sind tendenziell für alle Servermodi (mehrdimensionaler, tabellarischer und integrierter SharePoint-Modus) gleich. Sofern nicht spezifisch anders vermerkt, können Sie davon ausgehen, dass sich die Informationen in diesem Artikel auf alle Modi beziehen.  
  
## <a name="key-points"></a>Die wichtigsten Punkte  
 Da sich die Techniken zum Erzielen hoher Verfügbarkeit und Skalierbarkeit von denen des relationalen Datenbankmoduls unterscheiden, stellt eine kurze Zusammenfassung der wichtigsten Punkte eine wirksame Einführung in die für Analysis Services verwendeten Techniken dar:  
  
-   Analysis Services verwendet die in die Windows-Serverplattform integrierten Mechanismen für Hochverfügbarkeit und Skalierbarkeit: Netzwerklastenausgleich (NLB, Network Load Balancing), Windows Server Failover Clustering (WSFC) oder beide.  
  
    > [!NOTE]  
    >  Das Feature Always On des relationalen Datenbankmoduls erstreckt sich nicht auf Analysis Services.  Eine Analysis Services-Instanz kann nicht für die Ausführung in einer Always On-Verfügbarkeitsgruppe konfiguriert werden.  
    >   
    >  Zwar wird Analysis Services nicht in Always On-Verfügbarkeitsgruppen ausgeführt, jedoch können Daten aus relationalen Always On-Datenbanken sowohl abgerufen als auch verarbeitet werden. Anweisungen zum Konfigurieren einer hoch verfügbaren relationalen Datenbank für die Verwendung durch Analysis Services finden Sie unter [Analysis Services mit Always On-Verfügbarkeitsgruppen](../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md).  
  
-   Hohe Verfügbarkeit kann als einzelnes Ziel mithilfe von Serverredundanz in einem Failovercluster erreicht werden. Für Ersatzknoten wird eine mit dem aktiven Knoten identische Hard- und Softwarekonfiguration angenommen.  Bei eigenständigem Einsatz erhalten Sie durch WSFC Hochverfügbarkeit, jedoch ohne Skalierbarkeit.  
  
-   Skalierbarkeit mit oder ohne Verfügbarkeit wird mithilfe von NLB von schreibgeschützten Datenbanken erreicht.  Skalierbarkeit ist normalerweise eine Anforderung, wenn das Abfrageaufkommen groß ist oder plötzlichen Spitzen unterliegt.  
  
     Lastenausgleich in Verbindung mit mehreren schreibgeschützten Datenbanken gibt Ihnen sowohl Skalierbarkeit als auch Hochverfügbarkeit, da alle Knoten aktiv sind und die Anforderungen beim Ausfall eines Servers automatisch auf die verbleibenden Knoten verteilt werden. Wenn Sie sowohl Skalierbarkeit als auch Verfügbarkeit benötigen, ist ein NLB-Cluster die richtige Wahl.  
  
 Bei der Verarbeitung stellen die Ziele der Hochverfügbarkeit und Skalierbarkeit eine weniger große Herausforderung dar, da Sie den zeitlichen Ablauf und den Umfang des Betriebs steuern können. Die Verarbeitung kann sowohl teilweise als auch inkrementell über die Teilbereiche eines Modells verteilt erfolgen; allerdings muss an irgendeinem Punkt ein Modell vollständig auf einem einzelnen Server verarbeitet werden, um die Datenkonsistenz über alle Indizes und Aggregationen hinweg sicherzustellen. Eine robuste skalierbare Architektur baut auf Hardware auf, die die gesamte Verarbeitung in jedem praktisch geforderten Rhythmus leisten kann. Bei großen Lösungen ist diese Arbeit als unabhängiger Vorgang mit eigenen Hardwareressourcen strukturiert.  
  
##  <a name="bkmk_serverconfig"></a> Einzel- im Vergleich zu Mehrserverkonfigurationen  
 In einer gewöhnlichen Einzelserverbereitstellung werden Verarbeitungs- und Abfragearbeitsauslastungen parallel ausgeführt, unter der Annahme, dass die Systemressourcen für beide Aktivitäten ausreichen. Bei Analysis Services bleiben die vorhandenen Datenstrukturen intakt und unterstützen die Abfrageverarbeitung, während eine aktualisierte Version im Hintergrund verarbeitet wird. Der Besitz von genügend Arbeitsspeicher und Speicherplatz zum Verarbeiten temporärer Datenstrukturen ist eine Hardwareanforderung, die für alle Servermodi zutrifft, obwohl jeder Modus verschiedene Anforderungen an die Systemressourcen stellt und mit verschiedenen Graden der NUMA-Unterstützung einhergeht.  
  
 **Einzelserver und Skalierbarkeit**  
  
 Ein einzelner High-End-Server mit mehreren Prozessoren kann möglicherweise aus sich heraus ausreichende Skalierbarkeit zur Verfügung stellen. Auf einem High-End-System mit einer großen Anzahl Kerne, viel RAM und Speicherplatz auf Datenträgern lässt sich die Skalierbarkeit potenziell im Rahmen eines einzelnen Systems erzielen.  
  
 Bei mehrdimensionalen Datenbanken können die Eigenschaften der Serverkonfiguration angepasst werden, um Affinitäten zwischen Prozessen und Prozessoren zu schaffen. Weitere Informationen dazu finden Sie unter [Threadpooleigenschaften](../../analysis-services/server-properties/thread-pool-properties.md) .  
  
 **Mehrserverbereitstellungen**  
  
 Manchmal schreiben Betriebsbedingungen die Verwendung mehrerer Server vor. Beispielsweise bestehen Failovercluster definitionsgemäß aus mehreren Servern, wobei jeder Knoten auf identischer Hard- und Softwarekonfiguration ausgeführt wird.  
  
 Analog dazu verlangt ein dringender Bedarf an Hochverfügbarkeit bei Abfrageauslastungen nach mehreren Servern. In diesem Szenario ist die empfohlene Konfiguration für Analysis Services eine Mischung aus schreibgeschützten Datenbanken und Datenbanken mit Schreib-/Lesezugriff, die auf getrennten Instanzen von Analysis Services auf dedizierter Hardware ausgeführt werden. Schreibgeschützte Datenbanken verarbeiten Abfrageanforderungen. Datenbanken mit Schreib-/Lesetzugriff werden für die Verarbeitung verwendet. Eine erweiterte Beschreibung dieser häufig verwendeten Technik wird im nächsten Abschnitt gegeben.  
  
 **Virtuelle Maschinen und Hochverfügbarkeit**  
  
 Eine andere Strategie, um die Anforderungen von Hochverfügbarkeit zu erfüllen, könnte die Verwendung virtueller Computer einschließen. Wenn die geforderte Verfügbarkeit durch Bereitstellung eines Ersatzservers innerhalb von Stunden anstelle von Minuten erreicht werden kann, ist möglicherweise der Einsatz von virtuellen Computern sinnvoll, die bei Bedarf gestartet und mit aktualisierten Datenbanken geladen werden können, die bei einem zentralen Speicherort abgerufen werden.  
  
## <a name="scalability-using-read-only-and-read-write-databases"></a>Skalierbarkeit unter Verwendung von schreibgeschützten Datenbanken und Datenbanken mit Lese-/Schreibzugriff  
 Netzwerklastenausgleich wird für hohe oder eskalierende Abfrage- oder Verarbeitungsauslastungen empfohlen. Analysis Services-Datenbanken in einer NLB-Lösung werden als schreibgeschützte Datenbanken definiert, um über die Abfragen hinweg Konsistenz sicherzustellen.  
  
 Zwar sind die Ausführungen in [Horizontales Skalieren der Abfrageverarbeitung für Analysis Services mithilfe schreibgeschützter Datenbanken (Scale-out querying for Analysis Services using read-only databases; veröffentlicht 2008](https://technet.microsoft.com/library/ff795582\(v=sql.100\).aspx) ) recht alt, trotzdem sind sie im Allgemeinen noch gültig. Während sich Serverbetriebssysteme und Computerhardware entwickelt haben und die Verweise auf bestimmte Plattformen und Grenzen von CPUs veraltet sind, ist die grundlegende Technik, schreibgeschützte Datenbanken und Datenbanken mit Schreib-/Lesezugriff für große Abfragevolumina zu verwenden, unverändert geblieben.  
  
 Der Ansatz kann in folgender Weise zusammengefasst werden:  
  
-   Verwenden Sie dedizierte Hardware und dedizierte Instanzen von Analysis Services zum Verarbeiten der Datenbank. Versetzen Sie die Datenbank nach dem Abschluss der Verarbeitung in den schreibgeschützten Modus. Anweisungen finden Sie unter [Umschalten einer Analysis Services-Datenbank zwischen schreibgeschütztem Modus und Lese-/Schreibmodus](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) .  
  
-   Verwenden Sie mehrere identische Abfrageserver, um Kopien der gleichen schreibgeschützten Analysis Services-Datenbank auszuführen. Server werden in einem NLB-Cluster bereitgestellt; der Zugriff erfolgt über einen virtuellen Servernamen, der als einzelner Einstiegspunkt zum Cluster fungiert.  
  
-   Verwenden Sie robocopy, um ein gesamtes Datenverzeichnis vom Verarbeitungsserver auf jeden der Abfrageserver zu kopieren, und fügen Sie allen Abfrageservern die gleiche Datenbank im schreibgeschützten Modus hinzu. Sie können auch SAN-Momentaufnahmen, Synchronisierung oder beliebige andere Tools oder Methoden verwenden, die Sie einsetzen, um Produktionsdatenbanken zu verschieben.  
  
## <a name="resource-demands-for-tabular-and-multidimensional-workloads"></a>Ressourcenanforderungen bei tabellarischen und mehrdimensionalen Arbeitsauslastungen  
 Die folgende Tabelle ist eine abstrakte Zusammenfassung der Weise, wie Analysis Services Systemressourcen für Abfragen und Verarbeitung verwendet, getrennt aufgeführt nach Servermodus und Speicher. Diese Zusammenfassung kann Ihnen ein Verständnis dafür vermitteln, welche Aspekte in einer Mehrserverbereitstellung, die eine verteilte Arbeitsauslastung verarbeitet, besonders betont werden müssen.  
  
|||  
|-|-|  
|**Server- und Speichermodus**|**Auswirkung auf die Systemressource**|  
|Tabellarisch speicherintern (Standardwert); hier werden Abfragen als Durchsuchung von Tabellen von speicherinternen Datenstrukturen ausgeführt.|Schwerpunkt auf Arbeitsspeicher und CPUs mit hohen Taktraten.|  
|Tabellarisch im DirectQuery-Modus; hier werden Abfragen auf relationale Datenbankserver im Back-End ausgelagert, und die Verarbeitung ist auf die Konstruktion von Metadaten im Modell beschränkt.|Der Schwerpunkt liegt auf der Leistung der relationalen Datenbank, dem Verringern der Netzwerklatenz und dem Maximieren des Durchsatzes. Schnellere CPUs können darüber hinaus die Leistung des Analysis Services-Abfrageprozessors steigern.|  
|Mehrdimensionale Modelle mit MOLAP-Speicher|Wählen Sie eine ausgeglichene Konfiguration, die Datenträger-E/A zum schnellen Laden von Daten und ausreichend Arbeitsspeicher für gecachete Daten bietet.|  
|Mehrdimensionale Modelle mit ROLAP-Speicher|Maximieren Sie Datenträger-E/A, und minieren Sie Netzwerklatenz.|  
  
## <a name="highly-availability-and-redundancy-through-wsfc"></a>Hohe Verfügbarkeit und Redundanz mithilfe von WSFC  
 Analysis Services können auf einem vorhandenen Windows Server-Failovercluster (WSFC) installiert werden, um Hochverfügbarkeit zu erzielen, die den Dienst innerhalb der kürzest möglichen Zeit wiederherstellt.  
  
 Failovercluster bieten Vollzugriff (Lesen und Rückschreiben) auf die Datenbank, jedoch immer nur auf einem Knoten. Sekundäre Datenbanken werden auf weiteren Knoten im Cluster ausgeführt, die als Ersatzserver dienen, falls der erste Knoten ausfällt.  
  
 Der wichtigste Vorteil von Failoverclustern besteht in der schnellen Wiederherstellung nach einem Dienstausfall. Dieser Vorteil geht mit bestimmten Einschränkungen einher. Einerseits liegen dedizierte Ressourcen brach, sollte der Failover nie eintreten. Zweitens gehen im Fall eines Failovers alle Verbindungen verloren und entsprechend auch jede noch nicht per Commit festgeschriebene Arbeit. Die meisten Clientanwendungen sollten in der Lage sein, dieses Problem zu lösen; in den meisten Fällen können Sie die Ergebnisse über die Schaltfläche Aktualisieren der Anwendung wieder zurückholen. 
 
 Beim Erwägen eines WSFC sollten Sie die folgenden Punkte bedenken:

- Aktiv/Aktiv wird derzeit nicht unterstützt. Aktiv/Passiv (Failover) ist die einzige unterstützte WSFC-Konfiguration für Analysis Services.
- Stellen Sie bei einer Analysis Services-Clusteringlösung sicher, dass alle Knoten im Cluster auf identischer oder sehr ähnlicher Hardware ausgeführt werden. Sorgen Sie auch dafür, dass der Betriebskontext aller Knoten in den folgenden Punkten identisch ist: Betriebssystemversion und Service Packs, Analysis Services-Version und Service Packs (oder kumulative Updates) und Servermodus.
- Vermeiden Sie den Weiterbetrieb eines passiven Knotens als aktiven Knoten einer anderen Arbeitsauslastung. Kurzzeitige Vorteile bei der Computernutzung gehen bei einer tatsächlichen Failoversituation verloren, wenn der Knoten nicht in der Lage ist, beide Arbeitsauslastungen zu bewältigen.
 
 Ausführliche Anweisungen und Hintergrundinformationen zum Bereitstellen von Analysis Services auf einem Failovercluster finden Sie in diesem Whitepaper: [Clustern von SQL Server Analysis Services (How to Cluster SQL Server Analysis Services)](https://msdn.microsoft.com/library/dn736073.aspx). Zwar bezieht sich diese Hilfestellung auf SQL Server 2012, sie gilt jedoch auch für die neueren Versionen von Analysis Services.  
  
## <a name="see-also"></a>Siehe auch  
 [Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Das Erzwingen des NUMA-Affinität für tabellarische Analysis Services-Datenbanken](https://blogs.msdn.microsoft.com/sqlcat/2013/11/05/forcing-numa-node-affinity-for-analysis-services-tabular-databases/)   
 [Eine Analysis Services-Fallstudie: Verwenden von tabellarischen Modellen in umfangreichen kommerziellen Lösung](https://msdn.microsoft.com/library/dn751533.aspx)  
  
  
