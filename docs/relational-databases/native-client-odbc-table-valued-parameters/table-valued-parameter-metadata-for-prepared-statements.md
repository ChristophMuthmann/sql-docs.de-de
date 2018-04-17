---
title: Tabellenwertparameter-Metadaten für vorbereitete Anweisungen | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 55d92acb57fe98486b9cc3f75dc80c2fbd81eb9f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>Tabellenwertparameter-Metadaten für vorbereitete Anweisungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Eine Anwendung kann Metadaten für einen vorbereiteten Prozeduraufruf mit SQLNumParams und SQLDescribeParam abrufen. Für Tabellenwertparameter *DataTypePtr* auf SQL_SS_TABLE festgelegt ist. Zusätzliche Metadaten sind über SQLGetDescField für SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME und SQL_CA_SS_SCHEMA_NAME verfügbar.  
  
 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME und SQL_CA_SS_SCHEMA_NAME können mit SQLColumns verwendet werden, um Spaltenmetadaten für Tabellentypen mit Tabellenwertparametern erhalten. In diesem Fall muss SQL_SOPT_SS_NAME_SCOPE auf SQL_SS_NAME_SCOPE_TABLE_TYPE festgelegt werden, bevor SQLColumns aufgerufen wird. SQL_SOPT_SS_NAME_SCOPE sollte wieder auf den Standardwert SQL_SS_NAME_SCOPE_TABLE gesetzt werden, wenn die Anwendung alle Tabellenwertparameter-Spaltenmetadaten abgerufen hat.  
  
 SQL_CA_SS_TYPE_NAME , SQL_CA_SS_CATALOG_NAME und SQL_CA_SS_SCHEMA_NAME können auch mit CLR-benutzerdefinierten Typparametern verwendet werden.  
  
 Sie können keine Tabellenwertparameter-Metadaten für vorbereitete Anweisungen abrufen, bei denen es sich nicht um gespeicherte Prozeduraufrufe handelt. Wenn Sie dies dennoch versuchen, gibt die Anwendung den Fehler SQL_ERROR mit SQLSTATE 42000 sowie die Meldung "Syntaxfehler oder Zugriffsverletzung" zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenwertparameter &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
