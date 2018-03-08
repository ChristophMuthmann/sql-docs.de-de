---
title: Hierarchische Daten (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: relational-databases-misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [SQL Server], tables to support
- hierarchyid [Database Engine], concepts
- hierarchical tables [Database Engine]
- SqlHierarchyId
- hierarchyid [Database Engine]
- hierarchical queries [SQL Server], using hierarchyid data type
ms.assetid: 19aefa9a-fbc2-4b22-92cf-67b8bb01671c
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9eee39caae6b780e692ed0cee3440b6cb250da9f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="hierarchical-data-sql-server"></a>Hierarchische Daten (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Der integrierte Datentyp **hierarchyid** vereinfacht das Speichern und Abfragen hierarchischer Daten. **hierarchyid** wird zum Darstellen von Strukturen, dem häufigsten Typ hierarchischer Daten, optimiert.  
  
 Hierarchische Daten sind definiert als Satz von Datenelementen, die durch hierarchische Beziehungen miteinander verbunden sind. Hierarchische Beziehungen sind vorhanden, wenn ein Datenelement einem anderen Element übergeordnet ist. Beispiele für die hierarchischen Daten, die im Allgemeinen in Datenbanken gespeichert werden:  
  
-   Eine Organisationsstruktur  
  
-   Ein Dateisystem  
  
-   Eine Gruppe von Aufgaben in einem Projekt.  
  
-   Eine Taxonomie sprachlicher Termini  
  
-   Ein Diagramm der Links zwischen Webseiten  
  
 Mit dem Datentyp [hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md) können Sie Tabellen mit einer hierarchischen Struktur erstellen oder die hierarchische Struktur der Daten an einem anderen Speicherort beschreiben. Verwenden Sie die [hierarchyid-Funktionen](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06) in [!INCLUDE[tsql](../includes/tsql-md.md)] , um hierarchische Daten abzufragen und zu verwalten.  
  
##  <a name="keyprops"></a> Haupteigenschaften von hierarchyid  
 Ein Wert des **hierarchyid** -Datentyps stellt eine Position in einer Strukturhierarchie dar. Werte des Typs **hierarchyid** verfügen über die folgenden Eigenschaften:  
  
-   Äußerst komprimiert  
  
     Die durchschnittliche Zahl der Bits, die erforderlich sind, um einen Knoten in einer Struktur mit *n* Knoten darzustellen, hängt von der durchschnittlichen Anzahl der Verzweigungen (der durchschnittlichen Anzahl untergeordneter Knoten) eines Knotens ab. Bei wenigen Verzweigungen (0-7) entspricht diese Zahl etwa 6\*logA*n* Bit, wobei A die durchschnittliche Anzahl von Verzweigungen angibt. Ein Knoten in einer 100.000 Leute umfassenden Organisationshierarchie mit durchschnittlich 6 Verzweigungen benötigt etwa 38 Bit. Dieser Wert wird bei der Speicherung auf 40 Bit oder 5 Byte aufgerundet.  
  
-   Vergleiche erfolgen in Tiefensuchreihenfolge  
  
     Bei den beiden **hierarchyid**-Werten **a** und **b** bedeutet **a<b**, dass beim Durchlaufen der Struktur in der Tiefensuchreihenfolge a vor b kommt. Indizes für **hierarchyid**-Datentypen verwenden die Tiefensuchreihenfolge, und einander benachbarte Knoten werden bei der Tiefensuchreihenfolge nahe beieinander gespeichert. Einem Datensatz untergeordnete Datensätze werden zum Beispiel angrenzend an diesen Datensatz gespeichert.  
  
-   Unterstützung willkürlicher Einfüge- und Löschvorgänge  
  
     Mithilfe der [GetDescendant](../t-sql/data-types/getdescendant-database-engine.md) -Methode ist es immer möglich, rechts oder links von einem gegebenen Knoten einen gleichgeordneten Knoten zu generieren oder ihn auch zwischen zwei gleichgeordneten Knoten einzufügen. Die Vergleichseigenschaft bleibt auch dann gewahrt, wenn eine beliebige Anzahl von Knoten in die Hierarchie eingefügt oder aus ihr gelöscht wird. Die meisten Einfüge- und Löschoperationen behalten die Kompaktheitseigenschaft bei. Einfügungen zwischen zwei Knoten erzeugen jedoch hierarchyid-Werte in einer etwas weniger komprimierten Darstellung.  
  
  
##  <a name="limits"></a> Einschränkungen von hierarchyid  
 Für den **hierarchyid** -Datentyp gelten folgende Einschränkungen:  
  
-   Eine Spalte des Typs **hierarchyid** stellt nicht automatisch eine Baumstruktur dar. Es ist Aufgabe der Anwendung, **hierarchyid** -Werte so zu erstellen und zuzuweisen, dass die gewünschte Beziehung zwischen Zeilen anhand der Werte zu erkennen ist. Einige Anwendungen können eine Spalte vom Typ **hierarchyid** aufweisen, der den Speicherort in einer Hierarchie angibt, die in einer anderen Tabelle definiert ist.  
  
-   Es ist Aufgabe der Anwendung, die Parallelität zu verwalten, indem sie geeignete **hierarchyid** -Werte generiert und zuweist. Es gibt keine Garantie dafür, dass die **hierarchyid** -Werte einer Spalte eindeutig sind, sofern die Anwendung keine Einschränkung für einen eindeutigen Schlüssel verwendet oder selbst dafür sorgt, dass eindeutige Werte erzeugt werden.  
  
-   Hierarchische, durch **hierarchyid** -Werte dargestellte Beziehungen werden nicht wie Fremdschlüsselbeziehungen durchgesetzt. Es ist möglich und manchmal auch angemessen, eine hierarchische Beziehung herzustellen, in der das Element B dem Element A untergeordnet ist, um dann A zu löschen, wodurch B mit einer Beziehung zu einem nicht mehr vorhandenen Datensatz verbleibt. Wenn dieses Verhalten unannehmbar ist, muss die Anwendung vor dem Löschen von Elementen prüfen, ob untergeordnete Elemente vorhanden sind.  
  
  
##  <a name="alternatives"></a> Wann Alternativen zu hierarchyid zu verwenden sind  
 Zur Darstellung hierarchischer Daten gibt es zwei Alternativen zu **hierarchyid** . Diese sind:  
  
-   Über- und untergeordnet  
  
-   XML  
  
 **hierarchyid** ist diesen Alternativen im Allgemeinen überlegen. Jedoch gibt es bestimmte, unten aufgelistete Situationen, in denen diese Alternativen wahrscheinlich überlegen sind.  
  
### <a name="parentchild"></a>Über- und untergeordnet  
 Beim Ansatz mit über- und untergeordneten Elementen enthält jede Zeile einen Verweis auf das übergeordnete Element. Im folgenden Beispiel wird eine typische Tabelle definiert, welche die über- und untergeordneten Zeilen einer Über-/Unterordnungsbeziehung enthält.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE TABLE ParentChildOrg  
   (  
    BusinessEntityID int PRIMARY KEY,  
    ManagerId int REFERENCES ParentChildOrg(BusinessEntityID),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
```  
  
 Vergleich von über- und untergeordneten Elementen mit **hierarchyid** bei allgemeinen Vorgängen  
  
-   Teilstrukturabfragen sind mit **hierarchyid**bedeutend schneller.  
  
-   Abfragen für direkt untergeordnete Elemente sind bei **hierarchyid**etwas langsamer.  
  
-   Das Verschieben innerer Knoten erfolgt bei **hierarchyid**langsamer.  
  
-   Das Einfügen innerer Knoten und das Einfügen oder Verschieben von Blattknoten weisen bei **hierarchyid**die gleiche Komplexität auf.  
  
 Über- und untergeordnete Elemente könnten überlegen sein, wenn die folgenden Bedingungen vorliegen:  
  
-   Die Größe des Schlüssels ist wichtig. Bei gleicher Anzahl von Knoten ist ein **hierarchyid** -Wert gleich groß oder größer als ein Integer-Wert (**smallint**, **int**, **bigint**). Das ist allerdings nur in seltenen Fällen ein Grund, über- und untergeordnete Elemente zu verwenden, denn **hierarchyid** ist bezüglich E/A- und CPU-Auslastung weitaus effizienter als die allgemeinen Tabellenausdrücke, die bei Verwendung einer Über-/Unterordnungsstruktur erforderlich sind.  
  
-   Abfragen erstrecken sich selten über Abschnitte der Hierarchie. Eine Abfrage bezieht sich mit anderen Worten in der Regel auf einen bestimmten Punkt in der Hierarchie. In diesen Fällen ist die benachbarte Speicherung der Elemente nicht wichtig. Eine Struktur über- und untergeordneter Elemente ist beispielsweise dann überlegen, wenn die Organisationstabelle nur für die Verarbeitung von Gehaltsdaten einzelner Angestellter verwendet wird.  
  
-   Innere Knotenteilstrukturen verschieben sich häufig, und dabei ist die Leistung sehr wichtig. Wird in einer Über-/Unterordnungsstruktur die Position einer Zeile in der Hierarchie geändert, ist davon nur eine einzelne Zeile betroffen. Die Änderung der Position einer Zeile in einer **hierarchyid** -Struktur betrifft *n* Zeilen, wobei *n* die Zahl der Knoten angibt, die in der Teilstruktur verschoben werden.  
  
     Wenn sich innere Knotenteilstrukturen häufig verschieben und die Leistung wichtig ist, jedoch die meisten Verschiebeoperationen auf einer wohldefinierten Ebene der Hierarchie stattfinden, sollten Sie erwägen, die höheren und niedrigeren Ebenen in zwei Hierarchien aufzuteilen. Dadurch beschränken sich alle Verschiebungen auf Blattebenen der höheren Hierarchie. Betrachten Sie beispielsweise eine Hierarchie der von einem Dienst gehosteten Websites. Websites enthalten viele auf hierarchische Weise angeordnete Seiten. Gehostete Sites können an einen anderen Ort innerhalb der Site-Hierarchie verschoben werden, jedoch werden die untergeordneten Seiten nur selten neu angeordnet. Dies könnte wie folgt dargestellt werden:  
  
    ```  
    CREATE TABLE HostedSites   
       (  
        SiteId hierarchyid, PageId hierarchyid  
       ) ;  
    GO  
    ```  
  
  
### <a name="xml"></a>XML  
 Ein XML-Dokument ist eine Baumstruktur, daher kann eine einzige Instanz eines XML-Datentyps eine vollständige Hierarchie repräsentieren. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ein XML-Index erstellt, werden intern **hierarchyid** -Werte verwendet, welche die Position in der Hierarchie angeben.  
  
 Die Verwendung des XML-Datentyps kann überlegen sein, wenn alle folgenden Punkte zutreffen:  
  
-   Es wird immer die vollständige Hierarchie gespeichert und abgerufen.  
  
-   Die Daten werden von der Anwendung im XML-Format verarbeitet.  
  
-   Prädikatssuchen werden äußerst selten verwendet und die Leistung ist nicht wichtig.  
  
 Wenn eine Anwendung zum Beispiel mehrere Organisationen verfolgt, immer die gesamte Organisationshierarchie speichert und abruft sowie keine einzelne Organisation abfragt, dann könnte eine Tabelle der folgenden Form sinnvoll sein:  
  
```  
CREATE TABLE XMLOrg   
    (  
    Orgid int,  
    Orgdata xml  
    ) ;  
GO  
```  
  
  
##  <a name="indexing"></a> Indizieren von Strategien für hierarchische Daten  
 Für die Indizierung hierarchischer Daten gibt es zwei Strategien:  
  
-   **Tiefensuche**  
  
     Bei einem Tiefensuchindex werden Zeilen in einer Teilstruktur nahe beieinander gespeichert. Zum Beispiel werden alle Mitarbeiter, die einem bestimmten Manager berichten, in der Nähe des Datensatzes dieses Managers gespeichert.  
  
     In einem Tiefensuchindex sind alle Knoten in der Teilstruktur eines Knotens zusammen angeordnet. Daher sind Tiefensuchindizes besonders effizient bei der Abfrage von Teilstrukturen, etwa bei Abfragen des Typs "Ermittle alle Dateien in diesem Ordner und seinen Unterordnern".  
  
-   **Breitensuche**  
  
     Bei einem Breitensuchindex werden die Zeilen jeder Ebene der Hierarchie zusammen gespeichert. Zum Beispiel werden die Datensätze aller Mitarbeiter, die direkt einem bestimmten Manager berichten, nahe beieinander gespeichert.  
  
     In einem Breitensuchindex sind alle einem Knoten untergeordneten Knoten zusammen angeordnet. Daher sind Breitensuchindizes besonders effizient bei der Abfrage von unmittelbar untergeordneten Elementen, etwa bei Abfragen des Typs "Ermittle alle Angestellten, die direkt diesem Manager berichten".  
  
 Ob Sie einen Tiefen- oder Breitensuchindex verwenden und welchen Sie (wenn überhaupt) als Gruppierungsschlüssel definieren, hängt von der relativen Wichtigkeit der oben genanten Abfragetypen ab sowie von der relativen Wichtigkeit von SELECT- gegenüber DML-Vorgängen. Ein ausführliches Beispiel zu Indizierungsstrategien finden Sie unter [Tutorial: Using the hierarchyid Data Type](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md).  
  
  
### <a name="creating-indexes"></a>Erstellen von Indizes  
 Die Methode „GetLevel()“ kann verwendet werden, um eine Breitensuchreihenfolge zu erstellen. Im folgenden Beispiel werden sowohl Breitensuch- als auch Tiefensuchindizes erstellt:  
  
```wmimof  
USE AdventureWorks2012 ;   
GO  
  
CREATE TABLE Organization  
   (  
    BusinessEntityID hierarchyid,  
    OrgLevel as BusinessEntityID.GetLevel(),   
    EmployeeName nvarchar(50) NOT NULL  
   ) ;  
GO  
  
CREATE CLUSTERED INDEX Org_Breadth_First   
ON Organization(OrgLevel,BusinessEntityID) ;  
GO  
  
CREATE UNIQUE INDEX Org_Depth_First   
ON Organization(BusinessEntityID) ;  
GO  
```  
  
  
## <a name="examples"></a>Beispiele  
  
### <a name="simple-example"></a>Einfaches Beispiel  
 Das folgende Beispiel wurde absichtlich einfach gehalten, um Ihnen die ersten Schritte zu erleichtern. Erstellen Sie zunächst eine Tabelle, in der einige geografischen Daten gespeichert werden sollen.  
  
```  
CREATE TABLE SimpleDemo  
(Level hierarchyid NOT NULL,  
Location nvarchar(30) NOT NULL,  
LocationType nvarchar(9) NULL);  
```  
  
 Fügen Sie nun Daten für einige Kontinente, Länder, Bundesstaaten und Städte ein.  
  
```  
INSERT SimpleDemo  
VALUES   
('/1/', 'Europe', 'Continent'),  
('/2/', 'South America', 'Continent'),  
('/1/1/', 'France', 'Country'),  
('/1/1/1/', 'Paris', 'City'),  
('/1/2/1/', 'Madrid', 'City'),  
('/1/2/', 'Spain', 'Country'),  
('/3/', 'Antarctica', 'Continent'),  
('/2/1/', 'Brazil', 'Country'),  
('/2/1/1/', 'Brasilia', 'City'),  
('/2/1/2/', 'Bahia', 'State'),  
('/2/1/2/1/', 'Salvador', 'City'),  
('/3/1/', 'McMurdo Station', 'City');  
```  
  
 Wählen Sie die Daten aus, und fügen Sie eine Spalte hinzu, durch die die Daten für die Ebene (Level) in einen leicht verständlichen Textwert konvertiert werden. Mit dieser Abfrage wird das Ergebnis auch nach dem **hierarchyid** -Datentyp sortiert.  
  
```  
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], *   
FROM SimpleDemo ORDER BY Level;  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
Converted Level  Level     Location         LocationType  
/1/              0x58      Europe           Continent  
/1/1/            0x5AC0    France           Country  
/1/1/1/          0x5AD6    Paris            City  
/1/2/            0x5B40    Spain            Country  
/1/2/1/          0x5B56    Madrid           City  
/2/              0x68      South America    Continent  
/2/1/            0x6AC0    Brazil           Country  
/2/1/1/          0x6AD6    Brasilia         City  
/2/1/2/          0x6ADA    Bahia            State  
/2/1/2/1/        0x6ADAB0  Salvador         City  
/3/              0x78      Antarctica       Continent  
/3/1/            0x7AC0    McMurdo Station  City  
```  
  
 Beachten Sie, dass die Hierarchie über eine gültige Struktur verfügt, obwohl sie intern nicht konsistent ist. Bahia ist der einzige Bundesstaat. Er wird in der Hierarchie als gleichgeordnetes Element der Stadt Brasilia angezeigt. Entsprechend wird auch für McMurdo Station kein übergeordnetes Land angegeben. Die Benutzer müssen entscheiden, ob dieser Hierarchietyp für ihre Zwecke geeignet ist.  
  
 Fügen Sie eine weitere Zeile hinzu, und wählen Sie die Ergebnisse aus.  
  
```  
INSERT SimpleDemo  
VALUES ('/1/3/1/', 'Kyoto', 'City'), ('/1/3/1/', 'London', 'City');  
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], * FROM SimpleDemo ORDER BY Level;  
```  
  
 Dadurch werden weitere potenzielle Probleme deutlich. Kyoto kann als Ebene `/1/3/1/` eingefügt werden, obwohl keine übergeordnete Ebene `/1/3/`vorhanden ist. Darüber hinaus verfügen sowohl London als auch Kyoto für **hierarchyid**über denselben Wert. Auch in diesem Fall müssen die Benutzer entscheiden, ob dieser Hierarchietyp für sie geeignet ist und Werte blockieren, die nicht brauchbar sind.  
  
 Auch in dieser Tabelle wurde die oberste Hierarchieebene `'/'`nicht verwendet. Sie wurde weggelassen, weil die Kontinente kein gemeinsames übergeordnetes Element aufweisen. Sie können den gesamten Planeten hinzufügen, falls Sie ein gemeinsames übergeordnetes Element benötigen.  
  
```  
INSERT SimpleDemo  
VALUES ('/', 'Earth', 'Planet');  
```  
  
##  <a name="tasks"></a> Verwandte Aufgaben  
  
###  <a name="migrating"></a> Migrieren von über- und untergeordneten Elementen zu hierarchyid  
 Die meisten Strukturen werden mit über- und untergeordneten Elementen dargestellt. Der einfachste Weg, eine Über-/Unterordnungsstruktur in eine Tabelle zu migrieren, die **hierarchyid** verwendet, führt über eine temporäre Spalte oder eine temporäre Tabelle, in der die Anzahl von Knoten auf jeder Ebene der Hierarchie festgehalten wird. Ein Beispiel für die Migration einer über- und untergeordneten Tabelle finden Sie in Lektion 1 von [Tutorial: Verwenden des hierarchyid-Datentyps](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md).  
  
  
###  <a name="BKMK_ManagingTrees"></a> Verwalten einer Struktur mit hierarchyid  
 Eine **hierarchyid** -Spalte muss zwar nicht notwendigerweise eine Struktur darstellen, jedoch kann eine Anwendung dies auf einfache Weise sicherstellen.  
  
-   Führen Sie eine der folgenden Maßnahmen durch, wenn Sie neue Werte erstellen:  
  
    -   Halten Sie die Nummer des letzten untergeordneten Elements in der übergeordneten Zeile fest.  
  
    -   Berechnen Sie das letzte untergeordnete Element. Für die effiziente Ausführung dieser Berechnung ist ein Breitensuchindex erforderlich.  
  
-   Setzen Sie Eindeutigkeit durch, indem Sie für die Spalte, vielleicht als Teil eines Gruppierungsschlüssels, einen eindeutigen Index erstellen. Um sicherzustellen, dass eindeutige Werte eingefügt werden, führen Sie eine der folgenden Maßnahmen durch:  
  
    -   Spüren Sie Verletzungen des eindeutigen Indexes auf und wiederholen Sie den Vorgang.  
  
    -   Bestimmen Sie die Eindeutigkeit eines jeden neuen untergeordneten Knotens, und fügen Sie ihn als Teil einer serialisierbaren Transaktion ein.  
  
  
#### <a name="example-using-error-detection"></a>Beispiel für Fehlererkennung  
 Der Code im folgenden Beispiel berechnet den **EmployeeId** -Wert des neuen untergeordneten Elements, und spürt anschließend eine Schlüsselverletzung auf, worauf er zur Markierung **INS_EMP** zurückkehrt, um den **EmployeeId** -Wert für die neue Zeile neu zu berechnen:  
  
```  
USE AdventureWorks ;  
GO  
  
CREATE TABLE Org_T1  
   (  
    EmployeeId hierarchyid PRIMARY KEY,  
    OrgLevel AS EmployeeId.GetLevel(),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
  
CREATE INDEX Org_BreadthFirst ON Org_T1(OrgLevel, EmployeeId)  
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50) )   
AS  
BEGIN  
    DECLARE @last_child hierarchyid  
