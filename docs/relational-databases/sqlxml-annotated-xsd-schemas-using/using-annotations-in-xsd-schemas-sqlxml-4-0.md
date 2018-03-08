---
title: Verwenden von Anmerkungen in XSD-Schemas (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c124bb466416e06768444ac7040c47a6267ae0d6
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>Verwenden von Anmerkungen in XSD-Schemas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
In [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 unterstützt die XSD-Schemasprache Anmerkungen auf ähnliche Weise wie die in der XDR-Schemasprache (XML-Data Reduced) eingeführten Anmerkungen. Es gibt weitere in XSD eingeführte Anmerkungen, die in XDR nicht unterstützt werden.  
  
 Diese Anmerkungen können innerhalb des XSD-Schemas verwendet werden, um Zuordnungen von XML zu relationalen Daten anzugeben. Dazu gehört die Zuordnung von Elementen und Attributen im XSD-Schema zu Tabellen (Sichten) und Spalten in den Datenbanken.  
  
 Wenn Sie die Anmerkungen nicht angeben, wird die Standardzuordnung vorgenommen. Standardmäßig wird ein XSD-Element mit einem komplexen Typ einem Tabellennamen (Sichtnamen) in der angegebenen Datenbank zugeordnet, und ein Element oder Attribut mit einem einfachen Typ wird der Spalte mit demselben Namen wie das Element oder Attribut zugeordnet.  
  
 Diese Anmerkungen können auch zur Angabe der hierarchischen Beziehungen in XML verwendet werden und somit die Beziehungen in der Datenbank darstellen, denn ein XSD-Schema ist nicht anderes als eine XML-Sicht relationaler Daten.  
  
 Dieser Abschnitt enthält Beschreibungen der Anmerkungen, die Sie mit XSD-Schemas verwenden können, sowie Anwendungsbeispiele.  
  
> [!NOTE]  
>  Alle Beispiele in diesem Abschnitt geben einfache Xpath-Abfragen für das mit Anmerkungen versehene XSD-Schema an, das in dem jeweiligen Beispiel beschrieben wird. Kenntnisse der XPath-Sprache werden vorausgesetzt.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [XSD-Anmerkungen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
 Enthält eine Liste der Anmerkungen, die Sie mit XSD-Schemas verwenden können, ihre Beschreibungen und die entsprechenden Anmerkungen für XDR.  
  
 [Standardzuordnung von XSD-Elementen und-Attributen zu Tabellen und Spalten &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 Erläutert die Standardzuordnung und enthält Beispiele für Tasks, die im Zusammenhang mit der Standardzuordnung stehen.  
  
 [Explizite Zuordnung von XSD-Elementen und-Attributen zu Tabellen und Spalten &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 Erklärt die explizite Zuordnung mit der **SQL: Relation** und **SQL: field** Anmerkungen, und stellt Beispiele bereit.  
  
 [Angeben von Beziehungen mithilfe von SQL: Relationship &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **SQL: Relationship** Anmerkung.  
  
 [Angeben des SQL: Inverse-Attribut für SQL: Relationship &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 Beschreibt die **SQL: inverse** Anmerkung.  
  
 [Erstellen von konstanter Elemente mithilfe von Sql: ist Konstante &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **Sql: ist Konstante** Anmerkung.  
  
 [Ausschließen von Schemaelementen aus der resultierenden XML-Dokument mit Sql: zugeordnet &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 Beschreibt und enthält Beispiele für die **Sql: zugeordnet** Anmerkung.  
  
 [Filtern von Werten mithilfe von ' SQL: Limit-Feld und ' SQL: Limit-Value &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **' SQL: Limit-Feld** und **' SQL: Limit-Wert** Anmerkungen.  
  
 [Identifizieren von Schlüsselspalten mithilfe von SQL: Key-Felder &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **SQL: Key-Felder** Anmerkung.  
  
 [Angeben eines Target Namespace mithilfe der TargetNamespace-Attribut &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **TargetNamespace** Attribut.  
  
 [Erstellen die gültige ID, IDREF und IDREFS-Typ-Attribute Sql:prefix &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **Sql:prefix** Anmerkung.  
  
 [Datentypumwandlungen und die SQL: DataType-Anmerkung &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **SQL: DataType** Anmerkung.  
  
 [Zuordnen von XSD-Datentypen zu XPath-Datentypen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)  
 Enthält eine Tabelle, in der die Datentypen XSD, XDR und Xpath verglichen werden, und listet die relevanten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konvertierungen auf.  
  
 [Erstellen von CDATA-Abschnitten mithilfe von SQL: use-Cdata &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **SQL: Use-Daten** Anmerkung.  
  
 [Anfordern von URL-Verweise auf BLOB-Daten mithilfe von Sql: Codieren &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **Sql: Codieren** Anmerkung.  
  
 [Abrufen von nicht verbrauchten Daten mithilfe der SQL: Overflow-Feld &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)  
 Beschreibt und enthält Beispiele für die **Overflow-Feld** Anmerkung.  
  
 [Ausblenden von Elementen und Attributen mit sql:hide](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)  
 Beschreibt und enthält Beispiele für die **SQL: hide** Anmerkung.  
  
 [Verwenden der Anmerkungen 'sql:identity' und 'sql:guid'](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)  
 Beschreibt und enthält Beispiele für die **Sql:identity** und **Sql:guid** Anmerkungen.  
  
 [Angeben der Tiefe von rekursiven Beziehungen mit 'sql:max-depth'](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 Beschreibt und enthält Beispiele für die **Sql:max-Tiefe** Anmerkung.  
  
## <a name="see-also"></a>Siehe auch  
 [Überlegungen zur Sicherheit von Schemas mit Anmerkungen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
