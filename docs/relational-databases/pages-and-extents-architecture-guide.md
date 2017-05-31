---
title: "Handbuch zur Architektur von Seiten und Blöcken | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- page and extent architecture guide
- guide, page and extent architecture
ms.assetid: 83a4aa90-1c10-4de6-956b-7c3cd464c2d2
caps.latest.revision: 2
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 970981a0f8db1baa802a68ea1186211f031488e6
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="pages-and-extents-architecture-guide"></a>Handbuch zur Architektur von Seiten und Blöcken
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

Die Seite ist die grundlegende Einheit für die Datenspeicherung in SQL Server. Ein Block ist eine Auflistung von acht physisch zusammenhängenden Seiten. Blöcke tragen zu einer effizienten Verwaltung von Seiten bei. In diesem Handbuch werden die Datenstrukturen beschrieben, die zum Verwalten von Seiten und Blöcken in allen Versionen von SQL Server verwendet werden. Kenntnisse der Architektur von Seiten und Blöcken sind Voraussetzung für das Entwerfen und Entwickeln von effizienten Datenbanken.

## <a name="pages-and-extents"></a>Seiten und Blöcke

Die grundlegende Einheit für die Datenspeicherung in SQL Server ist die Seite. Der Speicherplatz, der einer Datendatei (MDF- oder NDF-Datei) in einer Datenbank zugeordnet wird, ist logisch in Seiten unterteilt, die fortlaufend von 0 bis n nummeriert sind. Datenträger-E/A-Operationen werden auf Seitenebene ausgeführt. Dies bedeutet, dass SQL Server ganze Datenseiten liest oder schreibt.

Blöcke sind Auflistungen von acht physisch zusammenhängenden Seiten; sie werden zum effizienten Verwalten der Seiten verwendet. Alle Seiten werden in Blöcken gespeichert.

### <a name="pages"></a>Seiten

In SQL Server beträgt die Größe einer Seite 8 KB. Dies bedeutet, dass SQL Server-Datenbanken über 128 Seiten pro 1 MB verfügen. Jede Seite beginnt mit einem 96 Byte umfassenden Header, der zum Speichern von Systeminformationen zu der betreffenden Seite verwendet wird. Diese Informationen umfassen die Seitennummer, den Typ der Seite, den Umfang des freien Speicherplatzes auf der Seite und die ID der Zuordnungseinheit, die Besitzer der Seite ist.

Die folgende Tabelle zeigt die Seitentypen, die in Datendateien einer SQL Server-Datenbank verwendet werden.

|Seitentyp | Inhalt |
|-------|-------|
|Data |Datenzeilen mit allen Daten, ausgenommen Daten der Typen text, ntext, image, nvarchar(max), varchar(max), varbinary(max) und xml, wenn „text in row“ auf ON festgelegt wurde. |
|Index |Indexeinträge |
|Test/Image |LOB-Datentypen (Large Object): (text, ntext, image, nvarchar(max), varchar(max), varbinary(max) und xml) <br> Spalten variabler Länge, wenn die Datenzeile 8 KB übersteigt: (varchar, nvarchar, varbinary und sql_variant) |
|Global Allocation Map, Shared Global Allocation Map |Informationen dazu, ob Blöcke zugeordnet sind. |
|Page Free Space (PFS) |Informationen zur Seitenzuordnung sowie zum freien Speicherplatz, der auf Seiten verfügbar ist. |
|Index Allocation Map (IAM) |Informationen zu Blöcken, die von einer Tabelle oder einem Index pro Zuordnungseinheit verwendet werden. |
|Bulk Changed Map |Informationen zu Blöcken, die seit der letzten Ausführung der BACKUP LOG-Anweisung pro Zuordnungseinheit durch Massenvorgänge geändert wurden. |
|Differential Changed Map |Informationen zu Blöcken, die seit der letzten Ausführung der BACKUP DATABASE-Anweisung pro Zuordnungseinheit geändert wurden. |

> [!NOTE]
> Protokolldateien enthalten keine Seiten; sie enthalten eine Folge von Protokolldatensätze.