INS_EMP:   
    SELECT @last_child = MAX(EmployeeId) FROM Org_T1   
    WHERE EmployeeId.GetAncestor(1) = @mgrid  
INSERT Org_T1 (EmployeeId, EmployeeName)  
SELECT @mgrid.GetDescendant(@last_child, NULL), @EmpName   
-- On error, return to INS_EMP to recompute @last_child  
IF @@error <> 0 GOTO INS_EMP   
END ;  
GO  
```  
  
  
#### <a name="example-using-a-serializable-transaction"></a>Beispiel für eine serialisierbare Transaktion  
 Für den **Org_BreadthFirst** -Index stellt sicher, dass **@last_child** mittels einer Bereichssuche ermittelt wird. Zusätzlich zu anderen Fehlerfällen könnte eine Anwendung prüfen, ob eine Verletzung aufgrund doppelter Schlüssel darauf hindeutet, dass versucht wurde, mehrere Angestellte mit der gleichen ID einzufügen, weshalb **@last_child** neu berechnet werden muss. Im folgenden Code werden eine serialisierbare Transaktion und ein Breitensuchindex verwendet, um den neuen Knotenwert zu berechnen:  
  
```  
CREATE TABLE Org_T2  
    (  
    EmployeeId hierarchyid PRIMARY KEY,  
    LastChild hierarchyid,   
    EmployeeName nvarchar(50)   
    ) ;  
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50))   
AS  
BEGIN  
DECLARE @last_child hierarchyid  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION   
  
