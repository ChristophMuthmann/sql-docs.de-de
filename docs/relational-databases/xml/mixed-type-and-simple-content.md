---
title: Mixed-Datentyp und Simple-Inhalt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mixed types [SQL Server]
ms.assetid: 6ea1f11d-e64b-4ebb-ab68-4eb6e4027665
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c6ca3595ced1ff8d74c625d25e507b246f84342
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mixed-type-and-simple-content"></a>Mixed-Datentyp und Simple-Inhalt
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt das Beschränken eines mixed-Datentyps auf simple-Inhalt nicht.  
  
## <a name="example"></a>Beispiel  
 In der folgenden XML-Schemaauflistung ist `myComplexTypeA` ein complex-Datentyp, der leer sein kann. Das heißt, bei beiden Elementen wurde `minOccurs` auf 0 festgelegt. Der Versuch, dies wie in der `myComplexTypeB` -Deklaration auf einen einfachen Inhalt zu beschränken, wird nicht unterstützt. Daher schlägt die Erstellung der folgenden XML-Schemaauflistung fehl:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns"  
xmlns:ns1="http://ns1">  
  
    <complexType name="myComplexTypeA" mixed="true">  
        <sequence>  
            <element name="a" type="string" minOccurs="0"/>  
            <element name="b" type="string" minOccurs="0" maxOccurs="23"/>  
        </sequence>  
    </complexType>  
  
    <complexType name="myComplexTypeB">  
        <simpleContent>  
            <restriction base="ns:myComplexTypeA">  
                <simpleType>  
                    <restriction base="int">  
                        <minExclusive value="25"/>  
                    </restriction>  
                </simpleType>  
            </restriction>  
        </simpleContent>  
    </complexType>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  

