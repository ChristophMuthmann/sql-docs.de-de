---
title: SQLBrowseConnect-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f8117cc5238576f840cdb98f5ffaded38aed0d6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLBrowseConnect** unterstützt eine iterative Methode zum Erkennen und auflisten, die Attribute und Attributwerte, die Verbindung mit einer Datenquelle erforderlich sind. Jeder Aufruf von **SQLBrowseConnect** gibt aufeinander folgende Ebenen der Attribute und Attributwerte. Wenn alle Ebenen wurde aufgelistet, eine Verbindung mit der Datenquelle abgeschlossen ist und eine vollständige Verbindungszeichenfolge zurückgegebenes **SQLBrowseConnect**. Ein Rückgabecode von SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO gibt an, dass alle Verbindungsinformationen angegeben wurde und die Anwendung mit der Datenquelle verbunden ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
 *InConnectionString*  
 [Eingabe] Durchsuchen Sie die Verbindungszeichenfolge für die Anforderung (finden Sie unter "*InConnectionString* Argument" in "Kommentare").  
  
 *StringLength1*  
 [Eingabe] Länge des **InConnectionString* in Zeichen.  
  
 *OutConnectionString*  
 [Ausgabe] Zeiger auf einen Puffer aus Zeichen in der Verbindungszeichenfolge die Durchsuchen-Ergebnis zurück (finden Sie unter "*OutConnectionString* Argument" in "Kommentare").  
  
 Wenn *OutConnectionString* NULL ist, *StringLength2Ptr* gibt weiterhin zurück, die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) verfügbar, die in den Puffer zurückgegeben verweist *OutConnectionString*.  
  
 *Pufferlänge*  
 [Eingabe] Länge in Zeichen, d. h. von der **OutConnectionString* Puffer.  
  
 *StringLength2Ptr*  
 [Ausgabe] Die Gesamtanzahl der verfügbaren Zeichen ist (außer Null-Terminierung) im zurückzugebenden \* *OutConnectionString*. Wenn die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich ist *Pufferlänge*, die Verbindungszeichenfolge in \* *OutConnectionString* auf abgeschnitten * Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLBrowseConnect** gibt SQL_ERROR, SQL_SUCCESS_WITH_INFO oder SQL_NEED_DATA zurück, die einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und ein *Handle des Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLBrowseConnect** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *OutConnectionString* war nicht groß genug für die gesamte durchsuchen Verbindung Ergebniszeichenfolge zurückzugeben, damit die Zeichenfolge abgeschnitten wurden. Der Puffer **StringLength2Ptr* enthält die Länge der Ergebniszeichenfolge Verbindung ungekürzte durchsuchen. (Funktion gibt SQL_NEED_DATA zurück.)|  
