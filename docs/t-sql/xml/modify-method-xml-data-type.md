---
title: modify()-Methode (xml-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 718b350793573527e822f0c28bd02f90e8a266fd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="modify-method-xml-data-type"></a>modify()-Methode (xml-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
 Da für die **modify()** -Methode eine Zeichenfolge in der XML Data Manipulation Language (DML) erforderlich ist, sind die Beispiele für **modify()** in den Themen zur Beschreibung der XML DML-Anweisungen enthalten. Diese Beispiele finden Sie unter [insert &#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md), [delete &#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md) und [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;Data Modification Language&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
