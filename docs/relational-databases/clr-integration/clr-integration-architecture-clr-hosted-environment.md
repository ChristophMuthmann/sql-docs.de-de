---
title: CLR-gehosteten Umgebung | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- type-safe code [CLR integration]
- UNSAFE permission set
- run-time environments [CLR integration]
- common language runtime [SQL Server], about CLR integration
- application domains [CLR integration]
- host protection attributes [CLR integration]
- managed code [SQL Server], common language runtime
- permission sets [CLR integration]
- reliability [CLR integration]
- SAFE permission set
- code access security [CLR integration]
- EXTERNAL_ACCESS permission set
- verifying type safety
- scalability [CLR integration]
- hosted environments [CLR integration]
- HPAs [CLR integration]
ms.assetid: d280d359-08f0-47b5-a07e-67dd2a58ad73
caps.latest.revision: 60
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 603b0d66a4a8b7f406708442f18e9c98c4414b26
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="clr-integration-architecture---clr-hosted-environment"></a>Architektur der CLR-Integration - gehostete CLR-Umgebung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Integration von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in die .NET Framework-CLR (Common Language Runtime) ermöglicht Datenbankprogrammierern die Verwendung von Sprachen wie Visual C#, Visual Basic .NET und Visual C++. Funktionen, gespeicherte Prozeduren, Trigger, Datentypen und Aggregate gehören zu den Arten von Geschäftslogik, die Programmierer in diesen Sprachen schreiben können.  
  
  Die CLR bietet der Garbage Collection unterworfenen Arbeitsspeicher, präemptives Threading, Metadatendienste (geben Sie „reflection“ ein), Codeüberprüfbarkeit und Codezugriffssicherheit. Die CLR verwendet Metadaten zum Suchen und Laden von Klassen, Anordnen von Instanzen im Speicher, Auflösen von Methodenaufrufen, Generieren von systemeigenem Code, Erzwingen von Sicherheit und zum Festlegen von Begrenzungen im Laufzeitkontext.  
  
 Die CLR und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterscheiden sich als Laufzeitumgebungen in der Weise, wie sie Arbeitsspeicher, Threads und Synchronisierung behandeln. Dieses Thema beschreibt, wie die beiden Laufzeiten integriert werden, sodass alle Systemressourcen einheitlich verwaltet werden. Ferner wird hier behandelt, wie CLR-Codezugriffssicherheit (CAS) und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherheit integriert werden, um eine zuverlässige und sichere Ausführungsumgebung für Benutzercode bereitzustellen.  
  
## <a name="basic-concepts-of-clr-architecture"></a>Grundlegende Konzepte der CLR-Architektur  
 In .NET Framework schreibt ein Programmierer in einer Hochsprache, die eine Klasse implementiert, die die Struktur (z. B. die Felder oder Eigenschaften der Klasse) und Methoden definiert. Einige dieser Methoden können statische Funktionen sein. Bei der Kompilierung des Programms wird eine Datei erstellt, eine so genannte Assembly, die den kompilierten Code in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Intermediate Language (MSIL) sowie ein Manifest enthält, das alle Verweise auf abhängige Assemblys umfasst.  
  