|01 S 00|Ungültiges Attribut für Verbindungszeichenfolge|Ein ungültiges Attribut-Schlüsselwort in der Verbindungszeichenfolge der durchsuchen-Anforderung angegeben wurde (*InConnectionString*). (Funktion gibt SQL_NEED_DATA zurück.)<br /><br /> Ein Attribut-Schlüsselwort in der Verbindungszeichenfolge der durchsuchen-Anforderung angegeben wurde (*InConnectionString*), die gilt nicht für den aktuellen Verbindungsebene. (Funktion gibt SQL_NEED_DATA zurück.)|  
|01 S 02|Der Wert wurde geändert|Der Treiber nicht den angegebenen Wert, der die *ValuePtr* Argument in **SQLSetConnectAttr** und einen ähnlichen Wert ersetzt. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08001|Client kann keine Verbindung herstellen|Der Treiber konnte nicht zum Herstellen einer Verbindung mit der Datenquelle.|  
|08002|Name der Verbindung verwendet|(DM) die angegebene Verbindung wurde bereits zum Herstellen einer Verbindung mit einer Datenquelle verwendet, und die Verbindung geöffnet wurde.|  
|08004|Der Server wies die Verbindung|Die Datenquelle die Einrichtung der Verbindung Gründen abgelehnt Implementierung definiert.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und der Datenquelle, zu der der Treiber versucht hat, die Verbindung, konnte nicht vor der Verarbeitung für die Funktion abgeschlossen.|  
|28000|Ungültige Autorisierungsangabe|Der Bezeichner des Benutzers oder der autorisierungszeichenfolge oder beides entsprechend den Angaben in die Schaltfläche zum Durchsuchen, anfordern Verbindungszeichenfolge (*InConnectionString*), durch die Datenquelle definierten Einschränkungen verletzt.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber-Manager (DM) konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.<br /><br /> Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Ein asynchroner Vorgang abgebrochen wurde, durch den Aufruf [SQLCancelHandle Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md). Klicken Sie dann die ursprüngliche Funktion erneut auf aufgerufen wurde die *Verbindungshandle*.<br /><br /> Ein Vorgang wurde abgebrochen, durch den Aufruf **SQLCancelHandle** auf die *Verbindungshandle* aus einem anderen Thread in einer multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *Verbindungshandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) für Argument angegebene Wert *StringLength1* kleiner als 0 und nicht wurde SQL_NTS gleich.<br /><br /> (DM) für Argument angegebene Wert *Pufferlänge* war kleiner als 0.|  
|HY114|Verbindung Ebene asynchrone Ausführung unterstützt-Treiber nicht.|(DM) aktiviert die Anwendung den asynchronen Vorgang auf dem Verbindungshandle vor dem Herstellen der Verbindung. Allerdings unterstützt der Treiber nicht asynchronen Vorgang für Verbindungshandle.|  
|HYT00|Timeout abgelaufen|Das Timeout für die Anmeldung ist abgelaufen, bevor die Verbindung mit der Datenquelle abgeschlossen. Das Zeitlimit wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber, der angegebene Name der Datenquelle entspricht der Funktion nicht unterstützt.|  
|IM002|Datenquelle wurde nicht gefunden und kein Standardtreiber angegeben|(DM) die Datenquelle in der Verbindungszeichenfolge der durchsuchen-Anforderung angegebene Name (*InConnectionString*) wurde nicht gefunden, in die Systeminformationen noch gab es eine Standard-Treiber-Spezifikation.<br /><br /> (DM) ODBC-Quelle und Standard-Treiber Dateninformationen konnte nicht in die Systeminformationen gefunden werden.|  
|IM003|Angegebene Treiber konnte nicht geladen werden|(DM) der Treiber aufgeführt, die in der Angabe der Datenquelle in die Systeminformationen oder gemäß der **Treiber** Schlüsselwort wurde nicht gefunden oder konnte nicht in einem anderen Grund geladen werden.|  
|IM004|Des Treibers **SQLAllocHandle** auf SQL_HANDLE _ENV fehlgeschlagen|(DM) während der **SQLBrowseConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLAllocHandle** -Funktion mit einer *HandleType* SQL_HANDLE_ENV und der Treiber zurückgegebenen ein Fehler.|  
|IM005|Des Treibers **SQLAllocHandle** auf SQL_HANDLE_DBC auf Fehler|(DM) während der **SQLBrowseConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLAllocHandle** -Funktion mit einer *HandleType* SQL_HANDLE_DBC auf, und der Treiber zurückgegebenen ein Fehler.|  
|IM006|Des Treibers **SQLSetConnectAttr** fehlgeschlagen|(DM) während der **SQLBrowseConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLSetConnectAttr** -Funktion und der Treiber hat einen Fehler zurückgegeben.|  
|IM009|Kann nicht geladen werden Konvertierungs-DLL|Der Treiber konnte den Konvertierungs-DLL zu laden, die für die Datenquelle oder für die Verbindung angegeben wurde.|  
|IM010|Der Datenquellenname ist zu lang|(DM) wurde der Attributwert für das DSN-Schlüsselwort SQL_MAX_DSN_LENGTH Zeichen überschreitet.|  
|IM011|Der Treibername ist zu lang|(DM) der Attributwert für das DRIVER-Schlüsselwort wurde mehr als 255 Zeichen.|  
|IM012|Treiber-Schlüsselwort-Syntaxfehler|(DM) die Schlüsselwort-Wert-Paar für das DRIVER-Schlüsselwort enthalten einen Syntaxfehler.|  
|IM014|Der angegebene DSN enthält ein Architektur-Konflikt zwischen der Treiber und die Anwendung|(DM)-32-Bit-Anwendung wird einen DSN, Herstellen einer Verbindung mit einer 64-Bit-Treiber verwendet. oder umgekehrt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
|S1118|Asynchrone Benachrichtigung unterstützt-Treiber nicht.|Wenn der Treiber die asynchrone Benachrichtigung nicht unterstützt, kann nicht SQL_ATTR_ASYNC_DBC_EVENT oder SQL_ATTR_ASYNC_DBC_RETCODE_PTR festgelegt werden.|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString-Argument  
 Eine Verbindungszeichenfolge für Durchsuchen-Anforderung hat die folgende Syntax:  
  
 *Verbindungszeichenfolgen* :: = *Attribut*[;] &#124; *Attribut*; *Verbindung Stringattribute* :: = *Attribut-Schlüsselwort*=*Attribut / Wert-* &#124; Treiber [{}] =*Attribut / Wert-[*}]*Attribut-Schlüsselwort* :: = DSN &#124; UID &#124; PWD &#124; *-Treiber-definierten--Keywordattribute-Attributwert* :: = *Zeichen-Stringdriver-definierten-Attribut-Schlüsselwort* :: = *Bezeichner*  
  
 wobei *Zeichenfolge* wurde NULL oder mehr Zeichen; *Bezeichner* verfügt über eine oder mehrere Zeichen; *Attribut-Schlüsselwort* ist nicht beachtet werden soll; *Attribut / Wert-* möglicherweise Groß-/Kleinschreibung beachtet; und der Wert der **DSN** Schlüsselwort nicht ausschließlich aus Leerzeichen bestehen. Aufgrund der Zeichenfolge und Initialisierung Datei Grammatik, Schlüsselwörter und Attribut Verbindungswerte, die die Zeichen enthalten **[] {} (),? \*=! @** sollte vermieden werden. Aufgrund der Grammatik in die Systeminformationen, Schlüsselwörter und Namen von Datenquellen können den umgekehrten Schrägstrich enthalten (\\) Zeichen. Für einen ODBC-2. *x* Treiber, geschweifte Klammern sind erforderlich, um den Attributwert für das DRIVER-Schlüsselwort.  
  
 Wenn keine Schlüsselwörter in der Verbindungszeichenfolge der durchsuchen Anforderung wiederholt werden, verwendet der Treiber den zugeordneten Wert durch das erste Vorkommen des Schlüsselworts. Wenn die **DSN** und **Treiber** Schlüsselwörter in der gleichen Verbindungszeichenfolge für den Durchsuchen-Anforderung enthalten sind, die Treiber-Manager und Treiber verwenden, unabhängig davon, welche Schlüsselwort an erster Stelle steht.  
  
 Weitere Informationen dazu, wie eine Anwendung eine Datenquelle oder Treiber auswählt, finden Sie unter [Auswählen der Datenquelle oder Treiber](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString-Argument  
 Die Durchsuchen-Ergebnis-Verbindungszeichenfolge ist eine Liste der Verbindungsattribute. Ein Verbindungsattribut besteht aus einem Attribut-Schlüsselwort und einen entsprechenden Attributwert. Die Verbindungszeichenfolge der durchsuchen Ergebnis hat die folgende Syntax:  
  
 *Verbindungszeichenfolgen* :: = *Attribut*[;] &#124; *Attribut*; *Verbindung Stringattribute* :: = [\*]*Attribut-Schlüsselwort = Attribut-Valueattribute-Schlüsselwort* :: = *ODBC-Attribut-Schlüsselwort* &#124; *driver-defined-attribute-keywordODBC-attribute-keyword* = {UID &#124; PWD} [:*lokalisiert Bezeichner*]*-definierten-Attribut-Schlüsselwort Driver* :: = *Bezeichner*[:*lokalisiert-Bezeichner*]*Attribut / Wert-* :: = {*Wert Attributliste*} &#124;? (Die Klammern sind literal; sie werden vom Treiber zurückgegeben.) *Wert Attributliste* :: = *zechenfolgen* [:*lokalisierte Zeichenfolge*] &#124; *zechenfolgen* [:*lokalisierte Zeichenfolge*], *Attribut-Wert-Liste*  
  
 wobei *Zeichenfolge* und *lokalisierte Zeichenfolge* NULL oder mehr Zeichen lang sein; *Bezeichner* und *lokalisiert Bezeichner* haben Sie ein oder mehrere Zeichen; *Attribut-Schlüsselwort* ist nicht beachtet werden soll; und *Attribut / Wert-* möglicherweise Groß-/Kleinschreibung beachtet werden. Aufgrund der Verbindung Zeichenfolge und die Initialisierung Datei Grammatik, Schlüsselwörter, lokalisierte Bezeichner und Attributwerte zurück, die die Zeichen enthalten **[] {} (),? \*=! @** sollte vermieden werden. Aufgrund der Grammatik in die Systeminformationen, Schlüsselwörter und Namen von Datenquellen können den umgekehrten Schrägstrich enthalten (\\) Zeichen.  
  
 Die Verbindungszeichenfolgensyntax zum Durchsuchen von Ergebnis wird gemäß den folgenden semantischen Regeln verwendet:  
  
-   Wenn ein Sternchen (\*) vorangestellt ist ein *Attribut-Schlüsselwort*, die *Attribut* ist optional und kann ausgelassen werden, in dem nächsten Aufruf von **SQLBrowseConnect**.  
  
-   Die Attribut-Schlüsselwörter **UID** und **PWD** haben dieselbe Bedeutung wie definiert in **SQLDriverConnect**.  
  
-   Ein *-definierten-Attribut-Schlüsselwort Driver* benennt die Art des Attributs für den Attributwert angegeben werden kann. Angenommen, es möglicherweise **SERVER**, **Datenbank**, **HOST**, oder **DBMS**.  
  
-   *Schlüsselwörter für ODBC-Attribut* und *-Treiber-definierte-Attribut-Schlüsselwörter* enthalten eine lokalisierte oder benutzerfreundliche Version des Schlüsselworts. Dies kann von Anwendungen als Bezeichnung in einem Dialogfeld verwendet werden. Allerdings **UID**, **PWD**, oder die *Bezeichner* allein muss verwendet werden, wenn eine Zeichenfolge der durchsuchen-Anforderung an den Treiber übergeben.  
  
-   Der {*Wert Attributliste*} gilt eine Enumeration von tatsächlichen Werten für den entsprechenden *Attribut-Schlüsselwort*. Beachten Sie, dass die geschweiften Klammern ({}) eine Liste mit Auswahlmöglichkeiten nicht angegeben werden. Sie werden vom Treiber zurückgegeben. Es kann z. B. eine Liste von Servernamen oder eine Liste von Datenbanknamen verwendet werden.  
  
-   Wenn die *Attribut / Wert-* ist ein einzelnes Question Mark ("?"), ein einzelnen Wert entspricht der *Attribut-Schlüsselwort*. Z. B. UID = JohnS; PWD = Symbol.  
  
-   Jeder Aufruf von **SQLBrowseConnect** gibt nur die erforderlichen Informationen an die nächste Ebene des Verbindungsprozesses erfüllen. Der Treiber ordnet dem Verbindungshandle Zustandsinformationen, damit der Kontext immer bei jedem Aufruf bestimmt werden kann.  
  
## <a name="using-sqlbrowseconnect"></a>SQLBrowseConnect verwenden  
 **SQLBrowseConnect** erfordert eine zugeordnete Verbindung. Der Treiber-Manager lädt den Treiber, die angegeben wurde oder ab, der in der Verbindungszeichenfolge der anfänglichen durchsuchen Anforderung angegebene Datenquellenname entspricht. Informationen, wenn dies geschieht, finden Sie im Abschnitt "Kommentare" [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md). Der Treiber kann während der Suche nach Prozess eine Verbindung mit der Datenquelle herstellen. Wenn **SQLBrowseConnect** gibt SQL_ERROR zurück, ausstehende Verbindungen getrennt werden und die Verbindung zu einem nicht verbundenen Zustand zurückgegeben wird.  
  
> [!NOTE]  
>  **SQLBrowseConnect** Verbindungspooling nicht unterstützt. Wenn **SQLBrowseConnect** aufgerufen wird, während das Verbindungspooling aktiviert ist, SQLSTATE HY000 (Allgemeine Fehler) zurückgegeben.  
  
 Wenn **SQLBrowseConnect** wird aufgerufen, zum ersten Mal für eine Verbindung die Verbindungszeichenfolge der durchsuchen-Anforderung enthalten muss die **DSN** Schlüsselwort oder der **Treiber** Schlüsselwort. Wenn die Verbindungszeichenfolge der durchsuchen-Anforderung enthält die **DSN** Schlüsselwort, das der Treiber-Manager sucht nach einem entsprechenden datenquellenspezifikation in die Systeminformationen:  
  
-   Wenn der Treiber-Manager die entsprechenden datenquellenspezifikation findet, lädt er die zugehörige Treiber-DLL; der Treiber kann Informationen über die Datenquelle aus der Systeminformationen abrufen.  
  
-   Der Treiber-Manager die entsprechenden datenquellenspezifikation gefunden, sucht die Standard-datenquellenspezifikation und die zugehörige Treiber-DLL lädt; der Treiber kann Informationen über die Standarddatenquelle vom die Systeminformationen abzurufen. "DEFAULT" werden für den DSN an den Treiber übergeben.  
  
-   Wenn der Treiber-Manager die entsprechenden datenquellenspezifikation finden kann, und es keine Standard-datenquellenspezifikation ist, gibt SQL_ERROR mit SQLSTATE IM002 zurück (Datenquelle wurde nicht gefunden und kein Standardtreiber angegeben).  
  
 Wenn die Verbindungszeichenfolge der durchsuchen-Anforderung enthält die **Treiber** Schlüsselwort, das der Treiber-Manager lädt die angegebenen Treiber; es wird nicht versucht, eine Datenquelle in die Systeminformationen gesucht werden soll. Da die **Treiber** Schlüsselwort keine Informationen aus der Systeminformationen verwendet, der Treiber muss genügend Schlüsselwörter definieren, sodass ein Treiber eine Verbindung mit einer Datenquelle, die nur die Informationen in den Verbindungszeichenfolgen des suchen-Anforderung mit herstellen kann.  
  
 Bei jedem Aufruf **SQLBrowseConnect**, die Anwendung gibt die Werte des Attributs in der Verbindungszeichenfolge der durchsuchen-Anforderung an. In der Verbindungszeichenfolge der durchsuchen Ergebnis gibt der Treiber die aufeinander folgenden Ebenen der Attribute und Attributwerte; Es wird SQL_NEED_DATA zurückgegeben, als stehen Verbindungsattribute, die noch nicht in der Verbindungszeichenfolge der durchsuchen Anforderung aufgelistet wurden. Die Anwendung verwendet den Inhalt der Ergebniszeichenfolge Verbindung Durchsuchen zum Erstellen der Verbindungszeichenfolge des durchsuchen-Anforderung für den nächsten Aufruf von **SQLBrowseConnect**. Alle erforderlichen Attribute (die nicht durch ein Sternchen im Voraus den *OutConnectionString* Argument) enthalten sein müssen, in dem nächsten Aufruf von **SQLBrowseConnect**. Beachten Sie, dass die Anwendung den Inhalt des vorherigen durchsuchen Ergebnis Verbindungszeichenfolgen, beim Erstellen der Verbindungszeichenfolge der aktuellen durchsuchen Anforderung verwenden kann. Es kann nicht das heißt, verschiedene Werte für Attribute in der vorherigen Ebenen festgelegt festlegen.  
  
 Wenn alle Ebenen der Verbindung und die zugehörigen Attribute aufgelistet wurden, der Treiber gibt SQL_SUCCESS zurück, die Verbindung mit der Datenquelle abgeschlossen ist und eine vollständige Verbindungszeichenfolge wird an die Anwendung zurückgegeben. Die Verbindungszeichenfolge eignet sich zum Verwenden in Verbindung mit **SQLDriverConnect**, mit der SQL_DRIVER_NOPROMPT-Option, um eine andere Verbindung herzustellen. Die vollständige Verbindungszeichenfolge kann nicht verwendet werden, in einem weiteren Aufruf von **SQLBrowseConnect**jedoch; wenn **SQLBrowseConnect** erneut aufrufen würden, den gesamten Aufrufsequenz müsste wiederholt werden.  
  
 **SQLBrowseConnect** auch wird SQL_NEED_DATA zurückgegeben, wenn während des Prozesses durchsuchen; z. B. ungültigen Kennwort- oder eine Attribut-Schlüsselwort, die von der Anwendung bereitgestellte wiederherstellbare, nicht schwerwiegende Fehler aufgetreten sind. Wenn wird SQL_NEED_DATA zurückgegeben, und die Durchsuchen-Ergebnis-Verbindungszeichenfolge ist unverändert, ein Fehler aufgetreten und die Anwendung aufrufen kann **SQLGetDiagRec** SQLSTATE durchsuchen-Time-Fehler zurückgegeben. Dies ermöglicht die Anwendung korrigieren das Attribut und die Schaltfläche zum Durchsuchen zu fortfahren.  
  
 Eine Anwendung kann den Prozess zum Durchsuchen jederzeit beenden, durch den Aufruf **SQLDisconnect**. Der Treiber alle ausstehenden Verbindungen beendet und die Verbindung zu einem nicht verbundenen Zustand zurückgegeben.  
  
 Aktivierte asynchrone Vorgänge auf dem Verbindungshandle **SQLBrowseConnect** möglicherweise auch SQL_STILL_EXECUTING zurück. Wenn SQL_NEED_DATA zurückgegeben wird, muss eine Anwendung verwenden **SQLDisconnect** zum Abbrechen des Prozesses durchsuchen. Wenn **SQLBrowseConnect** gibt SQL_STILL_EXECUTING, eine Anwendung die zu verwendende **SQLCancelHandle** Abbrechen des Vorgangs ausgeführt. Aufrufen von **SQLCancelHandle** , nachdem die Funktion gibt SQL_NEED_DATA hat keine Auswirkungen.  
  
 Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md).  
  
 Wenn ein Treiber unterstützt **SQLBrowseConnect**, in die Systeminformationen für den Treiber im Abschnitt Schlüsselwort Driver darf die **ConnectFunctions** Schlüsselwort mit dem dritten Zeichen legen Sie auf "Y" zurück.  
  
