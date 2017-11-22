---
title: Charset-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Stream::Charset
helpviewer_keywords: Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ded981a9ed4905aa607d8b19fe010682b61b5780
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="charset-property-ado"></a>Charset-Eigenschaft (ADO)
Gibt den Zeichensatz in das der Inhalt von Text [Stream](../../../ado/reference/ado-api/stream-object-ado.md) übersetzt werden soll, für die Speicherung in den internen Puffer der **Stream** Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert, der angibt, das Zeichen festgelegt, in dem der Inhalt des der **Stream** übersetzt werden. Der Standardwert ist **Unicode**. Zulässige Werte sind typische Zeichenfolgen, die als Internet Satz Zeichennamen (z. B. "Iso-8859-1", "Windows-1252" usw.) über die Schnittstelle übergeben. Eine Liste der Namen Satz Zeichen, die von einem System bekannt sind, finden Sie unter dem Unterschlüssel des HKEY_CLASSES_ROOT\MIME\Database\Charset in der Windows-Registrierung.  
  
## <a name="remarks"></a>Hinweise  
 In einem Text **Stream** -Objekt Textdaten befindet sich in den angegebenen Zeichensatz der **Charset** Eigenschaft. Der Standardwert ist Unicode. Die **Charset** Eigenschaft wird zum Konvertieren von Daten in der **Stream** oder kommenden aus der **Stream**. Z. B. wenn die **Stream** enthält ISO-8859-1-Daten und Daten in einen BSTR kopiert die **Stream** Objekt die Daten in Unicode konvertiert. Das Gegenteil trifft ebenfalls zu.  
  
 Für eine offene **Stream**, den aktuellen [Position](../../../ado/reference/ado-api/position-property-ado.md) muss am Anfang der **Stream** (0) festlegen können **Charset**.  
  
 **CharSet** wird verwendet, nur mit Text **Stream** Objekte ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeText**). Diese Eigenschaft wird ignoriert, wenn **Typ** ist **AdTypeBinary**.  
  
 Ein Codebeispiel finden Sie unter [Schritt 4: Füllen Sie das Textfeld "Details"](../../../ado/guide/data/step-4-populate-the-details-text-box.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
