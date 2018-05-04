---
title: Mit der Verarbeitung mehrerer Resultsets IMultipleResults | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
ms.assetid: 754d3f30-7d94-4b67-8dac-baf2699ce9c6
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f3ab7376bcbb6b8237aa2600ac19fb5a13b6304f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Verwenden von 'IMultipleResults' zur Verarbeitung mehrerer Resultsets
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Consumer verwenden die **IMultipleResults** Schnittstelle zum Verarbeiten von zurückgegebenen Ergebnisse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befehlsausführung für Native Client OLE DB-Anbieter. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter sendet einen Befehl zur Ausführung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] führt die Anweisungen aus und gibt die Ergebnisse zurück.  
  
 Ein Client muss alle Ergebnisse der Befehlsausführung verarbeiten. Da die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befehlsausführung für Native Client OLE DB-Anbieters mehrere Rowsetobjekte als Ergebnis generieren können, verwenden Sie die **IMultipleResults** Schnittstelle, um sicherzustellen, dass Datenabruf für die Anwendung beendet wird, die Client initiierten Roundtrip.  
  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung generiert mehrere Rowsets, von denen einige Zeilendaten aus der **OrderDetails** Tabelle und einige enthaltenden Ergebnisse der COMPUTE BY-Klausel:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Wenn ein Consumer einen Befehl ausführt, der diesen Text enthält, und ein Rowset als Schnittstelle für die zurückgegebenen Ergebnisse anfordert, wird nur der erste Satz Zeilen zurückgegeben. Der Consumer kann alle Zeilen im zurückgegebenen Rowset verarbeiten. Jedoch wenn DBPROP_MULTIPLECONNECTIONS-Datenquelleneigenschaft auf festgelegt ist VARIANT_FALSE und MARS nicht für die Verbindung aktiviert ist, können keine weiteren Befehle für das Sitzungsobjekt ausgeführt werden (die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter erstellt keine anderen Verbindung), bis der Befehl abgebrochen wird. Wenn MARS nicht für die Verbindung aktiviert ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter gibt DB_E_OBJECTOPEN-Fehler zurück, wenn DBPROP_MULTIPLECONNECTIONS VARIANT_FALSE lautet, und E_FAIL zurück, wenn eine aktive Transaktion vorhanden ist.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter wird auch zurückgegeben, DB_E_OBJECTOPEN Verwendung gestreamt Output-Parameter und die Anwendung sind nicht alle zurückgegebenen Ausgabeparameterwerte vor dem Aufruf verbraucht **IMultipleResults:: GetResults**  auf das nächste Resultset abzurufen. Wenn MARS nicht aktiviert ist und die Verbindung ist ausgelastet Ausführen eines Befehls, der kein Rowset produziert wird, oder, erzeugt ein Rowset, das kein Servercursor ist, und die DBPROP_MULTIPLECONNECTIONS-Datenquelleneigenschaft auf VARIANT_TRUE festgelegt ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter erstellt zusätzliche Verbindungen um gleichzeitige Befehlsobjekte zu unterstützen, wenn eine Transaktion aktiv ist, in diesem Fall gibt einen Fehler. Transaktionen und Sperren werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf Verbindungsbasis verwaltet. Wenn eine zweite Verbindung hergestellt wird, nutzt der Befehl auf den anderen Verbindungen Sperren nicht gemeinsam. Es muss darauf geachtet werden, dass ein Befehl einen anderen nicht blockiert, indem er Zeilen gesperrt hält, die von einem anderen Befehl angefordert werden. Wenn MARS aktiviert ist, können mehrere Befehle für die Verbindungen aktiv sein, und bei der Verwendung expliziter Transaktionen nutzen die Befehle alle eine gemeinsame Transaktion.  
  
 Der Consumer kann den Befehl entweder mit Abbrechen [issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) oder alle Verweise auf das Befehlsobjekt und das abgeleitete Rowset freigibt.  
  
 Mit **IMultipleResults** in allen Instanzen ermöglicht es, alle Rowsets durch befehlsausführung zu erhalten, und ermöglicht es Consumern zu ermitteln, wann die befehlsausführung abgebrochen und ein Sitzungsobjekt für die Verwendung durch andere Befehle.  
  
> [!NOTE]  
>  Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Cursor verwenden, erstellt die Befehlsausführung den Cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt den Erfolg oder Fehler der Cursorerstellung zurück. Der Roundtrip zur Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist damit nach der Rückkehr der Befehlsausführung abgeschlossen. Jede **GetNextRows** -Aufruf wird dann zum Roundtrip ausgeführt. Auf diese Weise können mehrere Befehlsobjekte vorhanden sein, und jedes verarbeitet ein Rowset, das das Ergebnis eines Abrufs vom Servercursor ist. Weitere Informationen finden Sie unter [Rowsets und SQL Server-Cursor](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Befehle](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
