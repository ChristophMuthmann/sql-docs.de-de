---
title: Hierarchyid (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- hierarchyid
- hierarchyid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Hierarchy data type
- hierarchyid data type
ms.assetid: 69b756e0-a1df-45b3-8a24-6ded8658aefe
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 44299e7ddb90bdd52e2638dd859993513bd6f966
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchyid-data-type-method-reference"></a>Hierarchyid-Datentyp-Methodenverweis
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Die **Hierarchyid** -Datentyp ist eine Variable Länge-Systemdatentyp. Verwendung **Hierarchyid** Position in einer Hierarchie darstellen. Eine Spalte des Typs **hierarchyid** stellt nicht automatisch eine Baumstruktur dar. Es ist Aufgabe der Anwendung, **hierarchyid** -Werte so zu erstellen und zuzuweisen, dass die gewünschte Beziehung zwischen Zeilen anhand der Werte zu erkennen ist.
  
Ein Wert des **hierarchyid** -Datentyps stellt eine Position in einer Strukturhierarchie dar. Werte des Typs **hierarchyid** verfügen über die folgenden Eigenschaften:
  
-   Äußerst komprimiert  
     Die durchschnittliche Zahl der Bits, die erforderlich sind, um einen Knoten in einer Struktur mit *n* Knoten darzustellen, hängt von der durchschnittlichen Anzahl der Verzweigungen (der durchschnittlichen Anzahl untergeordneter Knoten) eines Knotens ab. Für kleine Verzweigungen entspricht diese Zahl (0-7), die Größe beträgt etwa 6\*LogA *n*  Bits, wobei A die durchschnittliche Anzahl der Verzweigungen. Ein Knoten in einer 100.000 Leute umfassenden Organisationshierarchie mit durchschnittlich 6 Verzweigungen benötigt etwa 38 Bit. Dieser Wert wird bei der Speicherung auf 40 Bit oder 5 Byte aufgerundet.  
-   Vergleiche erfolgen in Tiefensuchreihenfolge  
     Bei den beiden **hierarchyid**-Werten **a** und **b** bedeutet **a<b**, dass beim Durchlaufen der Struktur in der Tiefensuchreihenfolge a vor b kommt. Indizes für **hierarchyid**-Datentypen verwenden die Tiefensuchreihenfolge, und einander benachbarte Knoten werden bei der Tiefensuchreihenfolge nahe beieinander gespeichert. Einem Datensatz untergeordnete Datensätze werden zum Beispiel angrenzend an diesen Datensatz gespeichert. Weitere Informationen finden Sie unter [hierarchische Daten &#40; SQLServer &#41; ](../../relational-databases/hierarchical-data-sql-server.md).  
-   Unterstützung willkürlicher Einfüge- und Löschvorgänge  
     Mithilfe der [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) -Methode ist es immer möglich, rechts oder links von einem gegebenen Knoten einen gleichgeordneten Knoten zu generieren oder ihn auch zwischen zwei gleichgeordneten Knoten einzufügen. Die Vergleichseigenschaft bleibt auch dann gewahrt, wenn eine beliebige Anzahl von Knoten in die Hierarchie eingefügt oder aus ihr gelöscht wird. Die meisten Einfüge- und Löschoperationen behalten die Kompaktheitseigenschaft bei. Einfügungen zwischen zwei Knoten erzeugen jedoch hierarchyid-Werte in einer etwas weniger komprimierten Darstellung.  
-   Die Codierung die **Hierarchyid** Typ ist auf 892 Bytes beschränkt. Folglich nicht Knoten, die über zu viele Ebenen in ihrer Darstellung, um in 892 Bytes zu passen dargestellt werden, durch die **Hierarchyid** Typ.  
  
Die **Hierarchyid** -Typ steht CLR-Clients als die **SqlHierarchyId** -Datentyp.
  
## <a name="remarks"></a>Hinweise  
Die **Hierarchyid** Typ codiert Informationen logisch über einen einzelnen Knoten in einer Hierarchiestruktur codieren Sie den Pfad vom Stamm der Struktur auf den Knoten. Ein solcher Pfad wird logisch dargestellt als eine Sequenz von Knotenbezeichnungen aller untergeordneten Elemente nach dem Stammelement. Die Darstellung beginnt mit einem Schrägstrich, und ein Pfad, der nur das Stammelement enthält, wird durch einen einzelnen Schrägstrich dargestellt. Für Ebenen unter dem Stammelement wird jede Bezeichnung als eine Sequenz von ganzen Zahlen codiert, die durch Punkte getrennt sind. Ein Vergleich zwischen untergeordneten Elementen wird ausgeführt, indem die durch Punkte getrennten Sequenzen von ganzen Zahlen in Wörterbuchreihenfolge verglichen werden. Auf jede Ebene folgt ein Schrägstrich. Deshalb werden übergeordnete Elemente von ihren untergeordneten Elementen durch einen ein Schrägstrich getrennt. Im folgenden sind z. B. gültige **Hierarchyid** -Pfade mit Längen, 1, 2, 2, 3 und 3 Ebenen bzw.:
  
-   /  
  
-   /1/  
  
-   /0.3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
Knoten können an jedem Speicherort eingefügt werden. Knoten eingefügt wird, nachdem **/1/2/** aber vor **/1/3/** dargestellt werden kann, als **/1/2.5/**. Knoten, die vor 0 eingefügt wurden, werden in der logischen Darstellung als eine negative Zahl dargestellt. Z. B. ein Knoten, der vorangeht **/1/1/** dargestellt werden kann, als **/1/1 /**. Knoten können nicht über führende Nullen verfügen. Beispielsweise **/1/1.1/** ist gültig, aber **/1/1.01/** ist ungültig. Um Fehler zu vermeiden, fügen Sie auf den Knoten, indem die [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) Methode.
  
## <a name="data-type-conversion"></a>Datentypkonvertierung
Die **Hierarchyid** -Datentyp konvertiert werden kann in andere Datentypen wie folgt:
-   Verwenden der [ToString()](../../t-sql/data-types/tostring-database-engine.md) -Methode zum Konvertieren der **Hierarchyid** Wert, der der logischen Darstellung als eine **nvarchar(4000)** -Datentyp.  
-   Verwendung [lesen ()](../../t-sql/data-types/read-database-engine.md) und [Write ()](../../t-sql/data-types/write-database-engine.md) konvertieren **Hierarchyid** auf **Varbinary**.  
-   Übertragen **Hierarchyid** -Parameter über SOAP wandeln sie zuerst als Zeichenfolgen.  
  
## <a name="upgrading-databases"></a>Aktualisieren von Datenbanken
Beim Upgrade einer Datenbank zu [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], die neue Assembly und die **Hierarchyid** Datentyp automatisch installiert werden soll. Der Upgrade Advisor-Regeln erkennen alle Benutzertypen oder Assemblys mit in Konflikt stehenden Namen. Der Upgrade Advisor schlägt im Fall von in Konflikt stehenden Assemblys das Umbenennen vor, und bei in Konflikt stehenden Typen das Umbenennen oder das Verwenden von zweiteiligen Namen im Code, um auf diesen bereits existierenden Benutzertypen zu verweisen.
  
Wenn bei einem Datenbankupgrade eine Benutzerassembly mit in Konflikt stehendem Namen entdeckt wird, wird diese Assembly automatisch umbenannt und die Datenbank in den Fehlerverdachtmodus versetzt.
  
Sollte während des Upgrades ein Benutzertyp mit in Konflikt stehendem Namen vorhanden sein, werden keine speziellen Schritte ausgeführt. Nach dem Upgrade sind sowohl der alte Benutzertyp als auch der neue Systemtyp vorhanden. Der Benutzertyp steht nur bei Verwendung von zweiteiligen Namen zur Verfügung.
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>Verwenden von Hierarchyid-Spalten in replizierten Tabellen
Spalten vom Typ **Hierarchyid** können in jeder replizierten Tabelle verwendet werden. Die Anforderungen für Ihre Anwendung hängen davon ab, ob die Replikation eindirektional oder bidirektional ist, und davon, welche Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden.
  
### <a name="one-directional-replication"></a>Eindirektionale Replikation
Zur eindirektionalen Replikation gehören die Momentaufnahmereplikation, die Transaktionsreplikation und die Mergereplikation, bei denen Änderungen nicht auf dem Abonnenten vorgenommen werden. Wie **Hierachyid** Spalten arbeiten mit einem eindirektionaler Replikation hängt von der Version des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Abonnenten ausgeführt wird.
-   Ein [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Verleger replizieren kann **Hierachyid** Spalten aus, die eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Abonnenten jederzeit problemlos.  
-   Ein [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Verleger muss konvertieren **Hierarchyid** Spalten, um sie an einen Abonnenten zu replizieren, die ausgeführt wird [!INCLUDE[ssEW](../../includes/ssew-md.md)] oder einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)]und frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen keine **Hierarchyid** Spalten. Wenn Sie mit einer dieser Versionen arbeiten, können Sie trotzdem Daten auf einen Abonnenten replizieren. Dazu müssen Sie eine Schemaoption oder (bei der Mergereplikation) den Veröffentlichungskompatibilitätsgrad festlegen, sodass die Spalte in einen kompatiblen Datentyp konvertiert werden kann.  
  
Die Spaltenfilterung wird in beiden dieser Szenarios unterstützt. Dies beinhaltet auch das Filtern **Hierarchyid** Spalten. Zeilenfilterung wird unterstützt, solange der Filter nicht beinhaltet eine **Hierarchyid** Spalte.
  
### <a name="bi-directional-replication"></a>Bidirektionale Replikation
Zur bidirektionalen Replikation gehören die Transaktionsreplikation mit aktualisierbaren Abonnements, die Peer-zu-Peer-Transaktionsreplikation und die Mergereplikation, bei denen Änderungen auf dem Abonnenten vorgenommen werden. Mit Replikationen können Sie eine Tabelle mit konfigurieren **Hierarchyid** Spalten für die bidirektionale Replikation. Beachten Sie die folgenden Voraussetzungen und Überlegungen.
-   Der Verleger und alle Abonnenten müssen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ausführen.  
-   Bei der Replikation werden die Daten als Bytes repliziert, und die Integrität der Hierarchie wird nicht überprüft.  
-   Die Hierarchie der Änderungen, die an der Quelle vorgenommen wurden (Verleger oder Abonnent) wird nicht beibehalten, wenn die Änderungen auf den Abonnenten repliziert werden.  
-   Die Hashwerte für **Hierarchyid** Spalten gelten für die Datenbank, in dem sie generiert werden. Aus diesem Grund könnte der gleiche Wert auf dem Verleger und dem Abonnenten generiert, jedoch auf verschiedene Zeilen angewendet werden. Replikation wird für diese Bedingung nicht überprüft, und es gibt keine integrierte Option zum Partition **Hierarchyid** -Spaltenwerte für IDENTITY-Spalten vorhanden ist. Anwendungen müssen Einschränkungen oder andere Mechanismen verwenden, um solche unerkannten Konflikte zu vermeiden.  
-   Es ist möglich, dass Zeilen, die auf dem Abonnenten eingefügt werden, verwaist werden. Die übergeordnete Zeile der eingefügten Zeile könnte auf dem Verleger gelöscht worden sein. Dies führt zu einem unerkannten Konflikt, wenn die Zeile vom Abonnenten auf dem Verleger eingefügt wird.  
-   Filter für Datenspalten können nicht herausfiltern NULL- **Hierarchyid** Spalten: Einfügevorgänge vom Abonnenten schlagen fehl, da es kein Standardwert für ist die **Hierarchyid** -Spalte auf dem Verleger.  
-   Zeilenfilterung wird unterstützt, solange der Filter nicht beinhaltet eine **Hierarchyid** Spalte.  
  
## <a name="see-also"></a>Siehe auch
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