> [!NOTE]  
>  Assemblys sind ein wichtiges Element in der Architektur der CLR. Sie sind die Einheiten für Verpackung, Bereitstellung und Versionsverwaltung des Anwendungscodes in .NET Framework. Durch die Verwendung von Assemblys können Sie Anwendungscode in der Datenbank verfügbar machen und eine einheitliche Methode zur Verwaltung, Sicherung und Wiederherstellung kompletter Datenbankanwendungen bereitstellen.  
  
 Das Assemblymanifest enthält Metadaten über die Assembly, die sämtliche Strukturen, Felder, Eigenschaften, Klassen, Vererbungsbeziehungen, Funktionen und Methoden beschreiben, die im Programm definiert sind. Das Manifest legt die Identität der Assembly fest, gibt die Dateien an, aus denen die Assemblyimplementierung besteht, gibt die Typen und Ressourcen an, aus denen die Assembly besteht, legt die Abhängigkeiten von anderen Assemblys für die Kompilierungszeit einzeln fest und gibt den Berechtigungssatz an, der für die ordnungsgemäße Ausführung der Assembly erforderlich ist. Diese Informationen werden zur Laufzeit verwendet, um Verweise aufzulösen, Versionsbindungsrichtlinien zu erzwingen und die Integrität geladener Assemblys zu validieren.  
  
 .NET Framework unterstützt benutzerdefinierte Attribute zum Hinzufügen von Anmerkungen zu Klassen, Eigenschaften, Funktionen und Methoden in Form von zusätzlichen Informationen, die von der Anwendung in Metadaten erfasst werden können. Alle .NET Framework-Compiler verwenden diese Anmerkungen ohne Auslegung und speichern sie als Assemblymetadaten. Diese Anmerkungen können auf die gleiche Weise wie beliebige andere Metadaten untersucht werden.  
  
 Verwalteter Code ist MSIL-Code, der in der CLR anstatt direkt vom Betriebssystem ausgeführt wird. Anwendungen mit verwaltetem Code verfügen über CLR-Dienste, z. B. automatische Garbage Collection, Typüberprüfung zur Laufzeit, Sicherheitsunterstützung usw. Diese Dienste stellen eine einheitliche Webplattform und sprachunabhängiges Verhalten von Anwendungen mit verwaltetem Code bereit.  
  
## <a name="design-goals-of-clr-integration"></a>Entwurfsziele der CLR-Integration  
 Bei der Ausführung von Benutzercode in der CLR-gehosteten Umgebung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (CLR-Integration genannt), gelten die folgenden Entwurfsziele:  
  
###### <a name="reliability-safety"></a>Zuverlässigkeit (Sicherheit)  
 Vom Benutzercode sollten keine Vorgänge ausgeführt werden dürfen, die die Integrität des Prozesses der Datenbank-Engine gefährden, z. B. die Anzeige eines Meldungsfelds, in dem eine Benutzerantwort verlangt wird, oder in dem der Prozess beendet wird. Benutzercode sollte nicht in der Lage sein, Arbeitsspeicherpuffer der Datenbank-Engine oder interne Datenstrukturen zu überschreiben.  
  
###### <a name="scalability"></a>Skalierbarkeit  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und CLR verwenden unterschiedliche interne Modelle für Planung und Speicherverwaltung. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt ein kooperatives, nicht präemptives Threadingmodell, in dem die Threads freiwillig die Ausführung in regelmäßigen Abständen oder beim Warten auf Sperren oder Eingaben/Ausgaben unterbrechen. Die CLR unterstützt ein präemptives Threadingmodell. Wenn die Threadinggrundelemente des Betriebssystems direkt von Benutzercode aufgerufen werden können, der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, ist keine einwandfreie Integration in den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Taskplaner möglich, und die Skalierbarkeit des Systems kann beeinträchtigt werden. Die CLR macht keinen Unterschied zwischen virtuellem und physischem Arbeitsspeicher, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwaltet physischen Arbeitsspeicher jedoch direkt und muss physischen Arbeitsspeicher innerhalb eines konfigurierbaren Grenzwerts verwenden.  
  
 Die unterschiedlichen Modelle für Threading, Planung und Arbeitsspeicherverwaltung stellen eine Integrationsherausforderung für ein relationales Datenbankverwaltungssystem (RDBMS) dar, das durch Skalierung Tausende von gleichzeitigen Benutzersitzungen unterstützt. Durch die Architektur sollte sichergestellt werden, dass die Skalierbarkeit des Systems nicht durch Benutzercode beeinträchtigt wird, der APIs (Application Programming Interfaces, Schnittstellen zur Anwendungsprogrammierung) für Threading-, Arbeitsspeicher- und Synchronisierungsgrundelemente direkt aufruft.  
  
