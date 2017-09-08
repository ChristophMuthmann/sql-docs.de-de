---
title: Modify()-Methode (Xml-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81838bf62f9b2c92dce4df8a167785fdfbf7abb2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="modify-method-xml-data-type"></a>modify()-Methode (xml-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ändert den Inhalt eines XML-Dokuments. Verwenden Sie diese Methode, um den Inhalt einer Spalte oder Variablen des **xml** -Datentyps zu ändern. Diese Methode verwendet eine XML DML-Anweisung, um Knoten in XML-Daten einzufügen, zu aktualisieren oder zu löschen. Die **modify()** -Methode des **xml** -Datentyps kann nur in der SET-Klausel einer UPDATE-Anweisung verwendet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>Argumente  
 XML_DML  
 Ist eine Zeichenfolge in XML DML (Data Manipulation Language). Das XML-Dokument wird anhand dieses Ausdrucks aktualisiert.  
  
> [!NOTE]  
>  Es wird ein Fehler zurückgegeben, wenn die **modify()** -Methode für einen NULL-Wert aufgerufen wird oder einen NULL-Wert ergibt.  
  
## <a name="examples"></a>Beispiele  
 Da für die **modify()** -Methode eine Zeichenfolge in der XML Data Manipulation Language (DML) erforderlich ist, sind die Beispiele für **modify()** in den Themen zur Beschreibung der XML DML-Anweisungen enthalten. Diese Beispiele finden Sie unter [Insert &#40; XML DML &#41; ](../../t-sql/xml/insert-xml-dml.md), [&#40; löschen XML DML &#41; ](../../t-sql/xml/delete-xml-dml.md) und [ersetzen Wert &#40; XML DML &#41; ](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML Data Modification Language &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

