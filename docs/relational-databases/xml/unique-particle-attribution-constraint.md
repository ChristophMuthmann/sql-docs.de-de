---
title: "Einschränkung für eindeutige Partikelzuordnung | Microsoft-Dokumentation"
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
f1_keywords: unique particle attribution
helpviewer_keywords:
- schema collections [SQL Server], unique particle attribution
- XML schema collections [SQL Server], unique particle attribution
- UPA constraint rule
- unique particle attribution constraint rule
ms.assetid: 6bb879e9-a5ee-402e-94e4-fe8cec5966b0
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 712668f3b495017765205b939c390db0f0d75456
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="unique-particle-attribution-constraint"></a>Einschränkung für eindeutige Partikelzuordnung
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] In XSD werden komplexe Inhaltsmodelle durch die UPA-Einschränkungsregel (Unique Particle Attribution, eindeutige Partikelzuordnung) eingeschränkt. Diese Regel verlangt, dass jedes Element in einem Instanzdokument eindeutig genau einem `<xsd:element>` - oder `<xsd:any>` -Partikel im übergeordneten Inhaltsmodell entspricht. Jedes Schema, das einen Typ mit einem potenziell mehrdeutigen Inhaltsmodell enthält, wird zurückgewiesen.  
  
 Die häufigste Ursache für Mehrdeutigkeit sind `<xsd:any>`-Platzhalterzeichen und -partikel, die variable Vorkommensbereiche aufweisen, z. B. minOccurs < maxOccurs. Das folgende Inhaltsmodell ist z. B. mehrdeutig, da ein <`e1`>-Element dem `<xsd:element>`- oder dem `<xsd:any>`-Element entsprechen kann.  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
            <xsd:element name="e1"/>  
            <xsd:any namespace="##any"/>  
        </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 Das folgende Inhaltsmodell ist ebenfalls mehrdeutig:  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:sequence>  
            <xsd:element name="e1" maxOccurs="2"/>  
            <xsd:element name="e2" minOccurs="0"/>  
            <xsd:element name="e1"/>  
        </xsd:sequence>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 Ein Dokument wie z. B. `<root><e1/><e2/><e1/></root>` kann zwar eindeutig überprüft werden, ein Dokument wie z. B. `<root><e1/><e1/></root>` hingegen nicht, weil nicht eindeutig ist, welchem `<xsd:element>` die zweite Angabe `<e1/>` entspricht. Auch wenn einige Dokumente eindeutig überprüft werden können, wird das Schema aufgrund potenzieller Mehrdeutigkeit zurückgewiesen.  
  
 Beachten Sie, dass ein Inhaltsmodell in der Lage sein muss, jede Instanz ohne Lookahead eindeutig zu überprüfen, damit es gültig ist. Betrachten Sie z. B. das folgende Inhaltsmodell:  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e2"/>  
           </xsd:sequence>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e3"/>  
           </xsd:sequence>  
       </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 Für ein Dokument wie z. B. `<root><e1/><e3/></root>`entspricht die Sequenz `<e1/><e3/>` eindeutig der zweiten Sequenz `<xsd:sequence>`. Da das `<xsd:element>` , dem `<e1/>` entspricht, jedoch nicht ohne Lookahead auf `<e3/>`ermittelt werden kann, verletzt das Inhaltsmodell die UPA-Einschränkungsregel.  
  
## <a name="finding-more-information"></a>Weitere Informationsquellen  
 Das folgende Dokument wird vom W3C (World Wide Web Consortium) veröffentlicht; es enthält die technische Beschreibung der UPA-Einschränkung:  
  
 "XML Schema Part 1: Structures Second Edition, W3C Proposed Edited Recommendation":  
  
-   Section 3.8.6: Constraints on Model Group Schema Components  
  
-   Appendix H: Analysis of the Unique Particle Attribution Constraint (non-normative)  
  
 Wenn Sie das Dokument anzeigen möchten, besuchen Sie [http://www.w3.org/TR/xmlschema-1](http://go.microsoft.com/fwlink/?linkid=48881).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