###### <a name="security"></a>Sicherheit  
 In der Datenbank ausgeführter Benutzercode muss beim Zugreifen auf Datenbankobjekte, wie Tabellen und Spalten, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierungs- und Autorisierungsregeln folgen. Darüber hinaus sollten Datenbankadministratoren in der Lage sein, den Zugriff auf Ressourcen des Betriebssystems, wie Dateien und Netzwerkzugriff, vom Benutzercode aus zu steuern, der in der Datenbank ausgeführt wird. Dies ist wichtig, da verwaltete Programmiersprachen (im Gegensatz zu nicht verwalteten Sprachen wie Transact-SQL) APIs zum Zugreifen auf diese Ressourcen bereitstellen. Das System muss eine sichere Methode bereitstellen, damit über Benutzercode außerhalb des [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Prozesses auf Computerressourcen zugegriffen werden kann. Weitere Informationen finden Sie unter [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
###### <a name="performance"></a>Leistung  
 In [!INCLUDE[ssDE](../../includes/ssde-md.md)] ausgeführter verwalteter Benutzercode sollte über eine vergleichbare Ausführungsleistung verfügen wie derselbe Code, der außerhalb des Servers ausgeführt wird. Datenbankzugriff von verwaltetem Benutzercode ist nicht so schnell wie systemeigener [!INCLUDE[tsql](../../includes/tsql-md.md)]. Weitere Informationen finden Sie unter [Performance of CLR Integration](../../relational-databases/clr-integration/clr-integration-architecture-performance.md).  
  
## <a name="clr-services"></a>CLR Services  
 Die CLR bietet eine Reihe von Diensten, um die Entwurfsziele der CLR-Integration mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu erreichen.  
  
###### <a name="type-safety-verification"></a>Typsicherheitsüberprüfung  
 Als typsicherer Code wird Code bezeichnet, der nur auf genau definierte Weise auf Arbeitsspeicherstrukturen zugreift. Bei typsicherem Code ist z. B. bei einem gültigen Objektverweis der Speicherzugriff an festen Offsets möglich, die tatsächlichen Feldmembern entsprechen. Wenn der Code jedoch auf den Speicher an beliebigen Offsets innerhalb oder außerhalb des Gültigkeitsbereichs des Speichers zugreift, der zu dem Objekt gehört, ist er nicht typsicher. Wenn Assemblys in die CLR geladen werden, bevor die MSIL mithilfe der JIT-Kompilierung (Just-In-Time) kompiliert wurde, führt die Laufzeit eine Überprüfungsphase aus, die den Code hinsichtlich seiner Typsicherheit untersucht. Code, der diese Überprüfung erfolgreich besteht, wird nachweisbar typsicherer Code genannt.  
  
###### <a name="application-domains"></a>Anwendungsdomänen  
 Die CLR unterstützt die Definition von Anwendungsdomänen als Ausführungszonen in einem Hostprozess, bei dem verwaltete Codeassemblys geladen und ausgeführt werden können. Die Anwendungsdomänengrenze bietet Isolierung zwischen Assemblys. Die Assemblys werden hinsichtlich der Sichtbarkeit von statischen Variablen und Datenelementen und der Möglichkeit, Code dynamisch aufzurufen, isoliert. Anwendungsdomänen sind auch der Mechanismus zum Laden und Entladen von Code. Code kann aus dem Arbeitsspeicher durch das Entladen der Anwendungsdomäne entfernt werden. Weitere Informationen finden Sie unter [Anwendungsdomänen und Sicherheit der CLR-Integration](http://msdn.microsoft.com/library/54ee904e-e21a-4ee7-b4ad-a6f6f71bd473).  
  
###### <a name="code-access-security-cas"></a>Codezugriffssicherheit (Code Access Security, CAS)  
 Das CLR-Sicherheitssystem bietet eine Methode zum Steuern der Vorgangstypen, die von verwaltetem Code ausgeführt werden können, indem dem Code Berechtigungen zugewiesen werden. Codezugriffsberechtigungen werden auf der Grundlage der Identität des Codes (z. B. die Signatur der Assembly oder die Quelle des Codes) zugewiesen.  
  
 Die CLR sorgt für eine Richtlinie, die auf dem gesamten Computer gilt und vom Computeradministrator festgelegt werden kann. Diese Richtlinie definiert die Berechtigungen für den gesamten verwalteten Code, der auf dem Computer ausgeführt wird. Ferner besteht eine Sicherheitsrichtlinie auf Hostebene, die vom Host verwendet werden kann, z. B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Festlegen zusätzlicher Einschränkungen des verwalteten Codes.  
  
 Wenn eine verwaltete API in .NET Framework Operationen für Ressourcen verfügbar macht, die durch eine Codezugriffsberechtigung geschützt sind, fordert die API vor dem Zugriff auf die Ressource diese Berechtigung an. Diese Anforderung löst im CLR-Sicherheitssystem eine umfangreiche Überprüfung jeder Codeeinheit (Assembly) in der Aufrufliste aus. Nur wenn die ganze Aufrufkette über eine Berechtigung verfügt, wird der Zugriff auf die Ressource gewährt.  
  
 Beachten Sie, dass die Funktion zum dynamischen Generieren von verwaltetem Code mit der Reflektionsausgabe-API innerhalb der CLR-gehosteten Umgebung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht unterstützt wird. Solcher Code hätte die CAS-Berechtigungen zum Ausführen nicht und würde deshalb zur Laufzeit fehlschlagen. Weitere Informationen finden Sie unter [CLR Integration Code Access Security](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
###### <a name="host-protection-attributes-hpas"></a>Hostschutzattribute (Hostschutzattribute)  
 Die CLR stellt einen Mechanismus zur Verfügung, um verwaltete APIs, die Teil von .NET Framework sind, mit Anmerkungen in Form von bestimmten Attributen zu versehen, die für einen Host der CLR interessant sein können. Beispiele für solche Attribute:  
  
-   SharedState - gibt an, ob die API die Fähigkeit zur Verfügung stellt, einen Freigabezustand (z. B. statische Klassenfelder) zu erstellen oder zu verwalten.  
  
-   Synchronization - gibt an, ob die API die Fähigkeit zur Verfügung stellt, die Synchronisierung zwischen Threads auszuführen.  
  
-   ExternalProcessMgmt - gibt an, ob die API eine Möglichkeit zur Kontrolle des Hostprozesses zur Verfügung stellt.  
  
 Anhand dieser Attribute kann der Host eine Liste mit Hostschutzattributen festlegen, wie das SharedState-Attribut, die in der gehosteten Umgebung nicht zugelassen werden. In diesem Fall weist die CLR Versuche des Benutzercodes zurück, APIs aufzurufen, die mit nicht zugelassenen Hostschutzattributen aus der Liste versehen sind. Weitere Informationen finden Sie unter [Hostschutzattribute und Programmieren von CLR-Integration](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
## <a name="how-sql-server-and-the-clr-work-together"></a>Zusammenarbeit von SQL Server und der CLR  
 In diesem Abschnitt wird besprochen, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Modelle für Threading, Planung, Synchronisierung und Arbeitsspeicherverwaltung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und der CLR integriert. Genauer wird in diesem Abschnitt auf die Integration im Hinblick auf Skalierbarkeit, Zuverlässigkeit und Sicherheit eingegangen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agiert im Grunde als Betriebssystem für die CLR, wenn sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gehostet wird. Die CLR ruft von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Threading, Planung, Synchronisierung und Speicherverwaltung implementierte Routinen auf niedriger Ebene auf. Diese sind dieselben Grundelemente, die von der übrigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Engine verwendet werden. Dieser Ansatz bietet mehrere Vorteile für Skalierbarkeit, Zuverlässigkeit und Sicherheit.  
  
###### <a name="scalability-common-threading-scheduling-and-synchronization"></a>Skalierbarkeit: Allgemeines Threading, Planung und Synchronisierung  
 CLR ruft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-APIs zur Erstellung von Threads auf, sowohl für ausgeführten Benutzercode als auch zur eigenen internen Verwendung. Um zwischen mehreren Threads zu synchronisieren, ruft die CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Synchronisierungsobjekte auf. Dadurch kann das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeitplanungsmodul andere Aufgaben planen, wenn ein Thread auf ein Synchronisierungsobjekt wartet. Wenn die CLR beispielsweise die Garbage Collection initiiert, warten alle zugehörigen Threads auf die Fertigstellung der Garbage Collection. Da das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeitplanungsmodul die CLR-Threads und die Synchronisierungsobjekte, auf die sie warten, kennt, kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Threads planen, die andere Datenbankaufgaben ausführen, bei denen die CLR nicht benötigt wird. Ferner kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dadurch Deadlocks erkennen, an denen von CLR-Synchronisierungsobjekten benötigte Sperren beteiligt sind, und traditionelle Techniken zur Entfernung von Deadlocks einsetzen.  
  
 Verwalteter Code wird präemptiv in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeitplanungsmodul kann Threads, die über eine längere Zeitspanne nicht aktiv waren, erkennen und anhalten. Die Funktion zum Verknüpfen von CLR-Threads mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Threads beinhaltet, dass das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeitplanungsmodul „Ausreißerthreads“ in der CLR erkennen und deren Priorität verwalten kann. Solche Ausreißerthreads werden angehalten und in die Warteschlange zurückgestellt. Threads, die mehrfach als Ausreißerthreads identifiziert werden, dürfen für einen gewissen Zeitraum nicht ausgeführt werden, damit andere Arbeitsthreads ausgeführt werden können.  
  
> [!NOTE]  
>  Verwalteter Code mit langer Laufzeit, der auf Daten zugreift oder genug Arbeitsspeicher zuordnet, um Garbage Collection auszulösen, wird automatisch aktiv. Verwalteter Code mit langer Laufzeit, der nicht auf Daten zugreift oder nicht genug Arbeitsspeicher zuweist, um Garbage Collection auszulösen, sollte explizit durch Aufrufen der Funktion System.Thread.Sleep() von .NET Framework aktiv werden.  
  
###### <a name="scalability-common-memory-management"></a>Skalierbarkeit: Allgemeine Arbeitsspeicherverwaltung  
 Die CLR ruft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Grundelemente zum Zuordnen und zum Aufheben der Zuordnung von Arbeitsspeicher auf. Da der von der CLR verwendete Arbeitsspeicher in der Gesamtspeicherauslastung des System berücksichtigt wird, kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] innerhalb der konfigurierten Arbeitsspeichergrenzwerte bleiben und sicherstellen, dass die CLR und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht gegenseitig um Arbeitsspeicher konkurrieren. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann CLR-Arbeitsspeicheranforderungen auch ablehnen, wenn der verfügbare Systemspeicher gering ist, und die CLR anweisen, die Arbeitsspeicherverwendung zu reduzieren, wann andere Tasks Arbeitsspeicher benötigen.  
  
###### <a name="reliability-application-domains-and-unrecoverable-exceptions"></a>Zuverlässigkeit: Anwendungsdomänen und nicht behebbare Ausnahmen  
 Wenn in verwaltetem Code in .NET Framework-APIs schwerwiegende Ausnahmen auftreten, wie nicht genügend Arbeitsspeicher oder Stapelüberlauf, ist es nicht immer möglich, diese Fehler zu beheben und konsistente und korrekte Semantik für die Implementierung zu gewährleisten. Diese APIs lösen als Reaktion auf diese Fehler eine Threadabbruchausnahme aus.  
  
 Beim Hosten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden solche Threadabbrüche folgendermaßen behandelt: Die CLR erkennt jeden Freigabezustand in der Anwendungsdomäne, in der der Threadabbruch auftritt. Die CLR überprüft dazu das Vorhandensein von Synchronisierungsobjekten. Wenn es einen Freigabezustand in der Anwendungsdomäne gibt, dann wird die Anwendungsdomäne selbst entladen. Die Entladung aus der Anwendungsdomäne beendet Datenbanktransaktionen, die gerade in dieser Anwendungsdomäne ausgeführt werden. Da das Vorhandensein eines Freigabezustands die Auswirkungen dieser schwerwiegenden Ausnahmen auf Benutzersitzungen außer der Sitzung, die die Ausnahme ausgelöst hat, vergrößern kann, haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und die CLR Schritte unternommen, um die Wahrscheinlichkeit eines Freigabezustands zu verringern. Weitere Informationen hierzu finden Sie in der .NET Framework- Dokumentation.  
  
###### <a name="security-permission-sets"></a>Sicherheit: Berechtigungssätze  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer können die Zuverlässigkeits- und Sicherheitsanforderungen für Code angeben, der in der Datenbank bereitgestellt wird. Beim Hochladen von Assemblys in die Datenbank kann der Verfasser der Assembly für diese einen von drei Berechtigungssätzen angeben: SAFE, EXTERNAL_ACCESS und UNSAFE.  
  
|||||  
|-|-|-|-|  
|Berechtigungssatz|SAFE|EXTERNAL_ACCESS|UNSAFE|  
|Codezugriffssicherheit|Nur ausführen|Ausführen + Zugriff auf externe Ressourcen|Uneingeschränkt|  
|Beschränkungen des Programmiermodells|ja|Ja|Keine Einschränkungen|  
|Überprüfbarkeit erforderlich|ja|ja|nein|  
|Aufrufbarkeit von systemeigenem Code|nein|Nein|ja|  
  
 SAFE ist der zuverlässigste und sicherste Modus, der mit Einschränkungen hinsichtlich des zulässigen Programmiermodells einhergeht. Assemblys der Stufe SAFE verfügen über ausreichende Berechtigungen für die Ausführung, die Durchführung von Berechnungen und den Zugriff auf die lokale Datenbank. Assemblys der Stufe SAFE müssen nachweislich typsicher sein und dürfen keinen nicht verwalteten Code aufrufen.  
  
 UNSAFE ist für hoch vertrauenswürdigen Code vorgesehen, der nur von Datenbankadministratoren erstellt werden kann. Dieser vertrauenswürdige Code verfügt über keine Codezugriffs-Sicherheitsbeschränkungen und kann nicht verwalteten (systemeigenen) Code aufrufen.  
  
 EXTERNAL_ACCESS stellt eine mittlere Sicherheitsebene dar, bei der Code auf Ressourcen außerhalb der Datenbank zugreifen kann, die aber dennoch so zuverlässig wie SAFE ist.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird mithilfe der auf Hostebene festgelegten Stufe der CAS-Richtlinie eine Hostrichtlinie eingerichtet, die anhand des in den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Katalogen gespeicherten Berechtigungssatzes einen von drei Berechtigungssätzen gewährt. Verwaltetem Code, der in der Datenbank ausgeführt wird, wird immer einer dieser Codezugriffsberechtigungssätze abgerufen.  
  
### <a name="programming-model-restrictions"></a>Einschränkungen des Programmiermodells  
 Im Programmiermodell für verwalteten Code in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Funktionen zum Schreiben, Prozeduren und Typen benötigt, für die normalerweise weder der über mehrere Aufrufe gespeicherte Zustand noch die Freigabe des Zustands über mehrere Benutzersitzungen erforderlich sind. Darüber hinaus kann ein Freigabezustand, wie bereits erläutert, zu schwerwiegenden Ausnahmen führen, die die Skalierbarkeit und Zuverlässigkeit der Anwendung gefährden können.  
  
 Aus diesen Gründen raten wir von der Verwendung von statischen Variablen und Datenelementen von Klassen ab, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden. Bei Assemblys vom Typ SAFE und EXTERNAL_ACCESS untersucht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei der Ausführung von CREATE ASSEMBLY die Metadaten der Assembly. Wenn die Verwendung statischer Datenelemente oder Variablen ermittelt wird, wird die Assembly nicht erstellt.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Außerdem lässt keine Aufrufe von .NET Framework-APIs, die mit versehen sind die **SharedState**, **Synchronisierung** und **ExternalProcessMgmt** Hostschutzattribute. Dies verhindert, dass Assemblys des Typs SAFE und EXTERNAL_ACCESS APIs aufrufen, die die Freigabe des Zustands aktivieren, Synchronisierungen durchführen und die Integrität des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozesses beeinträchtigen. Weitere Informationen finden Sie unter [CLR Integration Programming Model Einschränkungen](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit der CLR-Integration](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Leistung der CLR-Integration](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  