Datenzeilen werden unmittelbar nach dem Header nacheinander auf der Seite gespeichert. Eine Zeilenoffsettabelle beginnt am Ende der Seite, und jede Zeilenoffsettabelle enthält einen Eintrag für jede Zeile auf der Seite. Jeder dieser Einträge zeichnet auf, wie weit das erste Byte der Zeile vom Beginn der Seite entfernt ist. Die Einträge in der Zeilenoffsettabelle befinden sich in umgekehrter Reihenfolge zur Reihenfolge der Zeilen auf der Seite.

![page_architecture](../relational-databases/media/page-architecture.gif)

**Unterstützung von umfangreichen Zeilen**  

Zeilen können sich nicht über mehrere Seiten erstrecken, Teile der Zeile können jedoch von der Seite der Zeile verschoben werden; die Zeile kann auf diese Weise sehr umfangreich sein. Die maximale Menge an Daten und Verwaltungsbytes, die in einer einzelnen Zeile auf einer Seite enthalten sein können, beträgt 8.060 Byte (8 KB). Dies schließt jedoch nicht die Daten ein, die im Text/Image-Seitentyp gespeichert werden. Diese Einschränkung wurde für Tabellen gelockert, die varchar-, nvarchar-, varbinary- oder sql_variant-Spalten enthalten. Wenn die Gesamtzeilengröße aller festen und variablen Spalten in einer Tabelle den Grenzwert von 8.060 Bytes übersteigt, verschiebt SQL Server eine oder mehrere Spalten variabler Länge dynamisch auf Seiten in der ROW_OVERFLOW_DATA-Zuordnungseinheit. Dabei wird mit der Spalte mit der größten Breite begonnen. Dieser Vorgang wird immer ausgeführt, wenn die Gesamtgröße der Zeile durch einen Einfüge- oder Updatevorgang den Maximalwert von 8.060 Byte übersteigt. Wenn eine Spalte auf eine Seite in der ROW_OVERFLOW_DATA-Zuordnungseinheit verschoben wird, wird ein 24-Byte-Zeiger auf die ursprüngliche Seite in der IN_ROW_DATA-Zuordnungseinheit verwaltet. Falls eine nachfolgende Operation die Spaltengröße verringert, verschiebt SQL Server die Spalten dynamisch zurück auf die ursprüngliche Datenseite. 


### <a name="extents"></a>Extents 

Blöcke sind die Grundeinheit, in der Speicherplatz verwaltet wird. Ein Block umfasst acht zusammenhängende Seiten, also 64 KB. Dies bedeutet, dass SQL Server-Datenbanken über 16 Blöcke pro 1 MB verfügen.

Um eine effiziente Speicherplatzzuordnung zu erzielen, ordnet SQL Server keine ganzen Blöcke zu Tabellen zu, die nur einen geringen Umfang an Daten enthalten. SQL Server verfügt über zwei Arten von Blöcken: 

* Einheitliche Blöcke befinden sich im Besitz eines einzigen Objekts; alle acht Seiten in dem Block können nur vom besitzenden Objekt verwendet werden.
* Gemischte Blöcke werden für bis zu acht Objekte freigegeben. Jede der acht Seiten im Block kann im Besitz eines anderen Objekts sein.


Für eine neue Tabelle oder einen neuen Index werden normalerweise Seiten aus gemischten Blöcken zugewiesen. Wenn eine Tabelle oder ein Index so groß geworden ist, dass sie bzw. er acht Seiten umfasst, werden bei nachfolgenden Zuweisungen einheitliche Blöcke zugewiesen. Wenn Sie einen Index für eine vorhandene Tabelle erstellen, die über genügend Zeilen verfügt, um acht Seiten im Index zu generieren, erfolgen alle Zuweisungen für den Index in Form von einheitlichen Blöcken.

![Extents](../relational-databases/media/extents.gif)

## <a name="managing-extent-allocations-and-free-space"></a>Verwalten von Blockzuordnungen und freiem Speicherplatz 

