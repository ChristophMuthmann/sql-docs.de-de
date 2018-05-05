---
title: VDI-Spezifikation Backup - SQLServer on Linux | Microsoft Docs
description: SQL Server Backup Virtual Device Interface Specification.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: 39d554e1da11745e1ea21537c7cc6b56ec9e83b7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server auf Linux VDI-Client-SDK-Spezifikation

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieses Dokument behandelt die Schnittstellen, die von SQL Server auf Linux virtual Device Interface (VDI) Client-SDK bereitgestellt wird. Unabhängige Softwarehersteller (ISVs) können die virtuellen Sicherung Gerät Application Programming Interface (API), SQL Server in ihre Produkte integrieren. Im Allgemeinen verhält sich VDI unter Linux auf ähnliche Weise zu VDI unter Windows mit folgenden Änderungen:

- Windows-Shared Memory wird POSIX freigegebenen Speicher.
- Windows-Semaphoren sind POSIX Semaphoren.
- Windows-Datentypen wie HRESULT und DWORD ganzzahligen Entsprechungen geändert werden.
- Die COM-Schnittstellen werden entfernt und durch ein Paar von C++-Klassen ersetzt.
- SQL Server unter Linux unterstützt benannte Instanzen nicht, damit Verweise auf die Instanznamen entfernt wurden. 
- Die freigegebene Bibliothek wird in libsqlvdi.so am /opt/mssql/lib/libsqlvdi.so installiert implementiert.

