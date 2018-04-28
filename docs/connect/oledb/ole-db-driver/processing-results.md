---
title: Verarbeiten von Ergebnissen | Microsoft Docs
description: Verarbeiten von Ergebnissen
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 706b47396ef0c9ff57f39f144a9545d7eec68da8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="processing-results"></a>Ergebnisverarbeitung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Wenn ein Rowsetobjekt durch die Ausführung eines Befehls oder vom Anbieter direkt erzeugt wird, muss der Consumer die Daten im Rowset abrufen und darauf zugreifen können.  
  
 Rowsets sind die zentralen Objekte, mit denen der OLE DB-Treiber für SQL Server, um Daten in tabellarischer Form verfügbar zu machen. Grundsätzlich ist ein Rowset ein Satz von Zeilen, in dem jede Zeile Spaltendaten aufweist. Ein Rowsetobjekt macht Schnittstellen verfügbar, z. B. **IRowset** (enthält Methoden zum sequenziellen Abrufen von Zeilen aus dem Rowset), **IAccessor** (ermöglicht die Definition einer Gruppe von spaltenbindungen, beschreibt die Möglichkeit, die Tabellendaten an Programmvariablen des Consumers gebunden ist), **IColumnsInfo** (bietet Informationen zu den Spalten im Rowset), und **IRowsetInfo** (bietet Informationen zu Schemarowsets).  
  
 Ein Consumer aufrufen kann die **IRowset:: GetData** Methode, um eine Zeile mit Daten in einen Puffer aus dem Rowset abrufen. Vor dem **GetData** wird aufgerufen, beschreibt der Consumer den Puffer mit einem Satz von DBBINDING-Strukturen. Jede Bindung beschreibt, wie eine Spalte des Rowsets in einem Puffer des Consumer gespeichert werden soll, und enthält folgende Angaben:  
  
-   Ordnungszahl der Spalte (oder des Parameters), auf den sich die Bindung bezieht  
  
-   Informationen darüber, was gebunden wird (z. B. Datenwert, Länge der Daten und Bindungsstatus)  
  
-   Informationen zur Größe des Offsets im Puffer zu jedem dieser Teile  
  
-   Länge und den Typ der Datenwerte, die im Puffer des Consumers vorhanden sind  
  
 Beim Abruf der Daten bestimmt der Anbieter anhand der Informationen in jeder Bindung, wo und wie die Daten aus dem Puffer des Consumers abzurufen sind. Beim Einfügen der Daten in den Puffer des Consumers bestimmt der Anbieter anhand der Informationen in jeder Bindung, wo und wie die Daten in diesen Puffer einzufügen sind.  
  
 Nachdem die DBBINDING-Strukturen angegeben sind, wird ein Accessor erstellt (**IAccessor:: CreateAccessor**). Ein Accessor ist eine Sammlung von Bindungen. Er dient zum Abrufen oder Einfügen von Daten in den Puffer des Consumers.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einen OLE DB-Treiber für SQL Server-Anwendung](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [OLE DB-Themen zur Vorgehensweise](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
