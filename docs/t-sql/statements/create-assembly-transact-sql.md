---
title: CREATE ASSEMBLY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ASSEMBLY
- CREATE ASSEMBLY
- CREATE_ASSEMBLY_TSQL
- ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], validating
- validating assemblies
- CREATE ASSEMBLY statement
- assemblies [CLR integration], creating
ms.assetid: d8d1d245-c2c3-4325-be52-4fc1122c2079
caps.latest.revision: 94
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 62fb31b65d89180fa14d75670a7c4bdbf7e9942c
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="create-assembly-transact-sql"></a>CREATE ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  Erstellt ein verwaltetes Anwendungsmodul, das Klassenmetadaten und verwalteten Code als Objekt in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält. Durch Verweisen auf dieses Modul können CLR-Funktionen (Common Language Runtime), gespeicherte Prozeduren, Trigger, benutzerdefinierte Aggregate und benutzerdefinierte Typen in der Datenbank erstellt werden.  
  
[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

>  [!WARNING]
>  CLR verwendet die Codezugriffssicherheit (Code Access Security, CAS) im .NET Framework, die nicht länger als Sicherheitsbegrenzung unterstützt wird. Eine CLR-Assembly, die mit `PERMISSION_SET = SAFE` erstellt wurde, kann womöglich auf externe Systemressourcen zugreifen, nicht verwalteten Code aufrufen und sysadmin-Privilegien erwerben. Ab [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] wird eine `sp_configure`-Option mit der Bezeichnung `clr strict security` eingeführt, um die Sicherheit von CLR-Assemblys zu erhöhen. `clr strict security` ist standardmäßig aktiviert und behandelt `SAFE`- und `EXTERNAL_ACCESS`-Assemblys so, als wären Sie als `UNSAFE` gekennzeichnet. Die Option `clr strict security` kann für die Abwärtskompatibilität deaktiviert werden, es wird jedoch nicht empfohlen. Microsoft empfiehlt, dass alle Assemblys durch ein Zertifikat oder einen asymmetrischen Schlüssel mit einem entsprechenden Anmeldenamen signiert werden, dem `UNSAFE ASSEMBLY`-Berechtigung für die Masterdatenbank gewährt wurde. Weitere Informationen finden Sie unter [CLR Strict Security](../../database-engine/configure-windows/clr-strict-security.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE ASSEMBLY assembly_name  
[ AUTHORIZATION owner_name ]  
FROM { <client_assembly_specifier> | <assembly_bits> [ ,...n ] }  
[ WITH PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE } ]  
[ ; ]  
<client_assembly_specifier> :: =  
        '[\\computer_name\]share_name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```  
  
## <a name="arguments"></a>Argumente  
 *assembly_name*  
 Der Name der Assembly. Dieser Name muss innerhalb der Datenbank eindeutig und ein gültiger [Bezeichner](../../relational-databases/databases/database-identifiers.md) sein.  
  
 AUTHORIZATION *owner_name*  
 Gibt den Namen eines Benutzers oder einer Rolle als Besitzer der Assembly an. *owner_name* muss der Name einer Rolle sein, deren Mitglied der aktuelle Benutzer ist, oder der aktuelle Benutzer benötigt die IMPERSONATE-Berechtigung für *owner_name*. Wird kein Wert angegeben, wird der aktuelle Benutzer zum Besitzer.  
  
 \<client_assembly_specifier>  
Gibt den lokalen Pfad oder den Netzwerkspeicherort an, unter dem die Assembly gespeichert ist, die hochgeladen wird. Außerdem wird damit der Manifestdateiname angegeben, der der Assembly entspricht.  \<client_assembly_specifier> kann als feste Zeichenfolge oder als zu einer festen Zeichenfolge ausgewerteter Ausdruck mit Variablen ausgedrückt werden. Das Laden von Assemblys mit mehreren Modulen wird von CREATE ASSEMBLY nicht unterstützt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sucht auch nach abhängigen Assemblys dieser Assembly an demselben Speicherort und lädt sie mit demselben Besitzer wie die Assembly auf Stammebene hoch. Wenn keine abhängigen Assemblys gefunden werden und diese noch nicht in der aktuellen Datenbank geladen sind, wird für CREATE ASSEMBLY ein Fehler gemeldet. Wenn die abhängigen Assemblys bereits in der aktuellen Datenbank geladen sind, muss der Besitzer dieser Assemblys mit dem Besitzer der neu erstellten Assembly identisch sein.
  
 \<client_assembly_specifier> kann nicht angegeben werden, wenn für den angemeldeten Benutzer ein Identitätswechsel ausgeführt wird.  
  
 \<assembly_bits>  
 Die Liste der Binärwerte, aus denen die Assembly und die abhängigen Assemblys bestehen. Der erste Wert in der Liste wird als Assembly auf Stammebene betrachtet. Die Werte, die den abhängigen Assemblys entsprechen, können in einer beliebigen Reihenfolge bereitgestellt werden. Werte, die nicht Abhängigkeiten der Stammassembly entsprechen, werden ignoriert.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 *varbinary_literal*  
 Ist ein **varbinary**-Literal.  
  
 *varbinary_expression*  
 Ist ein Ausdruck vom Typ **varbinary**.  
  
 PERMISSION_SET { **SAFE** | EXTERNAL_ACCESS | UNSAFE }  
 >  [!IMPORTANT]  
 >  Die Option `PERMISSION_SET` wird von der Option `clr strict security` beeinflusst, was in der Warnung beschrieben wird. Wenn `clr strict security` aktiviert ist, werden alle Assemblys als `UNSAFE` behandelt.
 
 Gibt Codezugriffsberechtigungen an, die der Assembly erteilt werden, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] darauf zugreift. Wird kein Wert angegeben, wird SAFE als Standardwert verwendet.  
  
 Es wird empfohlen, SAFE zu verwenden. SAFE ist der restriktivste Berechtigungssatz. Code, der von einer Assembly mit SAFE-Berechtigungen ausgeführt wird, hat keinen Zugriff auf externe Systemressourcen wie z. B. Dateien, das Netzwerk, Umgebungsvariablen oder die Registrierung.  
  
 EXTERNAL_ACCESS ermöglicht Assemblys den Zugriff auf bestimmte externe Systemressourcen wie z. B. Dateien, Netzwerke, Umgebungsvariablen und die Registrierung.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 UNSAFE ermöglicht Assemblys den uneingeschränkten Zugriff auf Ressourcen innerhalb und außerhalb einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Code, der innerhalb einer UNSAFE-Assembly ausgeführt wird, kann nicht verwalteten Code aufrufen.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
