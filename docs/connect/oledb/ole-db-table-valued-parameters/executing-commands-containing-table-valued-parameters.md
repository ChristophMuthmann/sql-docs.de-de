---
title: Ausführen von Befehlen mit Tabellenwertparametern | Microsoft Docs
description: Ausführen von Befehlen, Tabellenwertparameter
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c3901c4f74ad911b90405209831e51cba92a93d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="executing-commands-containing-table-valued-parameters"></a>Ausführen von Befehlen, die Tabellenwertparameter enthalten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ausführen eines Befehls mit Tabellenwertparametern erfordert zwei Phasen:  
  
1.  Angeben der Parametertypen  
  
2.  Binden der Parameterdaten  
  
## <a name="table-valued-parameter-specification"></a>Tabellenwertparameter-Spezifikation  
 Der Consumer kann den Typ des Tabellenwertparameters angeben. Diese Angabe enthält den Typnamen des Tabellenwertparameters. Darüber hinaus den Schemanamen, wenn der benutzerdefinierte Tabellentyp für den Tabellenwertparameter im aktuellen Standardschema für die Verbindung nicht. Je nach serverunterstützung kann der Consumer kann auch optionale Metadateninformationen, z. B. die Sortierreihenfolge der Spalten angeben und kann darauf hinweisen, dass alle Zeilen für bestimmte Spalten Standardwerte aufweisen.  
  
 Um einen Tabellenwertparameter anzugeben, der Consumer ISSCommandWithParamter::SetParameterInfo aufruft, und ruft optional isscommandwithparameters:: SetParameterProperties. Für einen Tabellenwertparameter der *PwszDataSourceType* Feld in der DBPARAMBINDINFO-Struktur hat den Wert DBTYPE_TABLE. Die *UlParamSize* -Feld auf festgelegt wurde ~ 0 an, dass diese Länge ist unbekannt. Bestimmte Eigenschaften für Tabellenwertparameter, z. B. Schemaname, Typname, Spaltenreihenfolge und Standardspalten, können durch isscommandwithparameters:: SetParameterProperties festgelegt werden.  
  
## <a name="table-valued-parameter-binding"></a>Tabellenwertparameter-Bindung  
 Ein Tabellenwertparameter kann ein beliebiges Rowsetobjekt sein. Während der Ausführung liest der Anbieter beim Senden von Tabellenwertparametern an den Server aus diesem Objekt.  
  
 Um den Tabellenwertparameter zu binden, ruft der Consumer IAccessor:: CreateAccessor. Die *wType* -Feld der DBBINDING-Struktur für den Tabellenwertparameter wird auf DBTYPE_TABLE festgelegt. Die *pObject* Mitglied der DBBINDING-Struktur ist ungleich NULL, und die *pObject*des *Iid* Elementgruppe auf IID_IRowset oder ein anderes Objekt des Tabellenwertparameter-Rowset Schnittstellen. Die verbleibenden Felder in der DBBINDING-Struktur sollte die gleiche Weise festgelegt werden, die sie für gestreamte BLOBs festgelegt sind.  
  
 Für die Bindungen des Tabellenwertparameters und des einem Tabellenwertparameter zugeordneten Rowsetobjekts gelten die folgenden Einschränkungen:  
  
-   Die einzigen Statuswerte, die für Rowsetspaltendaten von Tabellenwertparametern zulässig sind, lauten DBSTATUS_S_ISNULL und DBSTATUS_S_OK. DBSTATUS_S_DEFAULT führt zu einem Fehler, und der gebundene Statuswert wird auf DBSTATUS_E_BADSTATUS festgelegt werden.  
  
-   Ein Tabellenwertparameter kann mit dem Status DBSTATUS_S_DEFAULT markiert werden. Die einzigen gültigen Werte sind DBSTATUS_S_DEFAULT und DBSTATUS_S_OK. Wenn der Status auf DBSTATUS_S_DEFAULT festgelegt ist, entspricht der Wert des Tabellenwertparameters einer leeren Tabelle.  
  
-   Schreibgeschützte Spalten in Tabellenwertparametern (Identitätsspalte und berechnete Spalte) müssen mit der SSPROP_PARAM_TABLE_DEFAULT_COLUMNS-Eigenschaft als Standard markiert werden. Spalten, die einen Standardwert aufweisen, müssen ebenfalls mit der SSPROP_PARAM_TABLE_DEFAULT_COLUMNS-Eigenschaft als Standard markiert werden. Dann kann der Standardwert als Datenwert einer Spalte für einen bestimmten Tabellenwertparameter verwendet werden. Der Anbieter ignoriert die Datenwerte, die an als Standard markierte Spalten gebunden sind.  
  
-   Für Spalten mit DBPROP_COL_AUTOINCREMENT oder SSPROP_COL_COMPUTED werden Daten an den Server gesendet, sofern nicht auch SSPROP_PARAM_TABLE_DEFAULT festgelegt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenwertparameter &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Verwenden des Table-Valued Parameters & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
