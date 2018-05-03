---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Microsoft Docs'
description: "'ISSCommandWithParameters::GetParameterProperties' (OLE DB)"
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e14ad816408347e17a8b5d5ff12b678bcc49377f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>'ISSCommandWithParameters::GetParameterProperties' (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Gibt ein Array aus SSPARAMPROPS-Eigenschaftensatzstrukturen zurück – einen SSPARAMPROPS-Eigenschaftensatz für jeden UDT- oder XML-Parameter.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argumente  
 *pcParams*[out] [in]  
 Ein Zeiger auf den Arbeitsspeicher, der die Anzahl von SSPARAMPROPS-Strukturen enthält, die in *prgParamProperties*zurückgegeben werden.  
  
 *prgParamProperties*[out]  
 Ein Zeiger auf den Arbeitsspeicher, in den ein Array aus SSPARAMPROPS-Strukturen zurückgegeben wird. Der Anbieter teilt Speicher für die Strukturen und gibt die Adresse zu diesem Arbeitsspeicher zurück, der Consumer gibt diesen Arbeitsspeicher mit **IMalloc:: Free** wenn er die Strukturen nicht mehr benötigt. Vor dem Aufruf **IMalloc:: Free** für *PrgParamProperties*, der Consumer muss auch aufrufen, **VariantClear** für die *vValue* Eigenschaft Geben Sie z. B. einen BSTR, jeder DBPROP-Struktur, um einen Speicherverlust in Fällen zu vermeiden, in dem die Variante einen Verweis enthält. Wenn *PcParams* ist 0 (null) bei der Ausgabe oder ein anderer Fehler als DB_E_ERRORSOCCURRED auftritt, teilt der Anbieter keine Arbeitsspeicher und wird sichergestellt, dass *PrgParamProperties* bei Ausgabe ein null-Zeiger ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Die **GetParameterProperties** Methodenrückgabe die gleichen Fehlercodes wie die OLE DB- **ICommandProperties:: GetProperties** -Methode, mit Ausnahme von DB_S_ERRORSOCCURRED und DB_E_ERRORSOCCURED nicht möglich wird ausgelöst.  
  
## <a name="remarks"></a>Hinweise  
 **ISSCommandWithParameters::GetParameterProperties** method behaves consistently with respect to **GetParameterInfo**. Wenn [isscommandwithparameters:: SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) oder **SetParameterInfo** nicht aufgerufen wurden oder gleich 0 (null), einem aufgerufen worden **GetParameterInfo**Parameterinformationen abgeleitet und gibt ihn zurück. Wenn **isscommandwithparameters:: SetParameterProperties** oder **SetParameterInfo** aufgerufen wurden, für mindestens einen Parameter **isscommandwithparameters:: Getparameterproperties**  Methodenrückgabe Eigenschaften nur für die Parameter für die **isscommandwithparameters:: SetParameterProperties** aufgerufen wurde. Wenn **isscommandwithparameters:: SetParameterProperties** wird aufgerufen, nachdem **isscommandwithparameters:: Getparameterproperties** oder **GetParameterInfo**, nachfolgende Aufrufe **isscommandwithparameters:: Getparameterproperties** die überschriebenen Werte für jene Parameter zurück, für die **isscommandwithparameters:: SetParameterProperties** -Methode aufgerufen wurde.  
  
 Die SSPARAMPROPS-Struktur ist folgendermaßen definiert:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Member|Description|  
|------------|-----------------|  
|*iOrdinal*|Die Ordnungszahl des übergebenen Parameters|  
|*cPropertySets*|Die Anzahl von DBPROPSET-Strukturen in *rgPropertySets*|  
|*rgPropertySets*|Ein Zeiger auf den Speicher, in den ein Array aus DBPROPSET-Strukturen zurückgegeben werden soll|  
  
## <a name="see-also"></a>Siehe auch  
 [ISSCommandWithParameters & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
