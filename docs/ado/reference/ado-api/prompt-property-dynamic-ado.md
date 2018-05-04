---
title: Auffordern (ADO) für das dynamische Eigenschaft | Microsoft Docs
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
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc7285d03db3edf52ddb89a91b2b73c5d3ae74c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="prompt-property-dynamic-ado"></a>Prompt-Eigenschaft dynamisch (ADO)
Gibt an, ob der OLE DB-Anbieter den Benutzer zur Initialisierungsinformationen aufzufordern sollten.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest, und gibt eine [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) Wert.  
  
## <a name="remarks"></a>Hinweise  
 **Prompt** ist eine dynamische Eigenschaft, die angefügt werden kann die [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) des Objekts [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung über den OLE DB-Anbieter. Um Initialisierung Informationen aufzufordern, werden der OLE DB-Anbieter ein Dialogfeld in der Regel dem Benutzer angezeigt.  
  
 Dynamische Eigenschaften der eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt sind verloren, wenn die **Verbindung** geschlossen wird. Die **Prompt** Eigenschaft muss zurückgesetzt werden, vor dem erneuten Öffnen der **Verbindung** auf einen anderen Wert als den Standardwert verwenden.  
  
> [!NOTE]
>  Geben Sie an, dass der Anbieter über fordert den Benutzer in Szenarien sollte in der der Benutzer nicht auf das Dialogfeld reagieren kann. Beispielsweise wird der Benutzer nicht reagieren, wenn die Anwendung auf einem Serversystem nicht auf dem Client des Benutzers ausgeführt wird, oder wenn die Anwendung auf einem System mit ohne angemeldeten Benutzer ausgeführt wird. In diesen Fällen wird die Anwendung unbegrenzt auf eine Antwort warten und scheinbar abgestürzt.  
  
## <a name="usage"></a>Verwendung  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Gilt für  
 [Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
