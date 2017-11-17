---
title: "Das Ändern der ASSEMBLY (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ASSEMBLY_TSQL
- ALTER ASSEMBLY
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], modifying
- refreshing assemblies
- assemblies [CLR integration], versioning
- assemblies [CLR integration], adding files
- modifying assemblies
- adding files
- ALTER ASSEMBLY statement
ms.assetid: 87bca678-4e79-40e1-bb8b-bd5ed8f34853
caps.latest.revision: 76
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b69c3ea4cc94c6b0b318cc13453d9d04b57df0b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-assembly-transact-sql"></a>ALTER ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert eine Assembly durch Ändern der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Katalogeigenschaften der Assembly. ALTER ASSEMBLY Aktualisierung auf die letzte Kopie der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Module, die ihre Implementierung enthalten und hinzugefügt oder entfernt Dateien, die mit ihm verknüpft sind. Assemblys werden erstellt, mit [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md).  

>  [!WARNING]
>  CLR verwendet die Codezugriffssicherheit (Code Access Security, CAS) im .NET Framework, die nicht länger als Sicherheitsbegrenzung unterstützt wird. Eine CLR-Assembly, die mit `PERMISSION_SET = SAFE` erstellt wurde, kann womöglich auf externe Systemressourcen zugreifen, nicht verwalteten Code aufrufen und sysadmin-Privilegien erwerben. Ab [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] wird eine `sp_configure`-Option mit der Bezeichnung `clr strict security` eingeführt, um die Sicherheit von CLR-Assemblys zu erhöhen. `clr strict security` ist standardmäßig aktiviert und behandelt `SAFE`- und `EXTERNAL_ACCESS`-Assemblys so, als wären Sie als `UNSAFE` gekennzeichnet. Die Option `clr strict security` kann für die Abwärtskompatibilität deaktiviert werden, es wird jedoch nicht empfohlen. Microsoft empfiehlt, dass alle Assemblys durch ein Zertifikat oder einen asymmetrischen Schlüssel mit einem entsprechenden Anmeldenamen signiert werden, dem `UNSAFE ASSEMBLY`-Berechtigung für die Masterdatenbank gewährt wurde. Weitere Informationen finden Sie unter [CLR Strict Security](../../database-engine/configure-windows/clr-strict-security.md).  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER ASSEMBLY assembly_name  
    [ FROM <client_assembly_specifier> | <assembly_bits> ]  
    [ WITH <assembly_option> [ ,...n ] ]  
    [ DROP FILE { file_name [ ,...n ] | ALL } ]  
    [ ADD FILE FROM   
    {   
        client_file_specifier [ AS file_name ]   
      | file_bits AS file_name   
    } [,...n ]   
    ] [ ; ]  
<client_assembly_specifier> :: =  
    '\\computer_name\share-name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
    { varbinary_literal | varbinary_expression }  
  
<assembly_option> :: =  
    PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
  | VISIBILITY = { ON | OFF }  
  | UNCHECKED DATA  
  
