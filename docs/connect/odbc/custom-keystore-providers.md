---
title: Benutzerdefinierte-Schlüsselspeicher-Anbieter | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
caps.latest.revision: 1
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: ea1e976d4759951c229aa528c18436dbddcfa889
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="custom-keystore-providers"></a>Benutzerdefinierte-Schlüsselspeicher-Anbieter
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Übersicht

Die Funktion "Spalte Verschlüsselung" von SQL Server 2016 erfordert, dass der verschlüsselte Spaltenverschlüsselungsschlüssel (ECEKs) auf dem Server gespeichert werden durch den Client abgerufen und um Spaltenverschlüsselungsschlüssel (CEKs) dann entschlüsselt werden, um Zugriff auf die Daten in verschlüsselten Spalten gespeichert. ECEKs von Spaltenhauptschlüsseln (CMKs) verschlüsselt werden und die Sicherheit des CMK ist wichtig, die Sicherheit der spaltenverschlüsselung. Daher sollten die CMK an einem sicheren Ort gespeichert werden. eine Spalte Keystore Verschlüsselungsanbieter dient zur Verfügung zu stellen eine Schnittstelle, damit diese sicheren Zugriff auf die ODBC-Treiber kann CMKs gespeichert. Für Benutzer mit ihren eigenen sichere Speicherung bietet die benutzerdefinierte Keystore Provider-Schnittstelle ein Framework für die Implementierung Zugriff zum Sichern von Speicherung von den CMK für den ODBC-Treiber, die zum Ausführen der CEK Ver- und Entschlüsselung verwendet werden kann.

Jede Schlüsselspeicheranbieter enthält und verwaltet eine oder mehrere CMKs, der durch Schlüsselpfade - Zeichenfolgen in einem Format identifiziert werden, die vom Anbieter definierten. Hierzu kann zusammen mit der Verschlüsselungsalgorithmus, der auch eine Zeichenfolge, die vom Anbieter definierten verwendet werden, die einen CEK-Verschlüsselung und die Entschlüsselung des ein ECEK ausführen. Der Algorithmus, zusammen mit den ECEK und den Namen des Anbieters an, in die Datenbank verschlüsselungsmetadaten gespeichert; finden Sie unter [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) und [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) für Weitere Informationen. Daher sind die beiden grundlegenden Vorgänge schlüsselverwaltung:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

in dem die `CEKeystoreProvider_name` dient zum Identifizieren der bestimmten Spalte Verschlüsselung-Schlüsselspeicheranbieter (CEKeystoreProvider), und die anderen Argumente werden von der CEKeystoreProvider zum Verschlüsseln/Entschlüsseln des CEK (E) verwendet. Den Namen und die Schlüsselpfad werden durch die CMK-Metadaten bereitgestellt, während dem Algorithmus und dem ECEK Wert durch die CEK-Metadaten bereitgestellt werden. Mehrere Schlüsselspeicher-Anbieter können zusammen mit der Standardeinstellung integrierte Anbieter vorhanden sein. Beim Ausführen eines Vorgangs, das CEK erfordert, wird der Treiber verwendet den CMK-Metadaten zum Suchen der entsprechenden Schlüsselspeicheranbieter nach Namen und führt seine Entschlüsselungsvorgang, der als ausgedrückt werden kann:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

Obwohl der Treiber nicht erforderlich, verschlüsseln CEKs aufweist, müssen möglicherweise ein Verwaltungstool, um Vorgänge wie z. B. CMK erstellen und Rotieren implementieren; Dies erfordert die Umkehroperation zum Ausführen:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>CEKeyStoreProvider-Schnittstelle

Dieses Dokument beschreibt ausführlich das CEKeyStoreProvider-Schnittstelle. Ein Schlüsselspeicheranbieter implementiert diese Schnittstelle kann von Microsoft ODBC Driver für SQL Server verwendet werden. Dieses Handbuch können CEKeyStoreProvider Implementierer weiterentwickeln, indem Sie den Treiber benutzerdefinierte-Schlüsselspeicher-Anbieter verwendet werden kann.

Eine Anbieterbibliothek Keystore ("Anbieterbibliothek") ist eine Dynamic Link Library die vom ODBC-Treiber geladen werden kann und einen oder mehrere Schlüsselspeicher-Anbieter enthält. Das Symbol `CEKeystoreProvider` muss von einem Anbieterbibliothek exportiert werden, und die Adresse ein mit Null endendes Array von Zeigern auf `CEKeystoreProvider` Strukturen, eine für jede Schlüsselspeicheranbieter innerhalb der Bibliothek.