Dieses Dokument ist eine Ergänzung zu **vbackup.chm** mit Informationen zu den Windows-VDI-Spezifikation. Herunterladen der [Windows VDI-Spezifikation](http://www.microsoft.com/download/details.aspx?id=17282).

Überprüfen Sie auch die beispiellösung für VDI-Sicherung auf die [SQL Server Samples GitHub-Repository](http://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux).

## <a name="user-permissions-setup"></a>Benutzereinrichtung-Berechtigungen

Unter Linux werden POSIX primitive Besitz des Benutzers erstellen sie und ihre Standardgruppe. Für Objekte, die von SQL Server erstellt werden werden diese standardmäßig der Mssql-Benutzer und der Gruppe "Mssql" Besitz sein. Um die gemeinsame Nutzung der SQL Server und die VDI-Clients zu ermöglichen, eine der folgenden beiden Methoden werden empfohlen:

1. Führen Sie die VDI-Client als dem Mssql-Benutzer
   
   Führen Sie den folgenden Befehl zum Wechseln zu Mssql-Benutzer:
   
   ```bash
   sudo su mssql
   ```

2. Der Mssql-Benutzer die Vdiuser Gruppe und die Vdiuser der Mssql-Gruppe hinzufügen.
   
   Führen Sie die folgenden Befehle ein:

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   Starten Sie den Server aus, um neue Gruppen für SQL Server und Vdiuser übernehmen

## <a name="client-functions"></a>Clientfunktionen

Das Kapitel enthält Beschreibungen der einzelnen Clientfunktionen. Die Beschreibungen enthalten die folgende Informationen an:

- Zweck der Funktion
- Funktionssyntax
- Parameterliste
- Rückgabewerte
- Hinweise

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**Zweck** diese Funktion erstellt das virtuelle Gerät festlegen.

**Syntax**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| | **name** | Dies identifiziert die virtuelles Gerät. Die Regeln für Namen von CreateFileMapping() verwendeten müssen folgen. Alle Zeichen außer dem umgekehrten Schrägstrich (\) verwendet werden kann. Dies ist eine Zeichenfolge. Die Zeichenfolge mit des Benutzers Produktwissen oder firmeninternem und Datenbankname vorangestellt wird empfohlen. |
| |**cfg** | Dies ist die Konfiguration für das virtuelle Gerät festlegen. Weitere Informationen finden Sie unter "Konfiguration" weiter unten in diesem Dokument.

| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** | Die Funktion wurde erfolgreich ausgeführt. |
| |**VD_E_NOTSUPPORTED** |Mindestens eines der Felder in der Konfiguration ist ungültig oder andernfalls nicht unterstützt. |
| |**VD_E_PROTOCOL** | Das virtuelle Gerät bereits vorhanden ist.

**"Hinweise"** erstellen Sie die Methode sollte nur einmal pro Backup- oder RESTORE-Vorgang aufgerufen werden. Nach dem Aufrufen der Close-Methode, kann der Client die Schnittstelle, um ein anderes virtuelles Gerät erstellen wiederverwenden.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**Zweck** diese Funktion dient zum Warten, bis des Servers so konfigurieren Sie das virtuelle Gerät festlegen.
**Syntax**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| | **timeout** | Dies ist das Timeout in Millisekunden. Verwenden Sie INFINITE oder eine negative ganze Zahl, um Timeouts zu verhindern.
| | **cfg** | Nach erfolgreicher Ausführung enthält diese Spalte die Konfiguration vom Server ausgewählt. Weitere Informationen finden Sie unter "Konfiguration" weiter unten in diesem Dokument.

| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** | Die Konfiguration wurde zurückgegeben.
| |**VD_E_ABORT** |SignalAbort wurde aufgerufen.
| |**VD_E_TIMEOUT** |Die Funktion ist ein Timeout aufgetreten.

**"Hinweise"** dieser Funktion in einem Warnbare Status blockiert. Nach dem erfolgreichen Aufruf können die Geräte in der Menge virtuelles Gerät geöffnet sein.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**Zweck** diese Funktion wird eines der Geräte in der Menge virtuelles Gerät geöffnet.
**Syntax**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| | **name** |Dies identifiziert die virtuelles Gerät.
| | **ppVirtualDevice** |Wenn die Funktion erfolgreich ausgeführt wird, wird ein Zeiger auf das virtuelle Gerät zurückgegeben. Dieses Gerät ist für GetCommand und CompleteCommand verwendet.

| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** |Die Funktion wurde erfolgreich ausgeführt.
| |**VD_E_ABORT** | Abbruch angefordert wurde.
| |**VD_E_OPEN** |  Alle Geräte sind geöffnet.
| |**VD_E_PROTOCOL** |  Die Gruppe ist nicht im Status "Initialisieren", oder dieses Gerät ist bereits geöffnet.
| |**VD_E_INVALID** |Der Gerätename ist ungültig. Es ist nicht mit den Namen bekannt, dass die Gruppe bilden.

**"Hinweise"** VD_E_OPEN ohne Problem zurückgegeben werden. Der Client möglicherweise OpenDevice mittels einer Schleife aufrufen, bis dieser Code zurückgegeben wird.
Wenn mehrere Geräte, z. B. konfiguriert ist *n* Geräte das virtuelle Gerät zurück *n* eindeutige Geräte-Schnittstellen.

Die `GetConfiguration` -Funktion kann verwendet werden, warten, bis die Geräte geöffnet werden können.
Wenn diese Funktion nicht erfolgreich ist, wird ein null-Wert durch die PpVirtualDevice zurückgegeben.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**Zweck** diese Funktion dient zum Abrufen des Nächstes Befehl in der Warteschlange auf einem Gerät. Wenn angefordert, wartet dieser Funktion für den nächsten Befehl.

**Syntax**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| |**timeout** |Dies ist die Zeit in Millisekunden zu warten. Verwenden Sie Infinite, um unbegrenzt zu warten. Verwenden Sie 0 für einen Befehl abrufen. VD_E_TIMEOUT wird zurückgegeben, wenn kein Befehl derzeit verfügbar ist. Wenn das Timeout auftritt, entscheidet der Client die nächste Aktion aus.
| |**Timeout** |Dies ist die Zeit in Millisekunden zu warten. Verwenden Sie Infinite oder einen negativen Wert, um unbegrenzt zu warten. Verwenden Sie 0 für einen Befehl abrufen. VD_E_TIMEOUT wird zurückgegeben, wenn kein Befehl verfügbar ist, bevor das Timeout abläuft. Wenn das Timeout auftritt, entscheidet der Client die nächste Aktion aus.
| |**ppCmd** |Wenn ein Befehl wurde erfolgreich zurückgegeben wird, wird die Adresse eines Befehls zum Ausführen von Parameters zurückgegeben. Der zurückgegebene Arbeitsspeicher ist schreibgeschützt. Wenn der Befehl abgeschlossen ist, wird dieser Zeiger an die Routine CompleteCommand übergeben. Weitere Informationen zu jedem Befehl finden Sie unter "Befehle" weiter unten in diesem Dokument.
        
| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** |Ein Befehl wurde abgerufen.
| |**VD_E_CLOSE** |Das Gerät wurde vom Server geschlossen.
| |**VD_E_TIMEOUT** |Es wurde kein Befehl verfügbar, und vor dem abgelaufenen Timeoutintervall.
| |**VD_E_ABORT** |Der Client oder der Server hat die SignalAbort verwendet, um ein Herunterfahren erzwungen.

**"Hinweise"** Wenn VD_E_CLOSE zurückgegeben wird zurückgegeben, SQL Server hat das Gerät geschlossen. Dies ist Teil der normalen Herunterfahren. Nachdem alle Geräte geschlossen wurden, ruft der Client ClientVirtualDeviceSet::Close, um den Satz virtuelles Gerät zu schließen.
Wenn diese Routine blockieren muss, warten Sie einen Befehl, wird der Thread in einen Warnbare Zustand belassen.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**Zweck** diese Funktion wird verwendet, um SQL Server zu informieren, die ein Befehl abgeschlossen ist. Informationen über den Abschluss des Befehls entsprechende sollte zurückgegeben werden. Weitere Informationen finden Sie unter "Befehle" weiter unten in diesem Dokument.

**Syntax** 

   ```
   int ClientVirtualDevice::CompleteCommand (
   VDC_Command pCmd,        // the command
   int  completionCode,     // completion code
   unsigned long    bytesTransferred,   // bytes transferred
   int64_t  position        // current position
   );
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| |**pCmd** |Dies ist die Adresse eines Befehls, der zuvor von ClientVirtualDevice::GetCommand zurückgegeben wird.
| |**completionCode** |Dies ist ein Statuscode "", der den Abschlussstatus angibt. Dieser Parameter muss für alle Befehle zurückgegeben werden. Der zurückgegebene Code sollte an den ausgeführten Befehl geeignet sein. ERROR_SUCCESS wird in allen Fällen verwendet, um einem erfolgreich ausgeführten Befehl zu kennzeichnen. Die vollständige Liste der möglichen Fehlercodes, finden Sie in der Datei vdierror.h. Eine Liste der typische Statuscodes für jeden Befehl wird in "Befehle" weiter unten in diesem Dokument.
| |**bytesTransferred** |Dies ist die Anzahl der erfolgreich übertragenen Bytes. Dies wird nur für die Datenübertragung zurückgegeben, Befehle lesen und schreiben.
| |**position** |Dies ist eine Antwort auf die GetPosition-Befehl.
        
| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** |Der Abschluss wurde korrekt hingewiesen.
| |**VD_E_INVALID** |pCmd war es sich nicht um einen aktiven Befehl.
| |**VD_E_ABORT** |Abbruch signalisiert wurde.
| |**VD_E_PROTOCOL** |Das Gerät ist nicht geöffnet werden.

**"Hinweise"** None

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**Zweck** diese Funktion wird verwendet, um zu signalisieren, dass eine nicht ordnungsgemäße Beendigung erfolgen soll.

**Syntax** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| |Keine | Nicht verfügbar
        
| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK**|Die Abort-Benachrichtigung wurde erfolgreich bereitgestellt.

**"Hinweise"** zu jedem Zeitpunkt kann der Client den Backup- oder RESTORE-Vorgang abgebrochen auswählen. Diese Routine signalisiert, dass alle Vorgänge beenden soll. Der Zustand des virtuellen Geräts Satzes wechselt Zustand fehlerbedingt beendet. Keine weiteren Befehle, die für alle Geräte zurückgegeben werden. Alle nicht abgeschlossenen Befehle werden automatisch vervollständigt, ERROR_OPERATION_ABORTED als ein Beendigungscode zurückgeben. Der Client sollte ClientVirtualDeviceSet::Close aufrufen, nachdem er alle ausstehenden Verwendung von Puffern, die an den Client bereitgestellten sicher beendet wurde. Weitere Informationen finden Sie unter "Nicht ordnungsgemäße Beendigung" weiter oben in diesem Dokument.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**Zweck** diese Funktion schließt die ClientVirtualDeviceSet::Create erstellte virtuelle Gerät Menge. Dies führt in der Version aller Ressourcen, die den Satz von virtuellen Gerät zugeordnet.

**Syntax** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| |Keine |Nicht verfügbar
        
| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** |Dies wird zurückgegeben, wenn der Satz virtuelles Gerät erfolgreich geschlossen wurde.
| |**VD_E_PROTOCOL** |Es wurde keine Aktion ausgeführt, da das virtuelle Gerät Satz nicht offen war.
| |**VD_E_OPEN** |Geräte wurden noch geöffnet.

**"Hinweise"** Schließen des Aufrufs ist eine Client-Deklaration, dass alle durch die Menge des virtuellen Geräts verwendete Ressourcen freigegeben werden sollen. Der Client muss sicherstellen, dass alle Aktivitäten im Zusammenhang mit Datenpuffer und virtuellen Geräte vor dem Aufrufen von Schließen beendet wird. Durch Schließen werden alle virtuellen Geräteschnittstellen OpenDevice zurückgegebenes ungültig.
Der Client ist zulässig, einen Aufruf erstellen, auf das virtuelle Gerät festgelegte Schnittstelle ausgeben, nachdem der schließen-Aufruf zurückgegeben wird. Solch ein Aufruf würde ein neues virtuelles Gerät legen Sie für ein nachfolgender BACKUP oder RESTORE-Vorgang erstellen.
Wenn schließen aufgerufen wird, wenn ein oder mehrere virtuelle Geräte noch geöffnet sind, wird VD_E_OPEN zurückgegeben. In diesem Fall wird SignalAbort intern ausgelöst, um eine ordnungsgemäße Herunterfahren nach Möglichkeit sicherzustellen. VDI-Ressourcen werden freigegeben. Ein Hinweis VD_E_CLOSE zurückgegeben auf jedem Gerät vor dem Aufrufen von ClientVirtualDeviceSet::Close sollte der Client wartet. Wenn der Client weiß, dass die virtuelles Gerät ist bereits in einem Zustand fehlerbedingt beendet, und er sollte nicht erwarten, dass einen Hinweis VD_E_CLOSE zurückgegeben von GetCommand und ClientVirtualDeviceSet::Close kann aufgerufen werden, sobald die Aktivität auf die freigegebenen Puffer beendet wird.
Weitere Informationen finden Sie unter "Nicht ordnungsgemäße Beendigung" weiter oben in diesem Dokument.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**Zweck** diese Funktion wird geöffnet, das virtuelle Gerät in einem sekundären Client festgelegt. Die primäre Client muss bereits Create "und" GetConfiguration verwendet haben, zum Einrichten der virtuellen Geräts festgelegt wird.

**Syntax** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| |**setName** |Hierdurch wird die Gruppe. Dieser Name wird Groß-/Kleinschreibung beachtet und muss mit dem Namen übereinstimmen vom primären Client verwendet werden, wenn er ClientVirtualDeviceSet::Create aufgerufen.

| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** |Die Funktion wurde erfolgreich ausgeführt.
| |**VD_E_PROTOCOL** |Welche virtuellen Geräts nicht erstellt wurde, wurde bereits auf diesem Client oder das virtuelle Gerät geöffnet festgelegte ist nicht zum Annehmen von geöffneten Anfragen von sekundären Clients bereit.
| |**VD_E_ABORT** |Der Vorgang wird abgebrochen wird.

**"Hinweise"** primäre Client ist dafür verantwortlich, normales und ungewöhnliches Beendigung der sekundären Clients erkennen, wenn Sie ein Prozessmodell mit mehreren verwenden zu können,.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**Zweck** einige Anwendungen erfordern mehrere Prozesse mit ClientVirtualDevice::GetCommand zurückgegebene Puffer zu arbeiten. In solchen Fällen wird können der Prozess, der den Befehl empfängt GetBufferHandle Sie eine unabhängige Prozesshandle abrufen, die den Puffer angibt. Dieses Handle kann dann zu einem anderen Prozess übermittelt werden, die auch dieselbe geöffnete virtuellen Gerät festgelegt hat. Dieser Prozess würde dann ClientVirtualDeviceSet::MapBufferHandle verwenden, die Adresse des Puffers beziehen. Die Adresse wird wahrscheinlich eine andere Adresse als in seinem Partner sein, da jeder Prozess Puffer unter verschiedenen Adressen zugeordnet werden kann.

**Syntax** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| |**pBuffer** |Dies ist die Adresse eines Puffers, der von einem Befehl Lese- oder Schreibzugriff abgerufen.
| |**BufferHandle** |Ein eindeutiger Bezeichner für den Puffer wird zurückgegeben.

| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** |Die Funktion wurde erfolgreich ausgeführt.
| |**VD_E_PROTOCOL** |Das virtuelle Gerät festgelegte ist nicht aktuell geöffneten.
| |**VD_E_INVALID** |Die pBuffer ist keine gültige Adresse.
"Hinweise", dass der Prozess, der die GetBufferHandle-Funktion aufruft, ist verantwortlich für ClientVirtualDevice::CompleteCommand aufrufen, wenn die Datenübertragung abgeschlossen ist.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**Zweck** diese Funktion wird verwendet, um eine gültige Pufferadresse aus einem Pufferhandle abgerufen, die von einem anderen Prozess zu erhalten. 

**Syntax** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| Parameter | Argument | Erklärung
| ----- | ----- | ------ |
| |**dwBuffer** |Dies ist das ClientVirtualDeviceSet::GetBufferHandle zurückgegebene Handle.
| |**ppBuffer** |Dies ist die Adresse des Puffers, der im aktuellen Prozess gültig ist.

| Rückgabewerte | Argument | Erklärung
| ----- | ----- | ------ |
| |**NOERROR ZURÜCK** |Die Funktion wurde erfolgreich ausgeführt.
| |**VD_E_PROTOCOL** |Das virtuelle Gerät festgelegte ist nicht aktuell geöffneten.
| |**VD_E_INVALID** |Die PpBuffer ist ein ungültiges Handle.

**"Hinweise"** muss darauf geachtet werden auf die Handles ordnungsgemäß zu kommunizieren. Ziehpunkte werden für einen einzelnen virtuellen Gerät Satz lokal. Die Partner-Prozesse, die Freigabe ein Handle müssen diesen Puffer sicherstellen, dass die Handles, nur innerhalb des Bereichs des virtuellen Geräts verwendet werden aus dem Puffer ursprünglich abgerufen wurde festgelegt.


