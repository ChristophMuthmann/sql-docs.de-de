---
title: Registrieren von benutzerdefinierten Typen in SQLServer | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs: TSQL
helpviewer_keywords:
- UDTs [CLR integration], maintaining
- user-defined types [CLR integration], maintaining
- dependencies [CLR integration]
- deploying user-defined types [CLR integration]
- CurrencyConversion function
- user-defined types [CLR integration], deploying
- Transact-SQL deploying UDTs
- assemblies [CLR integration], user-defined types
- cross-database UDT support
- CREATE ASSEMBLY statement
- DROP TYPE statement
- Currency UDT
- CREATE TYPE statement
- registering user-defined types
- UDTs [CLR integration], deploying
- removing user-defined types
- user-defined types [CLR integration], registering
- ALTER ASSEMBLY statement
- UDTs [CLR integration], registering
- ADD FILE clause
ms.assetid: f7da3e92-e407-4f0b-b3a3-f214e442b37d
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 788eeeb4acb1a2acc562f71dfe4d59a7f622192e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="registering-user-defined-types-in-sql-server"></a>Registrieren benutzerdefinierter Typen in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Um einen benutzerdefinierten Typ (UDT) in verwenden [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], müssen Sie ihn registrieren. Beim Registrieren eines UDT muss die Assembly registriert werden und der Typ in der Datenbank, in der er verwendet werden soll, erstellt werden. UDTs beschränken sich auf eine einzelne Datenbank und können nicht in mehreren Datenbanken verwendet werden, es sei denn die gleiche Assembly und der gleiche UDT wurden in jeder Datenbank registriert. Nachdem die UDT-Assembly registriert und der Typ erstellt wurden, können Sie den UDT in [!INCLUDE[tsql](../../includes/tsql-md.md)] und im Clientcode verwenden. Weitere Informationen finden Sie unter [Benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
## <a name="using-visual-studio-to-deploy-udts"></a>Verwenden von Visual Studio zum Bereitstellen von UDTs  
 Am einfachsten stellen Sie den UDT mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio bereit. Verwenden Sie jedoch bei komplexeren Bereitstellungsszenarios und für eine größere Flexibilität [!INCLUDE[tsql](../../includes/tsql-md.md)], wie nachfolgend in diesem Thema beschrieben.  
  
 Führen Sie die folgenden Schritte aus, um einen UDT mit Visual Studio zu erstellen und bereitzustellen:  
  
1.  Erstellen Sie ein neues **Datenbank** -Projekt in der **Visual Basic** oder **Visual C#-** -Sprachknoten.  
  
2.  Fügen Sie einen Verweis auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank hinzu, die den UDT enthalten wird.  
  
3.  Hinzufügen einer **User-Defined Type** Klasse.  
  
4.  Erstellen Sie den Code, um den UDT zu implementieren.  
  
5.  Aus der **erstellen** klicken Sie im Menü **bereitstellen**. Somit wird die Assembly registriert und der Typ in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank erstellt.  
  
## <a name="using-transact-sql-to-deploy-udts"></a>Verwenden von Transact-SQL zum Bereitstellen von UDTs  
 Mit der [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY-Syntax wird die Assembly in der Datenbank registriert, in der Sie den UDT verwenden möchten. Sie werden intern in Datenbanksystemtabellen gespeichert, nicht extern im Dateisystem. Wenn die UDTs von externen Assemblys abhängig sind, müssen sie auch in die Datenbank geladen werden. Mit der CREATE TYPE-Anweisung wird der UDT in der Datenbank erstellt, in der er verwendet werden soll. Weitere Informationen finden Sie unter [CREATE ASSEMBLY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-assembly-transact-sql.md) und [erstellen, geben Sie &#40; Transact-SQL &#41; ](../../t-sql/statements/create-type-transact-sql.md).  
  
### <a name="using-create-assembly"></a>Verwenden von CREATE ASSEMBLY  
 Mit der CREATE ASSEMBLY-Syntax wird die Assembly in der Datenbank registriert, in der Sie den UDT verwenden möchten. Sobald die Assembly registriert wurde, liegen keine Abhängigkeiten vor.  
  
 Das Erstellen mehrerer Versionen der gleichen Assembly in einer Datenbank ist nicht zulässig. Es ist jedoch möglich, mehrere Versionen der gleichen Assembly basierend auf der Kultur in einer bestimmten Datenbank zu erstellen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterscheidet verschiedene Kulturversionen einer Assembly anhand der Namen, die in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registriert wurden. Weitere Informationen finden Sie unter "Erstellen und Verwenden von Assemblys mit starkem Namen" im .NET Framework SDK.  
  
 Wenn CREATE ASSEMBLY mit dem SAFE- oder EXTERNAL_ACCESS-Berechtigungssatz ausgeführt wird, wird die Assembly überprüft, um sicherzustellen, dass sie überprüfbar und typsicher ist. Wenn Sie keinen Berechtigungssatz angeben, wird standardmäßig SAFE vorausgesetzt. Code mit dem UNSAFE-Berechtigungssatz wird nicht überprüft. Weitere Informationen zu assemblyberechtigungssätzen finden Sie unter [Entwerfen von Assemblys](../../relational-databases/clr-integration/assemblies-designing.md).  
  
#### <a name="example"></a>Beispiel  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung registriert die Point-Assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der **AdventureWorks** Datenbank mit dem SAFE-Berechtigungssatz. Wenn die WITH PERMISSION_SET-Klausel nicht angegeben wird, wird die Assembly mit dem SAFE-Berechtigungssatz registriert.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung registriert die Assembly mit *< Assembly_bits >* Argument in der FROM-Klausel. Dies **Varbinary** -Wert stellt die Datei als Datenstrom von Bytes.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 … 21ac78  
```  
  
### <a name="using-create-type"></a>Verwenden von CREATE TYPE  
 Nachdem die Assembly in die Datenbank geladen wurde, können Sie den Typ mit der [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE-Anweisung erstellen. Dadurch wird der Typ der Liste mit verfügbaren Typen für diese Datenbank hinzugefügt. Der Typ hat einen Datenbankbereich und kann nur in der Datenbank, in der er erstellt wurde, verwendet werden. Wenn der UDT bereits in der Datenbank vorhanden ist, schlägt die CREATE TYPE-Anweisung fehl.  
  
> [!NOTE]  
>  Die CREATE TYPE-Syntax dient außerdem zum Erstellen von systemeigenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Aliasdatentyp Datentypen, und ersetzen soll **Sp_addtype** als Mittel zum Erstellen von Aliasdatentypen. Einige der optionalen Argumente in der CREATE TYPE-Syntax beziehen sich auf das Erstellen von UDTs, sie gelten nicht für das Erstellen von Aliasdatentypen (z. B. Basistyp).  
  
 Weitere Informationen finden Sie unter [CREATE TYPE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-type-transact-sql.md).  
  
#### <a name="example"></a>Beispiel  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung erstellt die **Punkt** Typ. Der EXTERNAL NAME wird angegeben, mit der zweiteiligen Namensgebungssyntax *AssemblyName*. *UDTName*.  
  
```  
CREATE TYPE dbo.Point   
EXTERNAL NAME Point.[Point];  
```  
  
## <a name="removing-a-udt-from-the-database"></a>Entfernen eines UDTs aus der Datenbank  
 Mit der DROP TYPE-Anweisung wird ein UDT aus der aktuellen Datenbank entfernt. Sobald der UDT entfernt wurde, können Sie die Assembly mit der DROP ASSEMBLY-Anweisung aus der Datenbank löschen.  
  
 Die DROP TYPE-Anweisung wird nicht in den folgenden Situationen ausgeführt:  
  
-   Tabellen in der Datenbank, die mit dem UDT definierte Spalten enthalten.  
  
-   Funktionen, gespeicherte Prozeduren oder Trigger, die Variablen und Parameter des UDT verwenden und in der Datenbank mit der WITH SCHEMABINDING-Klausel erzeugt wurden.  
  
### <a name="example"></a>Beispiel  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] muss in der folgenden Reihenfolge ausgeführt werden. Zuerst die Tabelle verweist auf die **Punkt** UDT muss gelöscht werden, klicken Sie dann den Typ und zuletzt die Assembly.  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>Ermitteln von UDT-Abhängigkeiten  
 Wenn abhängige Objekte, z. B. Tabellen mit UDT-Spaltendefinitionen, vorliegen, schlägt die DROP TYPE-Anweisung fehl. Sie schlägt auch dann fehl, wenn sich in der Datenbank Funktionen, gespeicherte Prozeduren oder Trigger befinden, die mit der WITH SCHEMABINDING-Klausel erstellt wurden, wenn diese Routinen Variablen oder Parameter des benutzerdefinierten Typs verwenden. Sie müssen zuerst alle abhängigen Objekte löschen und dann die DROP TYPE-Anweisung ausführen.  
  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage sucht nach alle Spalten und Parameter, mit denen einen UDT in der **AdventureWorks** Datenbank.  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;  
```  
  
## <a name="maintaining-udts"></a>Verwalten von UDTs  
 Nachdem ein UDT in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank erstellt wurde, können Sie ihn nicht mehr ändern; Sie können jedoch die Assembly, auf der der Typ basiert, ändern. Meistens müssen Sie den UDT aus der Datenbank mit der [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP TYPE-Anweisung entfernen, Änderungen an der zugrunde liegenden Assembly vornehmen und sie dann mit der ALTER ASSEMBLY-Anweisung neu laden. Anschließend müssen der UDT und abhängige Objekte neu erstellt werden.  
  
### <a name="example"></a>Beispiel  
 Die ALTER ASSEMBLY-Anweisung wird erst verwendet, nachdem Sie Änderungen am Quellcode in der UDT-Anweisung vorgenommen und sie neu kompiliert haben. Die DLL-Datei wird auf den Server kopiert und dort zur neuen Assembly verbunden. Die vollständige Syntax finden Sie unter [ALTER ASSEMBLY &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-assembly-transact-sql.md).  
  
 Mit der folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY-Anweisung wird die Point.dll-Assembly erneut vom angegebenen Speicherort auf dem Datenträger geladen.  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>Verwenden von ALTER ASSEMBLY zum Hinzufügen von Quellcode  
 Die ADD FILE-Klausel in der ALTER ASSEMBLY-Syntax ist nicht in CREATE ASSEMBLY vorhanden. Sie können sie verwenden, um Quellcode oder beliebige andere Dateien hinzuzufügen, die einer Assembly zugeordnet sind. Die Dateien werden von ihren ursprünglichen Speicherorten kopiert und in Systemtabellen in der Datenbank gespeichert. Dadurch wird sichergestellt, dass stets der Quellcode oder andere Dateien verfügbar sind, wenn Sie die aktuelle Version des UDT neu erstellen oder dokumentieren müssen.  
  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY-Anweisung fügt der Point.cs-Klassenquellcode für den **Punkt** UDT. Dadurch wird der in der Datei Point.cs enthaltene Text kopiert und unter dem Namen "PointSource" in der Datenbank gespeichert.  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 Assemblyinformationen befindet sich in der **Sys. assembly_files** Tabelle in der Datenbank, in dem die Assembly installiert wurde. Die **Sys. assembly_files** Tabelle enthält die folgenden Spalten.  
  
 **assembly_id**  
 Der für die Assembly definierte Bezeichner. Diese Nummer wird allen Objekten mit Bezug auf dieselbe Assembly zugewiesen.  
  
 **name**  
 Der Name des Objekts.  
  
 **FILE_ID**  
 Eine Zahl, welche jedes Objekt, wobei das erste Objekt zugeordneten einer bestimmten **Assembly_id** wird der Wert 1 zugewiesen. Wenn mehrere mit dem verknüpften Objekte **Assembly_id**, wird jeder nachfolgende **File_id** -Wert um 1 erhöht.  
  
 **Inhalt**  
 Die Hexadezimaldarstellung der Assembly oder Datei.  
  
 Können Sie die CAST oder CONVERT-Funktion konvertiert den Inhalt der **Inhalt** -Spalte in lesbaren Text. Die folgende Abfrage konvertiert die Inhalte der Point.cs-Datei in lesbaren Text, wobei der Name in der WHERE-Klausel verwendet wird, um den Ergebnissatz auf eine einzelne Zeile zu beschränken.  
  
```  
SELECT CAST(content AS varchar(8000))   
  FROM sys.assembly_files   
  WHERE name='PointSource';  
```  
  
 Wenn Sie die Ergebnisse in einen Texteditor kopieren und einfügen, bleiben die Zeilenumbrüche und Leerstellen des Originals erhalten.  
  
## <a name="managing-udts-and-assemblies"></a>Verwalten von UDTs und Assemblys  
 Beim Planen der Implementierung von UDTs sollten Sie die Methoden berücksichtigen, die in der UDT-Assembly selbst benötigt werden und die in separaten Assemblys erstellt und als benutzerdefinierte Funktionen oder gespeicherte Prozeduren implementiert werden sollen. Durch das Trennen von Methoden in separate Assemblys können Sie Code ohne Auswirkungen auf die Daten, die in einer UDT-Spalte einer Tabelle gespeichert wurden, aktualisieren. Sie können die UDT-Assemblys nur ändern, ohne UDT-Spalten und andere abhängige Objekte zu löschen, wenn die neue Definition die vorherigen Werte lesen kann und sich die Signatur des Typs nicht ändert.  
  
 Die Trennung des Prozedurencodes, der sich vom Code zum Implementieren des UDT unterscheiden kann, vereinfacht den Verwaltungsaufwand. Wenn Sie nur Code einschließen, der für die Funktionsweise des UDT erforderlich ist, und die UDT-Definitionen so einfach wie möglich halten, können Sie das Risiko reduzieren, dass der UDT bei einer Codeüberarbeitung oder bei Fehlerbehebungen selbst aus der Datenbank gelöscht wird.  
  
### <a name="the-currency-udt-and-currency-conversion-function"></a>Der Currency-UDT und die Währungskonvertierungsfunktion  
 Die **Währung** UDT in der **AdventureWorks** Beispieldatenbank bietet ein gutes Beispiel für die empfohlene Methode, um die Struktur eines UDT und seiner zugeordneten Funktionen. Die **Währung** UDT für die Behandlung basierend auf dem Währungssystem einer bestimmten Kultur verwendet wird, und für die Speicherung von verschiedenen Currency-Typen, z. B. Dollar, Euro usw. ermöglicht. Die UDT-Klasse stellt einen Kulturnamen als Zeichenfolge und einen Geldbetrag als eine **decimal** -Datentyp. Alle notwendigen Serialisierungsmethoden sind in der Assembly enthalten, die die Klasse definiert. Die Funktion, die währungsumrechnung aus einer Kultur in eine andere wird als eine externe Funktion namens implementiert **ConvertCurrency**, und diese Funktion befindet sich in einer separaten Assembly. Die **ConvertCurrency** Funktion ihre Arbeit ausführt, durch das Abrufen von den Wechselkurs aus einer Tabelle in der **AdventureWorks** Datenbank. Wenn die Quelle der die Wechselkurse jemals ändern sollte oder wenn alle anderen Änderungen am vorhandenen Code festgelegt werden soll, die Assembly problemlos geändert werden, ohne Auswirkungen auf die **Währung** UDT.  
  
 Den Code für die **Währung** UDT und **ConvertCurrency** Funktionen finden Sie durch die common Language Runtime (CLR)-Beispiele installieren.  
  
### <a name="using-udts-across-databases"></a>Verwenden von UDTs über mehrere Datenbanken hinweg  
 UDTs sind definitionsgemäß auf eine einzelne Datenbank beschränkt. Aus diesem Grund kann ein UDT, der in einer Datenbank definiert wurde, nicht in einer Spaltendefinition in einer anderen Datenbank verwendet werden. Um UDTs in mehreren Datenbanken zu verwenden, müssen Sie die CREATE ASSEMBLY- und CREATE TYPE-Anweisungen in jeder Datenbank für identische Assemblys ausführen. Assemblys gelten als identisch, wenn die folgenden Werte gleich sind: Name, starker Name, Kultur, Version, Berechtigungssatz und binäre Inhalte.  
  
 Nachdem der UDT registriert wurde und der Zugriff darauf in beiden Datenbanken erfolgen kann, können Sie einen UDT-Wert aus einer Datenbank für die Verwendung in einer anderen Datenbank konvertieren. Identische UDTs können in den folgenden Szenarios über mehrere Datenbanken hinweg verwendet werden:  
  
-   Aufrufen einer gespeicherten Prozedur, die in anderen Datenbanken definiert ist.  
  
-   Abfragen von in anderen Datenbanken definierten Tabellen.  
  
-   Auswählen von UDT-Daten aus einer UDT-Spalte in einer Datenbanktabelle und Einfügen in eine zweite Datenbank mit einer identischen UDT-Spalte.  
  
 In diesen Szenarios findet die für den Server erforderliche Konvertierung automatisch statt. Sie können die Konvertierung nicht explizit mit den [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST- oder CONVERT-Funktionen durchführen.  
  
 Beachten Sie, dass Sie nicht für die Verwendung von UDTs Maßnahmen ergreifen müssen beim [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] erstellt Arbeitstabellen in der **Tempdb** Systemdatenbank. Dies umfasst die Handhabung von Cursorn, Tabellenvariablen und stellen Sie eine benutzerdefinierte Tabellenwertfunktionen, die enthalten UDTs und die Verwendung von **Tempdb**. Jedoch, wenn Sie explizit in eine temporäre Tabelle erstellen **Tempdb** , eine UDT-Spalte definiert, und klicken Sie dann der UDT muss registriert werden, **Tempdb** genauso wie bei einer Benutzerdatenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
