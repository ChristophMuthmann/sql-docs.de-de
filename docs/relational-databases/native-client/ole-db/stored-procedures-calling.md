---
title: Aufrufen einer gespeicherten Prozedur (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [SQL Server Native Client], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: 8e5738e5-4bbe-4f34-bd69-0c0633290bdd
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 901bea0996dd993f8238df9c73301f2cc874f65e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stored-procedures---calling"></a>Gespeicherte Prozeduren - aufrufen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Eine gespeicherte Prozedur kann 0 oder mehr Parameter haben. Sie kann auch einen Wert zurückgeben: Bei Verwendung der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter Parameter an eine gespeicherte Prozedur als übergeben werden können:  
  
-   Durch Hartcodierung des Datenwerts  
  
-   Durch Verwendung einer Parametermarkierung (?) zum Angeben von Parametern, Binden einer Programmvariablen an die Parametermarkierung und Einfügen des Datenwerts in die Programmvariable  
  
> [!NOTE]  
>  Wenn gespeicherte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Prozeduren, die benannte Parameter verwenden, mit OLE DB aufgerufen werden, müssen die Parameternamen mit dem Zeichen "@" beginnen. Dies ist eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-spezifische Einschränkung. Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter erzwingt diese Einschränkung strenger als MDAC.  
  
 Unterstützung von Parametern, die **ICommandWithParameters** Schnittstelle ist für das Command-Objekt verfügbar gemacht werden. Um Parameter zu verwenden, beschreibt der Consumer die Parameter an den Anbieter zunächst durch Aufrufen der **ICommandWithParameters:: SetParameterInfo** Methode (oder optional eine aufrufanweisung, die aufruft vorbereitet der **GetParameterInfo** Methode). Der Consumer erstellt dann einen Accessor, der die Struktur eines Puffers angibt und Parameterwerte in diesen Puffer einfügt. Schließlich übergibt er das Handle des Accessors und einen Zeiger auf den Puffer an **Execute**. Klicken Sie auf spätere Aufrufe an **Execute**, fügt der Consumer neue Parameterwerte in den Puffer ein und ruft **Execute** mit dem Accessor und Pufferzeiger auf.  
  
 Rufen Sie ein Befehl, der eine temporäre gespeicherte Prozedur mit Parametern aufruft muss zuerst **ICommandWithParameters:: SetParameterInfo** die Parameterinformationen zu definieren, bevor der Befehl erfolgreich vorbereitet werden kann. Der Grund dafür ist, dass der interne Name für eine temporär gespeicherte Prozedur anders lautet als der externe Name, der von einem Client verwendet wird. Zudem kann SQLOLEDB die Systemtabellen nicht abfragen, um die Parameterinformationen für eine temporär gespeicherte Prozedur zu ermitteln.  
  
 Der Parameterbindungsprozess umfasst folgende Schritte:  
  
1.  Geben Sie die Parameterinformationen in ein Array aus DBPARAMBINDINFO-Strukturen ein, also den Parameternamen, den anbieterspezifischen Namen für den Datentyp des Parameters oder einen standardmäßigen Datentypennamen usw. Jede Struktur im Array beschreibt einen Parameter. Dieses Array übergeben, die **SetParameterInfo** Methode.  
  
2.  Rufen Sie die **ICommandWithParameters:: SetParameterInfo** Methode, um Parameter an den Anbieter zu beschreiben. **SetParameterInfo** gibt den systemeigenen Datentyp jedes Parameters. **SetParameterInfo** Argumente sind:  
  
    -   Die Anzahl von Parametern, für die Typinformationen festzulegen sind  
  
    -   Ein Array aus Ordnungszahlen von Parametern, für die Typinformationen festzulegen sind  
  
    -   Ein Array aus DBPARAMBINDINFO-Strukturen  
  
3.  Erstellen Sie einen Parameteraccessor mithilfe der **IAccessor:: CreateAccessor** Befehl. Der Accessor gibt die Struktur eines Puffers an und fügt Parameterwerte in den Puffer ein. Die **CreateAccessor** Befehl erstellt einen Accessor aus einem Satz von Bindungen. Diese Bindungen werden vom Consumer mithilfe eines Arrays aus DBBINDING-Strukturen beschrieben. Jede Bindung ordnet dem Puffer des Consumers einen einzelnen Parameter zu und enthält Informationen wie z. B.:  
  
    -   Die Ordnungszahl des Parameters, auf den sich die Bindung bezieht  
  
    -   Die Angabe, was gebunden wird (der Datenwert, seine Länge und sein Status)  
  
    -   Den Offset im Puffer zu jedem dieser Teile  
  
    -   Die Länge und den Typ des Datenwerts, wie er im Puffer des Consumers vorhanden ist  
  
     Ein Accessor wird von seinem Handle identifiziert, das den Typ HACCESSOR aufweist. Dieses Handle wird zurückgegeben, durch die **CreateAccessor** Methode. Der Consumer muss aufrufen, sobald der Consumer einen Accessor, der **ReleaseAccessor** Methode zum Freigeben des Speichers enthält.  
  
     Wenn der Consumer Ruft eine Methode, z. B. **ICommand:: Execute**, übergibt er das Handle an einen Accessor und einen Zeiger auf den Puffer selbst. Der Anbieter verwendet diesen Accessor, um zu bestimmen, wie die im Puffer enthaltenen Daten übertragen werden.  
  
4.  Geben Sie die DBPARAMS-Struktur ein. Die consumervariablen, von welcher Eingabeparameter Eingabeparameterwerte übernommen und in der Output-Parameter die Werte geschrieben werden, zur Laufzeit zu übergeben sind **ICommand:: Execute** in der DBPARAMS-Struktur. Die DBPARAMS-Struktur beinhaltet drei Elemente:  
  
    -   Einen Zeiger auf den Puffer, aus dem der Anbieter Eingabeparameterdaten abruft und in den der Anbieter Ausgabeparameterdaten zurückgibt, gemäß den vom Accessorhandle angegebenen Bindungen  
  
    -   Die Anzahl von Parametersätzen im Puffer  
  
    -   Das in Schritt 3 erstellte Accessorhandle  
  
5.  Führen Sie den Befehl mit **ICommand:: Execute**.  
  
## <a name="methods-of-calling-a-stored-procedure"></a>Methoden zum Aufrufen einer gespeicherten Prozedur  
 Beim Ausführen einer gespeicherten Prozedur in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt die:  
  
-   ODBC CALL-Escapesequenz.  
  
-   RPC-Escapesequenz (Remote Procedure Call, Remoteprozeduraufruf)  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)]EXECUTE-Anweisung  
  
