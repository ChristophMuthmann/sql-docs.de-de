---
title: Angeben von Verbindungseigenschaften | Microsoft Docs
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
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a91a6c1346f352c2ee55cef79d502d81ad8119ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-connection-properties"></a>Angeben von Verbindungseigenschaften
Können Sie angeben, Großteil der Informationen, die gemäß einer [Verbindungszeichenfolge](../../../ado/guide/data/creating-a-connection-string.md) durch Festlegen der Eigenschaften der **Verbindung** Objekt vor dem Öffnen der Verbindung. Beispielsweise könnten Sie denselben Effekt erzielen, wie in die Verbindungszeichenfolge erläutert [Erstellen einer Verbindungszeichenfolge](../../../ado/guide/data/creating-a-connection-string.md) mithilfe des folgenden Codes.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase wird festgelegt, nachdem die Verbindung zu öffnen.  
  
> [!NOTE]
>  In ADO verwenden, müssen Sie kein Kennwort mit Semikolons (";"), wenn das Kennwort in einfache Anführungszeichen eingeschlossen ist.
