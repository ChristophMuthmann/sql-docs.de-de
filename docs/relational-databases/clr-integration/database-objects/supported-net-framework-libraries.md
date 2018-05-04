---
title: Unterstützt die .NET Framework-Bibliotheken | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 24cd0f69a0167b5e742381b0e2e88f2cc84d1a2c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="supported-net-framework-libraries"></a>Unterstützte .NET Framework-Bibliotheken
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mit in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gehosteter CLR (Common Language Runtime) können Sie gespeicherte Prozeduren, Trigger, benutzerdefinierte Funktionen, benutzerdefinierte Typen (User-Defined Types, UDT) und benutzerdefinierte Aggregate in verwaltetem Code erstellen. Mit den in den Bibliotheken der .NET Framework-Klasse verfügbaren Funktionen haben Sie Zugriff auf vorgefertigte Klassen, die Funktionen u. a. zur Zeichenfolgenbearbeitung, für erweiterte mathematische Vorgänge, den Dateizugriff und die Kryptografie bereitstellen. Auf diese Klassen können Sie von jeder verwalteten gespeicherten Prozedur, jedem benutzerdefinierten Typ, jedem Trigger, jeder benutzerdefinierten Funktion oder jedem benutzerdefinierten Aggregat aus zugreifen.  
  
> [!NOTE]  
>  Wenn Sie nicht unterstützte Assemblys im globalen Assemblycache (GAC) warten oder aktualisieren, funktioniert die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anwendung möglicherweise nicht mehr. Dies ist darauf zurückzuführen, dass durch das Warten oder Aktualisieren von Bibliotheken im GAC die entsprechenden Assemblys in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht aktualisiert werden. Wenn eine Assembly sowohl in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbank als auch im GAC vorhanden ist, müssen die beiden Kopien der Assembly genau übereinstimmen. Stimmen sie nicht überein, tritt ein Fehler auf, wenn die Assembly von der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR-Integration verwendet wird. Wenn Sie warten oder aktualisieren alle Assemblys im GAC, die auch in der Datenbank, einschließlich der nicht unterstützte .NET Framework-Assemblys registriert werden müssen Sie auch warten oder aktualisieren die Kopie der Assembly in Ihre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] von Datenbanken mit der  **ALTER ASSEMBLY** Anweisung. Weitere Informationen finden Sie unter [Knowledge Base-Artikel 949080](http://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Unterstützte Bibliotheken  
 Ab [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] verfügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] über eine Liste mit unterstützten .NET Framework-Bibliotheken, die auf Zuverlässigkeits- und Sicherheitsstandards zur Interaktion mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] getestet wurden. Unterstützte Bibliotheken müssen auf dem Server nicht explizit registriert werden, bevor sie in Ihrem Code verwendet werden können. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] lädt sie direkt in den globalen Assemblycache (Global Assembly Cache oder GAC).  
  
 Folgende Bibliotheken/Namespaces werden von der CLR-Integration in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt:  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   System  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>Nicht unterstützte Bibliotheken  
 Nicht unterstützte Bibliotheken können Sie nach wie vor von Ihren verwalteten gespeicherten Prozeduren, Triggern, benutzerdefinierten Funktionen, benutzerdefinierten Typen (User-Defined Types, UDT) und benutzerdefinierten Aggregaten aus aufrufen. Die nicht unterstützte Bibliotheken muss zunächst registriert werden, der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank mit der **CREATE ASSEMBLY** -Anweisung, bevor es in Ihrem Code verwendet werden kann. Alle nicht unterstützten Bibliotheken, die registriert und auf dem Server ausgeführt werden, sollten überprüft und auf Sicherheit und Zuverlässigkeit getestet werden.  
  
 Z. B. die **System.DirectoryServices** Namespace wird nicht unterstützt. Sie müssen die System.DirectoryServices.dll-Assembly mit registrieren **UNSAFE** Berechtigungen, bevor Sie sie aus dem Code aufrufen können. Die **UNSAFE** Berichtigung ist notwendig da Klassen in der **System.DirectoryServices** Namespace entsprechen nicht die Anforderungen für **sichere** oder  **EXTERNAL_ACCESS**. Weitere Informationen finden Sie unter [CLR Integration Programming Model Einschränkungen](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) und [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR-Integration: Beschränkungen des Programmiermodells](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
