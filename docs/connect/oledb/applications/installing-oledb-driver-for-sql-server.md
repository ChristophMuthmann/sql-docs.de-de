---
title: Installieren des OLE DB-Treiber für SQLServer | Microsoft Docs
description: Installieren und Deinstallieren von OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, uninstalling
- MSOLEDBSQL, installing
- MSOLEDBSQL, uninstalling
- Setup [OLE DB Driver for SQL Server]
- uninstalling OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server
- installing OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, installing
- data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server
- removing OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3cb05e6fbbc3507aec67f4faa61f621c4245e7c8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer installieren.
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Der OLE DB-Treiber für SQL Server Installation benötigen Sie msoledbsql.msi-Installer.
Führen Sie das Installationsprogramm, und stellen Sie Ihre bevorzugte Auswahl. Der OLE DB-Treiber für SQL Server können nebeneinander installiert, mit früheren Versionen von Microsoft OLE DB-Anbieter sein.

Der OLE DB-Treiber für SQL Server-Datenbankdateien (msoledbsql.dll, msoledbsqlr.rll) werden im installiert `%SYSTEMROOT%\system32\` . Darüber hinaus die msoledbsql.msi installiert die 32-Bit-Binärdateien in X64 `%SYSTEMROOT%\SysWOW64\`.

> [!NOTE]  
> Alle entsprechenden registrierungseinstellungen für den OLE DB-Treiber für SQL Server werden im Rahmen des Installationsprozesses festgelegt.  

Der OLE DB-Treiber für SQL Server-Header- und-Bibliotheksdateien (msoledbsql.h und msoledbsql.lib) werden im installiert `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`. Darüber hinaus die msoledbsql.msi die gleichen Dateien in installiert X64 `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`.  

Sie können den OLE DB-Treiber für SQL Server über msoledbsql.msi verteilen. Sie müssen möglicherweise OLE DB-Treiber für SQL Server installieren, wenn Sie eine Anwendung bereitstellen. Eine Möglichkeit, mehrere Pakete in mehreren Installationen, die für den Benutzer wie eine Installation aussehen, zu installieren, besteht in der Verwendung der Chainer- und Bootstrappertechnologie. Weitere Informationen finden Sie unter [Authoring a Custom Bootstrapper Package für Visual Studio 2005](http://go.microsoft.com/fwlink/?LinkId=115667) und [Adding Custom Prerequisites](http://go.microsoft.com/fwlink/?LinkId=115668).  
  
Die X64 msoledbsql.msi wird auch die 32-Bit-Version des OLE DB-Treiber für SQL Server installiert. Wenn Ihre Anwendung eine andere Plattform als, die es entwickelt wurde diejenige, können Sie Versionen von msoledbsql.msi für X64 und X86 herunterladen.

Wenn Sie msoledbsql.msi aufrufen, werden nur die Clientkomponenten standardmäßig installiert. Die Client Komponenten handelt es sich um Dateien, die Unterstützung der Ausführung einer Anwendung, die mithilfe von OLE DB-Treiber für SQL Server entwickelt wurde. Um auch die SDK-Komponenten zu installieren, geben Sie `ADDLOCAL=All` in der Befehlszeile an. Beispiel:  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>Installation ohne Eingreifen  
 Wenn Sie die/passiv, / qn, / qb oder/QR-Option mit Msiexec verwenden, müssen Sie auch angeben, auf IACCEPTMSOLEDBSQLLICENSETERMS = Ja, um ausdrücklich anzugeben, dass Sie die Bedingungen der Endbenutzerlizenz zustimmen. Diese Option muss in Großbuchstaben angegeben werden.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>OLE DB-Treiber für SQLServer als Abhängigkeit installieren  
Es ist wichtig, nicht auf die OLE DB-Treiber für SQL Server deinstallieren, bis alle abhängigen Anwendungen deinstalliert werden. Verwenden Sie zum Benutzer eine Warnung zur Verfügung stellen, dass der OLE DB-Treiber für SQL Server die Anwendung abhängt, die Installationsoption APPGUID im MSI wie folgt:  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

Der an APPGUID übergebene Wert ist Ihr spezifischer Produktcode. Der Produktcode muss beim Packen des Setupprogramms für die Anwendung mit Microsoft Installer erstellt werden.
Die APPGUID-Option muss das Installationsprogramm eine Eingabeaufforderung mit erhöhten Rechten ausgeführt werden.

## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem OLE DB-Treiber für SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
