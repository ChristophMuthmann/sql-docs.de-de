---
title: "Benutzerdefinierte Eigenschaften für OLE DB | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0b501e22b3112a130e6ea5c931fc2b3e2f9f2e40
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="ole-db-custom-properties"></a>Benutzerdefinierte Eigenschaften für OLE DB
  **Benutzerdefinierte Eigenschaften von Quellen**  
  
 Die OLE DB-Quelle verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften der OLE DB-Quelle beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftsname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Der zum Zugreifen auf die Datenbank verwendete Modus. Die möglichen Werte sind **Geöffnetes Rowset**, **Geöffnetes Rowset aus Variable**, **SQL-Befehl**und **SQL-Befehl aus Variable**. Der Standardwert ist **Geöffnetes Rowset**.|  
|AlwaysUseDefaultCodePage|Boolean|Ein Wert, der angibt, ob der Wert der **DefaultCodePage** -Eigenschaft für jede Spalte verwendet werden soll, oder ob versucht werden soll, die Codepage aus dem Gebietsschema der einzelnen Spalten abzuleiten. Der Standardwert dieser Eigenschaft ist **False**.|  
|CommandTimeOut|Integer|Die Anzahl der Sekunden, nach denen ein Befehl wegen eines Timeouts abgebrochen wird. Der Wert 0 steht für ein unbegrenztes Timeout.<br /><br /> Hinweis: Diese Eigenschaft ist nicht im **Quellen-Editor für OLE DB**verfügbar, kann jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden.|  
|DefaultCodePage|Integer|Die zu verwendende Codepage, wenn keine Codepageinformationen aus der Datenquelle verfügbar sind.|  
|OpenRowset|String|Der Name des Datenbankobjekts, das zum Öffnen eines Rowsets verwendet wird.|  
|OpenRowsetVariable|String|Die Variable, die den Namen des Datenbankobjekts enthält, das zum Öffnen eines Rowsets verwendet wird.|  
|ParameterMapping|String|Die Zuordnung von Parametern im SQL-Befehl zu Variablen.|  
|SqlCommand|String|Der auszuführende SQL-Befehl.|  
|SqlCommandVariable|String|Die Variable, die den auszuführenden SQL-Befehl enthält.|  
  
 Die Ausgabe und die Ausgabespalten der OLE DB-Quelle verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [OLE DB Source](../../integration-services/data-flow/ole-db-source.md).  
  
 **Benutzerdefinierte Eigenschaften von Zielen**  
  
 Das OLE DB-Ziel verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften des OLE DB-Ziels beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
> [!NOTE]  
>  Die hier aufgelisteten FastLoad-Optionen (FastLoadKeepIdentity, FastLoadKeepNulls und FastLoadOptions) entsprechen den Eigenschaften mit ähnlichen Bezeichnungen der **IRowsetFastLoad** -Schnittstelle, die vom Microsoft OLE DB Provider for SQL Server (SQLOLEDB) bereitgestellt wird. Weitere Informationen finden Sie unter IRowsetFastLoad in der MSDN Library.  
  
|Eigenschaftsname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Ganze Zahl (Enumeration)|Ein Wert, der angibt, wie das Ziel auf seine Zieldatenbank zugreift.<br /><br /> Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> <br /><br /> **OpenRowset** (0) – Sie geben den Namen einer Tabelle oder Sicht an.<br /><br /> **OpenRowset from Variable** (1) – Sie geben den Namen einer Variablen an, die den Namen einer Tabelle oder Sicht enthält.<br /><br /> **OpenRowset Using Fastload** (3) – Sie geben den Namen einer Tabelle oder Sicht an.<br /><br /> **OpenRowset Using Fastload from Variable** (4) – Sie geben den Namen einer Variablen an, die den Namen einer Tabelle oder Sicht enthält.<br /><br /> **SQL Command** (2) – Sie geben eine SQL-Anweisung an.|  
|AlwaysUseDefaultCodePage|Boolean|Ein Wert, der angibt, ob der Wert der **DefaultCodePage** -Eigenschaft für jede Spalte verwendet werden soll, oder ob versucht werden soll, die Codepage aus dem Gebietsschema der einzelnen Spalten abzuleiten. Der Standardwert dieser Eigenschaft ist **False**.|  
|CommandTimeOut|Integer|Die maximale Ausführungsdauer in Sekunden, bevor ein Timeout für den SQL-Befehl eintritt. Der Wert 0 steht für eine unbegrenzte Dauer. Der Standardwert dieser Eigenschaft ist 0.<br /><br /> Hinweis: Diese Eigenschaft ist nicht im **Ziel-Editor für OLE DB**verfügbar, kann jedoch mit dem **erweiterten Editor**festgelegt werden.|  
|DefaultCodePage|Integer|Die dem OLE DB-Ziel zugeordnete Standardcodepage.|  
|FastLoadKeepIdentity|Boolean|Ein Wert, der angibt, ob Identitätswerte beim Laden von Daten kopiert werden sollen. Diese Eigenschaft ist nur verfügbar, wenn eine der Optionen für das schnelle Laden verwendet wird. Der Standardwert dieser Eigenschaft ist **False**. Diese Eigenschaft entspricht der OLE-DB-[IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)-Eigenschaft **SSPROP_FASTLOADKEEPIDENTITY**.|  
|FastLoadKeepNulls|Boolean|Ein Wert, der angibt, ob NULL-Werte beim Laden von Daten kopiert werden sollen. Diese Eigenschaft ist nur verfügbar, wenn eine der Optionen für das schnelle Laden verwendet wird. Der Standardwert dieser Eigenschaft ist **False**. Diese Eigenschaft entspricht der OLE-DB-[IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)-Eigenschaft **SSPROP_FASTLOADKEEPNULLS**.|  
|FastLoadMaxInsertCommitSize|Integer|Ein Wert, der die Batchgröße angibt, für die das OLE DB-Ziel bei schnellen Ladevorgängen die Durchführung eines Commits versucht. Der Standardwert **0**gibt einen einzelnen Commitvorgang an, wenn alle Zeilen verarbeitet wurden.|  
|FastLoadOptions|String|Eine Auflistung von Optionen für schnelles Laden. Die Optionen für schnelles Laden beinhalten das Sperren von Tabellen und die Überprüfung von Einschränkungen. Sie können eines, beides oder keines von beiden angeben. Diese Eigenschaft entspricht der OLE DB-IRowsetFastLoad-Eigenschaft **SSPROP_FASTLOADOPTIONS** und akzeptiert Zeichenfolgenoptionen wie z.B. **CHECK_CONSTRAINTS** und **TABLOCK**.<br /><br /> Hinweis: Einige Optionen für diese Eigenschaft sind nicht im **Ziel-Editor für Excel**verfügbar, können jedoch mit dem **erweiterten Editor**festgelegt werden.|  
|OpenRowset|String|Wenn AccessMode **OpenRowset**ist, wird hier der Name der Tabelle oder der Sicht angegeben, auf die das OLE DB-Ziel zugreift.|  
|OpenRowsetVariable|String|Wenn AccessMode **OpenRowset from Variable**ist, wird hier der Name der Variablen angegeben, die den Namen der Tabelle oder Sicht enthält, auf die das OLE DB-Ziel zugreift.|  
|SqlCommand|String|Wenn AccessMode **SQL Command**ist, wird hier die Transact-SQL-Anweisung angegeben, mit der das OLE DB-Ziel die Zielspalten für die Daten angibt.|  
  
 Die Eingabe und die Eingabespalten des OLE DB-Ziels verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
