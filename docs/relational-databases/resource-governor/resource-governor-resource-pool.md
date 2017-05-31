---
title: "Ressourcenpool für die Ressourcenkontrolle | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, resource pool
- resource pool [SQL Server], overview
- resource pool [SQL Server]
ms.assetid: 306b6278-e54f-42e6-b746-95a9315e0cbe
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 10b74a185e59a6b2973ea17fb4c68b61e781953f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="resource-governor-resource-pool"></a>Ressourcenpool für die Ressourcenkontrolle
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressourcenkontrolle stellt ein Ressourcenpool eine Teilmenge der physischen Ressourcen einer Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s dar. Über die Ressourcenkontrolle können Sie Grenzwerte für die CPU, physische E/A und den Arbeitsspeicher festlegen, d. h. Ressourcen, die eingehenden Anwendungsanforderungen im Ressourcenpool zur Verfügung stehen. Jeder Ressourcenpool kann eine oder mehrere Arbeitsauslastungsgruppen enthalten. Wenn eine Sitzung gestartet wird, weist die Klassifizierungsfunktion der Ressourcenkontrolle die Sitzung einer bestimmten Arbeitsauslastungsgruppe zu, und die Sitzung muss mit den der Arbeitsauslastungsgruppe zugewiesenen Ressourcen ausgeführt werden.  
  
## <a name="resource-pool-concepts"></a>Konzepte von Ressourcenpools  
 Ein Ressourcenpool (Pool) stellt die physischen Ressourcen des Servers dar. Stellen Sie sich einen Pool als virtuelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz innerhalb einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz vor. Ein Pool besteht aus zwei Teilen. Ein Teil überschneidet sich nicht mit anderen Pools, wodurch eine minimale Reservierung von Ressourcen ermöglicht wird. Der andere Teil wird gemeinsam mit anderen Pools verwendet, wodurch eine maximale Ressourcenauslastung ermöglicht wird. Die Poolressourcen werden definiert, indem mindestens eine der folgenden Einstellungen für jede Ressource (CPU, Arbeitsspeicher und physische E/A) festgelegt wird:  
  
-   **MIN_CPU_PERCENT und MAX_CPU_PERCENT**  
  
     Falls ein CPU-Konflikt auftreten sollte, entsprechen diese Einstellungen dem Mindest- und Höchstwert der garantierten durchschnittlichen CPU-Bandbreite für alle Anforderungen im Ressourcenpool. Sie können diese Einstellungen festlegen, um eine vorhersagbare CPU-Ressourcenverwendung für mehrere Arbeitsauslastungen einzurichten, die auf den Anforderungen der einzelnen Arbeitsauslastungen basiert. Angenommen, die Vertriebs- und Marketingabteilung eines Unternehmens verwenden dieselbe Datenbank. Die Vertriebsabteilung verfügt über eine CPU-intensive Arbeitsauslastung mit Abfragen hoher Priorität. Die Marketingabteilung verfügt ebenfalls über eine CPU-intensive Arbeitsauslastung, führt jedoch Abfragen mit niedrigerer Priorität aus. Indem Sie einen separaten Ressourcenpool für jede Abteilung erstellen, können Sie einen *minimalen* CPU-Prozentsatz von 70 % für den Ressourcenpool der Vertriebsabteilung und einen *maximalen* CPU-Prozentsatz von 30 % für den Ressourcenpool der Marketingabteilung zuweisen. Dadurch wird sichergestellt, dass der Arbeitsauslastung der Vertriebsabteilung die erforderlichen CPU-Ressourcen zur Verfügung stehen und dass die Arbeitsauslastung der Marketingabteilung von den CPU-Anforderungen des Vertriebs isoliert ist. Beachten Sie, dass der maximale CPU-Prozentsatz ein opportunistischer Maximalwert ist. Wenn CPU-Kapazität verfügbar ist, wird diese von der Arbeitsauslastung bis zu 100 % genutzt. Der Maximalwert gilt nur bei einem CPU-Ressourcenkonflikt. Wenn die Arbeitsauslastung der Vertriebsabteilung beispielsweise heruntergefahren wird, kann die Marketingabteilung die CPU bei Bedarf zu 100 % nutzen.  
  