## <a name="code-example"></a>Codebeispiel  
  
> [!NOTE]  
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben `Trusted_Connection=yes` anstelle von Benutzerinformationen-ID und Kennwort in der Verbindungszeichenfolge angegeben.  
  
 Im folgenden Beispiel ruft die Anwendung **SQLBrowseConnect** wiederholt. Jedes Mal **SQLBrowseConnect** wird SQL_NEED_DATA zurückgegeben, übergibt Back Informationen zu den Daten, die er in muss \* *OutConnectionString*. Die Anwendung übergibt *OutConnectionString* an die Routine **GetUserInput** (nicht dargestellt). **GetUserInput** die Informationen analysiert, builds und zeigt ein Dialogfeld an und gibt die vom Benutzer eingegebene Informationen \* *InConnectionString*. Die Anwendung übergibt die Informationen des Benutzers an den Treiber in den nächsten Aufruf von **SQLBrowseConnect**. Nachdem die Anwendung alle erforderlichen Informationen für den Treiber für die Verbindung mit der Datenquelle bereitgestellt hat **SQLBrowseConnect** gibt SQL_SUCCESS zurück, und die Anwendung wird fortgesetzt.  
  
 Ein ausführlicheres Beispiel für das Herstellen einer Verbindung mit einer SQL Server-Treiber aufrufen **SQLBrowseConnect**, finden Sie unter [Durchsuchen von SQL Server-Beispiel](../../../odbc/reference/develop-app/sql-server-browsing-example.md).  
  
 Um auf die Daten der Quelle Sales zugreifen könnte z. B. die folgenden Aktionen ausgeführt. Zunächst die Anwendung übergibt die folgenden Zeichenfolge, die **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 Der Treiber-Manager lädt den Treiber die Datenquelle Sales zugeordnet. Er ruft dann des Treibers **SQLBrowseConnect** -Funktion mit den gleichen Argumenten, die sie von der Anwendung empfangen. Gibt die folgende Zeichenfolge in der Treiber **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 Die Anwendung übergibt diese Zeichenfolge seine **GetUserInput** Routine, die ein Dialogfeld builds fordert den Benutzer den roten, blauen oder grünen Server auswählen und eine Benutzer-ID und das Kennwort eingeben. Die Routine übergibt die folgende benutzerdefinierten Informationen zurück, \* *InConnectionString*, die an die Anwendung übergibt **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** verwendet diese Informationen zum Verbinden mit dem roten Server als Smith mit dem Kennwort-Symbol, und gibt anschließend die folgende Zeichenfolge in **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 Die Anwendung übergibt diese Zeichenfolge seine **GetUserInput** Routine, die ein Dialogfeld builds fordert den Benutzer auf eine Datenbank auszuwählen. Der Benutzer wählt Empdata und die Anwendung ruft **SQLBrowseConnect** ein letztes Mal mit dieser Zeichenfolge:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 Dies ist das letzte Stück Informationen, die der Treiber für die Verbindung mit der Datenquelle benötigt. **SQLBrowseConnect** gibt SQL_SUCCESS zurück, und **OutConnectionString* vervollständigte Verbindungszeichenfolge enthält:  
  
```  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Zuordnen eines Verbindungshandles|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle|[SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Trennen von einer Datenquelle|[SQLDisconnect-Funktion](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle mit einer Zeichenfolge oder ein Dialogfeld Verbindungsdialogfeld|[SQLDriverConnect-Funktion](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Zurückgeben von Beschreibungen der Treiber-Attribute|[SQLDrivers-Funktion](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Freigeben eines Verbindungshandles|[SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
