---
title: Verwaltete SQLXML-Klassen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f2d79aae0c863030a478ed2e3859785d491be61
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sqlxml-40-net-framework-support---managed-classes"></a>SQLXML 4.0 .NET Framework-Unterstützung - verwaltete Klassen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 unterstützt Funktionen, die Ihnen ermöglichen, Schreiben Anwendungen Zugriff auf XML-Daten aus einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], schalten Sie die Daten in die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Umgebung, die Daten verarbeiten und Senden der Updates zu zurück[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 
  
  Verwaltete [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML-Klassen machen die Funktionalität von SQLXML 4.0 im [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework verfügbar. Mit verwalteten SQLXML-Klassen können Sie eine Anwendung in C# schreiben, um von einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz auf XML-Daten zuzugreifen, die Daten in die .NET Framework-Umgebung einzubinden, die Daten zu verarbeiten und die Updates zur Anwendung als DiffGram an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zurückzusenden. Beim Anwenden von Updates auf eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbank, die verwaltete SQLXML-Klassen verwendet, müssen Sie ein Zuordnungsschema verwenden. Ein funktionierendes Beispiel finden Sie unter [zugreifen auf SQLXML-Funktionalität in der .NET-Umgebung](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 Um die verwalteten SQLXML-Klassen mit SQLXML 4.0 zu verwenden, müssen Sie Microsoft Visual Studio installieren.  
  
> [!NOTE]  
>  .NET Framework umfasst den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET-Datenanbieter. Mit diesem Anbieter kann von der .NET-Umgebung auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zugegriffen werden. Allerdings kann er nur herkömmliche SQL-Abfragen verarbeiten (d. h. Abfragen relationaler Datenbanken mit Ausnahme von FOR XML-Abfragen). Sie können weder XML-Vorlagen noch serverseitige XPath-Abfragen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausführen.  

 Informationen zum Zugreifen auf und Ändern von Daten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] innerhalb der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework sowie Informationen zur Verwendung von DiffGrams zum Aktualisieren von Daten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabellen finden Sie unter [zugreifen auf SQLXML-Funktionalität in der .NET-Umgebung](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
> [!NOTE]  
>  Sie können außerdem [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio-Anwendungen schreiben, um einen Massenladenvorgang für XML-Dokumente mit XML-Massenladen auszuführen. Weitere Informationen finden Sie unter [Ausführen von Massenladen von XML von Daten &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md). Sie müssen einen Verweis auf die XML-Massenladen-DLL (Xblkld4.dll) in der Anwendung hinzufügen. Dies ist eine COM-DLL, für das Visual Studio .NET die Wrapperbibliothek automatisch erstellt.  
  
  Dieser Abschnitt enthält Beispielanwendungen, die veranschaulichen, wie Sie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] verwalteten SQLXML-Klassen:  
 [Ausgeführte SQL-Abfragen &#40; Verwaltete SQLXML-Klassen &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)  
  [Ausführen von SQL-Abfragen mithilfe der „ExecuteXMLReader“-Methode](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)  
  [Die XML-Verarbeitung auf Clientseite &#40; Verwaltete SQLXML-Klassen &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/processing-xml-on-the-client-side-sqlxml-managed-classes.md)  
  [Ausführen von XPath-Abfragen &#40; Verwaltete SQLXML-Klassen &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)  
  [Ausführen von XPath-Abfragen mit Namespaces &#40; Verwaltete SQLXML-Klassen &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)  
  [Ausführen von Vorlagendateien mit der „CommandText“-Eigenschaft](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandtext-property.md)  
  [Ausführen von Vorlagendateien mit der „CommandStream“-Eigenschaft](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)  
  [Anwenden einer XSL-Transformation &#40; Verwaltete SQLXML-Klassen &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)  
  

  
  
