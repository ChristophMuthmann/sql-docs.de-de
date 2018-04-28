---
title: 'Ibcpsession:: Bcpcontrol (OLE DB) | Microsoft Docs'
description: IBCPSession::BCPControl (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPControl (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPControl method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: beb59a71630220278442dcff1c1b3e96a1c69338
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ibcpsessionbcpcontrol-ole-db"></a>IBCPSession::BCPControl (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Legt die Optionen für einen Massenkopiervorgang fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT BCPControl(   
      int eOption,  
      void *iValue);  
```  
  
## <a name="remarks"></a>Hinweise  
 Die **BCPControl** Methode verschiedene Steuerelementparameter für Massenkopiervorgänge einschließlich der Anzahl von Fehlern, die vor dem Abbrechen eines Massenkopiervorgangs die Nummern der ersten und letzten Zeilen zum Kopieren aus einer Datendatei und die Batchgröße zulässig sind.  
  
 Außerdem wird diese Methode dazu verwendet, die SELECT-Anweisung beim Massenkopieren von Daten aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anzugeben. Sie können festlegen, die **eOption** -Argument auf BCP_OPTION_HINTS und **iValue** Argument ein Zeiger auf eine Zeichenfolge mit Breitzeichen, die die SELECT-Anweisung enthält.  
  
 Mögliche Werte für *eOption* sind:  
  
|Option|Description|  
|------------|-----------------|  
|BCP_OPTION_ABORT|Beendet einen Massenkopiervorgang, der bereits ausgeführt wird. Sie erreichen die **BCPControl** Methode mit einem *eOption* -Argument von BCP_OPTION_ABORT aus einem anderen Thread um einen laufenden Massenkopiervorgang zu beenden. Die *iValue* Argument wird ignoriert.|  
|BCP_OPTION_BATCH|Die Anzahl der Zeilen pro Batch. Der Standardwert ist 0 (null), womit beim Extrahieren von Daten alle Zeilen in einer Tabelle oder beim Kopieren von Daten nach [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] alle Zeilen in der Benutzerdatendatei angegeben werden. Mit einem Wert kleiner als 1 wird BCP_OPTION_BATCH auf den Standardwert zurückgesetzt.|  
|BCP_OPTION_DELAYREADFMT|Ein boolescher Wert, wenn auf True festgelegt, führt dazu, dass [ibcpsession:: Bcpreadfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) , bei der Ausführung zu lesen. Wenn "false" (Standard), ibcpsession:: Bcpreadfmt sofort wird die Formatdatei zu lesen. Ein Sequenzfehler tritt auf Wenn **BCP_OPTION_DELAYREADFMT** ist "true", und Sie rufen ibcpsession:: BCPColumns oder ibcpsession:: BCPColFmt.<br /><br /> Ein Sequenzfehler tritt auch beim Aufrufen `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)FALSE))` nach dem Aufruf `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)TRUE)` und Bcpwritefmt.<br /><br /> Weitere Informationen finden Sie unter [Metadatenermittlung](../../oledb/features/metadata-discovery.md).|  
|BCP_OPTION_FILECP|Die *iValue* -Argument enthält die Nummer der Codepage für die Datendatei an. Sie können die Nummer der Codepage angeben, z. B. 1252 oder 850, oder einen der folgenden Werte:<br /><br /> BCP_FILECP_ACP: Daten in der Datei sind in der Microsoft Windows®-Codepage des Clients.<br /><br /> BCP_FILECP_OEMCP: Daten in der Datei sind in der OEM-Codepage des Clients (Standard).<br /><br /> BCP_FILECP_RAW: Daten in der Datei sind in der Codepage von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|BCP_OPTION_FILEFMT|Die Versionsnummer des Datendateiformats. Diese kann 80 ([!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]), 90 ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]), 100 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] or [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]), 110 ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) oder 120 ([!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]) sein. Der Standardwert ist 120. Dies ist beim Exportieren und Importieren von Daten in Formate nützlich, die in früheren Versionen des Servers unterstützt wurden.  Abgerufen z. B. zum Importieren von Daten aus einer Textspalte in eine [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] Server in einer **varchar(max)** Spalte in einer [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] -Server oder höher sollten Sie 80 angeben. Auf ähnliche Weise bei Angabe von 80, beim Exportieren von Daten aus einer **varchar(max)** Spalte wird gespeichert wie Textspalten im gespeichert sind die [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] formatieren und können in einer Textspalte importiert werden eine [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] Server.|  
|BCP_OPTION_FIRST|Die erste Datenzeile der zu kopierenden Datei oder Tabelle. Der Standard ist 1; ein Wert kleiner als 1 setzt diese Option auf den Standardwert zurück.|  
|BCP_OPTION_FIRSTEX|Gibt für BCP-OUT-Vorgänge die erste Zeile der Datenbanktabelle an, die in die Datendatei kopiert werden soll.<br /><br /> Gibt für BCP-IN-Vorgänge die erste Zeile der Datendatei an, die in die Datenbanktabelle kopiert werden soll.<br /><br /> Die *iValue* Parameter muss die Adresse einer 64-Bit-Ganzzahl mit Vorzeichen sein, die den Wert enthält. Der maximale Wert, der an BCPFIRSTEX übergeben werden kann, ist 2^63-1.|  
|BCP_OPTION_FMTXML|Gibt an, dass die generierte Formatdatei das XML-Format aufweisen sollte. Diese Option ist standardmäßig deaktiviert. Die Formatdateien werden standardmäßig als Textdateien gespeichert. Das XML-Format bietet größere Flexibilität, ist jedoch mit einigen Einschränkungen verbunden. Sie können beispielsweise das Präfix und das Abschlusszeichen für ein Feld nicht gleichzeitig angeben, was in älteren Formatdateien durchaus möglich war.<br /><br /> Hinweis: XML-Formatdateien werden nur unterstützt, wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tools zusammen mit OLE DB-Treiber für SQL Server installiert sind.|  
|BCP_OPTION_HINTS|Die *iValue* Argument enthält einen Breitzeichen-Zeichenfolgenzeiger. Die adressierte Zeichenfolge gibt entweder Verarbeitungshinweise für das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Massenkopieren oder eine [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung an, die ein Resultset zurückgibt. Wenn eine [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung angegeben ist, die mehr als ein Resultset zurückgibt, werden alle auf das erste Resultset folgenden Resultsets nicht berücksichtigt.|  
|BCP_OPTION_KEEPIDENTITY|Wenn die *iValue* Argument auf "true" festgelegt ist, wird diese Option gibt an, dass die massenkopiermethoden Datenwerte, die für einen bereitgestellten einfügen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Spalten mit einer Identity-Einschränkung definiert. Die Eingabedatei muss Werte für die IDENTITY-Spalten angeben. Wenn dies nicht festgelegt ist, werden neue Identitätswerte für die eingefügten Zeilen generiert. Alle in der Datei für die IDENTITY-Spalten vorhandenen Daten werden ignoriert.|  
|BCP_OPTION_KEEPNULLS|Bestimmt, ob leere Datenwerte in der Datei in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Tabelle in NULL-Werte konvertiert werden. Wenn die *iValue* -Argument auf "true" festgelegt ist werden leere Werte konvertiert werden, auf NULL in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle. In der Standardeinstellung werden leere Werte in einen Standardwert für die Spalte in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Tabelle konvertiert, sofern ein Standardwert angegeben ist.|  
|BCP_OPTION_LAST|Die letzte zu kopierende Zeile. Standardmäßig werden alle Zeilen kopiert. Ein Wert kleiner als 1 setzt diese Option auf den Standardwert zurück.|  
|BCP_OPTION_LASTEX|Gibt für BCP-OUT-Vorgänge die letzte Zeile der Datenbanktabelle an, die in die Datendatei kopiert werden soll.<br /><br /> Gibt für BCP-IN-Vorgänge die letzte Zeile der Datendatei an, die in die Datenbanktabelle kopiert werden soll.<br /><br /> Die *iValue* Parameter muss die Adresse einer 64-Bit-Ganzzahl mit Vorzeichen sein, die den Wert enthält. Der maximale Wert, der an BCPLASTEX übergeben werden kann, ist 2^63-1.|  
|BCP_OPTION_MAXERRS|Die Anzahl von Fehlern, die zulässig sind, bevor der Massenkopiervorgang fehlschlägt. Der Standardwert lautet 10. Ein Wert kleiner als 1 setzt diese Option auf den Standardwert zurück. Beim Massenkopieren sind maximal 65.535 Fehler zulässig. Wenn für diese Option größere Werte als 65.535 festgelegt werden, wird diese Option auf 65.535 festgelegt.|  
|BCP_OPTION_ROWCOUNT|Gibt die Anzahl von Zeilen zurück, auf die sich der aktuelle (oder letzte) BCP-Vorgang auswirkt.|  
|BCP_OPTION_TEXTFILE|Die Datendatei ist keine Binärdatei, sondern eine Textdatei. BCP stellt fest, ob es sich bei der Textdatei um eine Unicode-Datei handelt, indem der Unicode-Bytemarker in den ersten beiden Bytes der Datendatei überprüft wird.|  
|BCP_OPTION_UNICODEFILE|Wenn diese Option auf TRUE festgelegt wurde, bedeutet das, dass die Eingabedatei ein Unicode-Dateiformat ist.|  
  
## <a name="arguments"></a>Argumente  
 *eOption*[in]  
 Legen Sie eine der im obigen Abschnitt mit Hinweisen aufgelisteten Optionen fest.  
  
 *iValue*[in]  
 Der Wert für die angegebene *eOption*. Die *iValue* Argument ist ein Ganzzahlwert, der Umwandlung in einen void-Zeiger für zukünftige Erweiterungen auf 64-Bit-Werte zulassen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 S_OK  
 Die Methode wurde erfolgreich ausgeführt.  
  
 E_FAIL  
 Ein anbieterspezifischer Fehler aufgetreten. Ausführliche Informationen erhalten Sie die [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) Schnittstelle.  
  
 E_UNEXPECTED  
 Die Methode wurde unerwartet aufgerufen. Z. B. die [ibcpsession:: BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) Methode nicht vor dem Aufrufen dieser Funktion aufgerufen wurde.  
  
 E_OUTOFMEMORY  
 Fehler aufgrund nicht genügenden Arbeitsspeichers  
  
## <a name="see-also"></a>Siehe auch  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Durchführen von Massenkopiervorgängen](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