Ein `CEKeystoreProvider` Struktur definiert die Einstiegspunkte für einen einzelnen Schlüsselspeicheranbieter:

```
typedef struct CEKeystoreProvider {
    wchar_t *Name;
    int (*Init)(CEKEYSTORECONTEXT *ctx, errFunc *onError);
    int (*Read)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int *len);
    int (*Write)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len);
    int (*DecryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *ecek,
                        unsigned short ecekLen,
                        unsigned char **cekOut,
                        unsigned short *cekLen);
    int (*EncryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *cek,
                        unsigned short cekLen,
                        unsigned char **ecekOut,
                        unsigned short *ecekLen);
    void (*Free)();
} CEKEYSTOREPROVIDER;
```

|Feldname|Description|
|:--|:--|
|`Name`|Der Name des der Schlüsselspeicheranbieter. Es darf nicht identisch mit anderen Schlüsselspeicheranbieter, zuvor geladen wird, vom Treiber oder in dieser Bibliothek vorhanden sein. NULL-terminierte, wide-Zeichen * Zeichenfolge.|
|`Init`|Die Initialisierungsfunktion. Wenn eine Initialisierungsfunktion nicht erforderlich ist, kann dieses Feld null sein.|
|`Read`|Anbieter read-Funktion. Kann ggf. nicht null sein.|
|`Write`|Provider Write-Funktion. Erforderlich, wenn ein Lesevorgang nicht null ist. Kann ggf. nicht null sein.|
|`DecryptCEK`|ECEK Entschlüsselung-Funktion. Diese Funktion ist der Grund für einen Schlüsselspeicheranbieter vorhanden und darf nicht null sein.|
|`EncryptCEK`|CEK Verschlüsselung-Funktion. Der Treiber wird diese Funktion nicht aufgerufen, aber es dient für den programmgesteuerten Zugriff auf ECEK Erstellung von schlüsselverwaltungstools. Kann ggf. nicht null sein.|
|`Free`|Beendigungsfunktion. Kann ggf. nicht null sein.|