-   **CAP_CPU_PERCENT**  
  
     Diese Einstellung ist eine feste Obergrenze für die CPU-Bandbreite aller Anforderungen im Ressourcenpool. Die dem Pool zugeordneten Arbeitsauslastungen können eine CPU-Kapazität nutzen, die ggf. über den Wert MAX_CPU_PERCENT, nicht aber über den Wert CAP_CPU_PERCENT hinausgeht. Wir bleiben beim vorangehenden Beispiel und gehen davon aus, dass die genutzten Ressourcen der Marketingabteilung als Kosten angerechnet werden. Zur besseren Voraussagbarkeit der Kosten soll die CPU-Nutzung bei maximal 30 % gedeckelt werden. Dies lässt sich erreichen, indem die CAP_CPU_PERCENT-Einstellung für den Ressourcenpool "Marketing" auf 30 festgelegt wird.  
  
-   **MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT**  
  
     Diese Einstellungen geben die minimale und maximale Kapazität des für den Ressourcenpool reservierten Arbeitsspeichers an, der nicht gemeinsam mit anderen Ressourcenpools verwendet werden kann. Dieser reservierte Arbeitsspeicher ist der für die Abfrageausführung gewährte Arbeitsspeicher und kein Pufferpoolarbeitsspeicher (z. B. Daten- und Indexseiten). Durch das Festlegen eines Mindestarbeitsspeichers für einen Pool stellen Sie sicher, dass der angegebene prozentuale Arbeitsspeicher für alle Anforderungen verfügbar ist, die in diesem Ressourcenpool ausgeführt werden. Dies ist ein wichtiges Unterscheidungsmerkmal zu MIN_CPU_PERCENT, da der Arbeitsspeicher in diesem Fall im jeweiligen Ressourcenpool verbleibt, auch wenn der Pool keine Anforderungen für die zugehörigen Arbeitsauslastungsgruppen enthält. Daher sollte die Einstellung mit besonderer Vorsicht eingesetzt werden, weil dieser Arbeitsspeicher keinem anderen Pool zur Verfügung steht – auch dann nicht, wenn keine aktiven Anforderungen vorliegen. Das Festlegen eines maximalen Arbeitsspeicherwerts für einen Pool bewirkt, dass den in diesem Pool ausgeführten Anforderungen nie mehr Gesamtarbeitsspeicher zur Verfügung steht als durch diesen Prozentsatz angegeben.  
  
-   **AFFINITY**  
  
     Mit dieser Einstellung können Sie einen Ressourcenpool einem oder mehreren Zeitplanungsmodulen oder NUMA-Knoten zuordnen, um eine stärkere Isolierung von CPU-Ressourcen zu erzielen. Ausgehend vom obigen Beispiel setzen wir voraus, dass die Vertriebsabteilung eine stärker isolierte Umgebung benötigt und einen CPU-Kern durchgehend zu 100 % nutzen will. Durch die AFFINITY-Option können die Arbeitsauslastungen "Vertrieb" und "Marketing" für unterschiedliche CPUs geplant werden. Wenn die CAP_CPU_PERCENT-Einstellung für den Marketingpool immer noch wirksam ist, verwendet die Arbeitsauslastung "Marketing" weiterhin maximal 30 % eines Kerns, während die Arbeitsauslastung "Vertrieb" 100 % des anderen Kerns nutzt. Für die Arbeitsauslastungen der Vertriebs- und Marketingabteilung bedeutet das, dass sie quasi auf zwei isolierten Computern ausgeführt werden.  
  
