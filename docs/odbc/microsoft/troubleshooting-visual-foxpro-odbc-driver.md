---
title: Problembehandlung (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea6c45c362047d45275b6895d58faafe0250d26f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Problembehandlung (Visual FoxPro-ODBC-Treiber)
In den folgenden Abschnitten wird erläutert, wie auf die Leistung verbessern und Lösung von Problemen, die bei der Verwendung der Visual FoxPro-ODBC-Treiber auftreten können.  
  
## <a name="accessing-parameterized-views"></a>Zugreifen auf parametrisierten Ansichten  
 Sie können keine parametrisierte Sichten in einer Visual FoxPro-Datenbank, die mit dem Treiber zugreifen. Eine parametrisierte Ansicht erstellt eine WHERE-Klausel in der Ansicht SQL **wählen** -Anweisung, die die Datensätze beschränkt heruntergeladen, auf die Datensätze, die die Bedingungen der WHERE-Klausel erstellt wird, verwenden für den Parameter bereitgestellten Wert entsprechen. Da der Treiber übergeben von Parametern an die Sicht nicht unterstützt, schlägt der Versuch für eine parametrisierte Ansicht mithilfe des Treibers fehl.  
  
 Der Wert des Parameters zur Laufzeit bereitgestellt oder programmgesteuert an die Ansicht übergeben werden.  
  
## <a name="accessing-remote-views"></a>Beim Zugriff auf Remote-Ansichten  
 Sie können nicht remote Sichten in einer Visual FoxPro-Datenbank, die mit dem Treiber zugreifen. Remote-Ansichten sind Ansichten, die nicht FoxPro Daten oder eine Kombination von FoxPro und nicht FoxPro-Daten zugreifen. Verwenden Sie für den Zugriff auf remote-Ansichten, Visual FoxPro.  
  
## <a name="deleting-records"></a>Löschen von Datensätzen  
 Können Sie die Einträge zum Löschen, die mit dem Treiber markieren, aber Sie können nicht Einträge dauerhaft aus der Datenbank entfernen. Verwenden Sie Visual FoxPro, um Einträge dauerhaft aus einer Tabelle zu entfernen.  
  
## <a name="increasing-performance-using-background-fetching"></a>Erhöhen der Leistung mit Hintergrund abrufen  
 Sie können Leistung in großen Abrufvorgängen verbessern, indem Sie den Hintergrund des Treibers Funktion abrufen. Abrufen der Hintergrund verwendet einen eigenen Thread zum Abrufen von Daten aus einer bestimmten Datenquelle angefordert.  
  
 Sie können Hintergrund Abrufen von Zeilen für eine Datenquelle in einem der folgenden Methoden verwenden:  
  
-   Überprüfen Sie die **Abrufen von Daten im Hintergrund** Kontrollkästchen auf der [ODBC Visual FoxPro einrichten (Dialogfeld)](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Verwenden Sie das BackgroundFetch-Attribut-Schlüsselwort in der Verbindungszeichenfolge.  
  
 Weitere Informationen zu Schlüsselwörtern für Verbindungszeichenfolgen-Attribut, finden Sie unter [Verbindungszeichenfolgen verwenden](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Aktualisieren von Sichten mit mehreren Ebenen  
 Eine Sicht mit mehreren Ebenen ist eine Ansicht auf Basis einer oder mehreren Ansichten anstelle einer Basistabelle. Bei der Aktualisierung von Daten in einer Ansicht mit mehreren Ebenen ausfallen die Updates nur eine Ebene auf die Sicht, auf der die Ansicht der obersten Ebene basiert; Basistabellen werden nicht aktualisiert.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Mithilfe der Datendefinitionssprache (DDL) in gespeicherten Prozeduren  
 DDL, z. B. CREATE TABLE oder ALTER TABLE kann nicht in der Visual FoxPro-gespeicherten Prozeduren verwendet werden.  
  
 Informationen zur Sprache, die in gespeicherten Prozeduren verwendet werden können, finden Sie unter [Unterstützung für Regeln, Trigger, Standardwerte und gespeicherte Prozeduren](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Positionierte Updates verwenden  
 Der Treiber unterstützt keine positionierten Updates. Verwenden Sie die SQL-WHERE-Klausel, um die Zeilen zu identifizieren, die Sie aktualisieren möchten.  
  
## <a name="using-the-set-ansi-command"></a>Mithilfe der SET ANSI-Befehl  
 Wenn Sie ein Visual FoxPro-Entwickler sind, sollten Sie bewusst sein, dass die Standardeinstellung für SET ANSI auf für den Treiber, im Gegensatz zu einem Standardwert von OFF für Visual FoxPro ON festgelegt ist. Die Standard-Einstellung für SET ANSI ermöglicht Visual FoxPro-Datenquellen für andere ODBC-Datenquellen konsistentes Verhalten, die in der Regel genaue Vergleiche ausführen. Sie können die Standardeinstellung ändern. Weitere Informationen finden Sie unter [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
