---
title: Mit der Verarbeitung mehrerer Resultsets IMultipleResults | Microsoft Docs
description: Verwenden von IMultipleResults mehrere Resultsets verarbeiten
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b8cf31c2bf7d434b85168adbd7826556892418a7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Verwenden von 'IMultipleResults' zur Verarbeitung mehrerer Resultsets
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Consumer verwenden die **IMultipleResults** Schnittstelle vom OLE DB-Treiber für SQL Server-befehlsausführung zurückgegebenen Ergebnisse zu verarbeiten. Wenn der OLE DB-Treiber für SQL Server einen Befehl zur Ausführung übermittelt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] führt die Anweisungen aus und gibt die Ergebnisse zurück.  
  
 Ein Client muss alle Ergebnisse der Befehlsausführung verarbeiten. Da der OLE DB-Treiber für SQL Server-befehlsausführung mehrere Rowsetobjekte als Ergebnis generieren kann, verwenden Sie die **IMultipleResults** Schnittstelle, um sicherzustellen, dass Abrufen der Anwendungsdaten der Client initiierten Roundtrip abgeschlossen wird.  
  
 Die folgenden [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Anweisung generiert mehrere Rowsets, von denen einige Zeilendaten aus der **OrderDetails** Tabelle und einige enthaltenden Ergebnisse der COMPUTE BY-Klausel:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Wenn ein Consumer einen Befehl ausführt, der diesen Text enthält, und ein Rowset als Schnittstelle für die zurückgegebenen Ergebnisse anfordert, wird nur der erste Satz Zeilen zurückgegeben. Der Consumer kann alle Zeilen im zurückgegebenen Rowset verarbeiten. Jedoch wenn DBPROP_MULTIPLECONNECTIONS-Datenquelleneigenschaft auf festgelegt ist VARIANT_FALSE und MARS nicht für die Verbindung aktiviert ist, können keine weiteren Befehle für das Sitzungsobjekt (OLE DB-Treiber für SQL Server erstellt eine andere Verbindung keine) ausgeführt werden, bis die -Befehl abgebrochen. Wenn MARS nicht für die Verbindung aktiviert ist, gibt der OLE DB-Treiber für SQL Server DB_E_OBJECTOPEN-Fehler zurück, wenn DBPROP_MULTIPLECONNECTIONS VARIANT_FALSE lautet, und E_FAIL zurück, wenn eine aktive Transaktion vorhanden ist.  
  
 Der OLE DB-Treiber für SQL Server wird auch zurückgegeben, DB_E_OBJECTOPEN Verwendung gestreamt Output-Parameter und die Anwendung wurde nicht verarbeitet alle zurückgegebenen Ausgabeparameterwerte vor dem Aufruf **IMultipleResults:: GetResults** an Rufen Sie das nächste Resultset. Wenn MARS nicht aktiviert ist und die Verbindung ausgelastet ist, einem Befehl ausgeführt wird, ist kein Rowset produziert, oder, erzeugt ein Rowset, das einen Servercursor ist, und wenn die DBPROP_MULTIPLECONNECTIONS Eigenschaft Datenquelle auf VARIANT_TRUE fest, der OLE DB-Treiber für SQL Server festgelegt ist erstellt zusätzliche Verbindungen um gleichzeitige Befehlsobjekte zu unterstützen, wenn eine Transaktion aktiv ist, in diesem Fall gibt einen Fehler fest. Transaktionen und Sperren werden von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf Verbindungsbasis verwaltet. Wenn eine zweite Verbindung hergestellt wird, nutzt der Befehl auf den anderen Verbindungen Sperren nicht gemeinsam. Es muss darauf geachtet werden, dass ein Befehl einen anderen nicht blockiert, indem er Zeilen gesperrt hält, die von einem anderen Befehl angefordert werden. Wenn MARS aktiviert ist, können mehrere Befehle für die Verbindungen aktiv sein, und bei der Verwendung expliziter Transaktionen nutzen die Befehle alle eine gemeinsame Transaktion.  
  
 Der Consumer kann den Befehl entweder mit Abbrechen [issabort:: Abort](../../oledb/ole-db-interfaces/issabort-abort-ole-db.md) oder alle Verweise auf das Befehlsobjekt und das abgeleitete Rowset freigibt.  
  
 Mit **IMultipleResults** in allen Instanzen ermöglicht es, alle Rowsets durch befehlsausführung zu erhalten, und ermöglicht es Consumern zu ermitteln, wann die befehlsausführung abgebrochen und ein Sitzungsobjekt für die Verwendung durch andere Befehle.  
  
> [!NOTE]  
>  Wenn Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Cursor verwenden, erstellt die Befehlsausführung den Cursor. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gibt den Erfolg oder Fehler der Cursorerstellung zurück. Der Roundtrip zur Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ist damit nach der Rückkehr der Befehlsausführung abgeschlossen. Jede **GetNextRows** -Aufruf wird dann zum Roundtrip ausgeführt. Auf diese Weise können mehrere Befehlsobjekte vorhanden sein, und jedes verarbeitet ein Rowset, das das Ergebnis eines Abrufs vom Servercursor ist. Weitere Informationen finden Sie unter [Rowsets und SQL Server-Cursor](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Befehle](../../oledb/ole-db-commands/commands.md)  
  
  
