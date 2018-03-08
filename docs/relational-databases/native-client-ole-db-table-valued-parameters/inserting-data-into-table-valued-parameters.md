---
title: "Einfügen von Daten in Tabellenwertparameter | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters, inserting data into
ms.assetid: 9c1a3234-4675-40d3-b473-8df06208f880
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f40d26c1e3d44e90375907845ea5ee60ef414fb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="inserting-data-into-table-valued-parameters"></a>Einfügen von Daten in Tabellenwertparameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt zwei Modelle für den Consumer Daten für Tabellenwertparameter-Zeilen angeben: ein Push- und Pull-Modell. Ein Beispiel für die das Pullmodell ist verfügbar. finden Sie unter [Programmierbeispiele für SQL Server Data](http://msftdpprodsamples.codeplex.com/).  
  
> [!NOTE]  
>  Eine Tabellenwertparameter-Spalte muss entweder nicht standardmäßige oder standardmäßige Werte in allen Zeilen aufweisen. Es ist nicht möglich, dass Standardwerte nur in einigen Zeilen vorhanden sind. Daher sind in Tabellenwertparameter-Bindungen die einzigen für Tabellenwertparameter-Rowsetspaltendaten zugelassenen Statuswerte DBSTATUS_S_ISNULL und DBSTATUS_S_OK. DBSTATUS_S_DEFAULT führt zu einem Fehler, und der gebundene Statuswert wird auf DBSTATUS_E_BADSTATUS festgelegt.  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>Pushmodell (lädt alle Tabellenwertparameter-Daten im Arbeitsspeicher)  
 Das Pushmodell ähnelt der Verwendung von Parametersätzen (d. h. die DBPARAMS-Parameter in ICommand:: Execute). Das Pushmodell wird nur verwendet, wenn Tabellenwertparameter-Rowsetobjekte ohne benutzerdefinierte Implementierung von IRowset Schnittstellen verwendet werden. Die Verwendung des Pushmodells ist empfehlenswert, wenn die Anzahl der Zeilen im Tabellenwertparameter-Rowset gering ist und die Arbeitsspeicherauslastung für die Anwendung daher nicht allzu hoch ist. Diese Vorgehensweise ist einfacher als die des Pullmodells, da neben den aktuellen gängigen Funktionen in typischen OLE DC-Anwendungen keine zusätzlichen Funktionen der Consumeranwendung erforderlich sind.  
  
 Es wird vorausgesetzt, dass der Consumer vor der Ausführung eines Befehls alle Tabellenwertparameter-Daten für den Anbieter bereitstellt. Zum Bereitstellen der Daten füllt der Consumer ein Tabellenwertparameter-Rowsetobjekt für den Tabellenwertparameter auf. Das Tabellenwertparameter-Rowsetobjekt macht Vorgänge zum Einfügen, Festlegen und Löschen verfügbar, mit denen der Consumer die Tabellenwertparameter-Daten bearbeiten kann. Der Anbieter ruft die Daten zum Zeitpunkt der Ausführung von diesem Tabellenwertparameter-Rowsetobjekt ab.  
  
 Wenn ein Tabellenwertparameter-Rowsetobjekt für den Consumer bereitgestellt wird, kann dieser es als Rowsetobjekt verarbeiten. Der Consumer kann die Typinformationen der einzelnen Spalten (Typ, maximale Länge, Genauigkeit und Dezimalstellen) mithilfe der Schnittstellenmethode IColumnsInfo:: GetColumnInfo oder IColumnsRowset:: GetColumnsRowset abrufen. Der Consumer erstellt anschließend einen Accessor, um die Bindungen für die Daten anzugeben. Der nächste Schritt besteht darin, Zeilen mit Daten in das Tabellenwertparameter-Rowset einzufügen. Dies kann mithilfe von IRowsetChange:: InsertRow erfolgen. IRowsetChange:: SetData oder IRowsetChange:: DeleteRows kann auch für das Tabellenwertparameter-Rowsetobjekt verwendet werden, wenn Sie die Daten bearbeiten müssen. Tabellenwertparameter-Rowsetobjekte weisen einen Verweiszähler auf, ähnlich wie Datenstromobjekte.  
  
 Wenn IColumnsRowset:: GetColumnsRowset verwendet wird, werden nachfolgende Aufrufe der Methoden IRowset:: GetNextRows, IRowset:: GetData und IRowset:: ReleaseRows für Rowsetobjekte der Ergebnisspalte.  
  
 Nach der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter mit der befehlsausführung begonnen, die Tabellenwertparameter-Werte werden von diesem Tabellenwertparameter-Rowsetobjekt abgerufen und an den Server gesendet werden.  
  
 Das Pushmodell erfordert nur minimale Arbeitsschritte seitens des Consumers, es benötigt jedoch mehr Arbeitsspeicher als das Pullmodell, da sich alle Tabellenwertparameter-Daten zum Zeitpunkt der Ausführung im Arbeitsspeicher befinden müssen.  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>Pullmodell (Abrufen von Tabellenwertparameter-Daten bei Bedarf vom Consumer)  
 Das Pullmodell ist für zwei Szenarien nützlich:  
  
-   Zum Streamen von Zeilen.  
  
-   Wenn ein Rowset von einem anderen Anbieter als Tabellenwertparameter-Wert verwendet wird.  
  
 Im Pullmodell stellt der Consumer nach Bedarf Daten für den Anbieter bereit. Verwenden Sie diesen Ansatz, wenn Ihre Anwendung zahlreiche Dateneinfügungen aufweist und die Tabellenwertparameter-Rowsetdaten zu einer hohen Speicherauslastung führen würden. Wenn mehrere OLE DB-Anbieter verwendet werden, ermöglicht das Consumer-Pullmodell dem Consumer, ein beliebiges Rowsetobjekt als Tabellenwertparameter-Wert bereitzustellen.  
  
 Um das Pullmodell verwenden zu können, müssen Consumer ihre eigene Implementierung eines Rowsetobjekts bereitstellen. Bei Verwendung des Pullmodells mit Tabellenwertparameter-Rowsets (CLSID_ROWSET_TVP) muss der Consumer das Tabellenwertparameter-Rowsetobjekt aggregieren, die der Anbieter über das ITableDefinitionWithConstraints verfügbar macht:: CreateTableWithConstraints-Methode oder der IOpenRowset:: OpenRowset-Methode. Das Consumerobjekt soll nur die IRowset-Schnittstellenimplementierung überschreiben. Sie müssen die folgenden Funktionen überschreiben:  
  
-   IRowset::GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset::GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset::RestartPosition  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter liest jeweils eine oder mehrere Zeilen vom Rowsetobjekt des Consumers gleichzeitig, um das Streamingverhalten für Tabellenwertparameter zu unterstützen. Ein Beispiel: Dem Benutzer liegen die Tabellenwertparameter-Rowsetdaten auf einem Datenträger (nicht im Speicher) vor, und er implementiert die Funktion zum Lesen von Daten vom Datenträger, wenn dies für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter erforderlich ist.  
  
 Der Consumer teilt das Datenformat zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter IAccessor:: CreateAccessor für das Tabellenwertparameter-Rowsetobjekt mit. Beim Lesen der Daten vom Consumerpuffer überprüft der Anbieter, ob alle schreibbaren, nicht standardmäßigen Spalten über mindestens ein Accessorhandle verfügbar sind, und verwendet die entsprechenden Handles zum Lesen der Spaltendaten. Um Mehrdeutigkeiten zu vermeiden, sollte eine 1: 1-Entsprechung zwischen einer Tabellenwertparameter-Rowsetspalte und einer Bindung. Doppelte Bindungen zur gleichen Spalte führen zu einem Fehler. Darüber hinaus muss jeder Accessor haben die *iOrdinal* Mitglied DBBINDING nacheinander. Es werden so viele Aufrufe IRowset:: GetData als die Anzahl der Accessoren pro Zeile, und die Reihenfolge der Aufrufe basiert auf der Reihenfolge des *iOrdinal* Wert aus niedrigeren zu den höheren Werten.  
  
 Es wird davon ausgegangen, dass der Anbieter die meisten der Schnittstellen implementiert, die vom Tabellenwertparameter-Rowsetobjekt verfügbar gemacht werden. Der Consumer implementiert ein Rowsetobjekt mit minimalen Schnittstellen (IRowset). Aufgrund von "blinder" Aggregation werden die verbleibenden obligatorischen Rowsetobjektschnittstellen von Tabellenwertparameter-Rowsetobjekten implementiert.  
  
 Für jedes beliebige Rowsetobjekt, wie Rowsetobjekte, die für einen beliebigen OLE DB-Anbieter abgerufen werden, muss das vom Consumer bereitgestellt Rowset alle erforderlichen Rowsetobjektschnittstellen wie in der OLE DB-Spezifikation angegeben implementieren.  
  
 Zum Zeitpunkt der Ausführung erfolgt ein Rückruf des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieters an das Rowsetobjekt, um Zeilen abzurufen und Spaltendaten zu lesen  
  
## <a name="see-also"></a>Siehe auch  
 [Table-Valued Parameters &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Verwenden des Table-Valued Parameters &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
