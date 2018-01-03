---
title: Angeben von Verbindungseigenschaften | Microsoft Docs
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
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 80da1a4da2d2a04f6a73b05e57ab366d2cb40e97
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
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