-   **MIN_IOPS_PER_VOLUME und MAX_IOPS_PER_VOLUME**  
  
     Diese Einstellungen entsprechen den minimalen und maximalen physischen E/A-Vorgängen, die pro Sekunde und pro Datenträgervolume für einen Ressourcenpool ausgeführt werden. Über diese Einstellungen können Sie die physischen E/A-Befehle steuern, die für Benutzerthreads eines bestimmten Ressourcenpools ausgegeben werden. Beispielsweise generiert die Vertriebsabteilung mehrere Monatsabschlussberichte in großen Batches. Die in diesen Batches enthaltenen Abfragen können E/A-Vorgänge erzeugen, die das Datenträgervolume vollständig beanspruchen und die Leistung anderer Arbeitsauslastungen mit höherer Priorität in der Datenbank beeinträchtigen. Um diese Arbeitsauslastung zu isolieren, wird MIN_IOPS_PER_VOLUME auf 20 und MAX_IOPS_PER_VOLUME auf 100 für den Ressourcenpool der Vertriebsabteilung festgelegt, der die Anzahl der für die Arbeitsauslastung ausgegebenen E/A-Befehle steuert.  
  
 Bei der CPU- oder Arbeitsspeicherkonfiguration darf die Summe der MIN-Werte für alle Pools 100 Prozent der Serverressourcen nicht überschreiten. Außerdem können beim Konfigurieren der CPU oder des Arbeitsspeichers MAX und CAP auf beliebige Werte im Bereich zwischen MIN und 100 Prozent festgelegt werden.  
  
 Wenn bei einem Pool ein MIN-Wert definiert ist, der nicht 0 (null) entspricht, wird der effektive MAX-Wert anderer Pools erneut angepasst. Das Minimum des konfigurierten MAX-Werts eines Pool sowie die Summe der MIN-Werte der anderen Pools wird von 100 Prozent subtrahiert.  
  
 In der folgenden Tabelle werden einige der obigen Konzepte erläutert. Die Tabelle zeigt die Einstellungen für den internen Pool, den Standardpool und zwei benutzerdefinierte Pools. Die folgenden Formeln werden zum Berechnen der Prozentwerte für den effektiven MAX-Wert (MAX %) und den freigegebenen, d. h. gemeinsam verwendeten Teil (Shared %) herangezogen.  
  
-   Min(X,Y) bedeutet den kleineren Wert von X und Y.  
  
-   Sum(X) bedeutet die Summe der X-Werte in allen Pools.  
  
-   Shared % insgesamt = 100 - sum(MIN %).  
  
-   Effektiver MAX % = min(X,Y).  
  
-   Shared % = effektiver MAX % - MIN %.  
  
|Poolname|Einstellung für MIN %|Einstellung für MAX %|Berechneter effektiver MAX %|Berechneter Shared %|Anmerkung|  
|---------------|-------------------|-------------------|--------------------------------|-------------------------|-------------|  
|Interner Pool (internal)|0|100|100|0|Effektiver MAX % und Shared % gelten nicht für den internen Pool.|  
|default|0|100|30|30|Der effektive MAX-Wert wird berechnet als: min(100,100-(20+50)) = 30. Der berechnete Shared % ist der effektive MAX - MIN = 30.|  
|Pool 1|20|100|50|30|Der effektive MAX-Wert wird berechnet als: min(100,100-50) = 50. Der berechnete Shared % ist der effektive MAX - MIN = 30.|  
|Pool 2|50|70|70|20|Der effektive MAX-Wert wird berechnet als: min(70,100-20) = 70. Der berechnete Shared % ist der effektive MAX - MIN = 20.|  
  
 Anhand der obigen Tabelle als Beispiel können wir zeigen, welche Anpassungen vorgenommen werden, wenn ein weiterer Pool erstellt wird. Dieser Pool ist Pool 3 mit einer MIN %-Einstellung von 5.  
  
|Poolname|Einstellung für MIN %|Einstellung für MAX %|Berechneter effektiver MAX %|Berechneter Shared %|Anmerkung|  
|---------------|-------------------|-------------------|--------------------------------|-------------------------|-------------|  
|Interner Pool (internal)|0|100|100|0|Effektiver MAX % und Shared % gelten nicht für den internen Pool.|  
|default|0|100|25|25|Der effektive MAX-Wert wird berechnet als: min(100,100-(20+50+5)) = 25. Der berechnete Shared % ist der effektive MAX - MIN = 25.|  
|Pool 1|20|100|45|25|Der effektive MAX-Wert wird berechnet als: min(100,100-55) = 45. Der berechnete Shared % ist der effektive MAX - MIN = 25.|  
|Pool 2|50|70|70|20|Der effektive MAX-Wert wird berechnet als: min(70,100-25) = 70. Der berechnete Shared % ist der effektive MAX - MIN = 20.|  
|Pool 3|5|100|30|25|Der effektive MAX-Wert wird berechnet als: min(100,100-70) = 30. Der berechnete Shared % ist der effektive MAX - MIN = 25.|  
  
 Mit dem freigegebenen Teil des Pools wird angezeigt, wohin Ressourcen verlagert werden können, sofern Ressourcen verfügbar sind. Belegte Ressourcen gehen jedoch in den angegebenen Pool über und sind nicht mehr freigegeben. Hierdurch lässt sich ggf. die Ressourcenausnutzung verbessern, wenn in einem bestimmten Pool keine Anforderungen vorliegen und somit die für diesen Pool konfigurierten Ressourcen für andere Pools freigegeben werden können.  
  
 Beispiele für extreme Poolkonfigurationen:  
  