UPDATE Org_T2   
SET @last_child = LastChild = EmployeeId.GetDescendant(LastChild,NULL)  
WHERE EmployeeId = @mgrid  
INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(@last_child, @EmpName)  
COMMIT  
END ;  
```  
  
 Im folgenden Code wird die Tabelle mit drei Zeilen aufgefüllt. Anschließend werden die Ergebnisse zurückgegeben:  
  
```  
INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(hierarchyid::GetRoot(), 'David') ;  
GO  
AddEmp 0x , 'Sariya'  
GO  
AddEmp 0x58 , 'Mary'  
GO  
SELECT * FROM Org_T2  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
EmployeeId LastChild EmployeeName  
---------- --------- ------------  
0x        0x58       David  
0x58      0x5AC0     Sariya  
0x5AC0    NULL       Mary  
```  
  
  
###  <a name="BKMK_EnforcingTrees"></a> Durchsetzen einer Struktur  
 In den Beispielen oben wird veranschaulicht, wie eine Anwendung sicherstellen kann, dass eine Struktur gewahrt bleibt. Um eine Struktur mithilfe von Einschränkungen durchzusetzen, kann eine berechnete Spalte mit einer Fremdschlüsseleinschränkung für die Primärschlüssel-ID erstellt werden, die das übergeordnete Element jedes Knotens berechnet.  
  
```  
CREATE TABLE Org_T3  
(  
   EmployeeId hierarchyid PRIMARY KEY,  
   ParentId AS EmployeeId.GetAncestor(1) PERSISTED    
      REFERENCES Org_T3(EmployeeId),  
   LastChild hierarchyid,   
   EmployeeName nvarchar(50)  
)  
GO  
```  
  
 Diese Methode der Durchsetzung einer Beziehung ist dann vorzuziehen, wenn Code, dem bezüglich der Bewahrung der hierarchischen Struktur nicht vertraut werden kann, über direkten DML-Zugriff auf die Tabelle verfügt. Diese Methode könnte jedoch die Leistung reduzieren, da die Einschränkung bei jedem DML-Vorgang geprüft werden muss.  
  
  
###  <a name="findclr"></a> Suchen von Vorgängern mit CLR  
 Ein allgemeiner Vorgang, der zwei Knoten einer Hierarchie betrifft, ist die Ermittlung des kleinsten gemeinsamen Vorgängers. Dies kann in [!INCLUDE[tsql](../includes/tsql-md.md)] oder CLR geschrieben werden, weil der **hierarchyid** -Typ in beiden verfügbar ist. CLR wird empfohlen, da die Leistung höher ist.  
  
 Verwenden Sie den folgenden CLR-Code, um die Vorgänger aufzulisten und den kleinsten gemeinsamen Vorgänger zu ermitteln:  
  
```  
using System;  
using System.Collections;  
using System.Text;  
using Microsoft.SqlServer.Server;  
using Microsoft.SqlServer.Types;  
  
