---
title: Kommentare in XQuery | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- comments [XQuery]
- XQuery, comments
ms.assetid: 4d977268-de9d-4bf0-b310-b63f6a0fb0db
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ac26c6d480e591b9e82b91481f989dfe897f7ec2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="comments-in-xquery"></a>Kommentare in XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Sie können Kommentare zu XQuery hinzufügen. Die Kommentarzeichenfolgen werden mithilfe der Trennzeichen "`(:`" und "`:)`" hinzugefügt. Beispiel:  
  
```  
declare @x xml  
set @x=''  
SELECT @x.query('  
(: simple query to construct an element :)  
<ProductModel ProductModelID="10" />  
')  
```  
  
 Es folgt ein weiteres Beispiel, in denen eine Abfrage gegen eine Instruction-Spalte der angegeben wird, die **Xml** Typ:  
  
```  
SELECT Instructions.query('  
(: declare prefix and namespace binding in the prolog. :)  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  (: Following expression retrieves the <Location> element children of the <root> element. :)  
  /AWMI:root/AWMI:Location  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
  