-   Alle Pools weisen Mindestwerte auf, deren Summe 100 Prozent der Serverressourcen ergibt. In diesem Fall entsprechen die Höchstwerte den Mindestwerten. Dies kommt einer Einteilung der Ressourcen in sich nicht überlappende Teile gleich, unabhängig davon, ob die Ressourcen in den einzelnen Pools tatsächlich ausgenutzt werden.  
  
-   Alle Pools weisen einen Mindestwert von 0 (null) auf. Alle Pools stehen im Wettbewerb um verfügbare Ressourcen, und ihre letztendliche Größe ist abhängig von der Ressourcenbelegung in den einzelnen Pools. Andere Faktoren wie Richtlinien beeinflussen die endgültige Poolgröße.  
  
 Die Ressourcenkontrolle verfügt über zwei vordefinierte Ressourcenpools: den internen Pool und den Standardpool. Sie können weitere Pools hinzufügen.  
  
 **Interner Pool**  
  
 Der interne Pool entspricht den von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] belegten Ressourcen. Dieser unveränderliche Pool enthält immer nur die interne Gruppe. Die Ressourcenbelegung durch den internen Pool ist nicht eingeschränkt. Alle Arbeitsauslastungen im Pool gelten als unabdingbar für die Serverfunktion. Daher darf der interne Pool Druck auf andere Pools ausüben, selbst wenn dies zu einer Verletzung der Grenzwerte für die anderen Pools führt.  
  
> [!NOTE]  
>  Die durch den internen Pool und die interne Gruppe belegten Ressourcen werden nicht von den insgesamt belegten Ressourcen abgezogen. Prozentwerte werden auf Basis der insgesamt verfügbaren Ressourcen berechnet.  
  
 **Standardpool**  
  
 Der Standardpool ist der erste vordefinierte Benutzerpool. Bevor eine anderweitige Konfiguration vorgenommen wird, enthält der Standardpool nur die Standardgruppe. Der Standardpool kann nicht erstellt oder gelöscht, jedoch geändert werden. Er kann neben der Standardgruppe noch benutzerdefinierte Gruppen enthalten. Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] gibt es einen Standardressourcenpool für Routineoperationen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und einen externen Standardressourcenpool für externe Prozesse wie das Ausführen von R-Skripten.  
  
> [!NOTE]  
>  Die Standardgruppe kann zwar geändert, aber nicht aus dem Standardpool entfernt werden.  
  
 **Interner Pool**  
  
 Benutzer können einen externen Pool zum Festlegen der Ressourcen für externe Prozesse definieren. Dieser deckt für R Services speziell `rterm.exe`, `BxlServer.exe` und andere Prozesse ab, die von diesen ausführbaren Dateien generiert werden.  
  
 **Benutzerdefinierte Ressourcenpools**  
  
 Benutzerdefinierte Ressourcenpools sind Pools, die Sie für bestimmte Arbeitsauslastungen in der Umgebung erstellen. Die Ressourcenkontrolle stellt DDL-Anweisungen zum Erstellen, Ändern und Löschen von Ressourcenpools bereit.  
  
## <a name="resource-pool-tasks"></a>Aufgaben in Verbindung mit Ressourcenpools  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie ein Ressourcenpool erstellt wird.|[Erstellen eines Ressourcenpools](../../relational-databases/resource-governor/create-a-resource-pool.md)|  
|Beschreibt, wie Ressourcenpooleinstellungen geändert werden.|[Ändern der Einstellungen für den Ressourcenpool](../../relational-databases/resource-governor/change-resource-pool-settings.md)|  
|Beschreibt, wie ein Ressourcenpool gelöscht wird.|[Löschen eines Ressourcenpools](../../relational-databases/resource-governor/delete-a-resource-pool.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)   
 [Arbeitsauslastungsgruppe der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Klassifizierungsfunktion der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [Konfigurieren der Ressourcenkontrolle mit einer Vorlage](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Anzeigen der Eigenschaften der Ressourcenkontrolle](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  

