---
title: 'Isscommandwithparameters:: SetParameterProperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: dbd38ed336375cef79119f2fafb565bceeeb85bd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>'ISSCommandWithParameters::SetParameterProperties' (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Legt die Parametereigenschaften für einzelne Parameter nach Ordnungszahl fest oder legt Massenparametereigenschaften durch Angabe eines Arrays von SSPARAMPROPS-Strukturen fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argumente  
 *cParams*[in]  
 Die Anzahl der SSPARAMPROPS-Strukturen in den *RgParamProperties* Array. Wenn diese Anzahl Null ist, **isscommandwithparameters:: SetParameterProperties** werden alle Eigenschaften, die für alle Parameter im Befehl angegeben wurden möglicherweise gelöscht.  
  
 *RgParamProperties*[in]  
 Ein Array von SSPARAMPROPS-Strukturen, die festgelegt werden sollen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Die **isscommandwithparameters:: SetParameterProperties** Methodenrückgabe die gleichen Fehlercodes wie die OLE DB- **ICommandProperties:: SetProperties** Methode.  
  
## <a name="remarks"></a>Hinweise  
 Festlegen von Parametereigenschaften mit dieser Methode ist zulässig auf einer einzelparameterbasis nach Ordnungszahl oder mit einem einzelnen **isscommandwithparameters:: SetParameterProperties** aufrufen, sobald der SSPARAMPROPS aus dem Eigenschaftsarray erstellt wurde.  
  
 Die **SetParameterInfo** Methode muss aufgerufen werden, bevor die **isscommandwithparameters:: SetParameterProperties** Methode. Durch Aufrufen von `SetParameterProperties(0, NULL)` werden alle angegebenen Parametereigenschaften gelöscht, während der Aufruf von `SetParameterInfo(0,NULL,NULL)` alle Parameterinformationen löscht, einschließlich Eigenschaften, die einem Parameter zugeordnet sind.  
  
 Aufrufen von **isscommandwithparameters:: SetParameterProperties** Eigenschaften für einen Parameter angeben, die nicht vom Typ gibt DBTYPE_XML- oder DBTYPE_UDT DB_E_ERRORSOCCURRED oder DB_S_ERRORSOCCURRED und kennzeichnet die  *DwStatus* alle für diesen Parameter mit DBPROPSTATUS_NOTSET in SSPARAMPROPS enthaltenen DBPROPs Feld. Das DBPROP-Array jedes in SSPARAMPROPS enthaltenen DBPROPs sollte durchsucht werden, um zu ermitteln, auf welchen Parameter DB_E_ERRORSOCCURRED bzw. DB_S_ERRORSOCCURRED verweist.  
  
 Wenn **isscommandwithparameters:: SetParameterProperties** wird aufgerufen, um Geben Sie die Eigenschaften von Parametern, deren Parameterinformationen wurde mit nicht noch festgelegt **SetParameterInfo**, gibt der Anbieter E_ zurück UNERWARTETER mit der folgenden Fehlermeldung:  
  
 Die SetParameterProperties-Methode kann für die angegebenen Parameter nicht aufgerufen werden, ohne dass zunächst die SetParameterInfo-Methode aufgerufen wird. Die Parameterinformationen müssen vor dem Festlegen der Parametereigenschaften festgelegt werden.  
  
 Wenn der Aufruf von **isscommandwithparameters:: SetParameterProperties** enthält einige Parameter, in denen Parameterinformationen Satz wurde, und einige Parameter, in denen Parameterinformationen nicht, die DwStatus-Eigenschaften in festgelegt wurde, der DBPROPSET der SSPARAMPROPS-Eigenschaftensatz wird mit DBSTATUS_NOTSET zurückgegeben.  
  
 Die SSPARAMPROPS-Struktur ist folgendermaßen definiert:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Verbesserungen im Datenbankmodul ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] isscommandwithparameters:: SetParameterProperties genauere Beschreibungen der erwarteten Ergebnisse abrufen können. Diese genaueren Ergebnisse unterscheidet sich möglicherweise von der Rückgabewerte isscommandwithparameters:: SetParameterProperties in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Metadatenermittlung](../../relational-databases/native-client/features/metadata-discovery.md).  
  
|Member|Description|  
|------------|-----------------|  
|*iOrdinal*|Die Ordnungszahl des übergebenen Parameters|  
|*cPropertySets*|Die Anzahl von DBPROPSET-Strukturen in *rgPropertySets*|  
|*rgPropertySets*|Ein Zeiger auf den Speicher, in den ein Array aus DBPROPSET-Strukturen zurückgegeben werden soll|  
  
## <a name="see-also"></a>Siehe auch  
 [ISSCommandWithParameters & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
