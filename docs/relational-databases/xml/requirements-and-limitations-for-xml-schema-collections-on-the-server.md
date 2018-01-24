---
title: "Anforderungen und Einschränkungen für XML-Schemasammlungen auf dem Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
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
- identifiers [XML schema collections]
- XML schema collections [SQL Server], limitations
- substitution groups [XML in SQL Server]
- XML schema collections [SQL Server], guidelines
- lax validation
- enumeration facets [XML in SQL Server]
- decimal precision [XML in SQL Server]
- repeated XML schema collection values
- schema collections [SQL Server], limitations
- time zones [XML in SQL Server]
- precision decimals [XML in SQL Server]
- schema collections [SQL Server], guidelines
- lexical representation
ms.assetid: c2314fd5-4c6d-40cb-a128-07e532b40946
caps.latest.revision: "84"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d12b4ae5ef18aadaf580945f5326dc08f00c11ac
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="requirements-and-limitations-for-xml-schema-collections-on-the-server"></a>Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Die Überprüfung mit der XML-Schemadefinitionssprache (XSD) weist einige Einschränkungen für SQL-Spalten auf, die den **xml**-Datentyp verwenden. Die folgende Tabelle liefert Einzelheiten zu diesen Einschränkungen und stellt außerdem Richtlinien zum Ändern des XSD-Schemas für die Verwendung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bereit. Die Themen in diesem Abschnitt enthalten zusätzliche Informationen über bestimmte Einschränkungen sowie eine Anleitung zur Arbeit mit ihnen.  
  
