---
title: "Erstellen, Ändern und Löschen sekundärer, selektiver XML-Indizes | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa52c7a05fc0db049af7ce01f29ef0fd0801bdba
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>Erstellen, Ändern und Löschen sekundärer, selektiver XML-Indizes
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Beschreibt, wie ein neuer sekundärer, selektiver XML-Index erstellt bzw. ein vorhandener sekundärer, selektiver XML-Index geändert oder gelöscht wird.  
  
##  <a name="create"></a> Erstellen eines sekundären, selektiven XML-Indexes  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>Vorgehensweise: Erstellen eines sekundären, selektiven XML-Indexes  
 **Erstellen eines sekundären, selektiven XML-Indexes mit Transact-SQL**  
 Erstellen Sie einen sekundären, selektiven XML-Index, indem Sie die CREATE XML INDEX-Anweisung aufrufen. Weitere Informationen finden Sie unter [CREATE XML INDEX &#40;selektive XML-Indizes&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
 **Beispiel**  
  
 Im folgenden Beispiel wird ein sekundärer selektiver XML-Index für den Pfad `'pathabc'`erstellt. Der zu indizierende Pfad wird anhand des Namens identifiziert, der ihm bei der Erstellung durch die CREATE SELECTIVE XML INDEX-Anweisung zugewiesen wurde. Weitere Informationen finden Sie unter [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
```tsql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="alter"></a> Ändern eines sekundären, selektiven XML-Indexes  
 Die ALTER-Anweisung wird für sekundäre, selektive XML-Indizes nicht unterstützt. Um einen sekundären, selektiven XML-Index zu ändern, löschen Sie den vorhandenen Index und erstellen ihn erneut.  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>Vorgehensweise: Ändern eines sekundären, selektiven XML-Indexes  
 **Ändern eines sekundären, selektiven XML-Indexes mit Transact-SQL**  
 1.  Löschen Sie den vorhandenen sekundären, selektiven XML-Index, indem Sie die DROP INDEX-Anweisung aufrufen. Weitere Informationen finden Sie unter [DROP INDEX &#40;selektive XML-Indizes&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
2.  Erstellen Sie den Index mit den gewünschten Optionen neu, indem Sie die CREATE XML INDEX-Anweisung aufrufen. Weitere Informationen finden Sie unter [CREATE XML INDEX &#40;selektive XML-Indizes&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
 **Beispiel**  
  
 Im folgenden Beispiel wird ein sekundärer, selektiver XML-Index geändert, indem er gelöscht und neu erstellt wird.  
  
```tsql  
DROP INDEX filt_sxi_index_c  
  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="drop"></a> Löschen eines sekundären, selektiven XML-Indexes  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>Vorgehensweise: Löschen eines sekundären, selektiven XML-Indexes  
 **Löschen eines sekundären, selektiven XML-Indexes mit Transact-SQL**  
 Löschen Sie einen sekundären, selektiven XML-Index, indem Sie die DROP INDEX-Anweisung aufrufen. Weitere Informationen finden Sie unter [DROP INDEX &#40;selektive XML-Indizes&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
 **Beispiel**  
  
 Im folgenden Beispiel wird eine DROP INDEX-Anweisung veranschaulicht.  
  
```tsql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [Selektive XML-Indizes &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
