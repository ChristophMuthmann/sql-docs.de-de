---
title: "Kanonische Formen und Musterbeschränkungen | Microsoft-Dokumentation"
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
- pattern restrictions
- canonical forms
ms.assetid: 088314ec-7d0b-4a05-8a33-f35da5bfe59c
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 91512853c317e905feaf4c799516191458264c8e
ms.lasthandoff: 04/11/2017

---
# <a name="canonical-forms-and-pattern-restrictions"></a>Kanonische Formen und Musterbeschränkungen
  Das XSD-Musterfacet ermöglicht das Beschränken des lexikalischen Speicherplatzes für simple-Datentypen. Wenn einem Datentyp eine Musterbeschränkung auferlegt wird, für den mehrere mögliche lexikalische Darstellungen vorhanden sind, können einige Werte bei der Überprüfung unerwartetes Verhalten bewirken.  
  
 Dieses Verhalten tritt auf, weil die lexikalischen Darstellungen dieser Werte nicht in der Datenbank gespeichert werden. Daher werden die Werte in ihre kanonischen Darstellungen konvertiert, wenn sie als Ausgabe serialisiert werden. Wenn ein Dokument einen Wert enthält, dessen kanonische Form nicht der Musterbeschränkung für seinen Datentyp genügt, wird das Dokument zurückgewiesen, wenn ein Benutzer versucht, diesen Wert erneut einzufügen.  
  
 Um dies zu verhindern, lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle XML-Dokumente ab, die Werte enthalten, die nicht erneut eingefügt werden können, weil ihre kanonischen Formen die Musterbeschränkung verletzen. Bei der Überprüfung des Wertes „33.000“ mit einem von **xs:decimal** abgeleiteten Datentyp mit einer Musterbeschränkung von „33\\.0+“ tritt z.B. ein Fehler auf. Zwar genügt "33.000" diesem Muster, die kanonische Form "33" jedoch nicht.  
  
 Daher sollten Sie vorsichtig sein, wenn Sie Musterfacets auf Typen anwenden, die von den folgenden Grundtypen abgeleitet wurden: **boolean**, **decimal**, **float**, **double**, **dateTime**, **time**, **date**, **hexBinary**und **base64Binary**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt eine Warnung aus, wenn Sie einer Schemaauflistung solche Komponenten hinzufügen.  
  
 Die unpräzise Serialisierung von Gleitkommawerten weist ein ähnliches Problem auf. Aufgrund des von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendeten Gleitkommaserialisierungsalgorithmus ist es möglich, dass ähnliche Werte die gleiche kanonische Form gemeinsam verwenden. Wenn ein Gleitkommawert serialisiert und dann erneut eingefügt wird, kann sich sein Wert geringfügig ändern. In seltenen Fällen kann dieser Vorgang zu einem Wert führen, der einen der folgendes Facets für seinen Datentyp beim erneuten Einfügen verletzt: **enumeration**, **minInclusive**, **minExclusive**, **maxInclusive**oder **maxExclusive**. Damit dies verhindert wird, weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte von Datentypen zurück, die von `xs:float` oder `xs:double` abgeleitet sind und nicht serialisiert und erneut eingefügt werden können.  
  
## <a name="see-also"></a>Siehe auch  
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
