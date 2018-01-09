---
title: "Unterstützung für den OLE DB-Tabellenwertparameter-Typ (Methoden) | Microsoft Docs"
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
helpviewer_keywords: table-valued parameters (OLE DB), API support (methods)
ms.assetid: e3c2a450-8fd4-44cb-93d8-affe1b65c68e
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6dd054add63521e7ea2ced2a706bef426c497f77
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="ole-db-table-valued-parameter-type-support-methods"></a>OLE DB-Unterstützung von Tabellenwertparameter-Typen (Methoden)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die folgenden Standard-OLE DB-Methoden unterstützen Tabellenwertparameter:  
  
|Methode|Tabellenwertparameter-Unterstützung|  
|------------|-------------------------------------|  
|ITableDefinitionWithConstraints::CreateTableWithConstraints|Wird verwendet, wenn Sie den Typ des Tabellenwertparameters kennen und ein Tabellenwertparameter-Rowsetobjekt anhand der Typinformation instanziieren möchten.<br /><br /> Weitere Informationen finden Sie unter "Statischen Szenario" in [Table-Valued Parameter Rowseterstellung](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md).|  
|IOpenRowset::OpenRowset|Wird verwendet, wenn Sie den Typ eines Tabellenwertparameters nicht kennen und ein Tabellenwertparameter-Rowsetobjekt anhand der vom Server abgerufenen Metadateninformationen instanziieren möchten.<br /><br /> Weitere Informationen finden Sie unter "Dynamischen Szenario" in [Table-Valued Parameter Rowseterstellung](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md).|  
|ISSCommandWithParameters::SetParameterInfo|Um ein Tabellenwertparameter-Befehlsparameters gibt der Consumer den Typ des Parameters als 'Table' oder 'DBTYPE_TABLE' in der *PwszName* -Element der DBPARAMBINDINFO-Struktur. Die *UlParamSize* -Wert von ~ 0. Weitere Informationen finden Sie unter "Tabellenwertparameter-Spezifikation" in [Executing Commands Containing Table-Valued Parameter](../../relational-databases/native-client-ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md).|  
|Isscommandwithparameters:: SetParameterProperties|Legt spezielle Eigenschaften für Tabellenwertparameter fest, z. B. Schemaname, Typname, Spaltenreihenfolge und Standardspalten.<br /><br /> Der Consumer gibt die Ordnungszahl des Parameters in der *iOrdinal* der SSPARAMPROPS-Struktur. Die angeforderte Eigenschaftengruppe ist DBPROPSET_SQLSERVERPARAMETER.|  
|ISSCommandWithParameters::GetParameterInfo|Ruft die Typen aller Parameter zu einem angegebenen Befehl ab.<br /><br /> Für Tabellenwertparameter der *wType* Feld in der DBPARAMINFO-Struktur über den Typ DBTYPE_TABLE. Die *UlParamSize* Standardfeldsatz auf ~ 0, um unbekannte Länge anzugeben.|  
|Isscommandwithparameters:: Getparameterproperties|Ruft weitere Typinformationen für Parameter des DBTYPE_TABLE-Typs ab.<br /><br /> Der Consumer gibt die Ordnungszahl des Parameters in der *iOrdinal* -Element der SSPARAMPROPS-Struktur. Der Consumer kann beliebige Eigenschaften in der DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe anfordern, die unter isscommandwithparameters:: SetParameterProperties aufgelistet sind.<br /><br /> Da der Consumer den Tabellenwertparameter-Typ nicht kennt, muss der Anbieter für SSPROP_PARAM_TYPE_TYPENAME, SSPROP_PARAM_TYPE_SCHEMANAME und SSPROP_PARAM_TYPE_CATALOGNAME die korrekten Werte festlegen. Die übrigen Eigenschaften, SSPROP_PARAM_TABLE_DEFAULT_COLUMNS und SSPROP_PARAM_TABLE_COLUMN_SORT_ORDER, behalten ihre Standardwerte. Nachdem der Consumer die Tabellenwertparameter-Typnamen erkannt hat, verwendet er IOpenRowset:: OPENROWSET zum Erstellen einer Instanz dieses Tabellenwert-Parameters, der den Namen des Tabellenwertparameter-Typs angeben. Weitere Informationen finden Sie unter [Table-Valued Parameter Typermittlung](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md).|  
|IRowsetInfo:: GetProperties|Ruft Tabellenwertparameter-Rowseteigenschaften ab. Der Consumer kann diese Eigenschaften verwenden, um Bindungen optimal einzurichten.|  
|IColumnsRowset::GetColumnsRowset|Ruft Metadateninformationen zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle ab. Für Tabellenwertparameter stellt diese Schnittstelle ausführliche Metadateninformationen über jede Spalte bereit, darunter:<br /><br /> DBCOLUMN_FLAGS gibt die NULL-Zulässigkeit durch das DBCOLUMNFLAGS_ISNULLABLE-Bit an.<br /><br /> DBCOLUMN_ISUNIQUE gibt an, ob es sich bei der Spalte um eine Identitätsspalte handelt.<br /><br /> DBCOLUMN_COMPUTEMODE gibt an, ob die Spalte berechnet wird.|  
|IAccessor:: CreateAccessor|Um ein Tabellenwertparameter-Rowsetobjekt an einen Befehlsparameter zu binden, erstellen Sie einen Accessor mit seiner *wType* Members auf DBTYPE_TABLE festgelegt. IID_IRowset oder jede andere gültige Rowsetobjekt-Schnittstelle in der DBOBJECT-Struktur enthält die *Iid* Member. Die übrigen Felder werden ähnlich behandelt wie DBTYPE_IUNKNOWN.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Unterstützung des OLE DB-Tabellenwertparameter-Typ](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [Tabellenwertparameter-Rowseterstellung](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)   
 [Verwenden des Table-Valued Parameters &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
