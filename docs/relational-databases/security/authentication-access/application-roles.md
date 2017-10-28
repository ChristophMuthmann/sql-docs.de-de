---
title: Anwendungsrollen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application roles [SQL Server], about application roles
- principals [SQL Server], application roles
- credentials [SQL Server], roles
- application roles [SQL Server]
- roles [SQL Server], application
- permissions [SQL Server], roles
- users [SQL Server], application roles
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: dca18b8a-ca03-4b7f-9a46-8474d5b66f76
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a24b143d85660d979e61a103a077bddaef28029b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="application-roles"></a>Anwendungsrollen
  Eine Anwendungsrolle ist ein Datenbankprinzipal, mit dem eine Anwendung mit eigenen Berechtigungen ausgeführt werden kann. Sie können Anwendungsrollen verwenden, um den Zugriff auf bestimmte Daten nur den Benutzern zu ermöglichen, die über eine bestimmte Anwendung eine Verbindung herstellen. Im Gegensatz zu Datenbankrollen enthalten Anwendungsrollen keine Mitglieder und sind standardmäßig inaktiv. Anwendungsrollen können in beiden Authentifizierungsmodi verwendet werden. Anwendungsrollen werden mit **sp_setapprole**aktiviert, wofür ein Kennwort erforderlich ist. Da es sich bei Anwendungsrollen um einen Prinzipal auf Datenbankebene handelt, können sie auf andere Datenbanken nur über die Berechtigungen zugreifen, die in diesen Datenbanken dem Konto **guest**erteilt wurden. Anwendungsrollen anderer Datenbanken können daher auf keine Datenbank zugreifen, in der **guest** deaktiviert wurde.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]können Anwendungsrollen nicht auf Metadaten auf Serverebene zugreifen, da sie nicht mit einem Prinzipal auf Serverebene verbunden sind. Sie können diese Einschränkung deaktivieren und dabei den Anwendungsrollen den Zugriff auf Metadaten auf Serverebene ermöglichen, indem Sie das globale Flag 4616 festlegen. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) und [DBCC TRACEON &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md).  
  
## <a name="connecting-with-an-application-role"></a>Herstellen einer Verbindung mit einer Anwendungsrolle  
 Der Prozess, in dem eine Anwendungsrolle den Sicherheitskontext wechselt, besteht aus den folgenden Schritten:  
  
1.  Ein Benutzer führt eine Clientanwendung aus.  
  
2.  Die Clientanwendung stellt eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] als Benutzer her.  
  
3.  Die Anwendung führt dann die gespeicherte Prozedur **sp_setapprole** mit einem Kennwort aus, das nur der Anwendung bekannt ist.  
  
4.  Wenn der Name und das Kennwort der Anwendung gültig sind, wird die Anwendungsrolle aktiviert.  
  
5.  An diesem Punkt verliert die Verbindung die Berechtigungen des Benutzers und nimmt die Berechtigungen der Anwendungsrolle an.  
  
 Die über die Anwendungsrolle erhaltenen Berechtigungen bleiben für die Dauer der Verbindung wirksam.  
  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]bestand die einzige Möglichkeit für einen Benutzer, seinen ursprünglichen Sicherheitskontext nach dem Starten einer Anwendungsrolle zurückzuerhalten, darin, die Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu trennen und erneut eine Verbindung herzustellen. Seit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]besitzt **sp_setapprole** eine Option, die ein Cookie erstellt. Das Cookie enthält die vor der Aktivierung der Anwendungsrolle gültigen Kontextinformationen. Das Cookie kann von **sp_unsetapprole** zum Wiederherstellen des ursprünglichen Kontexts der Sitzung verwendet werden. Weitere Informationen über diese neue Option sowie ein Beispiel finden Sie unter [sp_setapprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)erteilt wurden.  
  
> [!IMPORTANT]  
>  Die **encrypt** -Option von ODBC wird von **SqlClient**nicht unterstützt. Wenn Sie vertrauliche Informationen über das Netzwerk übertragen, sollten Sie zum Verschlüsseln des Kanals SSL (Secure Sockets Layer) oder IPSec verwenden. Wenn Sie Anmeldeinformationen innerhalb der Clientanwendung persistent speichern müssen, verschlüsseln Sie diese mit den CryptoAPI-Funktionen. In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und höheren Versionen wird der *password* -Parameter als unidirektionaler Hash gespeichert.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|Erstellen einer Anwendungsrolle.|[Erstellen einer Anwendungsrolle](../../../relational-databases/security/authentication-access/create-an-application-role.md) und [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-application-role-transact-sql.md)|  
|Ändern einer Anwendungsrolle.|[ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-application-role-transact-sql.md)|  
|Löschen einer Anwendungsrolle.|[DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-application-role-transact-sql.md)|  
|Verwenden einer Anwendungsrolle.|[sp_setapprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern von SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  

