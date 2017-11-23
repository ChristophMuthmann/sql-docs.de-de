---
title: Abrufen von Zeilen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 5e6dbe36-b682-464d-adfa-8e886f9bd452
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2e3cb9f50806d4796d9f65b05c269f610bd33933
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="fetching-rows"></a>Abrufen von Zeilen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die **IRowset** Schnittstelle ist die grundlegende Rowset-Schnittstelle. Die **IRowset** Schnittstelle bietet Methoden zum sequenziellen Abrufen von Zeilen, die Daten aus diesen Zeilen abgerufen, und Verwalten von Zeilen. Consumer verwenden die Methoden in **IRowset** für alle grundlegenden rowsetvorgänge. Dazu gehört das Abrufen und erneute Freigeben von Zeilen und das Einlesen von Spaltenwerten.  
  
 Wenn ein Consumer einen Schnittstellenzeiger für ein Rowset erhält, ist der erste Schritt in der Regel um zu bestimmen, das die Funktionen des Rowsets mithilfe der **IRowsetInfo:: GetProperties** Methode. Auf diese Weise werden Informationen über die durch das Rowset verfügbar gemachten Schnittstellen zurückgegeben sowie über andere Möglichkeiten des Rowsets, die nicht als eigentliche Schnittstellen zu betrachten sind, wie beispielsweise die maximale Anzahl aktiver Zeilen und die Anzahl der Zeilen, die gleichzeitig ausstehende Updates aufweisen können.  
  
 Der nächste, vom Consumer auszuführende Schritt besteht darin, die Charakteristika – oder Metadaten – der Spalten im Rowset zu ermitteln. Dafür verwenden sie die **IColumnsInfo** Methode für die einfache Spalteninformationen oder **IColumnsRowset** Methode für erweiterte Spalteninformationen. Die **GetColumnInfo** Methodenrückgabe die folgende Informationen:  
  
-   Die Anzahl der Spalten im Resultset.  
  
-   Ein Array von DBCOLUMNINFO-Strukturen; eines pro Spalte.  
  
     Die Reihenfolge der Strukturen entspricht der Reihenfolge, in der die Spalten im Rowset erscheinen. Jede DBCOLUMNINFO-Struktur enthält Spaltenmetadaten wie den Spaltennamen, die Ordnungszahl der Spalte, maximal mögliche Länge eines Werts in der Spalte, Datentyp, Genauigkeit und Länge der Spalte.  
  
-   Den Zeiger auf einen Speicher für alle Zeichenfolgenwerte innerhalb eines einzelnen Zuordnungsblocks.  
  
 Der Consumer bestimmt, welche Spalten erforderlich sind, entweder auf der Grundlage der Metadaten oder basierend auf den Textbefehl, mit dem das Rowset generiert wurde. Die Ordnungszahlen der benötigten Spalten über die Reihenfolge der zurückgegebenen Spalteninformationen **IColumnsInfo** oder ausgehend von den Ordnungszahlen in dem vom zurückgegebenen spaltenmetadatenrowset **IColumnsRowset**.  
  
 Die **IColumnsInfo** und **IColumnsRowset** Schnittstellen werden verwendet, um Informationen zu den Spalten im Rowset zu extrahieren. Die **IColumnsInfo** Schnittstelle gibt eine begrenzte Anzahl von Informationen zurück, wohingegen **IColumnsRowset** alle Metadaten bereitstellt.  
  
> [!NOTE]  
>  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0 und früher, die optionale Metadatenspalte DBCOLUMN_COMPUTEMODE zurückgegebenes **IColumnsInfo:: GetColumnsInfo** zurückgegeben wird, DBSTATUS_S_ISNULL (anstelle der Werte, die beschreibt, ob die Spalte berechnet), da nicht ermittelt werden kann, ob die zugrunde liegende Spalte berechnet ist.  
  
 Die Ordnungszahlen werden verwendet, um eine Bindung an eine Spalte anzugeben. Eine Bindung ist eine Struktur, die einer Spalte ein Element der Struktur des Consumers zuordnet. Die Bindung kann den Datenwert, die Länge und den Statuswert der Spalte binden.  
  
 Ein Satz von Bindungen wird zusammen in einem Accessor erfasst. Dies wird erstellt, indem Sie mit der **IAccessor:: CreateAccessor** Methode. Ein Accessor kann mehrere Bindungen enthalten, sodass die Daten für mehrere Spalten durch einen einzigen Aufruf abgerufen oder festgelegt werden können. Der Consumer kann mehrere Accessoren erstellen, um in verschiedenen Teilen der Anwendung auf verschiedene Verwendungsmuster zu antworten. Er kann Accessoren erstellen und freigeben, solange das Rowset besteht.  
  
 Um Zeilen aus der Datenbank abzurufen, ruft der Consumer eine Methode, z. B. **IRowset:: GetNextRows** oder **IRowsetLocate:: GetRowsAt**. Diese Abrufvorgänge platzieren Zeilendaten vom Server in den Zeilenpuffer des Anbieters. Der Consumer hat keinen Direktzugriff auf den Zeilenpuffer des Anbieters. Der Consumer verwendet **IRowset:: GetData** Daten aus dem Puffer des Anbieters in den Consumerpuffer zu kopieren und **IRowsetChange:: SetData** datenänderungen vom Consumerpuffer in den Anbieterpuffer zu kopieren.  
  
 Der Consumer Ruft die **GetData** Methode und übergibt das Handle für eine Zeile, die das Handle für einen Accessor und einen Zeiger auf einen vom Consumer zugeordneten Puffer. **GetData** konvertiert die Daten und gibt die Spalten in der zum Erstellen des Accessors verwendeten Bindungen angegeben. Der Consumer kann Aufrufen **GetData** mehr als ein Mal für eine Zeile mit verschiedene Accessoren und Puffer und daher der Consumer mehrere Kopien derselben Daten abrufen kann.  
  
 Daten aus Spalten variabler Länge können auf mehrere Arten behandelt werden. Zunächst können solche Spalten an einen endlichen Abschnitt der Struktur des Consumers gebunden werden. Dies verursacht das Abschneiden von Daten, wenn die Länge der Daten die Länge des Puffers überschreitet. Der Consumer kann ermitteln, dass Daten abgeschnitten wurden, indem er den Status DBSTATUS_S_TRUNCATED überprüft. Die zurückgegebene Länge ist immer die wirkliche Länge in Byte, sodass der Consumer auch bestimmen kann, wie viele Daten abgeschnitten wurden.  
  
 Wenn der Consumer das Abrufen oder Aktualisieren von Zeilen beendet hat, diesen freigibt sie mit der **ReleaseRows** Methode. Auf diese Weise werden Ressourcen von der Kopie der Zeilen im Rowset frei, und es wird Platz für neue Zeilen geschaffen. Der Consumer kann den Zyklus des Abrufens oder Erstellens von Zeilen sowie des Zugreifens auf Daten in den Zeilen beliebig wiederholen.  
  
 Wenn der Consumer mit dem Rowset fertig ist, ruft er die **ReleaseAccessor** Methode, um Sie freizugeben. Ruft die **IUnknown:: Release** -Methode für alle Schnittstellen, die vom Rowset zum Freigeben des Rowsets verfügbar gemacht. Sobald das Rowset freigegeben ist, wird die Freigabe aller verbleibender Zeilen oder vom Consumer verwendeten Accessoren erzwungen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Nächste Abrufposition](../../relational-databases/native-client-ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Rowsets](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
