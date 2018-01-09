---
title: Tabellenwertparameter (ODBC) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC)
- ODBC, table-valued parameters
ms.assetid: ef06cd13-18e2-4c65-8ede-c3955d820e54
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34668c513774bcde42346f3a2837fa9559c97ec5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="table-valued-parameters-odbc"></a>Tabellenwertparameter (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die ODBC-Unterstützung für Tabellenwertparameter ermöglicht einer Clientanwendung die effizientere Versendung von parametrisierten Daten an einen Server, indem mehrere Zeilen über einen Aufruf an den Server gesendet werden.  
  
 Informationen zu Tabellenwertparametern auf dem Server finden Sie unter [Tabellenwertparametern &#40; Datenbankmodul &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
 In ODBC gibt es zwei Methoden zum Versenden von Tabellenwertparametern an den Server:  
  
-   Alle Tabellenwertparameter-Daten kann im Speicher zum Zeitpunkt SQLExecDirect oder SQLExecute aufgerufen wird. Wenn es mehrere Zeilen im Tabellenwert gibt, werden diese Daten in Arrays gespeichert.  
  
-   Eine Anwendung kann Data-at-Execution für einen Tabellenwertparameter angeben, wenn SQLExecDirect oder SQLExecute aufgerufen wird. In diesem Fall können Datenzeilen für den Tabellenwertparameter in Batches oder einzeln bereitgestellt werden, um die Speicheranforderungen zu reduzieren.  
  
 Die erste Option aktiviert gespeicherte Prozeduren, um mehr Geschäftslogik zu kapseln. Beispielsweise könnte eine einzeln gespeicherte Prozedur eine gesamte Bestellungseingabetransaktion kapseln, wenn die Bestellartikel als Tabellenwertparameter übergeben werden. Diese Option ist sehr effizient, da nur ein einzelner Roundtrip zum Server erforderlich ist. Alternativ könnten Sie verschiedene Prozeduren verwenden, um die Bestellungskopfzeile und die Bestellartikel separat zu behandeln. In diesem Fall wäre jedoch weiterer Code und ein komplexerer Vertrag zwischen Client und Server erforderlich.  
  
 Die zweite Methode stellt einen effizienten Mechanismus für Massenvorgänge mit sehr großen Datenmengen bereit. Dies ermöglicht es einer Anwendung, Datenzeilen zum Server zu streamen, ohne sie zuvor alle im Arbeitsspeicher puffern zu müssen.  
  
 Beim Erstellen der Tabellenvariablen können Sie Einschränkungen und Primärschlüssel erstellen. Einschränkungen sind eine gute Möglichkeit, um sicherzustellen, dass die Daten in einer Tabelle bestimmte Anforderungen erfüllen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Verwendungen von ODBC-Tabellenwertparametern](../../relational-databases/native-client-odbc-table-valued-parameters/uses-of-odbc-table-valued-parameters.md)  
 Beschreibt die wichtigsten Benutzerszenarien für Tabellenwertparameter und ODBC.  
  
 [ODBC-SQL-Typ für Tabellenwertparameter](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-sql-type-for-table-valued-parameters.md)  
 Beschreibt den SQL_SS_TABLE-Typ. Dies ist ein neuer ODBC SQL-Typ, der Tabellenwertparameter unterstützt.  
  
 [Deskriptorfelder für Tabellenwertparameter](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)  
 Beschreibt Deskriptorfelder, die Tabellenwertparameter unterstützen.  
  
 [Deskriptorfelder für aus Tabellenwertparameter bestehenden Spalten](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)  
 Beschreibt Deskriptorfelder, die eine Bedeutung für Tabellenwertparameter haben.  
  
 [Diagnosedatensatz-Felder für Tabellenwertparameter](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-diagnostic-record-fields.md)  
 Beschreibt zwei Diagnosefelder, die Diagnosedatensätzen hinzugefügt wurden, um Tabellenwertparameter zu unterstützen.  
  
 [Anweisungsattribute, die sich auf Tabellenwertparameter auswirken](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)  
 Beschreibt ein neues Deskriptorheaderfeld, das die Adressierung von Tabellenwertparameter-Spalten ermöglicht.  
  
 [Bindung und Datenübertragung von Tabellenwertparametern und Spaltenwerten](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)  
 Beschreibt die Parameterbindung und die Übergabe eines Tabellenwertparameters an den Server.  
  
 [Tabellenwertparameter-Metadaten für vorbereitete Anweisungen](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)  
 Beschreibt, wie eine Anwendung Metadaten für einen vorbereiteten Prozeduraufruf abrufen kann.  
  
 [Zusätzliche Tabellenwertparameter-Metadaten](../../relational-databases/native-client-odbc-table-valued-parameters/additional-table-valued-parameter-metadata.md)  
 Beschreibt, wie SQLProcedureColumns SQLTables und SQLColumns verwenden, um Metadaten für einen Tabellenwertparameter abzurufen.  
  
 [Tabellenwertparameter-Datenkonvertierung und andere Fehler und Warnungen](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-data-conversion-and-other-errors-and-warnings.md)  
 Beschreibt, wie Fehler in Tabellenwertparameter-Spaltenwerten verarbeitet werden.  
  
 [Versionsübergreifende Kompatibilität](../../relational-databases/native-client-odbc-table-valued-parameters/cross-version-compatibility.md)  
 Beschreibt Konflikte, die auftreten können, wenn Tabellenwertparameter von einem Client oder Server mit einer niedrigeren Version als [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] verwendet werden.  
  
 [Zusammenfassung der ODBC-Tabellenwertparameter-API](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-table-valued-parameter-api-summary.md)  
 Listet die ODBC-Funktionen auf, die Tabellenwertparameter unterstützen.  
  
 [Programmierbeispiele für ODBC-Tabellenwertparameter](http://msdn.microsoft.com/library/3f52b7a7-f2bd-4455-b79e-d015fb397726)  
 Beschreibt die Durchführung der häufigsten Aufgaben.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Table-Valued Parameters &#40; SQL Server Native Client &#41;](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
  
  
