---
title: Bestimmen, was unterstützt wird | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 835584da4c51f5e65306d0609b4e69f78a7d58b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707568"
---
# <a name="determining-what-is-supported"></a>Bestimmen der unterstützten Vorgänge
Die **unterstützt** Methode wird verwendet, um zu bestimmen, ob ein angegebenes **Recordset** Objekt unterstützt, eine bestimmte Art von Funktionalität. Es hat die folgende Syntax:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Hinweise  
 Die **unterstützt** Methode gibt einen booleschen Wert, der angibt, ob der Anbieter alle CursorOptions Argument identifizierten Funktionen unterstützt. Können Sie die **unterstützt** Methode, um zu bestimmen, welche Funktionalität einer **Recordset** -Objekt unterstützt. Wenn die **Recordset** Objekt unterstützt die Funktionen, deren entsprechenden Konstanten in sind *CursorOptions*, **unterstützt** Methodenrückgabe **"true"**. Andernfalls wird **"false"**.  
  
 Mithilfe der **unterstützt** -Methode, die Sie überprüfen können, für die Fähigkeit von der **Recordset** Objekt, das neue Datensätze hinzufügen, verwenden von Lesezeichen, verwenden Sie die **finden** verwenden Scrollen-Methode verwenden, die  **Index** -Eigenschaft, und zum Durchführen von BatchUpdates. Eine vollständige Liste von Konstanten und ihre Bedeutungen, finden Sie unter [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md).  
  
 Obwohl die **unterstützt** Methodenrückgabewert möglicherweise **"true"** für eine bestimmte Funktionalität, dies garantiert nicht, dass der Anbieter das Feature unter allen Umständen zur Verfügung stellen kann. Die **unterstützt** -Methode einfach zurückgegeben, ob der Anbieter unterstützt den angegebenen Funktionen können unter bestimmten Bedingungen erfüllt sind. Z. B. die **unterstützt** Methode hinweisen, die eine **Recordset** -Objekt unterstützt die Aktualisierung, auch wenn der Cursor auf einen Join mit mehreren Tabellen basiert – einige Spalten der sind nicht aktualisierbar.
