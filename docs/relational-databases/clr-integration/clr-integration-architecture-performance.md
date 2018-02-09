---
title: Leistung der CLR-Integration | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- common language runtime [SQL Server], compilation process
- performance [CLR integration]
ms.assetid: 7ce2dfc0-4b1f-4dcb-a979-2c4f95b4cb15
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 327c531d44fc883afa144252dda3ba43d188682a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="clr-integration-architecture----performance"></a>Architektur der CLR-Integration - Leistung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In diesem Artikel werden einige der Entwurfsoptionen, die die Leistung verbessern [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Integration in die [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework common Language Runtime (CLR).  
  
## <a name="the-compilation-process"></a>Der Kompilierungsprozess  
 Wenn während der Kompilierung von SQL-Ausdrücken ein Verweis auf eine verwaltete Routine gefunden wird, wird ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] Intermediate Language (MSIL)-Stub generiert. Dieser Stub enthält Code zum Marshallen der Routineparameter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu CLR, zum Aufrufen der Funktion und zur Rückgabe des Ergebnisses. Dieser "Verbindungscode" basiert auf dem Parametertyp und der Parameterrichtung (IN, OUT oder Verweis).  
  
 Der Verbindungscode ermöglicht typspezifische Optimierungen und stellt die wirksame Durchsetzung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Semantik sicher, wie beispielsweise NULL-Zulässigkeit, Einschränkungsfacets, Nach-Wert-Verarbeitung und standardmäßige Ausnahmebehandlung. Durch die Codegenerierung für genaue Argumenttypen vermeiden Sie Kosten für Typenumwandlung und die Erstellung von Wrapperobjekten ("Boxing" genannt) über die Aufrufgrenze hinweg.  
  
 Der generierte Stub wird dann mithilfe des Just-in-Time(JIT)-Kompilierungsdiensts von CLR in systemeigenen Code kompiliert und für die spezifische Hardwarearchitektur, in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, optimiert. Die JIT-Dienste werden auf Methodenebene aufgerufen und ermöglichen es der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hostumgebung, eine einheitliche Kompilierungseinheit zu erstellen, die sowohl [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als auch die CLR-Ausführung beinhaltet. Sobald der Stub kompiliert ist, wird der resultierende Funktionszeiger zur Laufzeitimplementierung der Funktion. Dieses Codegenerierungsverfahren stellt sicher, dass keine zusätzlichen Aufrufkosten durch Reflexion oder Metadatenzugriff zur Laufzeit entstehen.  
  
### <a name="fast-transitions-between-sql-server-and-clr"></a>Schnelle Übergänge zwischen SQL Server und CLR  
 Der Kompilierungsprozess erzeugt einen Funktionszeiger, der zur Laufzeit über systemeigenen Code aufgerufen werden kann. Bei benutzerdefinierten Skalarwertfunktionen erfolgt dieser Funktionsaufruf auf Zeilenbasis. Um die Kosten für den Übergang zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und CLR zu minimieren, verfügen Anweisungen, die verwaltete Aufrufe beinhalten, über einen Startschritt zur Identifizierung der Zielanwendungsdomäne. Dieser Identifizierungsschritt reduziert die Kosten für den Übergang der einzelnen Zeilen.  
  
## <a name="performance-considerations"></a>Überlegungen zur Leistung  
 Im Folgenden werden Informationen über Leistungsaspekte in Bezug auf die CLR-Integration in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gegeben. Ausführlichere Informationen finden Sie unter "[mithilfe der CLR-Integration in SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=50332)" auf der MSDN-Website. Allgemeine Informationen über die Leistungsfähigkeit von verwaltetem Code finden Sie "[verbessern .NET Application Performance and Scalability](http://go.microsoft.com/fwlink/?LinkId=50333)" auf der MSDN-Website.  
  
### <a name="user-defined-functions"></a>Benutzerdefinierte Funktionen  
 CLR-Funktionen profitieren im Vergleich zu benutzerdefinierten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen von einem schnelleren Aufrufpfad. Zudem bietet verwalteter Code im Vergleich zu [!INCLUDE[tsql](../../includes/tsql-md.md)] deutliche Leistungsvorteile in Bezug auf den prozeduralen Code, die Berechnung und die Zeichenfolgenbearbeitung. Rechenintensive CLR-Funktionen, die keinen Datenzugriff ausführen, sollten bevorzugt in verwaltetem Code geschrieben werden. [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen führen Datenzugriffe jedoch effizienter aus als die CLR-Integration.  
  
### <a name="user-defined-aggregates"></a>Benutzerdefinierte Aggregate  
 Verwalteter Code ist deutlich leistungsfähiger als die cursorbasierte Aggregation. Verwalteter Code ist in der Regel etwas langsamer als integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Aggregatfunktionen. Wir empfehlen daher, eine systemeigene integrierte Aggregatfunktion zu verwenden, sofern sie zur Verfügung steht. In Fällen, in denen die benötigte Aggregation nicht vom System unterstützt wird, sollten Sie aus Gründen der Leistungsfähigkeit ein CLR-benutzerdefiniertes Aggregat einer cursorbasierten Implementierung den Vorzug geben.  
  
### <a name="streaming-table-valued-functions"></a>Streaming-Tabellenwertfunktionen  
 Anwendungen müssen oft als Reaktion auf einen Funktionsaufruf eine Tabelle als Ergebnis zurückgeben. Beispiele dafür sind das Lesen von Tabellendaten aus einer Datei als Teil eines Importvorgangs oder die Konvertierung von durch Trennzeichen getrennten Werte in eine relationale Darstellung. In der Regel erreichen Sie dies durch Materialisieren und Auffüllen der Ergebnistabelle, bevor sie vom Aufrufer verwendet werden kann. Mit der Integration von CLR in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ein neuer Erweiterungsmechanismus eingeführt, der als Streaming-Tabellenwertfunktion (STVF) bezeichnet wird. Verwaltete STVF sind leistungsfähiger als vergleichbare Implementierungen mit erweiterten gespeicherten Prozeduren.  
  
 STVF sind verwaltete Funktionen, die Zurückgeben einer **IEnumerable** Schnittstelle. **IEnumerable** verfügt über Methoden, um das Resultset von STVF zurückgegebenen zu navigieren. Wenn die STVF aufgerufen wird, das zurückgegebene **IEnumerable** direkt mit dem Abfrageplan verbunden ist. Der Abfrageplan ruft **IEnumerable** Methoden, wenn er Zeilen abrufen muss. Dieses Iterationsmodell ermöglicht es, dass Ergebnisse sofort nach Abruf der ersten Zeile verarbeitet werden. Es muss nicht gewartet werden, bis die gesamte Tabelle aufgefüllt ist. Dadurch wird zudem der durch den Funktionsaufruf benötigte Arbeitsspeicher stark reduziert.  
  
### <a name="arrays-vs-cursors"></a>Arrays und Cursor  
 Wenn [!INCLUDE[tsql](../../includes/tsql-md.md)]-Cursor Daten traversieren müssen, die als Array einfacher auszudrücken sind, kann verwalteter Code verwendet und die Leistung dadurch gesteigert werden.  
  
### <a name="string-data"></a>Zeichenfolgendaten  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Zeichendaten, wie z. B. **Varchar**, kann vom Typ SqlString oder SqlChars in verwalteten Funktionen sein. SqlString-Variablen erstellen im Arbeitsspeicher eine Instanz des gesamten Werts. SqlChars-Variablen stellen eine Streamingschnittstelle bereit, mit der eine höhere Leistung und bessere Skalierbarkeit erreicht wird, die jedoch nicht zum Erstellen einer Instanz des gesamten Werts im Arbeitsspeicher verwendet werden kann. Dies ist besonders für Daten großer Objekte (Large Objects, LOB) wichtig. Darüber hinaus durch eine streamingschnittstelle zurückgegebene XML-Serverdaten zugegriffen werden kann **SqlXml.CreateReader()**.  
  
### <a name="clr-vs-extended-stored-procedures"></a>CLR und Erweiterte gespeicherte Prozeduren  
 Die Microsoft.SqlServer.Server-APIs (Application Programming Interfaces), die es verwalteten Prozeduren ermöglichen, Resultsets zurück an den Client zu senden, sind leistungsfähiger als die von erweiterten gespeicherten Prozeduren verwendeten Open Data Services(ODS)-APIs. Darüber hinaus die System.Data.SqlServer-APIs unterstützen Datentypen wie z. B. **Xml**, **varchar(max)**, **nvarchar(max)**, und **varbinary(max)**, die mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], während ODS-APIs nicht erweitert wurde, um die neuen Datentypen unterstützen.  
  
 Mit verwaltetem Code verwaltet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Verwendung von Ressourcen wie beispielsweise Arbeitsspeicher, Threads und Synchronisierung. Das rührt daher, dass die verwalteten APIs, die diese Ressourcen verfügbar machen, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressourcen-Manager implementiert werden. Hingegen verfügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] über keine Sicht für oder Kontrolle über die Ressourcenverwendung der erweiterten gespeicherten Prozedur. Wenn eine erweiterte gespeicherte Prozedur beispielsweise zu viel CPU- oder Speicherressourcen belegt, gibt es keine Möglichkeit, dies mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu erkennen oder zu kontrollieren. Mit verwaltetem Code kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hingegen erkennen, dass ein bestimmter Thread längere Zeit nicht aktiv war, und dann die Ausführung des Tasks erzwingen, damit andere Arbeit geplant werden kann. Infolgedessen kann mit verwaltetem Code eine bessere Skalierbarkeit und Systemressourcenverwendung erreicht werden.  
  
 Durch verwalteten Code können möglicherweise zusätzliche Kosten für die Aufrechterhaltung der Ausführungsumgebung sowie die Durchführung von Sicherheitsüberprüfungen entstehen. Das ist beispielsweise dann der Fall, wenn die Ausführung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfolgt und zahlreiche Übergänge von verwaltetem zu systemeigenem Code erforderlich sind (denn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss für threadspezifische Einstellungen beim Übergang in systemeigenen Code und zurück zusätzlichen Wartungsaufwand betreiben). Folglich können erweiterte gespeicherte Prozeduren die Leistung im Vergleich zu verwaltetem Code, der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, unter Umständen deutlich erhöhen, nämlich in Situationen mit häufigen Übergängen zwischen verwaltetem und systemeigenem Code.  
  
> [!NOTE]  
>  Es wird jedoch empfohlen, keine neuen erweiterten gespeicherten Prozeduren zu entwickeln, da diese Funktion veraltet ist.  
  
### <a name="native-serialization-for-user-defined-types"></a>Systemeigene Serialisierung für benutzerdefinierte Typen  
 Benutzerdefinierte Typen (UDTs) wurden als Erweiterungsmechanismus für das Skalartypsystem entworfen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]implementiert das Serialisierungsformat für UDTs **Format.Native**. Während der Kompilierung wird die Struktur des Typs zur Generierung von MSIL geprüft, das für die betreffende Typdefinition angepasst wird.  
  
 Die systemeigene Serialisierung ist die Standardimplementierung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die benutzerdefinierte Serialisierung ruft eine Methode auf, die vom Typautor für die Durchführung der Serialisierung definiert wurde. **Format.Native** Serialisierung zu verwendende möglichst für eine optimale Leistung.  
  
