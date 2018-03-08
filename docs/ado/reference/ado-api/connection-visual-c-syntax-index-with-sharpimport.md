---
title: 'Verbindung (Visual C++-Syntax Index mit #import) | Microsoft Docs'
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
- 'Connection collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 03f47eda-840d-4cab-83d9-ccddd873f342
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 840e50f51f2fdb2853f80634941eb883576457e8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="connection-visual-c-syntax-index-with-import"></a>Verbindung (Visual C++-Syntax Index mit #import)
## <a name="methods"></a>Methoden  
  
```  
HRESULT Cancel( );  
HRESULT Close( );  
_RecordsetPtr Execute( _bstr_t CommandText, VARIANT *  
    RecordsAffected,     long Options );  
long BeginTrans( );  
HRESULT CommitTrans( );  
HRESULT RollbackTrans( );  
HRESULT Open( _bstr_t ConnectionString, _bstr_t UserID,  
    _bstr_t Password,     long Options );  
_RecordsetPtr OpenSchema( enum SchemaEnum Schema, const  
    _variant_t &     Restrictions = vtMissing, const _variant_t &   
    SchemaID = vtMissing );  
```  
  
## <a name="properties"></a>Eigenschaften  
  
```  
_bstr_t GetConnectionString( );  
void PutConnectionString( _bstr_t pbstr );  
__declspec(property(get=GetConnectionString,put=PutConnectionString))  
    _bstr_t ConnectionString;  
long GetCommandTimeout( );  
void PutCommandTimeout( long plTimeout );  
__declspec(property(get=GetCommandTimeout,put=PutCommandTimeout)) long  
    CommandTimeout;  
long GetConnectionTimeout( );  
void PutConnectionTimeout( long plTimeout );  
__declspec(property(get=GetConnectionTimeout,put=PutConnectionTimeout))  
    long ConnectionTimeout;  
_bstr_t GetVersion( );  
__declspec(property(get=GetVersion)) _bstr_t Version;  
ErrorsPtr GetErrors( );  
__declspec(property(get=GetErrors)) ErrorsPtr Errors;  
_bstr_t GetDefaultDatabase( );  
void PutDefaultDatabase( _bstr_t pbstr );  
__declspec(property(get=GetDefaultDatabase,put=PutDefaultDatabase))  
    _bstr_t DefaultDatabase;  
enum IsolationLevelEnum GetIsolationLevel( );  
void PutIsolationLevel( enum IsolationLevelEnum Level );  
__declspec(property(get=GetIsolationLevel,put=PutIsolationLevel)) enum  
    IsolationLevelEnum IsolationLevel;  
long GetAttributes( );  
void PutAttributes( long plAttr );  
__declspec(property(get=GetAttributes,put=PutAttributes)) long  
    Attributes;  
enum CursorLocationEnum GetCursorLocation( );  
void PutCursorLocation( enum CursorLocationEnum plCursorLoc );  
__declspec(property(get=GetCursorLocation,put=PutCursorLocation)) enum  
    CursorLocationEnum CursorLocation;  
enum ConnectModeEnum GetMode( );  
void PutMode( enum ConnectModeEnum plMode );  
__declspec(property(get=GetMode,put=PutMode)) enum ConnectModeEnum  
    Mode;  
_bstr_t GetProvider( );  
void PutProvider( _bstr_t pbstr );  
__declspec(property(get=GetProvider,put=PutProvider)) _bstr_t  
    Provider;  
long GetState( );  
__declspec(property(get=GetState)) long State;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
