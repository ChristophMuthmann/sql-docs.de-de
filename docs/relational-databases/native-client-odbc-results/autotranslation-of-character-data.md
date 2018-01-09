---
title: "Automatische Übersetzung der Zeichendaten | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 566e248ce15929f8ff599602e920544df395a453
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="autotranslation-of-character-data"></a>Automatische Übersetzung der Zeichendaten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Zeichendaten, wie z. B. ANSI Zeichen mit SQL_C_CHAR deklarierte Variablen oder in gespeicherten Daten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der **Char**, **Varchar**, oder **Text** -Datentypen können Stellen Sie nur eine begrenzte Anzahl von Zeichen dar. Mit einem Byte pro Zeichen gespeicherte Zeichendaten können nur 256 Zeichen darstellen. Die in SQL_C_CHAR-Variablen gespeicherten Werte werden mithilfe der ANSI-Codepage (ACP) auf dem Clientcomputer interpretiert. Gespeicherte Werte **Char**, **Varchar**, oder **Text** Datentypen auf dem Server ausgewertet werden, mithilfe der ACP des Servers.  
  
 Wenn sowohl die Server-als auch die über die gleiche ACP, sie haben keine Probleme bei der Interpretation der in SQL_C_CHAR, gespeicherten Werte **Char**, **Varchar**, oder **Text** Objekte. Wenn der Server und der Client über unterschiedliche ACP verfügen, SQL_C_CHAR-Daten vom Client können als ein anderes Zeichen auf dem Server interpretiert werden, wenn er in dient **Char**, **Varchar**, oder **Text** Spalten, Variablen oder Parametern. Beispielsweise ein Zeichenbyte mit dem Wert 0xA5 wird als das Zeichen Ñ auf einem Computer mithilfe von Codepage 437 interpretiert und wird als Yen-Zeichen (¥) auf einem Computer mit der Codepage 1252 interpretiert.  
  
 Unicode-Daten werden mit zwei Bytes pro Zeichen gespeichert. Alle erweiterten Zeichen werden von der Unicode-Spezifikation abgedeckt, weshalb alle Unicode-Zeichen von allen Computern einheitlich interpretiert werden.  
  
 Die Funktion "autotranslate" angibt, der die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber versucht, die Probleme bei der Umstellung von Zeichendaten zwischen einem Client und einem Server zu minimieren, die unterschiedliche Codepages auf. "Autotranslate" kann festgelegt werden, in der Verbindungszeichenfolge von [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md), in der Konfigurationszeichenfolge von [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md), oder beim Konfigurieren von Datenquellen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-ODBC Treiber, die mit dem ODBC-Administrator.  
  
 Wenn "autotranslate" auf "Nein" festgelegt ist, werden keine Konvertierungen ausgeführt, auf Daten, die zwischen SQL_C_CHAR-Variablen, auf dem Client verschoben und **Char**, **Varchar**, oder **Text** Spalten, Variablen oder Parameter in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank. Die Bitmuster werden auf dem Client- und dem Servercomputer möglicherweise unterschiedlich interpretiert, wenn die Daten erweiterte Zeichen enthalten und die beiden Computer unterschiedliche Codepages verwenden. Die Daten werden einheitlich interpretiert, wenn beide Computer die gleiche Codepage verwenden.  
  
 Wenn "autotranslate" festgelegt ist, auf "yes", die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber Unicode verwendet, um Daten zwischen SQL_C_CHAR-Variablen, auf dem Client verschoben zu konvertieren und **Char**, **Varchar**, oder **Text** Spalten, Variablen oder Parameter in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank:  
  
-   Wenn Daten von einer SQL_C_CHAR-Variable auf dem Client gesendet werden eine **Char**, **Varchar**, oder **Text** Spalte, Variable oder Parameter in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die ODBC-Datenbank Treiber konvertiert zuerst von SQL_C_CHAR in Unicode mithilfe der ACP des Clients, klicken Sie dann aus Unicode wieder in Zeichen, die mithilfe der ACP des Servers.  
  
-   Beim Senden von einem **Char**, **Varchar**, oder **Text** Spalte, Variable oder Parameter in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank an eine SQL_C_CHAR-Variable auf dem Client, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber konvertiert zuerst von Zeichen in Unicode mithilfe der ACP des Servers, klicken Sie dann im Unicode SQL_C_CHAR, mithilfe der ACP des Clients an.  
  
 Da alle diese Konvertierungen, indem erfolgen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber auf dem Client, der Server-ACP Ausführen eines auf dem Clientcomputer installierten Codepages sein muss.  
  
 Indem die Zeichenkonvertierung über Unicode durchgeführt wird, ist sichergestellt, dass alle Zeichen, die auf beiden Codepages enthalten sind, korrekt konvertiert werden. Wenn ein Zeichen jedoch nur auf einer der beiden Codepages aufgeführt ist, kann es auf der Zielcodepage nicht dargestellt werden. Zum Beispiel umfasst die Codepage 1252 das Symbol für eingetragene Marken (®), während das Symbol auf der Codepage 437 nicht enthalten ist.  
  
 Die AutoTranslate-Einstellung wirkt sich auf die folgenden Konvertierungen nicht aus:  
  
-   Verschieben von Daten zwischen SQL_C_CHAR-Clientvariablen Zeichen und Unicode- **Nchar**, **Nvarchar**, oder **Ntext** Spalten, Variablen oder Parameter in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbanken.  
  
-   Verschieben von Daten zwischen Unicode SQL_C_WCHAR-Clientvariablen und Zeichen **Char**, **Varchar**, oder **Text** Spalten, Variablen oder Parameter in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbanken.  
  
 Daten müssen immer konvertiert werden, wenn sie vom Zeichenformat in Unicode übertragen werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verarbeitens von Ergebnissen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