|Element|Einschränkung|  
|----------|----------------|  
|**minOccurs** und **maxOccurs**|Die Werte für **minOccurs** - und **maxOccurs** -Attribute müssen in ganze 4-Byte-Zahlen passen. Schemas, die diese Bedingung nicht erfüllen, werden vom Server zurückgewiesen.|  
|**\<xsd:choice>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weist Schemas zurück, die einen **\<xsd:choice>**-Partikel ohne untergeordnete Elemente besitzen, es sei denn, der Partikel ist mit einem **minOccurs**-Attributwert von Null definiert.|  
|**\<xsd:include>**|Zurzeit unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dieses Element nicht. XML-Schemas, die dieses Element enthalten, werden vom Server zurückgewiesen.<br /><br /> Als Lösung können XML-Schemas, die die **\<<xsd:include>**-Direktive enthalten, so vorverarbeitet werden, dass die Inhalte aller enthaltenen Schemas kopiert und in einem einzigen Schema für den Upload auf den Server zusammengeführt werden. Weitere Informationen finden Sie unter [Vorverarbeiten eines Schemas zum Zusammenführen eingeschlossener Schemas](../../relational-databases/xml/preprocess-a-schema-to-merge-included-schemas.md).|  
|**\<xsd:key>**,  **\<xsd: keyref>** und **\<xsd: unique>**|Zurzeit unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diese XSD-basierten Einschränkungen zum Erzwingen der Eindeutigkeit oder zum Einrichten von Schlüsseln oder Schlüsselverweisen nicht. XML-Schemas, die diese Elemente enthalten, können nicht registriert werden.|  
|**\<xsd:redefine>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dieses Element nicht. Informationen über eine andere Möglichkeit, Schemas zu aktualisieren, finden Sie unter [Das &#60;xsd:redefine&#62;-Element](../../relational-databases/xml/the-xsd-redefine-element.md)bereit.|  
|**\<xsd:simpleType>**-Werte|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt nur Millisekundengenauigkeit für simple-Datentypen, die Sekundenkomponenten besitzen – mit Ausnahme von **xs:time** und **xs:dateTime**–, sowie eine Genauigkeit von 100 Nanosekunden für **xs:time** und **xs:dateTime**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] legt Einschränkungen für alle erkannten XSD-Enumerationen des einfachen Typs fest.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt nicht den „NaN“-Wert in **\<xsd:simpleType>**-Deklarationen.<br /><br /> Weitere Informationen finden Sie unter[Werte für &#60;xsd:simpleType&#62;-Deklarationen](../../relational-databases/xml/values-for-xsd-simpletype-declarations.md)bereit.|  
|**xsi:schemaLocation** und **xsi:noNamespaceSchemaLocation**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignoriert diese Attribute, wenn sie in den XML-Instanzdaten vorhanden sind, die in eine Spalte oder Variable des **xml** -Datentyps eingefügt werden.|  
|**xs:QName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt keine von **xs:QName** abgeleiteten Typen, die ein Beschränkungselement des XML-Schemas verwenden.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt keine union-Typen, die **xs:QName** als Memberelement besitzen.<br /><br /> Weitere Informationen finden Sie unter [Der xs:QName-Typ](../../relational-databases/xml/the-xs-qname-type.md).|  
|Hinzufügen von Elementen zu einer vorhandenen Ersetzungsgruppe|Das Hinzufügen von Elementen zu einer vorhandenen Ersetzungsgruppe in einer XML-Schemaauflistung wird nicht unterstützt. Eine Ersetzungsgruppe in einem XML-Schema ist insofern eingeschränkt, als das Headelement und alle seine Memberelemente in der gleichen {CREATE &#124; ALTER} XML SCHEMA COLLECTION-Anweisung definiert werden müssen.|  
|Kanonische Formen und Musterbeschränkungen|Die kanonische Darstellung eines Werts darf die Musterbeschränkung für seinen Typ nicht verletzen. Weitere Informationen finden Sie unter [Kanonische Formen und Musterbeschränkungen](../../relational-databases/xml/canonical-forms-and-pattern-restrictions.md).|  
|Enumerationsfacets|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt keine XML-Schemas mit Typen, die Musterfacets besitzen, oder Enumerationen, die diese Facets verletzen.|  
|Facetlänge|Die Facets **length**, **minLength**und **maxLength** werden als **long** -Datentyp gespeichert. Dieser Datentyp ist ein 32-Bit-Typ. Der Bereich der zulässigen Werte ist daher 2^31.|  
|ID-Attribut|Jede XML-Schemakomponente kann über ein ID-Attribut verfügen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erzwingt die Eindeutigkeit für **\<xsd:attribute>**-Deklarationen des **ID**-Typs, speichert die Werte aber nicht. Der Bereich für das Erzwingen der Eindeutigkeit wird durch die {CREATE &#124; ALTER} XML SCHEMA COLLECTION-Anweisung festgelegt.|  
|ID-Datentyp|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt keine Elemente vom Typ **xs:ID**, **xs:IDREF**oder **xs:IDREFS**. Ein Schema darf keine Elemente dieses Typs oder durch Beschränkung oder Erweiterung von diesem Typ abgeleitete Elemente deklarieren.|  
|Lokaler Namespace|Der lokale Namespace muss für das **\<xsd:any>**-Element explizit angegeben werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwirft Schemas, die eine leere Zeichenfolge ("") als Wert für das Namespace-Attribut verwenden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verlangt die ausdrückliche Verwendung von "##local" für die Angabe, dass ein nicht qualifiziertes Element oder Attribut als Instanz des Platzhalterzeichens verwendet wird.|  
|Mixed-Datentyp und simple-Inhalt|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt das Beschränken eines mixed-Datentyps auf simple-Inhalt nicht. Weitere Informationen finden Sie unter [Mixed-Datentyp und simple-Inhalt](../../relational-databases/xml/mixed-type-and-simple-content.md).|  
|NOTATION-Datentyp|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt den NOTATION-Datentyp nicht.|  
|Bedingungen des Typs Nicht genügend Arbeitsspeicher|Wenn Sie mit großen XML-Schemaauflistungen arbeiten, kann es vorkommen, dass nicht genügend Arbeitsspeicher verfügbar ist. Lösungen für dieses Problem finden Sie unter [Große XML-Schemasammlungen und Bedingungen des Typs „Nicht genügend Arbeitsspeicher“](../../relational-databases/xml/large-xml-schema-collections-and-out-of-memory-conditions.md).|  
|Wiederholte Werte|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weist Schemas zurück, in denen das block- oder final-Attribut wiederholte Werte aufweist, z.B. „restriction restriction“ oder „extension extension“.|  
|Schemakomponentenbezeichner|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beschränkt Bezeichner von Schemakomponenten auf eine maximale Länge von 1000 Unicode-Zeichen. Außerdem werden keine Ersatzzeichenpaare mit Bezeichnern unterstützt.|  
|Zeitzoneninformationen|In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen werden Zeitzoneninformationen für **xs:date**-, **xs:time**- und **xs:dateTime** -Werte zur XML-Schemaüberprüfung voll unterstützt. Im [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Abwärtskompatibilitätsmodus werden Zeitzoneninformationen immer zu koordinierter Weltzeit (Greenwich Mean Time) normalisiert. Für Elemente des **dateTime** -Datentyps konvertiert der Server die bereitgestellte Zeit mithilfe des Offsetwerts (-05:00) in GMT und gibt die entsprechende GMT-Zeit zurück.|  
|Union-Datentypen|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt keine Einschränkungen aus union-Datentypen.|  
|Variable Genauigkeitsdezimalwerte|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt keine variablen Genauigkeitsdezimalwerte. Der **xs:decimal** -Datentyp stellt Dezimalzahlen mit variabler Genauigkeit dar. Für minimal konforme XML-Prozessoren müssen Dezimalzahlen mit mindestens `totalDigits=18`unterstützt werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt `totalDigits=38,` , die Dezimalstellen sind jedoch auf 10 beschränkt. Alle durch **xs:decimal** instanziierten Werte werden intern durch den Server mithilfe des SQL-Datentyps „numeric (38, 10)“ dargestellt.|  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Canonical Forms and Pattern Restrictions](../../relational-databases/xml/canonical-forms-and-pattern-restrictions.md)|Beschreibt kanonische Formen und Musterbeschränkungen.|  
|[Platzhalterkomponenten und Inhaltsüberprüfung](../../relational-databases/xml/wildcard-components-and-content-validation.md)|Beschreibt die Einschränkungen bei der Verwendung von Platzhalterzeichen, lax-Überprüfung und anyType-Elementen mit XML-Schemaauflistungen.|  
|[Das &#60;xsd:redefine&#62;-Element](../../relational-databases/xml/the-xsd-redefine-element.md)|Erklärt die Einschränkung für die Verwendung des \<xsd:redefine>-Elements und beschreibt eine Problemumgehung.|  
|[Der xs:QName-Typ](../../relational-databases/xml/the-xs-qname-type.md)|Beschreibt die Einschränkung hinsichtlich des xs:QName-Typs.|  
|[Werte für &#60;xsd:simpleType&#62;-Deklarationen](../../relational-databases/xml/values-for-xsd-simpletype-declarations.md)|Beschreibt die Beschränkungen, die auf \<xsd:simpleType>-Deklarationen angewendet werden.|  
|[Enumeration Facets](../../relational-databases/xml/enumeration-facets.md)|Beschreibt die Einschränkung hinsichtlich der Enumerationsfacets.|  
|[Mixed Type and Simple Content](../../relational-databases/xml/mixed-type-and-simple-content.md)|Beschreibt die Einschränkung beim Beschränken eines gemischten Typs auf einfachen Inhalt.|  
|[Große XML-Schemasammlungen und Bedingungen des Typs „Nicht genügend Arbeitsspeicher“](../../relational-databases/xml/large-xml-schema-collections-and-out-of-memory-conditions.md)|Stellt Lösungen für Situationen bereit, in denen nicht genügend Arbeitsspeicher verfügbar ist, was gelegentlich bei großen Schemaauflistungen vorkommt.|  
|[Nicht deterministische Inhaltsmodelle](../../relational-databases/xml/non-deterministic-content-models.md)|Beschreibt die Einschränkungen hinsichtlich nicht deterministischer Inhaltsmodelle.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erteilen von Berechtigungen für eine XML-Schemaauflistung](../../relational-databases/xml/grant-permissions-on-an-xml-schema-collection.md)   
 [Einschränkung für eindeutige Partikelzuordnung](../../relational-databases/xml/unique-particle-attribution-constraint.md)   
 [XML-Schemasammlungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
