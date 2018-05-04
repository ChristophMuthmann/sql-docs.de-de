---
title: XML-Datentypunterstützung für SQLXML 4.0 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 68cb00ced8f77b5921be07a3f6383d4436f0bade
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>XML-Datentypunterstützung für SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Beginnend mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt XML typisierte Daten mithilfe der **Xml** -Datentyp. Dieses Thema enthält Informationen wie SQLXML 4.0 Instanzen von erkennt die **Xml** -Datentyp und implementiert die Unterstützung für sie.  
  
## <a name="working-with-xml-data-types"></a>Arbeiten mit XML-Datentypen  
 Um zu verstehen, Weitere Informationen zum Arbeiten mit SQL-Tabellen, die implementieren **Xml** Daten Spalten vom Typ in den folgenden Beispielen werden bereitgestellt:  
  
|Task|Beispiel|Thema|  
|----------|-------------|-----------|  
|Das zuordnen und enthalten eine **Xml** Spalte in eine XML-Sicht|"Zuordnen eines XML-Elements zu einer XML-Datentypspalte"|[Standardzuordnung von XSD-Elementen und-Attributen zu Tabellen und Spalten &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Gewusst wie: Einfügen von Daten in eine **Xml** -Spalte mit Updategrams|"Einfügen von Daten in eine XML-Datentypspalte"|[Einfügen von Daten mit XML-Updategrams &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Massenladen von XML-Daten in eine **Xml** Spalte|"Massenladen in XML-Datentypspalten"|[Beispiele für XML-Massenladen & #40; SQLXML 4.0 & #41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Richtlinien und Einschränkungen  
  
-   **\<XSD: alle >** kann nicht zugeordnet werden, um eine Spalte z. B. eine **Xml** -Datentyp. Unterstützung in SQLXML für dieses Szenario über erfolgt die **Overflow-Feld** Anmerkung. Eine weitere Möglichkeit besteht, Zuordnen einer **Xml** Datentypfelds als Element eines **xsd: anyType**. Diese Problemumgehung wird im Beispiel "Zuordnen eines XML-Elements zu einer XML-Datentypspalte" gezeigt, auf das in der oben stehenden Tabelle verwiesen wird.  
  
-   XPath-Abfrage in den Inhalten von **Xml** datentypspalten wird nicht unterstützt.  
  
-   Mithilfe einer **Xml** -Datentypspalte in Anmerkungen, in denen es nicht unterstützt (z. B. **SQL: Relationship** und **SQL: Key-Felder**) oder zulässig sind, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Fehler, die von Komponenten der mittleren Ebene, die Implementierung von SQLXML 4.0 nicht aufgefangen werden. Der Grund dafür ist, dass SQLXML keine SQL-Typinformationen erfordert. Dieses Verhalten von SQLXML ist dem für andere Datentypen ähnlich, z. B. BLOB und binäre Typen.  
  
-   Zuordnen von **Xml** Spalten wird nur für XSD-Schemas unterstützt. XDR-Schemas unterstützen keine Zuordnung **Xml** Spalten.  
  
-   SQLXML 4.0 verlässt sich auf die Unterstützung für die XML-Analyse, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt wird. Ein **Xml** Spalte kann entweder als typisiertes XML oder nicht typisiertes XML zugeordnet werden. In beiden Fällen überprüft SQLXML 4.0 die XML-Eingabe nicht.  Wenn die XML-Eingabe nicht gültig oder nicht wohlgeformt ist, sendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Meldung an SQLXML und gibt alle relevanten, vom Server an den Benutzer gesendeten Fehlerinformationen weiter.  
  
-   SQLXML 4.0 basiert auf der eingeschränkten Unterstützung für DTDs, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht es einer internen DTD in **Xml** -datentypdaten, die zu verwendenden um Standardwerte bereitzustellen und um Entitätsverweise durch ihren erweiterten Inhalt zu ersetzen. SQLXML übergibt die XML-Daten unverändert an den Server (einschließlich der internen DTD). Mithilfe von Drittanbieter-Tools können Sie DTDs in XML-Schemadokumente (XSD) konvertieren und die Daten mit XML-Inlineschemas in die Datenbank laden.  
  
-   SQLXML 4.0 behält nicht verarbeitungsanweisungen für XML-Deklaration (z. B.) basierend auf dem Verhalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Stattdessen wird die XML-Deklaration als Direktive für behandelt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML-Parser und seine Attribute (Version, Codierung und eigenständige) verloren, nachdem die Daten konvertiert werden, um die **Xml** -Datentyp. Die XML-Daten werden intern als UCS-2 gespeichert. Alle anderen verarbeitungsanweisungen in der XML-Instanz werden beibehalten. Sie dürfen der **Xml** Spalte und können durch SQLXML unterstützt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
