---
title: '@@DBTS (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@DBTS_TSQL'
- '@@DBTS'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@DBTS function'
- timestamp data type
ms.assetid: 91842ddd-91c0-4445-a03f-116f6bc991d0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 22d4089ac34ce7a1c4f08d1f289d2ea534ee221f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747448"
---
# <a name="x40x40dbts-transact-sql"></a>&#x40;&#x40;DBTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Diese Funkion gibt den aktuellen Wert vom Datentyp **timestamp** für die aktuelle Datenbank zurück. Die aktuelle Datenbank hat auf jeden Fall einen eindeutigen timestamp-Wert.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>Rückgabetypen
**varbinary**
  
## <a name="remarks"></a>Remarks  
@@DBTS gibt den zuletzt verwendeten Timestampwert der aktuellen Datenbank zurück. Ein neuer Timestampwert wird generiert, wenn eine Zeile mit einer **timestamp**-Spalte eingefügt oder aktualisiert wird.
  
Die Funktion @@DBTS ist nicht von Änderungen der Transaktionsisolationsstufen betroffen.
  
## <a name="examples"></a>Beispiele  
In diesem Beispiel wird der aktuelle **timestamp**-Wert aus der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>Siehe auch
[Configuration Functions &#40;Transact-SQL&#41; (Konfigurationsfunktionen (Transact-SQL))](../../t-sql/functions/configuration-functions-transact-sql.md)  
[Cursor Concurrency &#40;ODBC&#41; (Cursorparallelität (ODBC))](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  