Mit Ausnahme von frei, die Funktionen in dieser Schnittstelle, die alle verfügen über ein Paar von Parametern, **Ctx** und **OnError**. Die erste gibt den Kontext, in dem die Funktion aufgerufen wird, während Letzteres, zur Meldung von Fehlern verwendet wird. Finden Sie unter [Kontexten](#context-association) und [Fehlerbehandlung](#error-handling) unten für Weitere Informationen.

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
Platzhaltername für einen Anbieter definierte Initialisierungsfunktion. Der Treiber ruft diese Funktion einmal ein, nachdem ein Anbieter geladen wurde, aber vor dem ersten Zeit, die sie zum Ausführen von ECEK Entschlüsselung oder Read()/Write() benötigt anfordert. Verwenden Sie diese Funktion, um die Initialisierung auszuführen, die benötigten. 

|Argument|Description|
|:--|:--|
|`ctx`|[Eingabe] Der Vorgangskontext.|
|`onError`|[Eingabe] Fehlerberichterstattung Funktion.|
|`Return Value`|Zurückgeben Sie ungleich NULL wird Erfolg oder 0 (null), um einen Fehler anzuzeigen.|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

Platzhaltername für eine Kommunikation anbieterdefinierter-Funktion. Der Treiber ruft diese Funktion auf, wenn die Anwendung, die zum Lesen von Daten von einem (zuvor geschriebenen-in) Anbieter über das Verbindungsattribut SQL_COPT_SS_CEKEYSTOREDATA ermöglicht der Anwendung, lesen beliebige Daten vom Anbieter anfordert. Finden Sie unter [bei der Kommunikation mit dem Schlüsselspeicher-Anbieter](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) für Weitere Informationen.

|Argument|Description|
|:--|:--|
|`ctx`|[Eingabe] Der Vorgangskontext.|
|`onError`|[Eingabe] Fehlerberichterstattung Funktion.|
|`data`|[Ausgabe] Ein Zeiger auf einen Puffer, in dem der Anbieter von der Anwendung zu lesenden Daten schreibt. Dies entspricht dem Feld "Daten" der CEKEYSTOREDATA-Struktur.|
|`len`|[InOut] Zeiger auf einen Längenwert; Bei der Eingabe, ist dies die maximale Länge des Datenpuffers und der Anbieter wird nicht geschrieben werden mehr als * Len Bytes darauf. Nach der Rückgabe der Anbieter aktualisieren sollten * Len mit der Anzahl der tatsächlich geschriebenen Bytes.|
|`Return Value`|Zurückgeben Sie ungleich NULL wird Erfolg oder 0 (null), um einen Fehler anzuzeigen.|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
Platzhaltername für eine Kommunikation anbieterdefinierter-Funktion. Der Treiber ruft diese Funktion auf, wenn die Anwendung anfordert, um Daten zu einem Anbieter das Verbindungsattribut SQL_COPT_SS_CEKEYSTOREDATA verwenden, die die Anwendung, Schreiben beliebige Daten an den Anbieter zu schreiben. Finden Sie unter [bei der Kommunikation mit dem Schlüsselspeicher-Anbieter](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) für Weitere Informationen.

|Argument|Description|
|:--|:--|
|`ctx`|[Eingabe] Der Vorgangskontext.|
|`onError`|[Eingabe] Fehlerberichterstattung Funktion.|
|`data`|[Eingabe] Ein Zeiger auf einen Puffer mit den Daten für den Anbieter zum Lesen. Dies entspricht dem Feld "Daten" der CEKEYSTOREDATA-Struktur. Der Anbieter muss nicht mehr als Len Bytes dieser Puffer gelesen werden.|
|`len`|[Eingabe] Die Anzahl der Bytes in den Daten verfügbar. Dies entspricht dem DataSize-Feld der CEKEYSTOREDATA-Struktur.|
|`Return Value`|Zurückgeben Sie ungleich NULL wird Erfolg oder 0 (null), um einen Fehler anzuzeigen.|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
Platzhaltername für einen Anbieter definierte ECEK Entschlüsselung-Funktion. Der Treiber ruft diese Funktion, um eine ECEK verschlüsselt, die durch einen CMK, die diesem Anbieter zugeordnet sind, in einen CEK zu entschlüsseln.

|Argument|Description|
|:--|:--|
|`ctx`|[Eingabe] Der Vorgangskontext.|
|`onError`|[Eingabe] Fehlerberichterstattung Funktion.|
|`keyPath`|[Eingabe] Der Wert, der die [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) Metadatenattribut für den CMK auf den angegebenen ECEK verweist. NULL-terminierte wide-Zeichen * Zeichenfolge. Dies dient zum Identifizieren eines CMK von diesem Anbieter behandelt.|
|`alg`|[Eingabe] Der Wert, der die [Algorithmus](../../t-sql/statements/create-column-encryption-key-transact-sql.md) Metadatenattribut für den angegebenen ECEK. NULL-terminierte wide-Zeichen * Zeichenfolge. Dies dient als den Verschlüsselungsalgorithmus zum Verschlüsseln von bestimmten ECEK zu identifizieren.|
|`ecek`|[Eingabe] Ein Zeiger auf die ECEK entschlüsselt werden.|
|`ecekLen`|[Eingabe] Länge der ECEK.|
|`cekOut`|[Ausgabe] Der Anbieter muss genügend Arbeitsspeicher für den entschlüsselten ECEK und seine Adresse in der Zeiger verweist, CekOut zu schreiben. Es muss möglich sein, diese Block der using-Arbeitsspeicher freigeben der [LocalAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366730(v=vs.85).aspx) (Windows) oder frei (Linux/Mac)-Funktion. Der Anbieter so festlegen, war keine "Erinnerung" zugeordneten aufgrund eines Fehlers oder anderweitig, * CekOut auf einen null-Zeiger.|
|`cekLen`|[Ausgabe] Der Anbieter muss an die Adresse, die auf CekLen zeigt die Länge der entschlüsselten ECEK, die sie in geschrieben wurde schreiben ** CekOut.|
|`Return Value`|Zurückgeben Sie ungleich NULL wird Erfolg oder 0 (null), um einen Fehler anzuzeigen.|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
Platzhaltername für eine Funktion der anbieterdefinierter CEK-Verschlüsselung. Der Treiber nicht mit dieser Funktion wird noch seine Funktionalität über die ODBC-Schnittstelle verfügbar zu machen, aber es dient für den programmgesteuerten Zugriff auf ECEK Erstellung von schlüsselverwaltungstools.

|Argument|Description|
|:--|:--|
|`ctx`|[Eingabe] Der Vorgangskontext.|
|`onError`|[Eingabe] Fehlerberichterstattung Funktion.|
|`keyPath`|[Eingabe] Der Wert, der die [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) Metadatenattribut für den CMK auf den angegebenen ECEK verweist. NULL-terminierte wide-Zeichen * Zeichenfolge. Dies dient zum Identifizieren eines CMK von diesem Anbieter behandelt.|
|`alg`|[Eingabe] Der Wert, der die [Algorithmus](../../t-sql/statements/create-column-encryption-key-transact-sql.md) Metadatenattribut für den angegebenen ECEK. NULL-terminierte wide-Zeichen * Zeichenfolge. Dies dient als den Verschlüsselungsalgorithmus zum Verschlüsseln von bestimmten ECEK zu identifizieren.|
|`cek`|[Eingabe] Ein Zeiger auf den CEK verschlüsselt werden.|
|`cekLen`|[Eingabe] Die Länge des CEK.|
|`ecekOut`|[Ausgabe] Der Anbieter muss genügend Arbeitsspeicher für den verschlüsselten CEK und seine Adresse in der Zeiger verweist, EcekOut zu schreiben. Es muss möglich sein, diese Block der using-Arbeitsspeicher freigeben der [LocalAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366730(v=vs.85).aspx) (Windows) oder frei (Linux/Mac)-Funktion. Der Anbieter so festlegen, war keine "Erinnerung" zugeordneten aufgrund eines Fehlers oder anderweitig, * EcekOut auf einen null-Zeiger.|
|`ecekLen`|[Ausgabe] Der Anbieter muss an die Adresse, die auf EcekLen zeigt die Länge des verschlüsselten CEK, die sie in geschrieben wurde schreiben ** EcekOut.|
|`Return Value`|Zurückgeben Sie ungleich NULL wird Erfolg oder 0 (null), um einen Fehler anzuzeigen.|

```
void (*Free)();
```
Platzhaltername für einen Anbieter definierte Beendigungsfunktion. Der Treiber kann diese Funktion bei normaler Beendigung des Prozesses aufgerufen werden.

> [!NOTE]
> *Breitzeichen-Zeichenfolgen sind 2-Byte-Zeichen (UTF-16) aufgrund wie Sie SQL Server speichert.*


### <a name="error-handling"></a>Fehlerbehandlung

Als Fehler während der Verarbeitung eines Anbieters auftreten können, wird ein Mechanismus zum Melden von Fehlern zurück an den Treiber in spezifischere Details als eine boolesche Erfolg/Fehler zuzulassen bereitgestellt. Viele der Funktionen haben ein Paar von Parametern, **Ctx** und **OnError**, die für diesen Zweck zusätzlich zu den Erfolg/Fehler-Rückgabewert zusammen verwendet werden.

Die **Ctx** Parameter identifiziert den Kontext, in dem ein Anbietervorgang auftritt.

Die **OnError** Parameter verweist auf eine Funktion-Fehlerberichterstattung mit dem folgenden Prototyp:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|Argument|Description|
|:--|:--|
|`ctx`|[Eingabe] Der Kontext, der auf den Fehler zu melden.|
|`msg`|[Eingabe] Die Fehlermeldung zu Bericht. NULL-terminierte Breitzeichen-Zeichenfolge. Damit parametrisierte Informationen vorhanden sein können, kann diese Zeichenfolge einfügen Formatieren von Sequenzen des Formulars vom akzeptiert enthalten die [FormatMessage](https://msdn.microsoft.com/library/windows/desktop/ms679351(v=vs.85).aspx) Funktion. Erweiterte Funktionalität kann durch diesen Parameter angegeben werden, wie unten beschrieben.|
|...|[Eingabe] Zusätzliche Variadic-Parameter, die Formatbezeichner im msg, entsprechend anpassen.|

Um melden kann, wenn ein Fehler aufgetreten ist, wird vom Treiber und eine Fehlermeldung mit optionalen zusätzlichen Parametern darin formatiert werden der Anbieter Aufrufe OnError, die Angabe des Kontextparameters an die anbieterfunktion übergeben. Der Anbieter kann diese Funktion mehrmals aufrufen, mehrere Fehler innerhalb einer Anbieter-Funktionsaufruf fortlaufend zu übermitteln. Beispiel:

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


Die `msg` Parameter ist in der Regel eine Breitzeichen-Zeichenfolge, aber zusätzliche Erweiterungen sind verfügbar:

Mithilfe einer der vordefinierten spezielle Werte mit dem Makro IDS_MSG generische Fehlermeldungen, die bereits vorhandenen und in einer Form aussuchen, im Treiber kann verwendet werden. Wenn ein Anbieter wird nicht belegt werden, z. B. die `IDS_S1_001` "Speicherbelegungsfehlers" Nachricht verwendet werden kann:

`onError(ctx, IDS_MSG(IDS_S1_001));`

Für den Fehler vom Treiber anerkannt zu werden muss die anbieterfunktion Fehler zurückgeben. Wenn dies im Rahmen einer ODBC-Vorgang ausgeführt wird, werden die bereitgestellte Fehler zugegriffen werden kann, für die Verbindung oder Anweisung Handle über ODBC-Diagnose der Standardmechanismus sein (`SQLError`, `SQLGetDiagRec`, und `SQLGetDiagField`).


### <a name="context-association"></a>Kontext-Zuordnung

Die `CEKEYSTORECONTEXT` -Struktur, zusätzlich zur Bereitstellung von Kontext für den Fehlerrückruf kann auch zum Erstellen der ODBC-Kontext zu ermitteln, in dem ein Anbietervorgang ausgeführt wird. Dies ermöglicht einen Anbieter z. B. Zuordnen von Daten zu jedem dieser Kontexte zum Implementieren von pro-Verbindungskonfiguration. Zu diesem Zweck enthält die Struktur 3 nicht transparenten Zeiger, die für den Kontext Umgebung, Verbindungs- und -Anweisung:

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```
|Feld|Description|
|:--|:--|
|`envCtx`|Umgebungskontext.|
|`dbcCtx`|Der Verbindungskontext.|
|`stmtCtx`|Kontext der Anweisung.|

Jedes dieser Kontexte wird ein nicht transparenter Wert, der beim nicht identisch mit dem entsprechenden ODBC-Handle und als eindeutiger Bezeichner für das Handle verwendet werden kann: Wenn behandeln *X* bezieht sich auf Kontextwert *Y*, klicken Sie dann keine andere Umgebung, Verbindung oder Anweisung Handles die gleichzeitig zur gleichen Zeit wie vorhandenen *X* müssen als Kontextwert *Y*, und keine anderen Kontextwerte zugeordnet werden behandeln *X*. Kontextwert in der Struktur ist null, wenn der Anbietervorgang wird erreicht, verfügt nicht über einem bestimmten Handle-Kontext (z. B. SQLSetConnectAttr Aufrufe zu laden und die Konfiguration von Anbietern, in denen keine Anweisungshandle vorhanden ist) den entsprechenden.


## <a name="example"></a>Beispiel

### <a name="keystore-provider"></a>Schlüsselspeicheranbieter

Der folgende Code ist ein Beispiel für eine minimale Schlüsselspeicher-Anbieter-Implementierung.

```
/* Custom Keystore Provider Example

Windows:   compile with cl MyKSP.c /LD /MD /link /out:MyKSP.dll
Linux/Mac: compile with gcc -fshort-wchar -fPIC -o MyKSP.so -shared MyKSP.c

 */

#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#endif

#include <stdlib.h>
#include <sqltypes.h>
#include "msodbcsql.h"
#include <sql.h>
#include <sqlext.h>

int __stdcall KeystoreInit(CEKEYSTORECONTEXT *ctx, errFunc *onError) {
    printf("KSP Init() function called\n");
    return 1;
}

static unsigned char *g_encryptKey;
static unsigned int g_encryptKeyLen;

int __stdcall KeystoreWrite(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len) {
    printf("KSP Write() function called (%d bytes)\n", len);
    if (len) {
        if (g_encryptKey)
            free(g_encryptKey);
        g_encryptKey = malloc(len);
        if (!g_encryptKey) {
            onError(ctx, L"Memory Allocation Error");
            return 0;
        }
        memcpy(g_encryptKey, data, len);
        g_encryptKeyLen = len;
    }
    return 1;
}

// Very simple "encryption" scheme - rotating XOR with the key
int __stdcall KeystoreDecrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg,
    unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen) {
    unsigned int i;
    printf("KSP Decrypt() function called (keypath=%S alg=%S ecekLen=%u)\n", keyPath, alg, ecekLen);
    if (wcscmp(keyPath, L"TheOneAndOnlyKey")) {
        onError(ctx, L"Invalid key path");
        return 0;
    }
    if (wcscmp(alg, L"none")) {
        onError(ctx, L"Invalid algorithm");
        return 0;
    }
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
#ifndef _WIN32
    *cekOut = malloc(ecekLen);
#else
    *cekOut = LocalAlloc(LMEM_FIXED, ecekLen);
#endif
    if (!*cekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *cekLen = ecekLen;
    for (i = 0; i < ecekLen; i++)
        (*cekOut)[i] = ecek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

// Note that in the provider interface, this function would be referenced via the CEKEYSTOREPROVIDER
// structure. However, that does not preclude keystore providers from exporting their own functions,
// as illustrated by this example where the encryption is performed via a separate function (with a
// different prototype than the one in the KSP interface.)
#ifdef _WIN32
__declspec(dllexport)
#endif
int KeystoreEncrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError,
    unsigned char *cek, unsigned short cekLen,
    unsigned char **ecekOut, unsigned short *ecekLen) {
    unsigned int i;
    printf("KSP Encrypt() function called (cekLen=%u)\n", cekLen);
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
    *ecekOut = malloc(cekLen);
    if (!*ecekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *ecekLen = cekLen;
    for (i = 0; i < cekLen; i++)
        (*ecekOut)[i] = cek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

CEKEYSTOREPROVIDER MyCustomKSPName_desc = {
    L"MyCustomKSPName",
    KeystoreInit,
    0,
    KeystoreWrite,
    KeystoreDecrypt,
    0
};

#ifdef _WIN32
__declspec(dllexport)
#endif
CEKEYSTOREPROVIDER *CEKeystoreProvider[] = {
    &MyCustomKSPName_desc,
    0
};
```

### <a name="odbc-application"></a>ODBC-Anwendung

Der folgende Code ist ein demoanwendung, die der oben genannten Schlüsselspeicheranbieter verwendet. Wenn er ausgeführt wird, stellen Sie sicher, dass die Anbieterbibliothek in demselben Verzeichnis wie die Binärdateien der Anwendung, und die Verbindungszeichenfolge gibt (oder einen DSN enthält) der `ColumnEncryption=Enabled` Einstellung.

```
/*
 Example application for demonstration of custom keystore provider usage

Windows:   compile with cl /MD kspapp.c /link odbc32.lib
Linux/Mac: compile with gcc -o kspapp -fshort-wchar kspapp.c -lodbc -ldl
 
 usage: kspapp connstr

 */

#define KSPNAME L"MyCustomKSPName"
#define PROV_ENCRYPT_KEY "JHKCWYT06N3RG98J0MBLG4E3"

#include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#include <dlfcn.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include "msodbcsql.h"

/* Convenience functions */

int checkRC(SQLRETURN rc, char *msg, int ret, SQLHANDLE h, SQLSMALLINT ht) {
    if (rc == SQL_ERROR) {
        fprintf(stderr, "Error occurred upon %s\n", msg);
        if (h) {
            SQLSMALLINT i = 0;
            SQLSMALLINT outlen = 0;
            char errmsg[1024];
            while ((rc = SQLGetDiagField(
                ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
                || rc == SQL_SUCCESS_WITH_INFO) {
                fprintf(stderr, "Err#%d: %s\n", i, errmsg);
            }
        }
        if (ret)
            exit(ret);
        return 0;
    }
    else if (rc == SQL_SUCCESS_WITH_INFO && h) {
        SQLSMALLINT i = 0;
        SQLSMALLINT outlen = 0;
        char errmsg[1024];
        printf("Success with info for %s:\n", msg);
        while ((rc = SQLGetDiagField(
            ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
            || rc == SQL_SUCCESS_WITH_INFO) {
            fprintf(stderr, "Msg#%d: %s\n", i, errmsg);
        }
    }
    return 1;
}

void postKspError(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...) {
    if (msg > (wchar_t*)65535)
        wprintf(L"Provider emitted message: %s\n", msg);
    else
        wprintf(L"Provider emitted message ID %d\n", msg);
}

int main(int argc, char **argv) {
    char sqlbuf[1024];
    SQLHENV env;
    SQLHDBC dbc;
    SQLHSTMT stmt;
    SQLRETURN rc;
    unsigned char CEK[32];
    unsigned char *ECEK;
    unsigned short ECEKlen;
#ifdef _WIN32
    HMODULE hProvLib;
#else
    void *hProvLib;
#endif
    CEKEYSTORECONTEXT ctx = {0};
    CEKEYSTOREPROVIDER **ppKsp, *pKsp;
    int(__stdcall *pEncryptCEK)(CEKEYSTORECONTEXT *, errFunc *, unsigned char *, unsigned short, unsigned char **, unsigned short *);
    int i;
    if (argc < 2) {
        fprintf(stderr, "usage: kspapp connstr\n");
        return 1;
    }

    /* Load the provider library */
#ifdef _WIN32
    if (!(hProvLib = LoadLibrary("MyKSP.dll"))) {
#else
    if (!(hProvLib = dlopen("./MyKSP.so", RTLD_NOW))) {
#endif
        fprintf(stderr, "Error loading KSP library\n");
        return 2;
    }
#ifdef _WIN32
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)GetProcAddress(hProvLib, "CEKeystoreProvider"))) {
#else
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)dlsym(hProvLib, "CEKeystoreProvider"))) {
#endif
        fprintf(stderr, "The export CEKeystoreProvider was not found in the KSP library\n");
        return 3;
    }
    while (pKsp = *ppKsp++) {
        if (!memcmp(KSPNAME, pKsp->Name, sizeof(KSPNAME)))
            goto FoundProv;
    }
    fprintf(stderr, "Could not find provider in the library\n");
    return 4;
FoundProv:
    if (pKsp->Init && !pKsp->Init(&ctx, postKspError)) {
        fprintf(stderr, "Could not initialize provider\n");
        return 5;
    }
#ifdef _WIN32
    if (!(pEncryptCEK = (LPVOID)GetProcAddress(hProvLib, "KeystoreEncrypt"))) {
#else
    if (!(pEncryptCEK = dlsym(hProvLib, "KeystoreEncrypt"))) {
#endif
        fprintf(stderr, "The export KeystoreEncrypt was not found in the KSP library\n");
        return 6;
    }
    if (!pKsp->Write) {
        fprintf(stderr, "Provider does not support configuration\n");
        return 7;
    }

    /* Configure the provider with the key */
    if (!pKsp->Write(&ctx, postKspError, PROV_ENCRYPT_KEY, strlen(PROV_ENCRYPT_KEY))) {
        fprintf(stderr, "Error writing to KSP\n");
        return 8;
    }

    /* Generate a CEK and encrypt it with the provider */
    srand(time(0) ^ getpid());
    for (i = 0; i < sizeof(CEK); i++)
        CEK[i] = rand();

    if (!pEncryptCEK(&ctx, postKspError, CEK, sizeof(CEK), &ECEK, &ECEKlen)) {
        fprintf(stderr, "Error encrypting CEK\n");
        return 9;
    }

    /* Connect to Server */
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &env);
    checkRC(rc, "allocating environment handle", 2, 0, 0);
    rc = SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);
    checkRC(rc, "setting ODBC version to 3.0", 3, env, SQL_HANDLE_ENV);
    rc = SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc);
    checkRC(rc, "allocating connection handle", 4, env, SQL_HANDLE_ENV);
    rc = SQLDriverConnect(dbc, 0, argv[1], strlen(argv[1]), NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    checkRC(rc, "connecting to data source", 5, dbc, SQL_HANDLE_DBC);
    rc = SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt);
    checkRC(rc, "allocating statement handle", 6, dbc, SQL_HANDLE_DBC);

    /* Create a CMK definition on the server */
    {
        static char cmkSql[] = "CREATE COLUMN MASTER KEY CustomCMK WITH ("
            "KEY_STORE_PROVIDER_NAME = 'MyCustomKSPName',"
            "KEY_PATH = 'TheOneAndOnlyKey')";
        printf("Create CMK: %s\n", cmkSql);
        SQLExecDirect(stmt, cmkSql, SQL_NTS);
    }

    /* Create a CEK definition on the server */
    {
        const char cekSqlBefore[] = "CREATE COLUMN ENCRYPTION KEY CustomCEK WITH VALUES ("
            "COLUMN_MASTER_KEY = CustomCMK,"
            "ALGORITHM = 'none',"
            "ENCRYPTED_VALUE = 0x";
        char *cekSql = malloc(sizeof(cekSqlBefore) + 2 * ECEKlen + 2); /* 1 for ')', 1 for null terminator */
        strcpy(cekSql, cekSqlBefore);
        for (i = 0; i < ECEKlen; i++)
            sprintf(cekSql + sizeof(cekSqlBefore) - 1 + 2 * i, "%02x", ECEK[i]);
        strcat(cekSql, ")");
        printf("Create CEK: %s\n", cekSql);
        SQLExecDirect(stmt, cekSql, SQL_NTS);
        free(cekSql);
#ifdef _WIN32
        LocalFree(ECEK);
#else
        free(ECEK);
#endif
    }

#ifdef _WIN32
    FreeLibrary(hProvLib);
#else
    dlclose(hProvLib);
#endif

    /* Create a table with encrypted columns */
    {
        static char *tableSql = "CREATE TABLE CustomKSPTestTable ("
            "c1 int,"
            "c2 varchar(255) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CustomCEK, ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'))";
        printf("Create table: %s\n", tableSql);
        SQLExecDirect(stmt, tableSql, SQL_NTS);
    }

    /* Load provider into the ODBC Driver and configure it */
    {
        unsigned char ksd[sizeof(CEKEYSTOREDATA) + sizeof(PROV_ENCRYPT_KEY) - 1];
        CEKEYSTOREDATA *pKsd = (CEKEYSTOREDATA*)ksd;
        pKsd->name = L"MyCustomKSPName";
        pKsd->dataSize = sizeof(PROV_ENCRYPT_KEY) - 1;
        memcpy(pKsd->data, PROV_ENCRYPT_KEY, sizeof(PROV_ENCRYPT_KEY) - 1);
#ifdef _WIN32
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "MyKSP.dll", SQL_NTS);
#else
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "./MyKSP.so", SQL_NTS);
#endif
        checkRC(rc, "Loading KSP into ODBC Driver", 7, dbc, SQL_HANDLE_DBC);
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREDATA, (SQLPOINTER)pKsd, SQL_IS_POINTER);
        checkRC(rc, "Configuring the KSP", 7, dbc, SQL_HANDLE_DBC);
    }

    /* Insert some data */
    {
        int c1;
        char c2[256];
        rc = SQLBindParameter(stmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 0, 0, &c1, 0, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        rc = SQLBindParameter(stmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 255, 0, c2, 255, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        for (i = 0; i < 10; i++) {
            c1 = i * 10 + i + 1;
            sprintf(c2, "Sample data %d for column 2", i);
            rc = SQLExecDirect(stmt, "INSERT INTO CustomKSPTestTable (c1, c2) values (?, ?)", SQL_NTS);
            checkRC(rc, "Inserting rows query", 10, stmt, SQL_HANDLE_STMT);
        }
        printf("(Encrypted) data has been inserted into the [CustomKSPTestTable]. You may inspect the data now.\n"
            "Press Enter to continue...\n");
        getchar();
    }

    /* Retrieve the data */
    {
        int c1;
        char c2[256];
        rc = SQLBindCol(stmt, 1, SQL_C_LONG, &c1, 0, 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLBindCol(stmt, 2, SQL_C_CHAR, c2, sizeof(c2), 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLExecDirect(stmt, "SELECT c1, c2 FROM CustomKSPTestTable", SQL_NTS);
        checkRC(rc, "Retrieving rows query", 12, stmt, SQL_HANDLE_STMT);
        while (SQL_SUCCESS == (rc = SQLFetch(stmt)))
            printf("Retrieved data: c1=%d c2=%s\n", c1, c2);
        SQLFreeStmt(stmt, SQL_CLOSE);
        printf("Press Enter to clean up and exit...\n");
        getchar();
    }

    /* Clean up */
    {
        SQLExecDirect(stmt, "DROP TABLE CustomKSPTestTable", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN ENCRYPTION KEY CustomCEK", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN MASTER KEY CustomCMK", SQL_NTS);
        printf("Removed table, CEK, and CMK\n");
    }
    SQLDisconnect(dbc);
    SQLFreeHandle(SQL_HANDLE_DBC, dbc);
    SQLFreeHandle(SQL_HANDLE_ENV, env);
    return 0;
}

```

## <a name="see-also"></a>Siehe auch

[Mit "immer verschlüsselt" mit dem ODBC-Treiber](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
