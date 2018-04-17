---
title: NULL-Behandlung von (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73dfd298bfe9b6dd603c70ab22b20dc48af69957
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="null-handling-sqlxml-40"></a>Behandlung von NULL (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML-Syntax deutet NULL als eine Abwesenheit. Wenn ein Attribut- oder Elementwert beispielsweise NULL ist, ist das Attribut bzw. Element nicht in dem XML-Dokument vorhanden. In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, die **updg: NullValue** -Attributs können NULL für ein Element oder Attribut-Wert angeben.  
  
 Das folgende Updategram stellt z. B. sicher, dass die **Titel** -Wert eines Kontakts mit **ContactID** von 64 NULL ist, und aktualisiert dann die **Titel** Wert auf "Mr." auf "Mr.".  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Wenn Parameter an ein Updategram übergeben werden, kann NULL als Parameterwert übergeben werden. Dies erfolgt durch Angabe der **Nullvalue** Attribut in der  **\<Updg:header >** Block. Ein Beispiel finden Sie unter [übergeben von Parametern an Updategrams &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitsüberlegungen zu Updategrams &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