### <a name="odbc-call-escape-sequence"></a>ODBC CALL-Escapesequenz  
 Wenn Sie die Parameterinformationen kennen, rufen Sie **ICommandWithParameters:: SetParameterInfo** Methode, um die Parameter an den Anbieter zu beschreiben. Wenn hingegen die ODBC CALL-Syntax zum Aufrufen einer gespeicherten Prozedur verwendet wird, ruft der Anbieter eine Hilfsfunktion auf, um die Parameterinformationen der gespeicherten Prozedur zu ermitteln.  
  
 Wenn Sie nicht sicher sind, was die Parameterinformationen (Parametermetadaten) betrifft, empfiehlt sich die Verwendung der ODBC CALL-Syntax.  
  
 Die allgemeine Syntax zum Aufrufen einer Prozedur mit der ODBC CALL-Escapesequenz lautet:  
  
 {[**? =**]**Aufruf ***Procedure_name*[**(**[*Parameter*] [**,**[*Parameter*]]...** )**]}  
  
 Beispiel:  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>RPC-Escapesequenz  
 Die RPC-Escapesequenz ist der ODBC CALL-Syntax für den Aufruf einer gespeicherten Prozedur ähnlich. Wenn Sie die Prozedur mehrmals aufrufen müssen, ist die RPC-Escapesequenz von den drei Methoden zum Aufrufen einer gespeicherten Prozedur die leistungsfähigste.  
  
 Wenn die RPC-Escapesequenz zur Ausführung einer gespeicherten Prozedur verwendet wird, ruft der Anbieter keine Hilfsfunktion auf, um die Parameterinformationen zu ermitteln (wie dies bei der ODBC CALL-Syntax der Fall ist). Die RPC-Syntax ist einfacher als die ODBC CALL-Syntax, weshalb der Befehl schneller verarbeitet und die Leistung gesteigert wird. In diesem Fall müssen Sie die Parameterinformationen durch Ausführen von bereitstellen **ICommandWithParameters:: SetParameterInfo**.  
  
 Bei der RPC-Escapesequenz ist es erforderlich, einen Rückgabewert zu erhalten. Wenn die gespeicherte Prozedur keinen Wert zurückgibt, gibt der Server standardmäßig 0 (null) zurück. Außerdem können Sie keinen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Cursor für die gespeicherte Prozedur öffnen. Die gespeicherte Prozedur wird implizit vorbereitet und der Aufruf von **ICommandPrepare:: Prepare** schlägt fehl. Da es nicht möglich, einen RPC-Aufruf vorzubereiten können nicht Spaltenmetadaten abgefragt werden; IColumnsInfo:: GetColumnInfo und IColumnsRowset:: GetColumnsRowset geben db_e_notprepared zurück zurück.  
  
 Wenn Sie alle Parametermetadaten kennen, ist die RPC-Escapesequenz die empfohlene Methode für die Ausführung gespeicherter Prozeduren.  
  
 Es folgt ein Beispiel für eine RPC-Escapesequenz zum Aufrufen einer gespeicherten Prozedur:  
  
```  
{rpc SalesByCategory}  
```  
  
 Eine beispielanwendung, die eine RPC-Escapesequenz veranschaulicht, finden Sie unter [Ausführen einer gespeicherten Prozedur & #40; Mithilfe der RPC-Syntax & #41; und Verarbeiten von Return Rückgabecodes und Ausgabeparameter & #40; OLE DB & #41; ](../../../relational-databases/native-client-ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md).  
  
### <a name="transact-sql-execute-statement"></a>'EXECUTE'-Anweisung (Transact-SQL)  
 Die ODBC CALL-Escapesequenz und die RPC-Escapesequenz werden die bevorzugten Methoden zum Aufrufen einer gespeicherten Prozedur statt über das [EXECUTE](../../../t-sql/language-elements/execute-transact-sql.md) Anweisung. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter verwendet den RPC-Mechanismus von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] um die befehlsverarbeitung zu optimieren. Dieses RPC-Protokoll erhöht die Leistung, indem es einen Großteil der Parameterverarbeitung und Anweisungsauswertung auf dem Server überflüssig macht.  
  
 Dies ist ein Beispiel für die [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE** Anweisung:  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
