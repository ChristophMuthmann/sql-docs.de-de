---
title: hierarchyid (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 654bdd48517f903c61e30e847d6bd948bafde579
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="hierarchyid-data-type-method-reference"></a>Methodenverweis für den Datentyp „hierarchyid“
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Der **hierarchyid**-Datentyp ist ein Systemdatentyp mit variabler Länge. Sie können **hierarchyid** verwenden, um die Position in einer Hierarchie darzustellen. Eine Spalte des Typs **hierarchyid** stellt nicht automatisch eine Baumstruktur dar. Es ist Aufgabe der Anwendung, **hierarchyid** -Werte so zu erstellen und zuzuweisen, dass die gewünschte Beziehung zwischen Zeilen anhand der Werte zu erkennen ist.
  
Ein Wert des **hierarchyid** -Datentyps stellt eine Position in einer Strukturhierarchie dar. Werte des Typs **hierarchyid** verfügen über die folgenden Eigenschaften:
  
-   Äußerst komprimiert  
     Die durchschnittliche Zahl der Bits, die erforderlich sind, um einen Knoten in einer Struktur mit *n* Knoten darzustellen, hängt von der durchschnittlichen Anzahl der Verzweigungen (der durchschnittlichen Anzahl untergeordneter Knoten) eines Knotens ab. Bei wenigen Verzweigungen (0–7) entspricht diese Zahl etwa 6\*logA*n* Bit, wobei A die durchschnittliche Anzahl von Verzweigungen angibt. Ein Knoten in einer 100.000 Leute umfassenden Organisationshierarchie mit durchschnittlich 6 Verzweigungen benötigt etwa 38 Bit. Dieser Wert wird bei der Speicherung auf 40 Bit oder 5 Byte aufgerundet.  
-   Vergleiche erfolgen in Tiefensuchreihenfolge  
     Bei den beiden **hierarchyid**-Werten **a** und **b** bedeutet **a<b**, dass beim Durchlaufen der Struktur in der Tiefensuchreihenfolge a vor b kommt. Indizes für **hierarchyid**-Datentypen verwenden die Tiefensuchreihenfolge, und einander benachbarte Knoten werden bei der Tiefensuchreihenfolge nahe beieinander gespeichert. Einem Datensatz untergeordnete Datensätze werden zum Beispiel angrenzend an diesen Datensatz gespeichert. Weitere Informationen finden Sie unter [Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
-   Unterstützung willkürlicher Einfüge- und Löschvorgänge  
     Mithilfe der [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) -Methode ist es immer möglich, rechts oder links von einem gegebenen Knoten einen gleichgeordneten Knoten zu generieren oder ihn auch zwischen zwei gleichgeordneten Knoten einzufügen. Die Vergleichseigenschaft bleibt auch dann gewahrt, wenn eine beliebige Anzahl von Knoten in die Hierarchie eingefügt oder aus ihr gelöscht wird. Die meisten Einfüge- und Löschoperationen behalten die Kompaktheitseigenschaft bei. Einfügungen zwischen zwei Knoten erzeugen jedoch hierarchyid-Werte in einer etwas weniger komprimierten Darstellung.  
-   Die im **hierarchyid**-Typ verwendete Codierung ist auf 892 Bytes beschränkt. Knoten, die zu viele Ebenen in ihrer Darstellung haben, um in 892 Bytes zu passen, können nicht vom **hierarchyid**-Typ dargestellt werden.  
  
Der **hierarchyid**-Typ ist für CLR-Clients als **SqlHierarchyId**-Datentyp verfügbar.
  
## <a name="remarks"></a>Remarks  
Der **hierarchyid**-Typ codiert Informationen logisch über einen einzelnen Knoten in einer Hierarchiestruktur, indem der Pfad vom Stammelement der Struktur bis zum Knoten codiert wird. Ein solcher Pfad wird logisch dargestellt als eine Sequenz von Knotenbezeichnungen aller untergeordneten Elemente nach dem Stammelement. Die Darstellung beginnt mit einem Schrägstrich, und ein Pfad, der nur das Stammelement enthält, wird durch einen einzelnen Schrägstrich dargestellt. Für Ebenen unter dem Stammelement wird jede Bezeichnung als eine Sequenz von ganzen Zahlen codiert, die durch Punkte getrennt sind. Ein Vergleich zwischen untergeordneten Elementen wird ausgeführt, indem die durch Punkte getrennten Sequenzen von ganzen Zahlen in Wörterbuchreihenfolge verglichen werden. Auf jede Ebene folgt ein Schrägstrich. Deshalb werden übergeordnete Elemente von ihren untergeordneten Elementen durch einen ein Schrägstrich getrennt. Die folgenden Beispiele sind gültige **hierarchyid**-Pfade mit Längen von jeweils 1, 2, 2, 3 und 3 Ebenen:
  
-   /  
  
-   /1/  
  
-   /0.3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
Knoten können an jedem Speicherort eingefügt werden. Knoten, die nach **/1/2/**, aber vor **/1/3/** eingefügt werden, können als **/1/2.5/** dargestellt werden. Knoten, die vor 0 eingefügt wurden, werden in der logischen Darstellung als eine negative Zahl dargestellt. Beispielsweise kann ein Knoten vor **/1/1/** als **/1/–1/** dargestellt werden. Knoten können nicht über führende Nullen verfügen. Beispiel: **/1/1.1/** ist gültig, **/1/1.01/** hingegen nicht. Fügen Sie Knoten mit der [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md)-Methode ein, um Fehler zu vermeiden.
  
## <a name="data-type-conversion"></a>Datentypkonvertierung
Der **hierarchyid**-Datentyp kann folgendermaßen in andere Datentypen konvertiert werden:
-   Verwenden Sie die [ToString()](../../t-sql/data-types/tostring-database-engine.md)-Methode, um den **hierarchyid**-Wert als einen **nvarchar(4000)**-Datentyp in die logische Darstellung zu konvertieren.  
-   Verwenden Sie [Read()](../../t-sql/data-types/read-database-engine.md) und [Write()](../../t-sql/data-types/write-database-engine.md), um **hierarchyid** in **varbinary** zu konvertieren.  
-   Um **hierarchyid**-Parameter über SOAP zu übertragen, wandeln Sie sie zunächst in Zeichenfolgen um.  
  
## <a name="upgrading-databases"></a>Aktualisieren von Datenbanken
Wenn eine Datenbank auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aktualisiert wird, werden die neue Assembly und der **hierarchyid**-Datentyp automatisch installiert. Upgrade Advisor-Regeln erkennen alle Benutzertypen oder Assemblys mit in Konflikt stehenden Namen. Der Upgrade Advisor schlägt im Fall von in Konflikt stehenden Assemblys das Umbenennen vor, und bei in Konflikt stehenden Typen das Umbenennen oder das Verwenden von zweiteiligen Namen im Code, um auf diesen bereits existierenden Benutzertypen zu verweisen.
  
Wenn bei einem Datenbankupgrade eine Benutzerassembly mit in Konflikt stehendem Namen entdeckt wird, wird diese Assembly automatisch umbenannt und die Datenbank in den Fehlerverdachtmodus versetzt.
  
Sollte während des Upgrades ein Benutzertyp mit in Konflikt stehendem Namen vorhanden sein, werden keine speziellen Schritte ausgeführt. Nach dem Upgrade sind sowohl der alte Benutzertyp als auch der neue Systemtyp vorhanden. Der Benutzertyp steht nur bei Verwendung von zweiteiligen Namen zur Verfügung.
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>Verwenden von hierarchyid-Spalten in replizierten Tabellen
Spalten vom Typ **hierarchyid** können in jeder replizierten Tabelle verwendet werden. Die Anforderungen für Ihre Anwendung hängen davon ab, ob die Replikation eindirektional oder bidirektional ist, und davon, welche Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden.
  
### <a name="one-directional-replication"></a>Eindirektionale Replikation
Zur eindirektionalen Replikation gehören die Momentaufnahmereplikation, die Transaktionsreplikation und die Mergereplikation, bei denen Änderungen nicht auf dem Abonnenten vorgenommen werden. Wie **hierarchyid**-Spalten bei eindirektionaler Replikation funktionieren, hängt von der Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab, die der Abonnent ausführt.
-   Ein [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Verleger kann **hierarchyid**-Spalten problemlos für einen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Abonnenten replizieren.  
-   Ein [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Verleger muss **hierarchyid**-Spalten konvertieren, um sie auf einem Abonnenten zu replizieren, der [!INCLUDE[ssEW](../../includes/ssew-md.md)] oder eine frühere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführt. In [!INCLUDE[ssEW](../../includes/ssew-md.md)] und früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden **hierarchyid**-Spalten nicht unterstützt. Wenn Sie mit einer dieser Versionen arbeiten, können Sie trotzdem Daten auf einen Abonnenten replizieren. Dazu müssen Sie eine Schemaoption oder (bei der Mergereplikation) den Veröffentlichungskompatibilitätsgrad festlegen, sodass die Spalte in einen kompatiblen Datentyp konvertiert werden kann.  
  
Die Spaltenfilterung wird in beiden dieser Szenarios unterstützt. Dies beinhaltet auch das Filtern von **hierarchyid**-Spalten. Die Zeilenfilterung wird unterstützt, wenn der Filter keine **hierarchyid**-Spalte enthält.
  
### <a name="bi-directional-replication"></a>Bidirektionale Replikation
Zur bidirektionalen Replikation gehören die Transaktionsreplikation mit aktualisierbaren Abonnements, die Peer-zu-Peer-Transaktionsreplikation und die Mergereplikation, bei denen Änderungen auf dem Abonnenten vorgenommen werden. Bei der Replikation können Sie eine Tabelle mit **hierarchyid**-Spalten für die bidirektionale Replikation konfigurieren. Beachten Sie die folgenden Voraussetzungen und Überlegungen.
-   Der Verleger und alle Abonnenten müssen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ausführen.  
-   Bei der Replikation werden die Daten als Bytes repliziert, und die Integrität der Hierarchie wird nicht überprüft.  
-   Die Hierarchie der Änderungen, die an der Quelle vorgenommen wurden (Verleger oder Abonnent) wird nicht beibehalten, wenn die Änderungen auf den Abonnenten repliziert werden.  
-   Die Hashwerte für **hierarchyid**-Spalten sind für die Datenbank spezifisch, in der sie generiert werden. Aus diesem Grund könnte der gleiche Wert auf dem Verleger und dem Abonnenten generiert, jedoch auf verschiedene Zeilen angewendet werden. Bei der Replikation wird diese Bedingung nicht überprüft, und es gibt keine integrierte Methode, um **hierarchyid**-Spaltenwerte zu partitionieren (eine Methode, die für IDENTITY-Spalten zur Verfügung steht). Anwendungen müssen Einschränkungen oder andere Mechanismen verwenden, um solche unerkannten Konflikte zu vermeiden.  
-   Es ist möglich, dass Zeilen, die auf dem Abonnenten eingefügt werden, verwaist werden. Die übergeordnete Zeile der eingefügten Zeile könnte auf dem Verleger gelöscht worden sein. Dies führt zu einem unerkannten Konflikt, wenn die Zeile vom Abonnenten auf dem Verleger eingefügt wird.  
-   Spaltenfilter können **hierarchyid**-Spalten, die nicht auf Null festgelegt werden können, nicht filtern: Einfügevorgänge vom Abonnenten schlagen fehl, da es keinen Standardwert für die **hierarchyid**-Spalte auf dem Verleger gibt.  
-   Die Zeilenfilterung wird unterstützt, wenn der Filter keine **hierarchyid**-Spalte enthält.  
  
## <a name="see-also"></a>Siehe auch
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