```  
  
## <a name="arguments"></a>Argumente  
 *AssemblyName*  
 Der Name der Assembly, die Sie ändern möchten. *Assembly_name* muss bereits in der Datenbank vorhanden sein.  
  
 VON \<Client_assembly_specifier > | \<Assembly_bits >  
 Aktualisiert eine Assembly auf die letzte Kopie der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Module, die ihre Implementierung enthalten. Diese Option kann nur verwendet werden, wenn der angegebenen Assembly keine Dateien zugeordnet sind.  
  
 \<Client_assembly_specifier > Gibt an, das Netzwerk oder den lokalen Speicherort die Assembly aktualisiert wird. Der Netzwerkspeicherort enthält den Computernamen, den Freigabenamen und einen Pfad innerhalb dieser Freigabe. *Manifest_file_name* gibt den Namen der Datei, die das Manifest der Assembly enthält.  
  
 \<Assembly_bits > ist der Binärwert für die Assembly.  
  
 Es müssen separate ALTER ASSEMBLY-Anweisungen für alle abhängigen Assemblys ausgegeben werden, die ebenfalls aktualisiert werden müssen.  
  
 PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
>  [!IMPORTANT]  
>  Die `PERMISSION_SET` Option hat Auswirkungen auf die `clr strict security` Option in der Warnung öffnende beschrieben. Wenn `clr strict security` ist aktiviert, werden alle Assemblys als behandelt `UNSAFE`.  
 Gibt die Eigenschaft für den [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Codezugriff-Berechtigungssatz der Assembly an. Weitere Informationen zu dieser Eigenschaft finden Sie unter [CREATE ASSEMBLY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-assembly-transact-sql.md).  
  
> [!NOTE]  
>  Die Optionen EXTERNAL_ACCESS und UNSAFE sind in einer enthaltenen Datenbank nicht verfügbar.  
  
 VISIBILITY = { ON | OFF }  
 Gibt an, ob die Assembly zum Erstellen von CLR-Funktionen (Common Language Runtime), gespeicherten Prozeduren, Triggern, benutzerdefinierten Typen und benutzerdefinierten Aggregatfunktionen für die Assembly sichtbar ist. Falls der Wert auf OFF festgelegt ist, soll die Assembly nur von anderen Assemblys aufgerufen werden. Falls bereits vorhandene CLR-Datenbankobjekte für die Assembly erstellt wurden, kann die Sichtbarkeit der Assembly nicht geändert werden. Alle Assemblys verweist *Assembly_name* werden standardmäßig als nicht sichtbar hochgeladen.  
  
 UNCHECKED DATA  
 Standardmäßig erzeugt ALTER ASSEMBLY einen Fehler, wenn die Konsistenz einzelner Tabellenzeilen überprüft werden muss. Diese Option ermöglicht es, die Überprüfungen mithilfe von DBCC CHECKTABLE auf einen späteren Zeitpunkt zu verschieben. Falls angegeben, wird die ALTER ASSEMBLY-Anweisung auch dann von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt, wenn sich Tabellen in der Datenbank befinden, die Folgendes enthalten:  
  
-   Persistente berechnete Spalten, die entweder direkt oder indirekt auf Methoden in der Assembly über [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen oder -Methoden verweisen.  
  
-   CHECK-Einschränkungen, die direkt oder indirekt auf Methoden in der Assembly verweisen.  
  
-   Spalten eines CLR-benutzerdefinierten Typs, die abhängig von der Assembly und der Typ implementiert eine **UserDefined** (nicht -**Native**) Serialisierungsformat.  
  
-   Spalten eines CLR-benutzerdefinierten Typs, die auf mithilfe von WITH SCHEMABINDING erstellte Sichten verweisen.  
  
 Falls CHECK-Einschränkungen vorhanden sind, werden sie deaktiviert und als nicht vertrauenswürdig gekennzeichnet. Alle Tabellen, die von der Assembly abhängige Spalten enthalten, werden so gekennzeichnet, dass sie nicht überprüfte Daten enthalten. Dies wird erst nach einer expliziten Überprüfung dieser Tabellen geändert.  
  
 Nur Mitglieder der **Db_owner** und **Db_ddlowner** festen Datenbankrollen können diese Option angeben.  
  
 Erfordert die **ALTER ANY SCHEMA** Berechtigung, um diese Option anzugeben.  
  
 Weitere Informationen finden Sie unter [Assemblys implementieren](../../relational-databases/clr-integration/assemblies-implementing.md).  
  
 [DROP FILE { *File_name*[ **,***.. ...n*] | ALLE}]  
 Entfernt den dieser Assembly zugeordneten Dateinamen oder alle dieser Assembly zugeordneten Dateien aus der Datenbank. Falls gefolgt von ADD FILE, wird zuerst DROP FILE ausgeführt. Dadurch können Sie eine Datei mit demselben Dateinamen ersetzen.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 [ADD FILE FROM { *Client_file_specifier* [AS *File_name*] | *File_bits*AS *File_name*}  
 Lädt eine Datei mit der Assembly, z. B. Quellcode, verbunden sein, Debugdateien oder andere zugehörige Informationen, auf dem Server und in sichtbar gemacht werden, die **Sys. assembly_files** -Katalogsicht angezeigt. *Client_file_specifier* gibt den Speicherort, von dem die Datei hochladen. *File_bits* kann stattdessen verwendet werden, um die Liste der Binärwerte anzugeben, aus denen die Datei besteht. *File_name* gibt den Namen, unter dem die Datei soll, in der Instanz von gespeichert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *File_name* muss angegeben werden, wenn *File_bits* angegeben ist, und optional Wenn *Client_file_specifier* angegeben ist. Wenn *File_name* nicht angegeben wird, der "File_name"-Teil des *Client_file_specifier* dient als *File_name*.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
## <a name="remarks"></a>Hinweise  
 Mit ALTER ASSEMBLY werden zurzeit ausgeführte Sitzungen, die Code in der zu ändernden Assembly ausführen, nicht unterbrochen. Die Ausführung wird von den aktuellen Sitzungen abgeschlossen, indem die nicht geänderten Bits der Assembly verwendet werden.  
  
 Ist die FROM-Klausel angegeben, aktualisiert ALTER ASSEMBLY die Assembly in Bezug auf die letzten Kopien der bereitgestellten Module. Da CLR-Funktionen, gespeicherte Prozeduren, Trigger, Datentypen und benutzerdefinierte Aggregatfunktionen in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorhanden sein können, die bereits für die Assembly definiert wurden, bindet ALTER ASSEMBLY diese Elemente erneut an die neueste Implementierung der Assembly. Für diese Neubindung müssen die Methoden, die den CLR-Funktionen, gespeicherten Prozeduren und Triggern zugeordnet sind, in der geänderten Assembly mit denselben Signaturen vorhanden sein. Die Klassen, die CLR-benutzerdefinierte Typen und benutzerdefinierte Aggregatfunktionen implementieren, müssen weiterhin die Anforderungen für den benutzerdefinierten Typ oder das benutzerdefinierte Aggregat erfüllen.  
  
> [!CAUTION]  
>  Wird WITH UNCHECKED DATA nicht angegeben, versucht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die Ausführung von ALTER ASSEMBLY zu verhindern, wenn die neue Assemblyversion Auswirkungen auf vorhandene Daten in Tabellen, Indizes oder anderen persistenten Sites hat. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt jedoch nicht sicher, dass berechnete Spalten, Indizes, indizierte Sichten oder Ausdrücke mit den zugrunde liegenden Routinen und Typen konsistent sein werden, wenn die CLR-Assembly aktualisiert wird. Seien Sie vorsichtig beim Ausführen von ALTER ASSEMBLY, um sicherzustellen, dass kein Konflikt zwischen dem Ergebnis eines Ausdrucks ist und ein Wert auf Grundlage, dass der Ausdruck in der Assembly gespeichert.  
  
 Mit ALTER ASSEMBLY wird die Assemblyversion geändert. Das Token für Sprachraum und öffentlichen Schlüssel der Assembly wird nicht geändert.  
  
 Mit der ALTER ASSEMBLY-Anweisung kann Folgendes nicht geändert werden:  
  
-   Die Signaturen von CLR-Funktionen, Aggregatfunktionen, gespeicherten Prozeduren und Triggern in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf die Assembly verweisen. ALTER ASSEMBLY erzeugt einen Fehler, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht erneut mit der neuen Version der Assembly binden kann.  
  
-   Die Signaturen von Methoden in der Assembly, die von anderen Assemblys aufgerufen werden.  
  
-   Die Liste der Assemblys, die abhängig von der Assembly verwiesen wird, in der **DependentList** Eigenschaft der Assembly.  
  
-   Die Indizierbarkeit einer Methode, es sei denn, es hängen keine Indizes oder persistenten berechneten Spalten direkt oder indirekt von dieser Methode ab.  
  
-   Die **FillRow** -Methodennamenattribut für CLR-Tabellenwertfunktionen.  
  
-   Die **Accumulate** und **terminieren** Methodensignatur für benutzerdefinierte Aggregate.  
  
-   Die Systemassemblys.  
  
-   Der Assemblybesitz. Verwendung [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md) stattdessen.  
  
 Darüber hinaus kann für Assemblys, die benutzerdefinierte Typen implementieren, ALTER ASSEMBLY für nur folgende Änderungen verwendet werden:  
  
-   Ändern von öffentlichen Methoden der Klasse des benutzerdefinierten Typs, solange keine Signaturen oder Attribute geändert werden.  
  
-   Hinzufügen von neuen öffentlichen Methoden.  
  
-   Ändern von privaten Methoden auf beliebige Weise.  
  
 Felder in einem systemeigenen serialisierten benutzerdefinierten Typ, einschließlich Datenelemente oder Basisklassen, kann mithilfe von ALTER ASSEMBLY geändert werden. Alle anderen Änderungen werden nicht unterstützt.  
  
 Ist ADD FILE FROM nicht angegeben, werden von ALTER ASSEMBLY alle dieser Assembly zugeordneten Dateien gelöscht.  
  
 Wird ALTER ASSEMBLY ohne die UNCHECKED-Datenklausel ausgeführt, werden Überprüfungen ausgeführt, um sicherzustellen, dass die neue Assemblyversion keine Auswirkungen auf vorhandene Tabellendaten hat. Abhängig von der Menge der zu überprüfenden Daten kann dadurch die Leistung beeinträchtigt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Assembly. Es gelten folgende zusätzliche Anforderungen:  
  
-   Zum Ändern einer Assembly, deren vorhandene Berechtigung Satz EXTERNAL_ACCESS ist, erfordert**EXTERNAL ACCESS ASSEMBLY**Berechtigung auf dem Server.  
  
-   Zum Ändern einer Assembly, deren vorhandene Berechtigung auf UNSAFE festgelegt ist erfordert **UNSAFE ASSEMBLY** Berechtigung auf dem Server.  
  
-   So ändern Sie den Berechtigungssatz einer Assembly auf EXTERNAL_ACCESS erfordert**EXTERNAL ACCESS ASSEMBLY** Berechtigung auf dem Server.  
  
-   So ändern Sie den Berechtigungssatz einer Assembly auf UNSAFE, erfordert **UNSAFE ASSEMBLY** Berechtigung auf dem Server.  
  
-   Angabe WITH UNCHECKED DATA erfordert **ALTER ANY SCHEMA** Berechtigung.  


### <a name="permissions-with-clr-strict-security"></a>Berechtigungen mit strikte Sicherheit der CLR    
Die folgenden Berechtigungen erforderlich, um eine CLR-Assembly beim `CLR strict security` aktiviert ist:

- Der Benutzer muss über die `ALTER ASSEMBLY`-Berechtigung verfügen.  
- Eine der folgenden Bedingungen muss ebenfalls erfüllt sein:  
  - Die Assembly ist mit einem Zertifikat oder asymmetrischen Schlüssel signiert, der über einen entsprechenden Anmeldenamen mit der `UNSAFE ASSEMBLY`-Berechtigung auf dem Server verfügt. Es wird empfohlen, die Assembly zu signieren.  
  - Die `TRUSTWORTHY`-Eigenschaft der Datenbank ist auf `ON` festgelegt, und der Besitzer der Datenbank ist ein Anmeldename, der über `UNSAFE ASSEMBLY`-Berechtigungen auf dem Server verfügt. Diese Option wird nicht empfohlen.  
  
  
 Weitere Informationen zu assemblyberechtigungssätzen finden Sie unter [Entwerfen von Assemblys](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-refreshing-an-assembly"></a>A. Aktualisieren einer assembly  
 Das folgende Beispiel aktualisiert die Assembly `ComplexNumber` auf die aktuellste Kopie der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Module, die ihre Implementierung enthalten.  
  
> [!NOTE]  
>  Die `ComplexNumber`-Assembly kann durch Ausführen der UserDefinedDataType-Beispielskripts erstellt werden. Weitere Informationen finden Sie unter [benutzerdefinierte Typ](http://msdn.microsoft.com/library/a9b75f36-d7f5-47f7-94d6-b4448c6a2191).  
  
 ```
 ALTER ASSEMBLY ComplexNumber 
 FROM 'C:\Program Files\Microsoft SQL Server\130\Tools\Samples\1033\Engine\Programmability\CLR\UserDefinedDataType\CS\ComplexNumber\obj\Debug\ComplexNumber.dll' 
  ```
### <a name="b-adding-a-file-to-associate-with-an-assembly"></a>B. Hinzufügen einer Datei, die einer Assembly zugeordnet werden soll  
 Im folgenden Beispiel wird die Quellcodedatei `Class1.cs` hochgeladen, die der `MyClass`-Assembly zugeordnet werden soll. In diesem Beispiel wird davon ausgegangen, dass die `MyClass`-Assembly bereits in der Datenbank vorhanden ist.  
  
```  
ALTER ASSEMBLY MyClass   
ADD FILE FROM 'C:\MyClassProject\Class1.cs';  
```  
  
### <a name="c-changing-the-permissions-of-an-assembly"></a>C. Ändern der Berechtigungen einer Assembly  
 Im folgenden Beispiel wird der Berechtigungssatz der `ComplexNumber`-Assembly von SAFE in `EXTERNAL ACCESS` geändert.  
  
```  
ALTER ASSEMBLY ComplexNumber WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie die ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

