---
title: Schutz Ihres geistigen SQL Server-Eigentums | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- protecting intellectual property
- intellectual property
ms.assetid: 174a646a-d65c-4074-8249-d783e91be2dd
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 7b4f037616e0559ac62bbae5dbe04aeffe529b06
ms.openlocfilehash: 36377fe5db9440651b4e63a2c848efc290470d3e
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="protecting-your-sql-server-intellectual-property"></a>Schutz Ihres geistigen SQL Server-Eigentums
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Softwareentwickler fragen sich häufig, wie sie ihre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Datenanwendung am besten an die Kunden verteilen können. Und doch verhindern sie, dass Kunden die Anwendung analysieren und dekonstruieren. Entscheidend hierbei ist, dass der Schutz Ihres geistigen Eigentums ein rechtliches Problem und Teil Ihres Lizenzvertrags ist. Wenn [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] auf einem Computer installiert ist, der von anderen Benutzern verwaltet wird, verlieren Sie grundsätzlich einen Teil der Kontrolle. 

## <a name="nature-of-the-problem"></a>Ursache des Problems
Der Besitzer/Administrator eines Computers kann immer auf die auf diesem Computer installierte Instanz von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zugreifen. Wenn Sie die Anwendung auf dem Computer eines Kunden bereitstellen, kann er sich in seiner Funktion als Administrator mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] als Mitglied der festen Serverrolle **sysadmin** verbinden. Dies schließt die Möglichkeit zum Erteilen von Berechtigungen, Verwalten von Sicherungen (einschließlich dem Wiederherstellen von Sicherungen auf anderen Computern), Entschlüsseln und Verschieben von Datendateien usw. ein. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL Server, wenn Systemadministratoren gesperrt sind](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md). 

Gespeicherte Prozeduren und Daten können verschlüsselt, die Datenstruktur jedoch nicht ausgeblendet werden. Benutzer, die einen Debugger an den Serverprozess anfügen können, können entschlüsselte Prozeduren und Daten zur Laufzeit vom Arbeitsspeicher abrufen.

Wenn die Clients keine Administratoren auf dem Computer sind, können Sie ihren Zugriff verhindern. Mit [Transparente Datenverschlüsselung](../../relational-databases/security/encryption/transparent-data-encryption.md) können Sie Datendateien verschlüsseln, Sicherungen verschlüsseln und die Aktionen aller Benutzer überwachen. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Administratoren und Administratoren des [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computers können diese Aktionen jedoch umkehren.

## <a name="solution"></a>Lösung
Es gibt verschiedene Möglichkeiten, den Client-Datenzugriff zu konfigurieren, ohne [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] auf dem Computer Ihrer Clients zu installieren. Der einfachste Weg ist die Verwendung von [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], damit die Clients keine Administratoren sind, möglicherweise kombiniert mit [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Weitere Informationen zu den ersten Schritten mit [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] finden Sie unter [Was ist SQL-Datenbank? Einführung in SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview).  

Sie können auch ein [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] in Ihrem eigenen Netzwerk hosten und Clients den Zugriff auf Daten entweder direkt über das Netzwerk oder über eine Webanwendung gewähren.

## <a name="see-also"></a>Siehe auch

[Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[Sichern von SQL Server](../../relational-databases/security/securing-sql-server.md)  