public partial class HierarchyId_Operations  
{  
    [SqlFunction(FillRowMethodName = "FillRow_ListAncestors")]  
    public static IEnumerable ListAncestors(SqlHierarchyId h)  
    {  
        while (!h.IsNull)  
        {  
            yield return (h);  
            h = h.GetAncestor(1);  
        }  
    }  
    public static void FillRow_ListAncestors(Object obj, out SqlHierarchyId ancestor)  
    {  
        ancestor = (SqlHierarchyId)obj;  
    }  
  
    public static HierarchyId CommonAncestor(SqlHierarchyId h1, HierarchyId h2)  
    {  
        while (!h1.IsDescendant(h2))  
            h1 = h1.GetAncestor(1);  
  
        return h1;  
    }  
}  
```  
  
 Um die Methoden **ListAncestor** und **CommonAncestor** in den folgenden [!INCLUDE[tsql](../includes/tsql-md.md)] -Beispielen verwenden zu können, müssen Sie die DLL und die **HierarchyId_Operations** -Assembly in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erstellen, indem Sie Code ähnlich dem folgenden ausführen:  
  
```  
CREATE ASSEMBLY HierarchyId_Operations   
FROM '<path to DLL>\ListAncestors.dll'  
GO  
```  
  
  
###  <a name="ancestors"></a> Auflisten von Vorgängern  
 Die Erstellung einer Liste von Vorgängern, um beispielsweise die Position innerhalb einer Organisation anzuzeigen, ist ein häufig vorkommender Vorgang. Eine Möglichkeit dazu bietet die Verwendung einer Tabellenwertfunktion mithilfe der oben definierten **HierarchyId_Operations** -Klasse:  
  
 Verwenden von [!INCLUDE[tsql](../includes/tsql-md.md)]:  
  
```  
CREATE FUNCTION ListAncestors (@node hierarchyid)  
RETURNS TABLE (node hierarchyid)  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.ListAncestors  
GO  
```  
  
 Beispiel für die Verwendung:  
  
```  
DECLARE @h hierarchyid  
SELECT @h = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0' -- /1/1/5/2/  
  
