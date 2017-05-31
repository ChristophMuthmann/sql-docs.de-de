---
title: Beschreibung von gruppierten und nicht gruppierten Indizes | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query optimizer [SQL Server], index usage
- index concepts [SQL Server]
ms.assetid: b7d6b323-728d-4763-a987-92e6292f6f7a
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 01dfceee2f0d4fb1e0c475333be49e6dacec1c3f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="clustered-and-nonclustered-indexes-described"></a>Beschreibung von gruppierten und nicht gruppierten Indizes
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Ein Index ist eine Struktur auf dem Datenträger, die einer Tabelle oder einer Sicht zugeordnet ist und durch die das Abrufen von Zeilen aus der Tabelle oder Sicht beschleunigt wird. Ein Index enthält Schlüssel, die aus einer oder mehreren Spalten in der Tabelle oder Sicht erstellt werden. Diese Schlüssel werden in einer Struktur (B-Struktur) gespeichert, die es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht, die den Schlüsselwerten zugeordneten Zeilen schnell und effizient zu finden.  
  
 Eine Tabelle oder Sicht kann die folgenden Indextypen enthalten:  
  
-   Gruppiert  
  
    -   Gruppierte Indizes sortieren und speichern die Datenzeilen in der Tabelle oder Sicht basierend auf ihren Schlüsselwerten. Dies sind die Spalten, die in der Indexdefinition enthalten sind. Pro Tabelle kann nur ein gruppierter Index vorhanden sein, da die Datenzeilen nur in einer Reihenfolge sortiert werden können.  
  
    -   Datenzeilen in einer Tabelle werden nur dann in sortierter Reihenfolge gespeichert, wenn die Tabelle einen gruppierten Index enthält. Wenn eine Tabelle einen gruppierten Index besitzt, wird die Tabelle als gruppierte Tabelle bezeichnet. Wenn eine Tabelle nicht über einen gruppierten Index verfügt, werden die Datenzeilen in einer nicht geordneten Struktur gespeichert, die als Heap bezeichnet wird.  
  
-   Nicht gruppiert  
  
    -   Nicht gruppierte Indizes weisen eine Struktur auf, die von den Datenzeilen getrennt ist. Ein nicht gruppierter Index enthält die Schlüsselwerte des nicht gruppierten Indexes. Jeder Schlüsselwerteintrag verfügt über einen Zeiger auf die Datenzeile, die den Schlüsselwert enthält.  
  
    -   Der Zeiger von einer Indexzeile in einem nicht gruppierten Index auf eine Datenzeile wird als Zeilenlokator bezeichnet. Die Struktur des Zeilenlokators hängt davon ab, ob die Datenseiten in einem Heap oder einer gruppierten Tabelle gespeichert sind. Bei einem Heap ist der Zeilenlokator ein Zeiger auf die Zeile. Bei einer gruppierten Tabelle entspricht der Zeilenlokator dem Schlüssel des gruppierten Indexes.  
  
    -   Sie können der Blattebene des nicht gruppierten Indexes Nichtschlüsselspalten hinzufügen, um vorhandene Beschränkungen des Indexschlüssels (900 Bytes und 16 Schlüsselspalten) zu umgehen und vollständig abgedeckte, indizierte Abfragen auszuführen. Weitere Informationen finden Sie unter [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
 Sowohl gruppierte als auch nicht gruppierte Indizes können eindeutig sein. Dies bedeutet, dass nicht derselbe Indexschlüsselwert für zwei oder mehr Zeilen verwendet werden darf. Andernfalls handelt es sich nicht um einen eindeutigen Index, und mehrere Zeilen können denselben Schlüsselwert verwenden. Weitere Informationen finden Sie unter [Erstellen eindeutiger Indizes](../../relational-databases/indexes/create-unique-indexes.md).  
  
 Indizes werden bei jeder Änderung der Tabellendaten automatisch für eine Tabelle oder Sicht verwaltet.  
  
 Zusätzliche Indextypen für besondere Zwecke finden Sie unter [Indexes](../../relational-databases/indexes/indexes.md) .  
  
## <a name="indexes-and-constraints"></a>Indizes und Einschränkungen  
 Indizes werden automatisch erstellt, wenn PRIMARY KEY- und UNIQUE-Einschränkungen für Tabellenspalten definiert werden. Wenn Sie z. B. eine Tabelle erstellen und eine bestimmte Spalte als Primärschlüssel angeben, erstellt [!INCLUDE[ssDE](../../includes/ssde-md.md)] automatisch eine PRIMARY KEY-Einschränkung und einen Index für die betreffende Spalte. Weitere Informationen finden Sie unter [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md) und [Create Unique Constraints](../../relational-databases/tables/create-unique-constraints.md).  
  
## <a name="how-indexes-are-used-by-the-query-optimizer"></a>Verwenden von Indizes durch den Abfrageoptimierer  
 Sorgfältig entworfene Indizes können die E/A-Operationen dem Datenträger verringern und weniger Systemressourcen belegen. Sie optimieren aus diesem Grund die Abfrageleistung. Indizes können bei einer Vielzahl von Abfragen hilfreich sein, die die Anweisungen SELECT, UPDATE, DELETE oder MERGE enthalten. Sehen Sie sich die `SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250` -Abfrage in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank an. Wenn diese Abfrage ausgeführt wird, wertet der Abfrageoptimierer alle verfügbaren Methoden zum Abrufen der Daten aus und wählt dann die effizienteste Methode aus. Bei dieser Methode kann es sich um einen Tabellenscan oder möglicherweise um einen Scan eines Indexes oder mehrerer Indizes handeln, wenn Indizes vorhanden sind.  
  
 Bei der Ausführung eines Tabellenscans liest der Abfrageoptimierer alle Zeilen in der Tabelle und extrahiert dann die Zeilen, die die Abfragekriterien erfüllen. Ein Tabellenscan generiert zahlreiche E/A-Operationen des Datenträgers und kann ressourcenintensiv sein. Ein Tabellenscan kann jedoch die effizienteste Methode sein, wenn z. B. das Resultset der Abfrage einen großen Prozentsatz der Zeilen aus der Tabelle enthält.  
  
 Wenn der Abfrageoptimierer einen Index verwendet, werden die Indexschlüsselspalten durchsucht, der Speicherort der von der Abfrage benötigten Zeilen ermittelt und die entsprechenden Zeilen aus diesem Speicherort extrahiert. Im Allgemeinen ist das Durchsuchen des Indexes wesentlich schneller als das Durchsuchen der Tabelle, weil ein Index im Gegensatz zu einer Tabelle häufig nur sehr wenige Spalten pro Zeile enthält und die Zeilen eine sortierte Reihenfolge aufweisen.  
  
 Der Abfrageoptimierer wählt beim Ausführen von Abfragen normalerweise die effizienteste Methode aus. Wenn jedoch keine Indizes verfügbar sind, muss der Abfrageoptimierer einen Tabellenscan verwenden. Ihre Aufgabe besteht darin, Indizes zu entwerfen und zu erstellen, die optimal für Ihre Umgebung geeignet sind, damit der Abfrageoptimierer seine Auswahl unter mehreren effizienten Indizes treffen kann. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt den [Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md) bereit, der Sie bei der Analyse Ihrer Datenbankumgebung und der Auswahl der geeigneten Indizes unterstützt.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Erstellen gruppierter Indizes](../../relational-databases/indexes/create-clustered-indexes.md)  
  
 [Erstellen nicht gruppierter Indizes](../../relational-databases/indexes/create-nonclustered-indexes.md)  
  
  

