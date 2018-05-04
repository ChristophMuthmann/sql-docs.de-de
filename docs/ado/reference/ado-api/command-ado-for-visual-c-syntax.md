---
title: Befehl (ADO für Visual C++-Syntax) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Command collection [ADO], ADO for Visual C++ syntax
ms.assetid: cf12cbd1-25f7-4bb5-aa94-0fe823b3b6d6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 206b88fb2e8b8bf14f678b826bc4b5d52deb597d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="command-ado-for-visual-c-syntax"></a>Befehl (ADO für Visual C++-Syntax)
## <a name="methods"></a>Methoden  
  
```  
Cancel(void)  
CreateParameter(BSTR Name, DataTypeEnum Type, ParameterDirectionEnum Direction, long Size, VARIANT Value, _ADOParameter **ppiprm)  
Execute(VARIANT *RecordsAffected, VARIANT *Parameters, long Options, _ADORecordset **ppirs)  
```  
  
## <a name="properties"></a>Eigenschaften  
  
```  
get_ActiveConnection(_ADOConnection **ppvObject)  
put_ActiveConnection(VARIANT vConn)  
putref_ActiveConnection(_ADOConnection *pCon)  
get_CommandText(BSTR *pbstr)  
put_CommandText(BSTR bstr)  
get_CommandTimeout(LONG *pl)  
put_CommandTimeout(LONG Timeout)  
get_CommandType(CommandTypeEnum *plCmdType)  
put_CommandType(CommandTypeEnum lCmdType)  
get_Name(BSTR *pbstrName)  
put_Name(BSTR bstrName)  
get_Prepared(VARIANT_BOOL *pfPrepared)  
put_Prepared(VARIANT_BOOL fPrepared)  
get_State(LONG *plObjState)  
get_Parameters(ADOParameters **ppvObject)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
