---
title: Unterstützung für den OLE DB-Tabellenwertparameter-Typ (Eigenschaften) | Microsoft Docs
description: Datentypunterstützung für OLE DB Table-Valued-Parameter (Eigenschaften)
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
- table-valued parameters (OLE DB), API support (properties)
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: dbe4ff9ac8ccd23a4825ab0487d5fc5084ea64ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>OLE DB-Unterstützung von Tabellenwertparameter-Typen (Eigenschaften)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Dieses Thema stellt Informationen zu OLE DB-Eigenschaften und -Eigenschaftensätzen bereit, die Tabellenwertparameter-Rowsetobjekten zugeordnet werden.  
  
## <a name="properties"></a>Eigenschaften  
 Im folgenden wird die Liste der Eigenschaften, die über die Methode IRowsetInfo::GetPropeties für Tabellenwertparameter-Rowsetobjekte verfügbar gemacht werden. Beachten Sie, dass alle Tabellenwertparameter-Rowseteigenschaften schreibgeschützt sind. Aus diesem Grund versucht, eine Festlegen der Eigenschaften über IOpenRowset:: OPENROWSET oder ITableDefinitionWithConstraints::CreateTableWithConstraints führt zu einem Fehler Methoden mit ihren Standardwerten und kein Objekt erstellt werden.  
  
 Im Tabellenwertparameter-Rowsetobjekt nicht implementierte Eigenschaften werden hier nicht aufgelistet. Eine vollständige Liste von Eigenschaften finden Sie in der OLE DB-Dokumentation in den Windows Data Access Components.  
  
|Eigenschafts-ID|Wert|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|R/w: schreibgeschützt<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Lesezeichen sind für Tabellenwertparameter-Rowsetobjekte nicht zulässig.|  
|DBPROP_BOOKMARKSKIPPED|VARIANT_FALSE|  
|DBPROP_BOOKMARKTYPE|DBPROPVAL_BMK_NUMERIC|  
|DBPROP_CANHOLDROWS|VARIANT_FALSE|  
|DBPROP_CHANGEINSERTEDROWS|VARIANT_TRUE|  
|DBPROP_COLUMNRESTRICT|VARIANT_FALSE|  
|DBPROP_COMMANDTIMEOUT|0|  
|DBPROP_COMMITPRESERVE|VARIANT_TRUE|  
|DBPROP_DEFERRED|VARIANT_FALSE|  
|DBPROP_DELAYSTORAGEOBJECTS|VARIANT_FALSE|  
|DBPROP_IAccessor<br /><br /> DBPROP_IColumnsInfo<br /><br /> DBPROP_IConvertType<br /><br /> DBPROP_IRowset<br /><br /> DBPROP_IRowsetInfo,<br /><br /> DBPROP_IColumnsRowset|VARIANT_TRUE|  
|DBPROP_IConnectionPointContainer<br /><br /> DBPROP_IMultipleResults<br /><br /> DBPROP_IRowsetUpdate<br /><br /> DBPROP_IRowsetIdentity<br /><br /> DBPROP_IRowsetLocate<br /><br /> DBPROP_IRowsetScroll<br /><br /> DBPROP_IRowsetResynch|VARIANT_FALSE|  
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> Hinweis: Das Tabellenwertparameter-Rowsetobjekt unterstützt die IRowsetChange-Schnittstellen.<br /><br /> Ein mit DBPROP_IRowsetChange gleich VARIANT_TRUE erstelltes Rowset zeigt Verhaltensweisen des Sofortupdatemodus.<br /><br /> Jedoch wenn BLOB-Spalten als ISequentialStream-Objekte gebunden werden, muss der Consumer diese für die Lebensdauer des Tabellenwertparameter-Rowsetobjekts aufbewahrt werden sollen.|  
|DBPROP_ISupportErrorInfo|VARIANT_TRUE|  
|DBPROP_ISequentialStream|VARIANT_TRUE|  
|DBPROP_IMMOBILEROWS|VARIANT_TRUE|  
|DBPROP_LITERALIDENTITY|VARIANT_TRUE|  
|DBPROP_LOCKMODE|DBPROPVAL_LM_NONE|  
|DBPROP_MAXOPENROWS|0|  
|DBPROP_MAXPENDINGROWS|0|  
|DBPROP_MAXROWS|0|  
|DBPROP_NOTIFICATIONPHASES|0|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|0|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE|VARIANT_FALSE|  
|DBPROP_OWNINSERT<br /><br /> DBPROP_OWNUPDATEDELETE|VARIANT_TRUE|  
|DBPROP_QUICKRESTART|VARIANT_TRUE|  
|DBPROP_REENTRANTEVENTS|VARIANT_FALSE|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|  
|DBPROP_RETURNPENDINGINSERTS|VARIANT_TRUE|  
|DBPROP_ROWRESTRICT|VARIANT_FALSE|  
|DBPROP_ROWTHREADMODEL|DBPROPVAL_RT_FREETHREAD|  
|DBPROP_SERVERCURSOR|VARIANT_FALSE|  
|DBPROP_SERVERDATAONINSERT|VARIANT_FALSE|  
|DBPROP_STRONGIDENTITY|VARIANT_TRUE|  
|DBPROP_TRANSACTEDOBJECT|VARIANT_FALSE|  
|DBPROP_UNIQUEROWS|VARIANT_FALSE|  
|DBPROP_UPDATABILITY|DBPROPVAL_UP_CHANGE &AMP;#124; DBPROPVAL_UP_DELETE &AMP;#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>Eigenschaftensätze  
 Die folgenden Eigenschaftensätze unterstützen Tabellenwertparameter.  
  
