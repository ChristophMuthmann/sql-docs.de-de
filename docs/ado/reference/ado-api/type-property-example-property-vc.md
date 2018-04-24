---
title: Geben Sie die Beispiel-Eigenschaft (Eigenschaft) (VC++) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Type property [property] [ADO], VC++ example
ms.assetid: a4e23508-fbf3-4468-be55-212e7238802b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aaa756ce6f9a314a15421b68872cb28e610c1411
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="type-property-example-property-vc"></a>Type-Eigenschaft (Beispiel) (VC++)
Dieses Beispiel zeigt die [Typ](../../../ado/reference/ado-api/type-property-ado.md) Eigenschaft. Es ist ein Modell für ein Hilfsprogramm zum Auflisten von z. B. die Namen und Typen einer Auflistung [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md), [Felder](../../../ado/reference/ado-api/fields-collection-ado.md)usw.  
  
 Wir müssen nicht öffnen die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) für den Zugriff auf seine **Eigenschaften** Auflistung sind vorhanden, wenn die **Recordset** Objekt instanziiert wird. Allerdings Festlegen der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft, um **AdUseClient** fügt verschiedene Eigenschaften, die **Recordset** des Objekts **Eigenschaften** Auflistung, indem das Beispiel ein wenig interessanter. Zur besseren Übersichtlichkeit, verwenden wir explizit die [Element](../../../ado/reference/ado-api/item-property-ado.md) aufzurufende jeder Eigenschaft [Eigenschaft](../../../ado/reference/ado-api/property-object-ado.md) Objekt.  
  
```  
// BeginTypePropertyCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void TypeX();  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   TypeX();  
   ::CoUninitialize();  
}  
  
void TypeX() {  
   // Define ADO object pointers, initialize pointers. These are in the ADODB:: namespace  
   _RecordsetPtr pRst = NULL;  
   PropertyPtr pProperty = NULL;  
  
   // Define Other Variables  
   _bstr_t strMsg;  
   _variant_t vIndex;  
   int intLineCnt = 0;     
  
   try {  
      TESTHR(pRst.CreateInstance (__uuidof(Recordset)));  
  
      // Set the Recordset Cursor Location  
      pRst->CursorLocation = adUseClient;  
  
      for (short iIndex = 0; iIndex <= (pRst->Properties->GetCount() - 1);iIndex++) {  
         vIndex = iIndex;  
         pProperty = pRst->Properties->GetItem(vIndex);  
  
         int propType = (int)pProperty->GetType();  
  
         switch(propType) {  
         case adBigInt:  
            strMsg = "adBigInt";  
            break;  
         case adBinary:  
            strMsg = "adBinary";  
            break;  
         case adBoolean:  
            strMsg = "adBoolean";  
            break;  
         case adBSTR:  
            strMsg = "adBSTR";  
            break;  
         case adChapter:  
            strMsg = "adChapter";  
            break;  
         case adChar:  
            strMsg = "adChar";  
            break;  
         case adCurrency:  
            strMsg = "adCurrency";  
            break;  
         case adDate:  
            strMsg = "adDate";  
            break;  
         case adDBDate:  
            strMsg = "adDBDate";  
            break;  
         case adDBTime:  
            strMsg = "adDBTime";  
            break;  
         case adDBTimeStamp:  
            strMsg = "adDBTimeStamp";  
            break;  
         case adDecimal:  
            strMsg = "adDecimal";  
            break;  
         case adDouble:  
            strMsg = "adDouble";  
            break;  
         case adEmpty:  
            strMsg = "adEmpty";  
            break;  
         case adError:  
            strMsg = "adError";  
            break;  
         case adFileTime:  
            strMsg = "adFileTime";  
            break;  
         case adGUID:  
            strMsg = "adGUID";  
            break;  
         case adIDispatch:  
            strMsg = "adIDispatch";  
            break;  
         case adInteger:  
            strMsg = "adInteger";  
            break;  
         case adIUnknown:  
            strMsg = "adIUnknown";  
            break;  
         case adLongVarBinary:  
            strMsg = "adLongVarBinary";  
            break;  
         case adLongVarChar:  
            strMsg = "adLongVarChar";  
            break;  
         case adLongVarWChar:  
            strMsg = "adLongVarWChar";  
            break;  
         case adNumeric:  
            strMsg = "adNumeric";  
            break;  
         case adPropVariant:  
            strMsg = "adPropVariant";  
            break;  
         case adSingle:  
            strMsg = "adSingle";  
            break;  
         case adSmallInt:  
            strMsg = "adSmallInt";  
            break;  
         case adTinyInt:  
            strMsg = "adTinyInt";  
            break;  
         case adUnsignedBigInt:  
            strMsg = "adUnsignedBigInt";  
            break;  
         case adUnsignedInt:  
            strMsg = "adUnsignedInt";  
            break;  
         case adUnsignedSmallInt:  
            strMsg = "adUnsignedSmallInt";  
            break;  
         case adUnsignedTinyInt:  
            strMsg = "adUnsignedTinyInt";  
            break;  
         case adUserDefined:  
            strMsg = "adUserDefined";  
            break;  
         case adVarBinary:  
            strMsg = "adVarBinary";  
            break;  
         case adVarChar:  
            strMsg = "adVarChar";  
            break;  
         case adVariant:  
            strMsg = "adVariant";  
            break;  
         case adVarNumeric:  
            strMsg = "adVarNumeric";  
            break;  
         case adVarWChar:  
            strMsg = "adVarWChar";  
            break;  
         case adWChar:  
            strMsg = "adWChar";  
            break;  
         default:  
            strMsg = "*UNKNOWN*";  
            break;  
         }  
  
         intLineCnt++;  
  
         printf ("Property %d : %s,Type = %s\n",iIndex, (LPCSTR)pProperty->GetName(),  
            (LPCSTR)strMsg);  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      PrintComError(e);  
   }  
}  
  
void PrintComError(_com_error &e) {  
  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.    
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Property-Objekt (ADO)](../../../ado/reference/ado-api/property-object-ado.md)   
 [Type-Eigenschaft (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