SELECT LoginID, OrgNode.ToString() AS LogicalNode  
FROM HumanResources.EmployeeDemo AS ED  
JOIN ListAncestors(@h) AS A   
   ON ED.OrgNode = A.Node  
GO  
```  
  
  
###  <a name="lowestcommon"></a> Ermitteln des kleinsten gemeinsamen Vorgängers  
 Erstellen Sie mithilfe der oben definierten **HierarchyId_Operations** -Klasse die folgende [!INCLUDE[tsql](../includes/tsql-md.md)] -Funktion, die den kleinsten gemeinsamen Vorgänger zweier Knoten in einer Hierarchie ermittelt:  
  
```  
CREATE FUNCTION CommonAncestor (@node1 hierarchyid, @node2 hierarchyid)  
RETURNS hierarchyid  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.CommonAncestor  
GO  
```  
  
 Beispiel für die Verwendung:  
  
```  
DECLARE @h1 hierarchyid, @h2 hierarchyid  
  
SELECT @h1 = OrgNode   
FROM  HumanResources.EmployeeDemo   
WHERE LoginID = 'adventure-works\jossef0' -- Node is /1/1/3/  
  
SELECT @h2 = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0' -- Node is /1/1/5/2/  
  
SELECT OrgNode.ToString() AS LogicalNode, LoginID   
FROM HumanResources.EmployeeDemo    
WHERE OrgNode = dbo.CommonAncestor(@h1, @h2) ;  
```  
  
 Der resultierende Knoten ist /1/1/  
  
  
###  <a name="BKMK_MovingSubtrees"></a> Verschieben von Teilstrukturen  
 Ein anderer allgemeiner Vorgang ist das Verschieben von Teilstrukturen. Die Prozedur unten macht die Teilstruktur **@oldMgr** (einschließlich **@oldMgr**) zu einer Teilstruktur von **@newMgr**bedeutend schneller.  
  
```  
CREATE PROCEDURE MoveOrg(@oldMgr nvarchar(256), @newMgr nvarchar(256) )  
AS  
BEGIN  
DECLARE @nold hierarchyid, @nnew hierarchyid  
SELECT @nold = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @oldMgr ;  
  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION  
SELECT @nnew = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @newMgr ;  
  
SELECT @nnew = @nnew.GetDescendant(max(OrgNode), NULL)   
FROM HumanResources.EmployeeDemo WHERE OrgNode.GetAncestor(1)=@nnew ;  
  
UPDATE HumanResources.EmployeeDemo    
SET OrgNode = OrgNode.GetReparentedValue(@nold, @nnew)  
WHERE OrgNode.IsDescendantOf(@nold) = 1 ;  
  
COMMIT TRANSACTION  
END ;  
GO  
```  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)   
 [Tutorial: Using the hierarchyid Data Type](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)   
 [hierarchyid &#40;Transact-SQL&#41;](../t-sql/data-types/hierarchyid-data-type-method-reference.md)  
  
  