### <a name="dbpropsetsqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 Diese Eigenschaft wird vom Consumer ggf. beim Erstellen einer Tabellenwertparameter-Rowsetobjekt mit ITableDefinitionWithConstraints::CreateTableWithConstraints für jede Spalte über DBCOLUMNDESC-Struktur, bei Bedarf verwendet.  
  
|Eigenschafts-ID|Eigenschaftswert|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|R/W: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Typ: VT_BOOL<br /><br /> Beschreibung: Die Festlegung auf VARIANT_TRUE gibt an, dass die Spalte eine berechnete Spalte ist. VARIANT_FALSE gibt an, dass sie keine berechnete Spalte ist.|  
  
### <a name="dbpropsetsqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 Diese Eigenschaften sind vom Consumer beim Erkennen der Tabellenwertparameter-Typinformationen in Aufrufen an ISSCommandWithParamters::GetParameterProperties gelesen und vom Consumer festlegen bestimmte Eigenschaften zu den Tabellenwertparameter festgelegt über isscommandwithparameters:: SetParameterProperties.  
  
 In der folgenden Tabelle werden detaillierte Beschreibungen dieser Eigenschaften bereitgestellt.  
  
|Eigenschafts-ID|Eigenschaftswert|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|R/W: Lesen/Schreiben<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_BSTR<br /><br /> Beschreibung: Consumer verwenden diese Eigenschaft, um den Namen des Tabellenwertparameter-Typs abzurufen oder festzulegen.<br /><br /> Diese Eigenschaft kann auch mit CLR-benutzerdefinierten Typen verwendet werden.<br /><br /> Diese Eigenschaft kann optional angegeben werden, um einen Tabellentypnamen für einen Tabellenwertparameter bereitzustellen (im Falle eines ODBC-Abruf-Syntaxbefehls). Diese Eigenschaft ist für parametrisierte Ad-hoc-SQL-Abfragen erforderlich.|  
|SSPROP_PARAM_TYPE_SCHEMANAME|R/W: Lesen/Schreiben<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_BSTR<br /><br /> Beschreibung: Consumer verwenden diese Eigenschaft, um den Schemanamen des Tabellenwertparameter-Typs abzurufen oder festzulegen.<br /><br /> Diese Eigenschaft kann auch mit CLR-benutzerdefinierten Typen verwendet werden.|  
|SSPROP_PARAM_TYPE_CATALOGNAME|R/W: Schreibgeschützt<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_BSTR<br /><br /> Beschreibung: Consumer verwenden diese Eigenschaft, um den Katalognamen des Tabellenwertparameter-Typs abzurufen.<br /><br /> Diese Eigenschaft kann auch mit CLR-benutzerdefinierten Typen verwendet werden. Das Festlegen dieser Eigenschaft resultiert in einem Fehler. Benutzerdefinierte Tabellentypen müssen sich in derselben Datenbank wie die Tabellenwertparameter befinden, die die Tabellentypen verwenden.|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|R/W: Lesen/Schreiben<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_UI2 &#124; VT_ARRAY<br /><br /> Beschreibung: Consumer verwenden diese Eigenschaft, um anzugeben, welche Spaltengruppe im Rowset als Standard behandelt werden soll. Für diese Spalten werden keine Werte gesendet. Während Daten aus dem Consumerrowsetobjekt abgerufen werden, benötigt der Provider keine Bindung für diese Spalten.<br /><br /> Jedes Element des Arrays sollte eine Ordinalzahl einer Spalte im Rowsetobjekt sein. Ungültige Ordinalzahlen führen beim Ausführen des Befehls zu Fehlern.|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|R/W: Lesen/Schreiben<br /><br /> Standard: VT_EMPTY<br /><br /> Typ: VT_UI2 &#124; VT_ARRAY<br /><br /> Beschreibung: Diese Eigenschaft wird vom Consumer verwendet, um dem Server einen Hinweis zur Sortierreihenfolge der Spaltendaten bereitzustellen. Der Provider führt keinerlei Überprüfung durch und nimmt an, dass der Consumer der bereitgestellten Spezifikation entspricht. Der Server verwendet diese Eigenschaft, um Optimierungen durchzuführen.<br /><br /> Spaltenreihenfolgeninformationen für jede Spalte werden durch ein Paar von Elementen im Array dargestellt. Das erste Element im Paar ist die Nummer der Spalte. Das zweite Element im Paar ist 1 für eine aufsteigende Reihenfolge oder 2 für eine absteigende Reihenfolge.|  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützung des OLE DB-Tabellenwertparameter-Typ](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [Verwenden des Table-Valued Parameters & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
