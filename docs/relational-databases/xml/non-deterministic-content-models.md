---
title: Nicht deterministische Inhaltsmodelle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-deterministic content models
- content models [XML in SQL Server]
ms.assetid: 9d4513e7-dd19-4491-b7c7-28bc7c2f8589
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb63b006a05ac6b67989562fb5535617eeb90fe4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="non-deterministic-content-models"></a>Nicht deterministische Inhaltsmodelle
  Vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 (SP1) lehnte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML-Schemas ab, die nicht deterministische Inhaltsmodelle enthielten.  
  
 Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1 werden nicht deterministische Inhaltsmodelle jedoch akzeptiert, wenn die Vorkommenseinschränkungen „0,1“ oder „unbegrenzt“ lauten.  
  
## <a name="example-non-deterministic-content-model-rejected"></a>Beispiel: Nicht deterministisches Inhaltsmodell abgelehnt  
 Im folgenden Beispiel wird versucht, ein XML-Schema mit einem nicht deterministischen Inhaltsmodell zu erstellen. Der Code schlägt fehl, da unklar ist, ob das `<root>` -Element eine Sequenz mit zwei `<a>` -Elementen oder ob das `<root>` -Element zwei Sequenzen mit jeweils einem `<a>` -Element haben sollte.  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="1" maxOccurs="2">  
                <element name="a" type="string" minOccurs="1" maxOccurs="2"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
 Das Schema kann durch Verschieben der Vorkommenseinschränkung an einen eindeutigen Speicherort korrigiert werden. So kann z. B. die Einschränkung zum enthaltenden Sequenzpartikel verschoben werden:  
  
```  
<sequence minOccurs="1" maxOccurs="4">  
    <element name="a" type="string" minOccurs="1" maxOccurs="1"/>  
</sequence>  
```  
  
 Oder die Einschränkung kann zum enthaltenen Element verschoben werden:  
  
```  
<sequence minOccurs="1" maxOccurs="1">  
     <element name="a" type="string" minOccurs="1" maxOccurs="4"/>  
</sequence>  
```  
  
## <a name="example-non-deterministic-content-model-accepted"></a>Beispiel: Nicht deterministisches Inhaltsmodell akzeptiert  
 Das folgende Schema würde in Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die älter als [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1 sind, abgelehnt werden.  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="0" maxOccurs="unbounded">  
                <element name="a" type="string" minOccurs="0" maxOccurs="1"/>  
                <element name="b" type="string" minOccurs="1" maxOccurs="unbounded"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
