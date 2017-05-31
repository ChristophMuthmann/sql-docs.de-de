---
title: Importieren von Massendaten mithilfe von BULK INSERT oder OPENROWSET(BULK...) (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BULK INSERT statement, importing data from a remote data file
- bulk importing [SQL Server], methods
- bulk exporting [SQL Server], methods
- OPENROWSET function, BULK INSERT
- bulk importing [SQL Server], security
- bulk rowset providers [SQL Server]
- bulk exporting [SQL Server], BULK INSERT statement
- remote data access [SQL Server], bulk importing
- bulk importing [SQL Server], BULK INSERT statement
- Transact-SQL bulk export/import operations
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3abb7e7f582c7699b128d8b9d70b4aec34041424
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="import-bulk-data-by-using-bulk-insert-or-openrowsetbulk-sql-server"></a>Importieren von Massendaten mithilfe von BULK INSERT oder OPENROWSET(BULK...) (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  In diesem Thema erhalten Sie einen Überblick über die Verwendung der [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT-Anweisung und der INSERT...SELECT * FROM OPENROWSET(BULK...)-Anweisung, mit denen ein Massenimport von Daten aus einer Datendatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle ermöglicht wird. In diesem Thema werden zudem Sicherheitsaspekte beim Verwenden von BULK INSERT und OPENROWSET(BULK…) beschrieben, und mithilfe dieser Methoden wird ein Massenimport aus einer Remotedatenquelle ausgeführt.  
  
> **HINWEIS:** Für die Verwendung von BULK INSERT oder OPENROWSET(BULK…) ist es wichtig, nachvollziehen zu können, wie Identitätswechsel von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen verarbeitet werden. Weitere Informationen finden Sie unter "Sicherheitsüberlegungen" weiter unten in diesem Thema.  
  
## <a name="bulk-insert-statement"></a>BULK INSERT-Anweisung  
 BULK INSERT lädt Daten aus einer Datendatei in eine Tabelle. Die Funktionalität ähnelt derjenigen der Option **in** des **bcp** -Befehls. Die Datendatei wird jedoch vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess gelesen. Eine Beschreibung der BULK INSERT-Syntax finden Sie unter [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## <a name="bulk-insert-examples"></a>BULK INSERT-Beispiele  
 
  
-   [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
-   [Beispiele für den Massenimport und -export von XML-Dokumenten &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Beibehalten von Identitätswerten beim Massenimport von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Überspringen einer Tabellenspalte mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="openrowsetbulk-function"></a>OPENROWSET(BULK…)-Funktion  
 Auf den OPENROWSET-Massenrowsetanbieter wird durch Aufrufen der OPENROWSET-Funktion und Angeben der BULK-Option zugegriffen. Mithilfe der OPENROWSET(BULK…)-Funktion können Sie auf Remotedaten zugreifen, indem Sie über einen OLE DB-Anbieter eine Verbindung mit einer Remotedatenquelle (z. B. einer Datendatei) herstellen.  

**Gilt für:** `OPENROWSET` ist nicht verfügbar in [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].
  
 Für den Massenimport von Daten wird OPENROWSET(BULK…) aus der SELECT…FROM-Klausel einer INSERT-Anweisung aufgerufen. Die grundlegende Syntax für den Massenimport von Daten lautet:  
  
 INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
 Wenn OPENROWSET(BULK...) in einer INSERT-Anweisung verwendet wird, werden damit auch Tabellenhinweise unterstützt. Zusätzlich zu den regulären Tabellenhinweisen, z. B. TABLOCK, sind für die BULK-Klausel die folgenden speziellen Tabellenhinweise möglich: IGNORE_CONSTRAINTS (ignoriert nur die CHECK-Einschränkungen), IGNORE_TRIGGERS, KEEPDEFAULTS und KEEPIDENTITY. Weitere Informationen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Informationen zu den zusätzlichen Verwendungsmöglichkeiten der Option BULK finden Sie unter [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
## <a name="insertselect--from-openrowsetbulk-statements---examples"></a>INSERT...SELECT * FROM OPENROWSET(BULK...)-Anweisungen – Beispiele:
  
-   [Beispiele für den Massenimport und -export von XML-Dokumenten &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Beibehalten von Identitätswerten beim Massenimport von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Überspringen einer Tabellenspalte mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Auslassen eines Datenfelds mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="security-considerations"></a>Überlegungen zur Sicherheit  
 Wenn ein Benutzer einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen verwendet, wird das Sicherheitsprofil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozesskontos verwendet. Ein Anmeldename, für den die SQL Server-Authentifizierung verwendet wird, kann nicht außerhalb des Datenbankmoduls authentifiziert werden. Wenn ein BULK INSERT-Befehl durch einen Anmeldenamen initiiert wird, der die SQL Server-Authentifizierung verwendet, wird die Datenverbindung folglich mithilfe des Sicherheitskontexts des SQL Server-Prozesskontos (dem vom SQL Server-Datenbankmoduldienst verwendeten Konto) hergestellt. 
 
 Um die Quelldaten lesen zu können, müssen Sie dem vom SQL Server-Datenbankmodul verwendeten Konto Zugriff auf die Quelldaten gewähren. Wenn sich hingegen ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzer mithilfe der Windows-Authentifizierung anmeldet, können von diesem Benutzer nur die Dateien gelesen werden, auf die über das Benutzerkonto zugegriffen werden kann. Das Sicherheitsprofil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozesses wird dabei nicht berücksichtigt.  
  
 Angenommen, ein Benutzer hat sich mithilfe der Windows-Authentifizierung an einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angemeldet. Damit der Benutzer zum Importieren von Daten aus einer Datendatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle BULK INSERT oder OPENROWSET verwenden kann, muss das Konto über Lesezugriff für die Datendatei verfügen. Durch den Zugriff auf die Datendatei kann der Benutzer Daten aus der Datei in eine Tabelle importieren, selbst wenn für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess keine Berechtigung zum Zugreifen auf die Datei verfügbar ist. Der Benutzer muss dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess keine Dateizugriffsberechtigung erteilen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows können so konfiguriert werden, dass von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz eine Verbindung mit einer anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz hergestellt wird, indem die Anmeldeinformationen eines authentifizierten Windows-Benutzers weitergeleitet werden. Diese Anordnung wird als *Identitätswechsel* oder *Delegierung*bezeichnet. Es ist wichtig zu wissen, wie in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version die Sicherheit für den Benutzeridentitätswechsel verarbeitet wird, wenn Sie BULK INSERT oder OPENROWSET verwenden. Durch einen Benutzeridentitätswechsel kann sich die Datendatei auf einem anderen Computer befinden als der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess oder der Benutzer selbst. Wenn beispielsweise ein Benutzer auf **Computer_A** Zugriff auf eine Datendatei hat, die sich auf **Computer_B**befindet, und die Delegierung der Anmeldeinformationen entsprechend festgelegt ist, kann der Benutzer eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz herstellen, die auf **Computer_C**ausgeführt wird, auf die Datendatei auf **Computer_B**zugreifen und einen Massenimport von Daten aus der Datei in eine Tabelle auf **Computer_C**ausführen.  
  
## <a name="bulk-importing-from-a-remote-data-file"></a>Massenimport aus einer Remotedatendatei  
 Die Datendatei muss zwischen zwei Computern freigegeben sein, um mithilfe von BULK INSERT oder INSERT...SELECT \* FROM OPENROWSET(BULK...) den Massenimport von Daten von einem Computer zum anderen auszuführen. Verwenden Sie zum Angeben einer freigegebenen Datendatei den UNC-Namen (Universal Naming Convention) im allgemeinen Format **\\\\***Servername***\\***Freigabename***\\***Pfad***\\***Dateiname*. Zudem muss das Konto, mit dem auf die Datendatei zugegriffen wird, über die Berechtigungen verfügen, die zum Lesen der Datei auf dem Remotedatenträger erforderlich sind.  
  
 Beispielsweise wird mithilfe der folgenden `BULK INSERT` -Anweisung ein Massenimport von Daten aus der Datendatei `SalesOrderDetail` in die `AdventureWorks` -Tabelle der `newdata.txt`-Datenbank ausgeführt. Diese Datendatei befindet sich im freigegebenen Ordner `\dailyorders` auf dem `salesforce` -Netzwerkfreigabeverzeichnis des `computer2`-Systems.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';  
GO  
```  
  
> **HINWEIS:** Diese Einschränkung gilt nicht für das Hilfsprogramm **bcp** , da die Datei vom Client unabhängig von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gelesen wird.  
  
## <a name="see-also"></a>Siehe auch  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  

