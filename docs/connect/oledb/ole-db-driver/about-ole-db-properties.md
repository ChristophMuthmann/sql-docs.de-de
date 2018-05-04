---
title: Informationen zu OLE DB-Eigenschaften | Microsoft Docs
description: Informationen zu OLE DB-Eigenschaften
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
- OLE DB, properties
- OLE DB Driver for SQL Server, properties
- properties [OLE DB]
- property values [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: a5c6eadef1db6e37512818ae8bace603f3fb816c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="about-ole-db-properties"></a>Informationen zu OLE DB-Eigenschaften
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Consumer legen Eigenschaftswerte fest, um ein bestimmtes Objektverhalten anzufordern. Zum Beispiel verwenden Consumer Eigenschaften, um die Schnittstellen anzugeben, die von einem Rowset verfügbar gemacht werden sollen. Consumer rufen die Eigenschaftswerte ab, um die Fähigkeiten eines Objekts zu ermitteln, beispielsweise eines Rowsets, einer Sitzung oder eines Datenquellenobjekts.  
  
 Jede Eigenschaft verfügt über einen Wert, einen Typ, eine Beschreibung, ein Lese-/Schreibattribut. Rowset-Eigenschaften besitzen überdies einen Indikator, der angibt, ob die Eigenschaft auf einzelne Spalten des Rowsets angewendet werden kann.  
  
 Eine Eigenschaft wird durch eine GUID und eine ganze Zahl, welche die Eigenschaften-ID darstellt, identifiziert. Ein Eigenschaftensatz ist ein Satz aller Eigenschaften, die über die gleiche GUID verfügen. Zusätzlich zu den vordefinierten OLE DB-Eigenschaftensätzen implementiert der OLE DB-Treiber für SQL Server-anbieterspezifische Eigenschaftensätze und Eigenschaften in diesen an. Jede Eigenschaft gehört zu einer oder mehreren Eigenschaftengruppen. Eine Eigenschaftengruppe ist die Gruppe aller Eigenschaften, die für ein bestimmtes Objekt gelten. Beispiele für Eigenschaftengruppen sind die Initialisierungseigenschaftengruppe, die Datenquellen-Eigenschaftengruppe, die Sitzungseigenschaftengruppe, die Rowseteigenschaftengruppe, die Tabelleneigenschaftengruppe und die Spalteneigenschaftengruppe. Jede dieser Eigenschaftengruppen enthält Eigenschaften.  
  
 Das Festlegen von Eigenschaftswerten beinhaltet Folgendes:  
  
1.  Bestimmen der Eigenschaften, deren Werte festgelegt werden sollen  
  
2.  Bestimmen der Eigenschaftensätze, die die identifizierten Eigenschaften enthalten  
  
3.  Zuordnen eines Arrays von DBPROPSET-Strukturen, wobei für jeden identifizierten Eigenschaftensatz eine Struktur angegeben werden muss  
  
4.  Zuordnen eines Arrays von DBPROP-Strukturen, wobei für jeden Eigenschaftensatz eine Struktur angegeben werden muss. Die Anzahl der Elemente in jedem Array entspricht der Anzahl der Eigenschaften (die in Schritt 1 identifiziert wurden), die zu diesem Eigenschaftensatz gehören.  
  
5.  Füllen der DBPROP-Struktur für jede Eigenschaft  
  
6.  Eintragen der Daten (Eigenschaftensatz-GUID, Zähler für die Anzahl der Elemente und ein Zeiger auf das zugehörige DBPROP-Array) in die DBPROPSET-Struktur für jeden Eigenschaftensatz  
  
7.  Aufrufen einer Methode, um Eigenschaften festzulegen und die Anzahl und das Array von DBPROPSET-Strukturen zu übergeben  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einen OLE DB-Treiber für SQL Server-Anwendung](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [Eigenschaften (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=112207)  
  
  
