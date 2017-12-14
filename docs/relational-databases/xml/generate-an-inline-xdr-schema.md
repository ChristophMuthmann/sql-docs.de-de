---
title: Generieren eines XDR-Inlineschemas | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XDR schemas [SQL Server]
- inline XDR schema generation [SQL Server]
- XMLDATA option
- FOR XML clause, inline XDR schema generation
ms.assetid: 2a40d617-9724-4f7d-80a4-a85c702f14d0
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0fc5032dd5519876f1c9dfb8480094f87742a226
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="generate-an-inline-xdr-schema"></a>Generieren eines XDR-Inlineschemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Von der **XMLDATA**-Direktive in FOR XML wird ein XDR-Inlineschema zusammen mit dem Abfrageergebnis zurückgegeben. Allerdings unterstützt das XDR-Schema nicht alle neuen Datentypen und anderen Erweiterungen, die in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen eingeführt wurden. Stattdessen können Sie ein XSD-Inlineschema mithilfe der [XMLSCHEMA-Direktive](../../relational-databases/xml/generate-an-inline-xsd-schema.md)anfordern.  
  
> [!IMPORTANT]  
>  Die XMLDATA-Direktive zur FOR XML-Option ist veraltet. Verwenden Sie XSD-Generierung für RAW- und AUTO-Modus. Es gibt keinen Ersatz für die XMLDATA-Direktive im EXPLICIT-Modus. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Beachten Sie auch folgende Hinweise zur XDR-Inlineschemaunterstützung:  
  
-   Wenn das FOR XML-Abfrageergebnis Spalten vom Typ **xml** enthält und ein XDR-Inlineschema anfordert, wird ein Fehler zurückgegeben. Inline-XDR unterstützt diese Typen nicht.  
  
-   Die Typen **(n)varchar(max)** und **(n)varbinary(max)** werden **(n)varchar(n)** bzw. **varbinary(n)**zugeordnet.  
  
-   Wenn der Kompatibilitätsmodus auf 90 oder höher festgelegt ist, werden **timestamp** -Werte als **varbinary(8)** angesehen, wie Binärdaten behandelt und folgendermaßen zurückgegeben:  
  
    -   Base 64-Codierung wird verwendet, wenn **binary base64** angegeben wird.  
  
    -   URL-Codierung wird im AUTO-Modus verwendet, wenn **binary base64** nicht angegeben wurde.  
  
  
