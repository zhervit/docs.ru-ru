---
ms.openlocfilehash: a4e20e0468d861138ad801c9dbfa15340b3f388c
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394012"
---
### <a name="authentication-oauthhandler-exchangecodeasync-signature-changed"></a><span data-ttu-id="12f1f-101">Аутентификация. Изменение подписи OAuthHandler ExchangeCodeAsync</span><span class="sxs-lookup"><span data-stu-id="12f1f-101">Authentication: OAuthHandler ExchangeCodeAsync signature changed</span></span>

<span data-ttu-id="12f1f-102">В ASP.NET Core 3.0 сигнатура `OAuthHandler.ExchangeCodeAsync` была изменена с:</span><span class="sxs-lookup"><span data-stu-id="12f1f-102">In ASP.NET Core 3.0, the signature of `OAuthHandler.ExchangeCodeAsync` was changed from:</span></span>

```csharp
protected virtual System.Threading.Tasks.Task<Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse> ExchangeCodeAsync(string code, string redirectUri) { throw null; }
```

<span data-ttu-id="12f1f-103">В:</span><span class="sxs-lookup"><span data-stu-id="12f1f-103">To:</span></span>

```csharp
protected virtual System.Threading.Tasks.Task<Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse> ExchangeCodeAsync(Microsoft.AspNetCore.Authentication.OAuth.OAuthCodeExchangeContext context) { throw null; }
```

#### <a name="version-introduced"></a><span data-ttu-id="12f1f-104">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="12f1f-104">Version introduced</span></span>

<span data-ttu-id="12f1f-105">3.0</span><span class="sxs-lookup"><span data-stu-id="12f1f-105">3.0</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="12f1f-106">Старое поведение</span><span class="sxs-lookup"><span data-stu-id="12f1f-106">Old behavior</span></span>

<span data-ttu-id="12f1f-107">Строки `code` и `redirectUri` передавались как отдельные аргументы.</span><span class="sxs-lookup"><span data-stu-id="12f1f-107">The `code` and `redirectUri` strings were passed as separate arguments.</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="12f1f-108">Новое поведение</span><span class="sxs-lookup"><span data-stu-id="12f1f-108">New behavior</span></span>

<span data-ttu-id="12f1f-109">`Code` и `RedirectUri` являются свойствами `OAuthCodeExchangeContext`, которые можно задать с помощью конструктора `OAuthCodeExchangeContext`.</span><span class="sxs-lookup"><span data-stu-id="12f1f-109">`Code` and `RedirectUri` are properties on `OAuthCodeExchangeContext` that can be set via the `OAuthCodeExchangeContext` constructor.</span></span> <span data-ttu-id="12f1f-110">Новый тип `OAuthCodeExchangeContext` — это единственный аргумент, передаваемый в `OAuthHandler.ExchangeCodeAsync`.</span><span class="sxs-lookup"><span data-stu-id="12f1f-110">The new `OAuthCodeExchangeContext` type is the only argument passed to `OAuthHandler.ExchangeCodeAsync`.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="12f1f-111">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="12f1f-111">Reason for change</span></span>

<span data-ttu-id="12f1f-112">Это изменение позволяет предоставлять дополнительные параметры без критических изменений.</span><span class="sxs-lookup"><span data-stu-id="12f1f-112">This change allows additional parameters to be provided in a non-breaking manner.</span></span> <span data-ttu-id="12f1f-113">Создавать новые перегрузки `ExchangeCodeAsync` не нужно.</span><span class="sxs-lookup"><span data-stu-id="12f1f-113">There's no need to create new `ExchangeCodeAsync` overloads.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="12f1f-114">Рекомендуемое действие</span><span class="sxs-lookup"><span data-stu-id="12f1f-114">Recommended action</span></span>

<span data-ttu-id="12f1f-115">Создайте `OAuthCodeExchangeContext` с соответствующими значениями `code` и `redirectUri`.</span><span class="sxs-lookup"><span data-stu-id="12f1f-115">Construct an `OAuthCodeExchangeContext` with the appropriate `code` and `redirectUri` values.</span></span> <span data-ttu-id="12f1f-116">Необходимо указать экземпляр <xref:Microsoft.AspNetCore.Authentication.AuthenticationProperties>.</span><span class="sxs-lookup"><span data-stu-id="12f1f-116">An <xref:Microsoft.AspNetCore.Authentication.AuthenticationProperties> instance must be provided.</span></span> <span data-ttu-id="12f1f-117">Этот единственный `OAuthCodeExchangeContext` экземпляр можно передать в `OAuthHandler.ExchangeCodeAsync`, а не в несколько аргументов.</span><span class="sxs-lookup"><span data-stu-id="12f1f-117">This single `OAuthCodeExchangeContext` instance can be passed to `OAuthHandler.ExchangeCodeAsync` instead of multiple arguments.</span></span>

#### <a name="category"></a><span data-ttu-id="12f1f-118">Категория</span><span class="sxs-lookup"><span data-stu-id="12f1f-118">Category</span></span>

<span data-ttu-id="12f1f-119">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="12f1f-119">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="12f1f-120">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="12f1f-120">Affected APIs</span></span>

<xref:Microsoft.AspNetCore.Authentication.OAuth.OAuthHandler%601.ExchangeCodeAsync(System.String,System.String)?displayProperty=nameWithType>

<!--

#### Affected APIs

`M:Microsoft.AspNetCore.Authentication.OAuth.OAuthHandler`1.ExchangeCodeAsync(System.String,System.String)`

-->