---
title: Verwenden des Datenbankmodul-Cmdlets | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Convert-UrnToPath cmdlet
- PowerShell [SQL Server], cmdlets
- Cmdlets [SQL Server]
- PowerShell [SQL Server], Convert-UrnToPath
- Cmdlets [SQL Server], Convert-UrnToPath
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 720aa982-09ae-41a3-b603-a91004cfbe3e
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b3833567185c16097983cfce99fca2e33d61d88e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="use-the-database-engine-cmdlets"></a>Verwenden der Datenbankmodul-Cmdlets
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Windows PowerShell-Cmdlets sind Einzelfunktionsbefehle, für die i.d.R. eine Verb-Substantiv-Namenskonvention gilt, z.B. **Get-Help** oder **Set-MachineName**. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anbieter für Windows PowerShell bietet für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]spezifische Cmdlets.  
  
## <a name="database-engine-cmdlets"></a>Datenbankmodul-Cmdlets  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementiert eine kleine Anzahl von Cmdlets für [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Diese Cmdlets werden hauptsächlich zum Ausführen vorhandener Transact-SQL-Skripts aus neuen PowerShell-Skripts, Auswerten richtlinienbasierter Verwaltungsrichtlinien und Unterstützen beim Angeben von SQL Server-Bezeichnern in SQL Server-Anbieterpfaden verwendet.  
  
 Bei den meisten Windows PowerShell-Skripts wird [!INCLUDE[ssDE](../../includes/ssde-md.md)] genutzt. Hierbei kommen der SQL Server PowerShell-Anbieter und SQL Server-Verwaltbarkeits-Objektmodelle zum Einsatz. Weitere Informationen finden Sie unter [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md).  
  
### <a name="get-cmdlet-help"></a>Get-Help-Cmdlet  
 In der Windows PowerShell-Umgebung stellt das **Get-Help** -Cmdlet Hilfeinformationen für jedes Cmdlet bereit. **Get-Help** gibt Informationen wie Syntax, Parameterdefinitionen, Eingabe- und Ausgabetypen und eine Beschreibung der vom Cmdlet durchgeführten Aktion zurück. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
### <a name="partial-parameter-names"></a>Partielle Parameternamen  
 Sie müssen nicht den ganzen Namen eines Cmdlet-Parameters angeben. Sie müssen nur so viele Zeichen des Namens eingeben, dass dieser eindeutig von den anderen Parametern unterschieden werden kann, die von dem Cmdlet unterstützt werden. In diesen Beispielen werden drei Methoden zum Angeben des Parameters **Invoke-Sqlcmd-QueryTimeout** veranschaulicht:  
  
```  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTimeout 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTime 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryT 3  
```  
  
## <a name="database-engine-cmdlet-tasks"></a>Cmdlet-Tasks des Datenbankmoduls  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt die Verwendung von **Invoke-Sqlcmd** zum Ausführen von **sqlcmd** -Skripts oder -Befehlen, die [!INCLUDE[tsql](../../includes/tsql-md.md)] - oder XQuery-Anweisungen enthalten. Die **sqlcmd** -Eingabe wird entweder als Zeichenfolgen-Eingabeparameter oder als Name einer zu öffnenden Skriptdatei akzeptiert.|[Invoke-Sqlcmd-Cmdlet](../../powershell/invoke-sqlcmd-cmdlet.md)|  
|Beschreibt die Verwendung von **Invoke-PolicyEvaluation** zum Melden, ob ein Zielsatz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekten den in richtlinienbasierten Verwaltungsrichtlinien definierten Bedingungen entspricht. Optional können mit dem Cmdlet alle festlegbaren Optionen in den Zielobjekten neu konfiguriert werden, die den Richtlinienbedingungen nicht entsprechen.|[Invoke-PolicyEvaluation-Cmdlet](../../powershell/invoke-policyevaluation-cmdlet.md)|  
|Beschreibt die Verwendung von **Encode-Sqlname** und **Decode-Sqlname** zum Verarbeiten von SQL Server-Bezeichnern, die in Windows PowerShell-Pfaden nicht unterstützte Zeichen enthalten.|[Codierung und Decodierung von SQL Server-Bezeichnern](../../relational-databases/scripting/encode-and-decode-sql-server-identifiers.md)|  
|Beschreibt die Verwendung von **Convert-UrnToPath** zum Konvertieren eines URN (Uniform Resource Name, einheitlicher Name für Ressourcen) für SQL Server-Verwaltbarkeitsobjekte in den entsprechenden Pfad des SQL Server-Anbieters.|[Konvertieren von URNs in SQL Server-Anbieterpfade](../../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server PowerShell-Anbieter](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
[Übersicht über PowerShell-Cmdlets für Always On-Verfügbarkeitsgruppen (SQL Server)](../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)
  
  