Die SQL Server-Datenstrukturen, die Blockzuordnungen verwalten und freien Speicherplatz nachverfolgen, besitzen eine relativ einfache Struktur. Dies bringt folgende Vorteile mit sich: 

* Die Informationen zum freien Speicherplatz sind dicht gepackt, sodass nur relativ wenig Seiten benötigt werden, um diese Informationen aufzunehmen.   
  Auf diese Weise wird die Geschwindigkeit erhöht, da die Anzahl der Lesevorgänge vom Datenträger reduziert wird, die erforderlich sind, um Zuordnungsinformationen abzurufen. Hierdurch wird auch die Wahrscheinlichkeit erhöht, dass die Zuordnungsseiten im Arbeitsspeicher verbleiben und somit keine weiteren Lesevorgänge erforderlich sind. 

* Der größte Teil der Zuordnungsinformationen ist nicht miteinander verkettet. Hierdurch wird die Verwaltung der Zuordnungsinformationen vereinfacht.    
  Das Zuordnen oder Aufheben der Zuordnung der einzelnen Seiten kann sehr schnell erfolgen. So wird die Anzahl der Konflikte zwischen gleichzeitig ausgeführten Tasks reduziert, die Seiten zuordnen oder die Zuordnung von Seiten aufheben müssen. 

### <a name="managing-extent-allocations"></a>Verwalten von Blockzuordnungen

SQL Server verwendet zwei Arten von Zuordnungstabellen, um die Zuordnung von Blöcken aufzuzeichnen: 

* Global Allocation Map (GAM)   
  GAM-Seiten zeichnen auf, welche Blöcke zugeordnet wurden. Jede GAM erfasst 64.000 Blöcke, was fast 4 GB an Daten entspricht. Die GAM verfügt über ein Bit für jeden Block in dem Intervall, das von ihr abgedeckt wird. Hat das Bit den Wert 1, ist der Block frei; hat das Bit den Wert 0, ist der Block zugeordnet. 

* Shared Global Allocation Map (SGAM)   
  SGAM-Seiten zeichnen auf, welche Blöcke zurzeit als gemischte Blöcke verwendet werden und über mindestens eine nicht verwendete Seite verfügen. Jede SGAM erfasst 64.000 Blöcke, was fast 4 GB an Daten entspricht. Die SGAM verfügt über ein Bit für jeden Block in dem Intervall, das von ihr abgedeckt wird. Wenn das Bit den Wert 1 hat, wird der Block als gemischter Block verwendet und verfügt über eine freie Seite. Wenn das Bit den Wert 0 hat, wird der Block nicht als gemischter Block verwendet, oder er wird als gemischter Block verwendet, aber alle seine Seiten werden verwendet. 

Für jeden Block wird auf der Grundlage der aktuellen Verwendung eines der folgenden Bitmuster in der GAM oder der SGAM festgelegt. 

|Aktuelle Blockverwendung | GAM-Biteinstellung | SGAM-Biteinstellung |
|---------|----------|------| 
|Frei, wird nicht verwendet |1 |0 |
|Einheitlicher Block oder vollständig belegter gemischter Block |0 |0 |
|Gemischter Block mit freien Seiten |0 |1 |
 
Dies führt zu einfachen Algorithmen für die Blockverwaltung. Um einen einheitlichen Block zuzuweisen, durchsucht das Datenbankmodul die GAM nach einem Bit mit dem Wert 1 und legt es auf 0 fest. Um einen gemischten Block mit freien Seiten zu finden, durchsucht das Datenbankmodul die SGAM nach einem Bit mit dem Wert 1. Um einen gemischten Block zuzuordnen, durchsucht das Datenbankmodul die GAM nach einem Bit mit dem Wert 1 und legt es auf 0 fest. Anschließend wird das entsprechende Bit in der SGAM auf 1 festgelegt. Um einen Block freizugeben, stellt das Datenbankmodul sicher, dass das GAM-Bit auf 1 und das SGAM-Bit auf 0 festgelegt ist. Die Algorithmen, die vom Datenbankmodul tatsächlich intern verwendet werden, sind komplexer als in diesem Thema beschrieben, da das Datenbankmodul Daten gleichmäßig in der Datenbank verteilt. Aber auch die wirklich verwendeten Algorithmen konnten vereinfacht werden, da nunmehr keine verketteten Blockzuordnungsinformationen verwaltet werden müssen.

