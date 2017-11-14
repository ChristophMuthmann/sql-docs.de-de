---
title: ReadText-Methode | Microsoft Docs
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
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b134e064cc3d1dfa06c5d948d74e49f643756bd1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="readtext-method"></a>ReadText-Methode
Liest eine angegebene Anzahl von Zeichen aus einem Textobjekt [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parameter  
 *NumChars*  
 Optional. Ein **lange** Wert, der angibt, die Anzahl von Zeichen aus der Datei lesen oder eine [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) Wert. Der Standardwert ist **AdReadAll**.  
  
## <a name="return-value"></a>Rückgabewert  
 Die **ReadText** Methode liest eine angegebene Anzahl von Zeichen, eine ganze Zeile oder der gesamte Datenstrom aus einer **Stream** -Objekt und gibt das Ergebnis als Zeichenfolge zurück.  
  
## <a name="remarks"></a>Hinweise  
 Wenn *mit NUMCHARS angegebene* bleibt mehr als die Anzahl der Zeichen im Datenstrom, nur die verbleibenden Zeichen werden zurückgegeben. Die Zeichenfolge zu lesen, werden nicht entsprechend die vom angegebenen Länge aufgefüllt *mit NUMCHARS angegebene*. Wenn es sind keine um zu lesenden Zeichen vorhanden, wird ein Variant-Wert, dessen Wert null wird, zurückgegeben. **ReadText** kann nicht verwendet werden, um rückwärts zu lesen.  
  
> [!NOTE]
>  Die **ReadText** Methode wird verwendet, mit dem Text-Streams ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeText**). Für binäre Datenströme (**Typ** ist **AdTypeBinary**), verwenden Sie [lesen](../../../ado/reference/ado-api/read-method.md).  
  
 Abfragen, die eine große Menge von XML-Daten, die zurückgegeben wird, über die **ReadText** Methode des Datenstromobjekts ActiveX Data Object (ADO) kann viel Zeit für die Ausführung dauern, wenn dies in einer COM+-Komponente ausgeführt wird, der aufgerufen wird, aus einer ASP-Seite kann ein Timeout der Sitzung des Benutzers. ADO konvertiert Stream Objektdaten von UTF-8-Codierung in Unicode; die Konvertierung von eine große Menge von Daten, die gleichzeitig beteiligten häufiger speicherausschöpfungen neuzuordnungen ist sehr zeitaufwendig. Um zu beheben, stellen Sie wiederholte Aufrufe von der **ReadText** Methode von der ADO command-Objekt, und geben Sie eine kleinere Anzahl von Zeichen. Tests haben gezeigt, dass der Wert 128K (131.072) optimal ist. Antwortzeit verringert sich dieser Wert verringert wird. Weitere Informationen finden Sie im Knowledge Base-Artikel 280067, "PRB: Abrufen von sehr großen XML-Dokumente von SQLServer 2000 mit ReadText-Methode der ADO-Streamobjekt möglicherweise langsam", in der Microsoft Knowledge Base unter http://support.microsoft.com.  
  
## <a name="applies-to"></a>Gilt für  
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Read-Methode](../../../ado/reference/ado-api/read-method.md)

