---
title: "Hinzuf&#252;gen von Transact-SQL-Ausschnitten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 901c7995-8eb5-4d12-8bb0-de0a922b48f8
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Hinzuf&#252;gen von Transact-SQL-Ausschnitten
  Sie können dem Satz von vordefinierten Ausschnitten, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthalten sind, eigene Transact-SQL-Codeausschnitte hinzufügen.  
  
## Erstellen einer Transact-SQL-Ausschnittdatei  
 Der erste Teil des Erstellens eines [!INCLUDE[tsql](../../includes/tsql-md.md)]-Codeausschnitts besteht darin, eine XML-Datei mit dem Text des Codeausschnitts zu erstellen. Die Datei muss die Dateierweiterung SNIPPET aufweisen und die Anforderungen des [Codeausschnittschemas](http://go.microsoft.com/fwlink/?LinkId=207504)erfüllen. Legen Sie die Ausschnittsprache auf SQL fest.  
  
 Sie können die vordefinierten Ausschnitte, die im Lieferumfang von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthalten sind, als Beispiele verwenden. Um die vordefinierten Ausschnitte zu suchen, öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], wählen Sie das Menü **Extras** aus, und klicken Sie auf **Codeausschnitt-Manager**. Wählen Sie im Listenfeld **Sprache** die Option **SQL** aus; der Pfad zu den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Ausschnitten wird im Feld **Speicherort** angezeigt.  
  
## Registrieren des Codeausschnitts  
 Verwenden Sie nach dem Erstellen der Ausschnittdatei den Codeausschnitt-Manager, um den Ausschnitt bei [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]zu registrieren. Sie können entweder einen Ordner hinzufügen, der mehrere Ausschnitte enthält, oder einzelne Ausschnitte in den Ordner **Eigene Codeausschnitte** importieren.  
  
## Vorgehensweisen  
  
#### Hinzufügen eines Ausschnittordners  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Wählen Sie das Menü **Extras** aus, und klicken Sie auf **Codeausschnitt-Manager**.  
  
3.  Klicken Sie auf die Schaltfläche **Hinzufügen** .  
  
4.  Navigieren Sie zum Ordner, der die Codeausschnitte enthält, und klicken Sie auf die Schaltfläche **Ordner auswählen** .  
  
#### Importieren eines Ausschnitts  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Wählen Sie das Menü **Extras** aus, und klicken Sie auf **Codeausschnitt-Manager**.  
  
3.  Klicken Sie auf die Schaltfläche **Importieren** .  
  
4.  Navigieren Sie zum Ordner, der den Ausschnitt enthält, klicken Sie auf die SNIPPET-Datei, und klicken Sie auf die Schaltfläche **Öffnen** .  
  
## Beispiele  
 Im folgenden Beispiel wird ein **TRY-CATCH**-Umschließungsausschnitt erstellt und in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] importiert.  
  
1.  Fügen Sie den folgenden Code in Editor ein, speichern Sie die Datei dann unter dem Namen "TryCatch.snippet".  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
    <_locDefinition xmlns="urn:locstudio">  
        <_locDefault _loc="locNone" />  
        <_locTag _loc="locData">Title</_locTag>  
        <_locTag _loc="locData">Description</_locTag>  
        <_locTag _loc="locData">Author</_locTag>  
        <_locTag _loc="locData">ToolTip</_locTag>  
       <_locTag _loc="locData">Default</_locTag>  
    </_locDefinition>  
    <CodeSnippet Format="1.0.0">  
    <Header>  
    <Title>TryCatch</Title>  
                            <Shortcut></Shortcut>  
    <Description>Example Snippet for Try-Catch.</Description>  
    <Author>SQL Server Books Online Example</Author>  
    <SnippetTypes>  
                                    <SnippetType>SurroundsWith</SnippetType>  
    </SnippetTypes>  
    </Header>  
    <Snippet>  
    <Declarations>  
                                    <Literal>  
                                    <ID>CatchCode</ID>  
                                    <ToolTip>Code to handle the caught error</ToolTip>  
                                    <Default>CatchCode</Default>  
                                    </Literal>  
    </Declarations>  
    <Code Language="SQL"><![CDATA[  
    BEGIN TRY  
  
    $selected$ $end$  
  
    END TRY  
    BEGIN CATCH  
  
    $CatchCode$  
  
    END CATCH;  
    ]]>  
    </Code>  
    </Snippet>  
    </CodeSnippet>  
    </CodeSnippets>  
    ```  
  
2.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
3.  Wählen Sie das Menü **Extras** aus, und klicken Sie auf **Codeausschnitt-Manager**.  
  
4.  Klicken Sie auf die Schaltfläche **Importieren** .  
  
5.  Navigieren Sie zum Ordner, der die Datei "TryCatch.snippet" enthält, klicken Sie auf die Datei "TryCatch.snippet", und klicken Sie auf die Schaltfläche **Öffnen** . Im Ordner **Eigene Codeausschnitte** sollte kein TryCatch-Ausschnitt vorhanden sein.  
  
## Siehe auch  
 [Einfügen von Transact-SQL-Umschließungsausschnitten](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  