### <a name="tracking-free-space"></a>Nachverfolgen von freiem Speicherplatz

PFS-Seiten (Page Free Space) zeichnen den Zuordnungsstatus der einzelnen Seiten auf, ob eine einzelne Seite zugeordnet wurde und die Menge des freien Speicherplatzes auf den einzelnen Seiten. Der PFS verfügt über ein Byte pro Seite und zeichnet auf, ob die Seite zugeordnet ist, und sofern dies der Fall ist, ob sie leer, 1 bis 50 Prozent voll, 51 bis 80 Prozent voll, 81 bis 95 Prozent voll oder 96 bis 100 Prozent voll ist.

Nachdem ein Block einem Objekt zugeordnet wurde, verwendet das Datenbankmodul die PFS-Seiten, um aufzuzeichnen, welche Seiten in dem jeweiligen Block zugeordnet und welche Seiten frei sind. Diese Informationen werden verwendet, wenn das Datenbankmodul eine neue Seite zuordnen muss. Die Menge des freien Speicherplatzes auf einer Seite wird nur für Heap- und Text/Image-Seiten verwaltet. Diese Information wird verwendet, wenn das Datenbankmodul eine Seite mit verfügbarem freien Speicherplatz sucht, um eine neu eingefügte Zeile aufzunehmen. Indizes erfordern nicht, dass der Page Free Space nachverfolgt werden soll, da die Stelle, an der eine neue Zeile eingefügt werden soll, von den Indexschlüsselwerten festgelegt wird.

Eine PFS-Seite ist nach der Dateiheaderseite die erste Seite in einer Datendatei (Seitennummer 1). Auf diese folgt eine GAM-Seite (Seitennummer 2) und anschließend eine SGAM-Seite (Seite 3). Ungefähr alle 8.000 Seiten nach der ersten PFS-Seite folgt eine weitere PFS-Seite. 64.000 Blöcke nach der ersten GAM-Seite folgt eine weitere GAM-Seite auf Seite 2. Eine weitere SGAM-Seite folgt 64.000 Blöcke nach der ersten SGAM-Seite auf Seite 3. Folgende Abbildung veranschaulicht die Abfolge der Seiten, die vom Datenbankmodul für das Zuordnen und Verwalten von Blöcken verwendet werden.

![manage_extents](../relational-databases/media/manage-extents.gif)

## <a name="managing-space-used-by-objects"></a>Verwalten des von Objekten verwendeten Speicherplatzes 

Eine IAM-Seite (Index Allocation Map) enthält die in einem 4-Gigabyte-Teil (GB) einer von einer Zuordnungseinheit verwendeten Datenbankdatei enthaltenen Blöcke. Eine Zuordnungseinheit entspricht einem von drei möglichen Typen:

* IN_ROW_DATA   
    Enthält eine Partition eines Heap oder eines Index.

* LOB_DATA   
   Enthält LOB-Datentypen (Large Object) wie xml, varbinary(max) und varchar(max).

* ROW_OVERFLOW_DATA   
   Enthält Daten variabler Länge, die in varchar-, nvarchar-, varbinary- oder sql_variant-Spalten gespeichert sind, die das Zeilengrößenlimit von 8.060 Bytes überschreiten. 

Jede Partition eines Heap oder Index enthält mindestens eine IN_ROW_DATA-Zuordnungseinheit. Sie kann je nach dem Heap- oder Indexschema auch eine LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheit enthalten. Weitere Informationen zu Zuordnungseinheiten finden Sie unter „Organisationsstruktur von Tabellen und Indizes“.

