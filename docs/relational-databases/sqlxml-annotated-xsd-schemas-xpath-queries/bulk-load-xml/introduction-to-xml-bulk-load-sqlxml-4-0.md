---
title: "Einführung in XML-Massenladen (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 18950714bd976c224ef33627fb12528ad08b0584
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>Einführung in XML-Massenladen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XML-Massenladen ist ein eigenständiges COM-Objekt, das Ihnen ermöglicht, laden semistrukturierte XML-Daten in Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabellen.  
  
 Sie können XML-Daten in eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbank einfügen, indem Sie eine INSERT-Anweisung und die OPENXML-Funktion verwenden. Das Massenladen-Hilfsprogramm zeigt jedoch eine bessere Leistung beim Einfügen großer XML-Datenmengen.  
  
 Die Execute-Methode des XML-Massenladen-Objektmodells verwendet zwei Parameter:  
  
-   Eine XML-Schemadefinition (XSD) mit Anmerkungen oder ein XDR-Schema (XML-Data Reduced). Das XML-Massenladen-Hilfsprogramm interpretiert dieses Zuordnungsschema und die im Schema angegebenen Anmerkungen durch Identifizieren der SQL Server-Tabellen, in die die XML-Daten eingefügt werden sollen.  
  
-   Ein XML-Dokument oder Dokumentfragment (ein Dokumentfragment ist ein Dokument ohne Einzelelement auf der obersten Ebene). Sie können einen Dateinamen oder einen Datenstrom angeben, von dem XML-Massenladen lesen kann.  
  
 Das XML-Massenladen-Hilfsprogramm interpretiert das Zuordnungsschema und identifiziert die Tabelle(n), in die die XML-Daten eingefügt werden soll(en).  
  
 Es wird vorausgesetzt, dass Sie mit den folgenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Funktionen vertraut sind:  
  
