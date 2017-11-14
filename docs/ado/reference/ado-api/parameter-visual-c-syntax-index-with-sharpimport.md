---
title: 'Parameter (Visual C++-Syntax Index mit #import) | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- 'Parameter collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 6b43cf70-9695-47b0-9e68-f36898859b6b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2711de796936a8023ece248f92c7052dc859a720
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-visual-c-syntax-index-with-import"></a>Parameter (Visual C++-Syntax Index mit #import)
## <a name="methods"></a>Methoden  
  
```  
HRESULT AppendChunk( const _variant_t & Val );  
```  
  
## <a name="properties"></a>Eigenschaften  
  
```  
long GetAttributes( );  
void PutAttributes( long plParmAttribs );  
__declspec(property(get=GetAttributes,put=PutAttributes)) long  
    Attributes;  
  
enum ParameterDirectionEnum GetDirection( );  
void PutDirection( enum ParameterDirectionEnum plParmDirection );  
__declspec(property(get=GetDirection,put=PutDirection)) enum  
    ParameterDirectionEnum Direction;  
  
_bstr_t GetName( );  
void PutName( _bstr_t pbstr );  
__declspec(property(get=GetName,put=PutName)) _bstr_t Name;  
  
unsigned char GetNumericScale( );  
void PutNumericScale( unsigned char pbScale );  
__declspec(property(get=GetNumericScale,put=PutNumericScale)) unsigned  
    char NumericScale;  
  
unsigned char GetPrecision( );  
void PutPrecision( unsigned char pbPrecision );  
__declspec(property(get=GetPrecision,put=PutPrecision)) unsigned char  
    Precision;  
  
long GetSize( );  
void PutSize( long pl );  
__declspec(property(get=GetSize,put=PutSize)) long Size;  
  
enum DataTypeEnum GetType( );  
void PutType( enum DataTypeEnum psDataType );  
__declspec(property(get=GetType,put=PutType)) enum DataTypeEnum Type;  
  
_variant_t GetValue( );  
void PutValue( const _variant_t & pvar );  
__declspec(property(get=GetValue,put=PutValue)) _variant_t Value;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)