Eine IAM-Seite deckt einen 4-GB-Bereich in einer Datei ab und besitzt dieselbe Erfassung wie eine GAM- oder SGAM-Seite. Wenn die Zuordnungseinheit Blöcke mehrerer Dateien oder mehrere 4-GB-Bereiche einer Datei enthält, werden mehrere IAM-Seiten zu einer IAM-Kette verknüpft. Deshalb hat jede Zuordnungseinheit mindestens eine IAM-Seite für jede Datei, aus der sie Blöcke enthält. Es kann auch mehrere IAM-Seiten für eine Datei geben, wenn der Bereich der Blöcke aus der Datei, die für die Zuordnungseinheit zugeordnet ist, den Bereich übersteigt, den eine einzelne IAM-Seite aufzeichnen kann. 

![iam_pages](../relational-databases/media/iam-pages.gif)

IAM-Seiten werden je nach Bedarf für jede Zuordnungseinheit zugeordnet und nach dem Zufallsprinzip in der Datei verteilt. Die Systemsicht „sys.system_internals_allocation_units“ verweist auf die erste IAM-Seite für eine Zuordnungseinheit. Alle IAM-Seiten für diese Zuordnungseinheit werden in einer Kette miteinander verknüpft.

> [!IMPORTANT]
> Die Systemsicht „sys.system_internals_allocation_units“ ist nur zur internen Verwendung bestimmt und kann geändert werden. Kompatibilität wird nicht sichergestellt.

![iam_chain](../relational-databases/media/iam-chain.gif)
 
Pro Zuordnungseinheit in einer Kette verknüpfte IAM-Seiten. Eine IAM-Seite verfügt über einen Header, der den Anfangsblock des Bereichs von Blöcken kennzeichnet, die von der IAM-Seite zugeordnet werden. Die IAM-Seite verfügt darüber hinaus über ein großes Bitmuster, in dem jedes Bit einen Block darstellt. Das erste Bit in dem Bitmuster stellt den ersten Block im Bereich dar, das zweite Bit stellt den zweiten Block dar usw. Wenn ein Bit den Wert 0 hat, ist der Block, den es darstellt, nicht für die Zuordnungseinheit zugeordnet, die die IAM besitzt. Wenn das Bit den Wert 1 hat, ist der Block, den es darstellt, für die Zuordnungseinheit zugeordnet, die die IAM-Seite besitzt.

Wenn vom SQL Server-Datenbankmodul eine neue Zeile eingefügt werden muss und auf der aktuellen Seite kein Speicherplatz verfügbar ist, werden die IAM- und PFS-Seiten verwendet, um eine zuzuordnende Seite zu finden oder – bei einem Heap oder einer Text-/Image-Seite – um eine Seite mit ausreichend Platz zur Aufnahme der Zeile zu finden. Das Datenbankmodul verwendet IAM-Seiten, um die Blöcke zu suchen, die für die Zuordnungseinheit zugeordnet sind. Für jeden Block durchsucht das Datenbankmodul die PFS-Seiten, um herauszufinden, ob eine geeignete Seite vorhanden ist. Jede IAM- und PFS-Seite erfasst viele Datenseiten, sodass in jeder Datenbank nur wenige IAM- und PFS-Seiten enthalten sind. Dies bedeutet, dass sich die IAM- und PFS-Seiten normalerweise im Arbeitsspeicher des SQL Server-Pufferpools befinden, sodass sie schnell durchsucht werden können. Für Indizes wird die Einfügemarke einer neuen Zeile durch den Indexschlüssel festgelegt. In diesem Fall wird der zuvor beschriebene Suchprozess nicht verwendet.

Ein neuer Block wird nur dann vom Datenbankmodul zu einer Zuordnungseinheit zugeordnet, wenn es nicht schnell möglich ist, in einem vorhandenen Block eine Seite zu finden, die ausreichend Speicherplatz bietet, um die eingefügte Zeile aufnehmen zu können. Das Datenbankmodul ordnet Blöcke auf der Basis der verfügbaren Blöcke in der Dateigruppe zu und verwendet dazu einen proportionalen Zuordnungsalgorithmus. Wenn eine Dateigruppe zwei Dateien enthält, von denen die eine über doppelt so viel freien Speicherplatz wie die andere verfügt, werden in der Datei, die über mehr freien Speicherplatz verfügt, zwei Seiten für jede Seite zugeordnet, die in der anderen Datei zugeordnet wird. Dies bedeutet, dass der Anteil des verwendeten Speicherplatzes in allen Dateien einer Dateigruppe ähnlich groß sein sollte. 

 
## <a name="tracking-modified-extents"></a>Protokollieren geänderter Blöcke 

