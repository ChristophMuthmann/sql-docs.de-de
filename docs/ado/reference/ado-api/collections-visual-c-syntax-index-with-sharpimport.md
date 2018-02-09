---
title: 'Auflistungen (Visual C++-Syntax Index mit #import) | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 488f5dcc74f6b5b1d1ea89c794511a96dc3dea81
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="collections-visual-c-syntax-index-with-import"></a>Auflistungen (Visual C++-Syntax Index mit #import)
Es ist hilfreich zu wissen, dass Sammlungen bestimmte allgemeine Methoden und Eigenschaften erbt.  
  
 Alle Sammlungen erben die **Anzahl** Eigenschaft und **aktualisieren** -Methode und allen Sammlungen hinzufügen der **Element** Eigenschaft. Die **Fehler** fügt der Auflistung der **deaktivieren** Methode. Die **Parameter** Auflistung erbt die **Append** und **löschen** Methoden, während die **Felder** Auflistung fügt die **Append**, **löschen**, und **Update** Methoden.  
  
## <a name="properties-collection"></a>'Properties'-Sammlung  
  
### <a name="methods"></a>Methoden  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Eigenschaften  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>Fehlerauflistung  
  
### <a name="methods"></a>Methoden  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Eigenschaften  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Parameters-Auflistung  
  
### <a name="methods"></a>Methoden  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Eigenschaften  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>Fields-Auflistung  
  
### <a name="methods"></a>Methoden  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>Eigenschaften  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Errors-Auflistung (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Fields-Auflistung (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters-Auflistung (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