> [!IMPORTANT]  
>  SAFE ist die empfohlene Berechtigungseinstellung für Assemblys, die Berechnungs- und Datenverwaltungstasks ausführen, ohne auf Ressourcen außerhalb einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zuzugreifen.  
>   
>  Wir empfehlen die Verwendung von EXTERNAL_ACCESS für Assemblys, die auf Ressourcen außerhalb einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugreifen. EXTERNAL_ACCESS-Assemblys beinhalten die Zuverlässigkeit und Skalierbarkeit von SAFE-Assemblys, aber aus Sicht der Sicherheit sind sie mit UNSAFE-Assemblys vergleichbar. Code in EXTERNAL_ACCESS-Assemblys wird nämlich standardmäßig unter dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto ausgeführt, und der Code greift auf externe Ressourcen unter diesem Konto zu, außer der Code nimmt explizit die Identität des Aufrufers an. Deshalb sollte die Berechtigung zum Erstellen von EXTERNAL_ACCESS-Assemblys nur vertrauenswürdigen Anmeldenamen erteilt werden, die Code unter dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto ausführen. Weitere Informationen finden Sie unter [Sicherheit der CLR-Integration](../../relational-databases/clr-integration/security/clr-integration-security.md).  
>   
>  Wenn Sie UNSAFE angeben, kann der Code in der Assembly jegliche Vorgänge im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozessraum ausführen, die die Zuverlässigkeit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gefährden können. UNSAFE-Assemblys können außerdem potenziell das Sicherheitssystem von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder der CLR unterlaufen. UNSAFE-Berechtigungen sollten nur sehr vertrauenswürdigen Assemblys erteilt werden. Nur Mitglieder der festen Serverrolle **sysadmin** können UNSAFE-Assemblys erstellen und ändern.  
  
 Weitere Informationen zu Assemblyberechtigungen finden Sie unter [Entwerfen von Assemblys](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="remarks"></a>Remarks  
 CREATE ASSEMBLY lädt eine Assembly hoch, die zuvor als DLL-Datei von verwaltetem Code zum Verwenden in einer Instanz von SQL Server kompiliert wurde.  
 
Falls die Option `PERMISSION_SET` aktiviert ist, wir sie in den Anweisungen `CREATE ASSEMBLY` und `ALTER ASSEMBLY` zur Laufzeit ignoriert, jedoch werden die `PERMISSION_SET`-Optionen in den Metadaten beibehalten. Das Ignorieren dieser Option vermindert die Trennung vorhandener Codeanweisungen.
 
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist es nicht zulässig, verschiedene Versionen einer Assembly mit demselben Namen, derselben Kultur und demselben öffentlichen Schlüssel zu registrieren.  
  
Beim Versuch, auf die in \<client_assembly_specifier> angegebene Assembly zuzugreifen, nimmt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Sicherheitskontext des aktuellen Windows-Anmeldenamens an. Falls \<client_assembly_specifier> einen Netzwerkspeicherort (UNC-Pfad) angibt, wird der Identitätswechsel des aktuellen Anmeldenamens aufgrund von Delegierungsbeschränkungen nicht auf den neuen Netzwerkspeicherort übertragen. In diesem Fall erfolgt der Zugriff mithilfe des Sicherheitskontexts des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkontos. Weitere Informationen finden Sie unter [Anmeldeinformationen &#40;Datenbank-Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md).
  
 Neben der mit *assembly_name* angegebenen Stammassembly versucht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], alle Assemblys hochzuladen, auf die die Stammassembly, die hochgeladen wird, verweist. Falls eine Assembly, auf die verwiesen wird, aufgrund einer früheren CREATE ASSEMBLY-Anweisung bereits in die Datenbank hochgeladen wurde, wird diese Assembly nicht hochgeladen, ist aber für die Stammassembly verfügbar. Falls eine abhängige Assembly nicht zuvor hochgeladen wurde, aber [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Manifestdatei nicht im Quellverzeichnis findet, gibt CREATE ASSEMBLY einen Fehler zurück.  
  
 Wenn abhängige Assemblys, auf die von der Stammassembly verwiesen wird, nicht bereits in der Datenbank vorhanden sind und implizit zusammen mit der Stammassembly geladen werden, haben sie die gleichen Berechtigungen wie die Assembly auf Stammebene. Wenn die abhängigen Assemblys mit einem anderen Berechtigungssatz als die Assembly auf Stammebene erstellt werden müssen, müssen sie vor der Assembly auf Stammebene explizit mit dem entsprechenden Berechtigungssatz hochgeladen werden.  
  
## <a name="assembly-validation"></a>Assemblyüberprüfung  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft die Binärdaten der Assemblys, die mithilfe der CREATE ASSEMBLY-Anweisung hochgeladen wurden, um folgende Bedingungen sicherzustellen:  
  
-   Die Assemblybinärdatei ist wohlgeformt und enthält gültige Metadaten und Codesegmente, und die Codesegmente weisen gültige MSIL-Anweisungen (Microsoft Intermediate Language) auf.  
  
-   Die Systemassemblys, auf die verwiesen wird, entsprechen einer der folgenden unterstützten Assemblys in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: Microsoft.Visualbasic.dll, Mscorlib.dll, System.Data.dll, System.dll, System.Xml.dll, Microsoft.Visualc.dll, Custommarshallers.dll, System.Security.dll, System.Web.Services.dll, System.Data.SqlXml.dll, System.Core.dll und System.Xml.Linq.dll. Auf andere Systemassemblys kann verwiesen werden, aber sie müssen explizit in der Datenbank registriert sein.  
  
-   Für Assemblys, die mit den SAFE- oder EXTERNAL ACCESS-Berechtigungssätzen erstellt werden:  
  
    -   Der Assemblycode sollte typsicher sein. Die Typsicherheit wird durch Ausführen der CLR-Überprüfung (Common Language Runtime) für die Assembly erreicht.  
  
    -   Die Assembly sollte keine statischen Datenelemente in den Klassen enthalten, außer sie sind als schreibgeschützt gekennzeichnet.  
  
    -   Die Klassen in der Assembly dürfen keine Finalizer-Methoden enthalten.  
  
    -   Die Klassen oder Methoden der Assembly sollten nur mit zulässigen Codeattributen versehen werden. Weitere Informationen finden Sie unter [Benutzerdefinierte Attribute für CLR-Routinen](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
 Neben den vorherigen Überprüfungen, die zusammen mit CREATE ASSEMBLY ausgeführt werden, werden zur Ausführungszeit des Codes in der Assembly zusätzliche Überprüfungen vorgenommen:  
  
-   Beim Aufrufen bestimmter [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-APIs, die eine bestimmte Codezugriffsberechtigung erfordern, wird möglicherweise ein Fehler gemeldet, wenn diese Berechtigung im Berechtigungssatz der Assembly nicht enthalten ist.  
  
-   Für SAFE- und EXTERNAL_ACCESS-Assemblys wird für jeden Versuch, [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-APIs aufzurufen, die mit bestimmten HostProtectionAttributes versehen sind, ein Fehler gemeldet.  
  
 Weitere Informationen finden Sie unter [Entwerfen von Assemblys](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE ASSEMBLY-Berechtigung.  
  
 Falls PERMISSION_SET = EXTERNAL_ACCESS angegeben ist, wird **EXTERNAL ACCESS ASSEMBLY**-Berechtigung auf dem Server benötigt. Falls PERMISSION_SET = UNSAFE angegeben ist, wird **UNSAFE ASSEMBLY**-Berechtigung auf dem Server benötigt.  
  
 Der Benutzer muss der Besitzer von Assemblys sein, auf die von der Assembly verwiesen wird, die hochgeladen werden soll, falls die Assemblys bereits in der Datenbank vorhanden sind. Um eine Assembly mithilfe eines Dateipfads hochzuladen, muss der aktuelle Benutzer einen Anmeldenamen mit Windows-Authentifizierung haben oder ein Mitglied der festen Serverrolle **sysadmin** sein. Der Windows-Anmeldename des Benutzers, der CREATE ASSEMBLY ausführt, benötigt die Leseberechtigung für die Freigabe und für die Dateien, die in die Anweisung geladen werden.  

### <a name="permissions-with-clr-strict-security"></a>Berechtigungen mit CLR Strict Security    
Die folgenden Berechtigungen werden zum Erstellen einer CLR-Assembly benötigt, wenn `CLR strict security` aktiviert ist:

- Der Benutzer muss über die `CREATE ASSEMBLY`-Berechtigung verfügen.  
- Eine der folgenden Bedingungen muss ebenfalls erfüllt sein:  
  - Die Assembly ist mit einem Zertifikat oder asymmetrischen Schlüssel signiert, der über einen entsprechenden Anmeldenamen mit der `UNSAFE ASSEMBLY`-Berechtigung auf dem Server verfügt. Es wird empfohlen, die Assembly zu signieren.  
  - Die `TRUSTWORTHY`-Eigenschaft der Datenbank ist auf `ON` festgelegt, und der Besitzer der Datenbank ist ein Anmeldename, der über `UNSAFE ASSEMBLY`-Berechtigungen auf dem Server verfügt. Diese Option wird nicht empfohlen.  
  
 Weitere Informationen zu Assemblyberechtigungen finden Sie unter [Entwerfen von Assemblys](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="example-a-creating-an-assembly-from-a-dll"></a>Beispiel A: Erstellen einer Assembly aus einer dll  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel wird davon ausgegangen, dass die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Beispiele im Standardspeicherort des lokalen Computers gespeichert sind und dass die Beispielanwendung HelloWorld.csproj kompiliert ist. Weitere Informationen finden Sie unter [Beispiel „Hello World“](http://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7).  
  
```  
CREATE ASSEMBLY HelloWorld   
FROM <system_drive>:\Program Files\Microsoft SQL Server\100\Samples\HelloWorld\CS\HelloWorld\bin\debug\HelloWorld.dll  
WITH PERMISSION_SET = SAFE;  
```  
  
### <a name="example-b-creating-an-assembly-from-assembly-bits"></a>Beispiel B: Erstellen einer Assembly aus Assemblyteilen  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Ersetzen Sie die Beispielteile (die nicht abgeschlossen oder gültig sind) durch Ihre Assemblyteile.  
  
```  
CREATE ASSEMBLY HelloWorld  
    FROM 0x4D5A900000000000  
WITH PERMISSION_SET = SAFE;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Verwendungsszenarios und Beispiele für Common Language Runtime-Integration &#40;CLR&#41;](http://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
  
  