-   XSD- und XDR-Schemas mit Anmerkungen Weitere Informationen über XSD-Schemas mit Anmerkungen finden Sie unter [Einführung in XSD-Schemas mit Anmerkungen &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Informationen über XDR-Schemas mit Anmerkungen finden Sie unter [XDR-Schemas mit Anmerkungen &#40; veraltet in SQLXML 4.0 &#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] BULK insert Mechanismen, z. B. die [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT-Anweisung und das Bcp-Hilfsprogramm. Weitere Informationen finden Sie unter [BULK INSERT &#40; Transact-SQL &#41; ](../../../t-sql/statements/bulk-insert-transact-sql.md) und [Bcp (Hilfsprogramm)](../../../tools/bcp-utility.md).  
  
## <a name="streaming-of-xml-data"></a>Streaming von XML-Daten  
 Da das XML-Quelldokument unter Umständen groß ist, wird das gesamte Dokument für die Massenladenverarbeitung nicht in den Speicher gelesen. Stattdessen interpretiert XML-Massenladen die XML-Daten als Datenstrom und liest diesen. Während das Hilfsprogramm die Daten liest, identifiziert es die Datenbanktabelle(n), generiert den entsprechenden Datensatz bzw. Datensätze aus der XML-Datenquelle und sendet den Datensatz bzw. die Datensätze zum Einfügen an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Beispielsweise besteht der folgende XML-Quelldokument  **\<Kunden >** Elemente und  **\<Reihenfolge >** Unterelemente:  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 Als XML-Massenladen liest die  **\<Kunden >** Element, generiert es einen Datensatz für die Customertable. Beim Lesen der  **\</Customer >** Endtag, XML-Massenladen fügt diesen in der Tabelle im Datensatz [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. In der gleichen Weise beim Lesen der  **\<Reihenfolge >** Element, XML-Massenladen einen Datensatz für die Ordertable generiert und fügt dann diesen Datensatz in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Tabelle beim Lesen der  **\< / Order >** Endtag.  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>Transaktive und nicht durchgeführte XML-Massenladevorgänge  
 XML-Massenladen kann entweder in einem transaktiven oder einem nicht durchgeführten Modus operieren. Leistung ist in der Regel optimal, wenn Sie Massenladen in einem nicht durchgeführten Modus sind: d. h. die Transaktionseigenschaft auf "false" festgelegt ist) und eine der folgenden Bedingungen zutrifft:  
  
-   Die Tabellen, in die die Daten massengeladen werden, sind leer und ohne Indizes.  
  
-   Die Tabellen weisen Daten und eindeutige Indizes auf.  
  
 Der nicht durchgeführte Ansatz garantiert keinen Rollback, wenn beim Massenladen ein Fehler auftritt (Teilrollbacks sind allerdings möglich). Das nicht durchgeführte Massenladen ist geeignet, wenn die Datenbank leer ist. Wenn ein Fehler auftritt, können Sie so die Datenbank bereinigen und das XML-Massenladen erneut starten.  
  
> [!NOTE]  
>  Im nicht durchgeführten Modus verwendet XML-Massenladen eine interne Standardtransaktion und führt einen Commit dafür aus. Wenn die Transaktionseigenschaft auf "true" festgelegt ist, ruft XML-Massenladen nicht Commit dieser Transaktion auf.  
  
 Wenn die Transaktionseigenschaft auf "true" festgelegt ist, erstellt XML-Massenladen temporäre Dateien, eine für jede Tabelle, die im Zuordnungsschema identifiziert wird. XML-Massenladen speichert zunächst die Datensätze aus dem XML-Quelldokument in diesen temporären Dateien. Anschließend ruft eine [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT-Anweisung diese Datensätze aus den Dateien ab und speichert sie in den entsprechenden Tabellen. Sie können den Speicherort für die temporären Dateien angeben, mit der TempFilePath-Eigenschaft. Das für XML-Massenladen verwendete [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konto muss auf diesen Pfad zugreifen können. Wenn die TempFilePath-Eigenschaft nicht angegeben ist, wird der Standardpfad für die Datei, der in der Umgebungsvariablen TEMP angegeben wird verwendet, zum Erstellen der temporären Dateien.  
  
 Wenn die Transaktionseigenschaft auf "false" (Standardeinstellung) festgelegt ist, verwendet das XML-Massenladen die OLE DB-Schnittstelle IRowsetFastLoad für das Massenladen der Daten.  
  
 Wenn die "ConnectionString"-Eigenschaft die Verbindungszeichenfolge festlegt und die Transaktionseigenschaft auf "true" festgelegt ist, arbeitet XML-Massenladen in einen eigenen Transaktionskontext. (Zum Beispiel startet XML-Massenladen eine eigene Transaktion und führt ggf. einen Commit oder Rollback aus.)  
  
 Wenn der "connectioncommand"-Eigenschaft legt fest, die Verbindung mit einem vorhandenen Verbindungsobjekt und die Transaktionseigenschaft auf "true" festgelegt ist, XML-Massenladevorgang gibt keine aus ein COMMIT oder ROLLBACK-Anweisung im Erfolgsfall oder ein Fehler auftritt, bzw. Tritt ein Fehler auf, gibt XML-Massenladen die entsprechende Fehlermeldung zurück. Die Entscheidung, ob eine COMMIT- oder ROLLBACK-Anweisung ausgegeben wird, obliegt dem Client, der das Massenladen gestartet hat. Das Verbindungsobjekt, das für XML-Massenladen verwendet wird soll vom Typ ICommand oder ein ADO-Befehlsobjekt sein.  
  
 In SQLXML 4.0 kann eine ConnectionObject den Transaktionssatz-Eigenschaft auf "false" verwendet werden. Der nicht durchgeführte Modus wird nicht mit einem ConnectionObject unterstützt, da es nicht möglich, mehr als eine IRowsetFastLoad-Schnittstelle für eine übergebene Sitzung geöffnet ist.  
  
  