SQL Server verwendet zwei interne Datenstrukturen zum Nachverfolgen von durch Massenkopiervorgänge geänderten Blöcken sowie von Blöcken, die seit der letzten vollständigen Sicherung geändert wurden. Diese Datenstrukturen beschleunigen differenzielle Sicherungen erheblich. Sie beschleunigen außerdem das Protokollieren von Massenkopiervorgängen, wenn eine Datenbank das Modell der massenprotokollierten Wiederherstellung verwendet. Ähnlich wie bei den GAM-Seiten (Global Allocation Map) und den SGAM-Seiten (Shared Global Allocation Map) handelt es sich bei diesen Strukturen um Bitmuster, wobei jedes Bit einen einzelnen Block darstellt. 

* Differential Changed Map (DCM)   
   Protokolliert die Blöcke, die seit der letzten Ausführung der BACKUP DATABASE-Anweisung geändert wurden. Falls das Bit für einen Block den Wert 1 besitzt, wurde der Block seit der letzten Ausführung der BACKUP DATABASE-Anweisung geändert. Falls das Bit den Wert 0 aufweist, wurde der Block nicht geändert. Differenzielle Sicherungen lesen nur die DCM-Seiten, um zu ermitteln, welche Blöcke geändert wurden. Dadurch wird die Anzahl an Seiten, die eine differenzielle Sicherung scannen muss, erheblich verringert. Die Dauer der Ausführung einer differenziellen Sicherung ist proportional zu der Anzahl an Blöcken, die seit der letzten Ausführung der BACKUP DATABASE-Anweisung geändert wurden, und nicht proportional zu der Gesamtgröße der Datenbank. 

* Bulk Changed Map (BCM)   
   Protokolliert die Blöcke, die seit der letzten Ausführung der BACKUP LOG-Anweisung durch massenprotokollierte Vorgänge geändert wurden. Falls das Bit für einen Block den Wert 1 aufweist, wurde der Block seit der letzten Ausführung der BACKUP LOG-Anweisung durch einen massenprotokollierten Vorgang geändert. Falls das Bit den Wert 0 besitzt, wurde der Block nicht durch massenprotokollierte Vorgänge geändert. BCM-Seiten treten in allen Datenbanken auf, sind jedoch nur dann relevant, wenn die Datenbank das Modell der massenprotokollierten Wiederherstellung verwendet. Wenn bei diesem Wiederherstellungsmodell eine BACKUP LOG-Anweisung ausgeführt wird, scannt der Sicherungsvorgang die BCM-Seiten nach Blöcken, die geändert wurden. Diese Blöcke werden dann in die Protokollsicherung eingeschlossen. Dadurch können die massenprotokollierten Vorgänge wiederhergestellt werden, wenn die Datenbank aus einer Datenbanksicherung und einer Folge von Transaktionsprotokollsicherungen wiederhergestellt wird. BCM-Seiten sind in einer Datenbank, die das einfache Wiederherstellungsmodell verwendet, nicht relevant, da keine massenprotokollierten Vorgänge protokolliert sind. Sie sind in einer Datenbank, die das Modell der vollständigen Wiederherstellung verwendet, relevant, da bei diesem Wiederherstellungsmodell massenprotokollierte Vorgänge wie vollständig protokollierte Vorgänge behandelt werden. 

Der Abstand zwischen DCM-Seiten und BCM-Seiten ist derselbe Abstand wie zwischen GAM- und SGAM-Seiten; 64.000 Blöcke. Die DCM- und BCM-Seiten befinden sich direkt hinter den GAM- und SGAM-Seiten in einer physischen Datei:

![special_page_order](../relational-databases/media/special-page-order.gif)
 