### <a name="normalization-of-comparable-udts"></a>Normalisierung vergleichbarer UDTs  
 Relationale Vorgänge, z. B. die Sortierung und das Vergleichen von UDTs, verwenden direkt die binäre Darstellung des Werts. Zu diesem Zweck wird eine normalisierte (binär sortierte) Darstellung des UDT-Zustands auf Festplatte gespeichert.  
  
 Normalisierungen bieten zwei Vorteile: Erstens verringern sie den Arbeitsaufwand für den Vergleich erheblich, indem sie die Konstruktion der Typinstanz und die Kosten für den Methodenaufruf vermeiden. Zweitens erstellen sie eine binäre Domäne für den UDT und ermöglichen so die Konstruktion von Histogrammen, Indizes und Histogrammen für Werte des Typs. Daher haben normalisierte UDTs ein Leistungsprofil, das dem von systemeigenen integrierten Typen sehr ähnlich ist, wenn es sich um Vorgänge handelt, die keinen Methodenaufruf erfordern.  
  
### <a name="scalable-memory-usage"></a>Skalierbare Speicherverwendung  
 Damit die verwaltete Speicherbereinigung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] problemlos durchgeführt und skaliert werden kann, vermeiden Sie einzelne große Zuteilungen. Zuteilungen, die größer als 88 Kilobytes (KB) sind, werden im Objektheap für große Objekte positioniert. Das führt dazu, dass die automatische Speicherbereinigung schlechter ausgeführt und skaliert wird als bei vielen kleinen Zuteilungen. Wenn Sie beispielsweise ein großes mehrdimensionales Array zuteilen müssen, empfiehlt es sich, ein verzweigtes Array zuzuteilen.  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
