---
title: 'Field (Visual C++-Syntax Index mit #import) | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
dev_langs: C++
helpviewer_keywords: 'Field collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 90cb636a-9416-48a4-b4eb-bb11bbd40950
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4838bf808910100be1c7ad933cc40df7330aed09
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="field-visual-c-syntax-index-with-import"></a>Field (Visual C++-Syntax Index mit #import)
## <a name="methods"></a>Methoden  
  
```  
HRESULT AppendChunk( const _variant_t & Data );  
  
_variant_t GetChunk( long Length );  
```  
  
## <a name="properties"></a>Eigenschaften  
  
```  
long GetActualSize( );  
__declspec(property(get=GetActualSize)) long ActualSize;  
  
long GetAttributes( );  
void PutAttributes( long pl );  
__declspec(property(get=GetAttributes,put=PutAttributes)) long     Attributes;  
  
IUnknownPtr GetDataFormat( );  
void PutRefDataFormat( IUnknown * ppiDF );  
__declspec(property(get=GetDataFormat,put=PutRefDataFormat)) IunknownPtr  
    DataFormat;  
  
long GetDefinedSize( );  
void PutDefinedSize( long pl );  
__declspec(property(get=GetDefinedSize,put=PutDefinedSize)) long  
    DefinedSize;  
  
_bstr_t GetName( );  
__declspec(property(get=GetName)) _bstr_t Name;  
  
unsigned char GetNumericScale( );  
void PutNumericScale( unsigned char pbNumericScale );  
__declspec(property(get=GetNumericScale,put=PutNumericScale)) unsigned  
    char NumericScale;  
  
_variant_t GetOriginalValue( );  
__declspec(property(get=GetOriginalValue)) _variant_t OriginalValue;  
  
unsigned char GetPrecision( );  
void PutPrecision( unsigned char pbPrecision );  
__declspec(property(get=GetPrecision,put=PutPrecision)) unsigned char  
    Precision;  
  
enum DataTypeEnum GetType( );  
void PutType( enum DataTypeEnum pDataType );  
__declspec(property(get=GetType,put=PutType)) enum DataTypeEnum Type;  
  
_variant_t GetUnderlyingValue( );  
__declspec(property(get=GetUnderlyingValue)) _variant_t UnderlyingValue;  
  
_variant_t GetValue( );  
void PutValue( const _variant_t & pvar );  
__declspec(property(get=GetValue,put=PutValue)) _variant_t Value;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)
