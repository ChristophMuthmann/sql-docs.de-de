---
title: Angeben von Verbindungseigenschaften | Microsoft Docs
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
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e07a16be9d12aa905abbad4b2007726b853d805
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
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
