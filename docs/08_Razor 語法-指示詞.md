
分成兩大類，指示詞與指示詞屬性，



#### @attribute

`@attribute` 指示詞針對頁面增加屬性。

```csharp
@attribute [Authorize]
```

使該頁面增加 [Authorize] 屬性。

#### @code

`@code` 指示詞針對頁面增加成員(欄位、屬性和方法)。

```csharp
@code {
  private int currentCount = 0;
}
```

使該頁面增加私有數字欄位`currentCount`，且初始值為`0`。

#### @function

`@functions` 指示詞針對頁面增加成員(欄位、屬性和方法)。

疑～怎麼重複了？因為 `@code` 和 `@functions` 真的是一樣的作用，為了使程式碼語意更清楚，官方建議加入欄位或屬性使用 `@code`，而加入方法則使用 `@functions`。

```csharp
@functions{
   private void IncrementCount()
    {
        currentCount++;
    }
}
```

使該頁面增加私有方法`IncrementCount`，並與剛剛增加的`currentCount`欄位互動。

#### @implements 

`@implements` 指示詞針對頁面加入需實作的介面。

```csharp
@implements IDisposable

@functions {
    private bool _isDisposed;

    // ...

    public void Dispose() => _isDisposed = true;
}
```

使該頁面必須實作`IDisposable`介面的方法。

#### @inherits

`@inherits` 指示詞針對頁面加入繼承的父類。

先新增 `CustomRazorPage.razor` 檔案，並加入內容。

```csharp
@code {
    public string CustomText = "嗨嗨，我是米歐。";
}
```

```csharp
@inherits CustomRazorPage

<p>@CustomText</p>
```

使該頁面能夠使用父類`CustomRazorPage`內所能存取的成員。

#### @inject

`@inject` 指示詞針對頁面注入對應服務。

```csharp
@inject HttpClient httpClient
```

使該頁面能夠從 DI 容器中取得`HttpClient`實體。

後續文章將針對**相依性注入**詳細介紹。

#### @layout

`@layout` 指示詞針對頁面加入版面配置元件。

```csharp
@layout MainLayout
```

使該頁面增加`MainLayout`版面配置。

後續文章將針對**版面配置**詳細介紹。

#### @page

`@page` 指示詞設定頁面路由。

```
@page "/counter"
```

使該頁面的進入點為`/counter`。

後續文章將針對**路由**詳細介紹。

#### @using

`@using` 指示詞針對頁面加入其他命名空間的別名。

```csharp
@using System;
```

使該頁面能夠直接瀏覽`System`命名空間。



* https://docs.microsoft.com/zh-tw/aspnet/core/mvc/views/razor?view=aspnetcore-3.1#directives