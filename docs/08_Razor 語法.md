

元件實作於 Razor 檔(`.razor`)，Razor 檔是由 `C#` 和 `HTML` 標籤組合而成，所以第一步我們需要來了解 `Razor` 怎麼寫。

### Razor 語法介紹

Razor 語法使用 `@` 符號將 `HTML` 檔案轉譯成 `C#`，Razor 會評估 `C#` 運算式並輸出成 `HTML`。 

當 `@` 符號後面接著 Razor 保留關鍵字時，它會轉換為 Razor 特定的標記，否則會轉換成一般 C#。

若要 `@` 在標記中將符號進行 escape Razor ，請使用第二個 @ 符號：

```csharp
<p>@@文字</p>
```

HTML 屬性及含有電子郵件地址的內容不會將 `@` 符號視為轉換字元，下列範例中的電子郵件地址不會藉由剖析而改變 Razor ：

```csharp
<a href="mailto:mio093611@gmail.com">mio093611@gmail.com</a>
```

### 隱含 Razor 運算式

隱含 Razor 運算式的開頭 @ 是 c # 程式碼：

```csharp
<p>@DateTime.Now</p>
```

除了 C# await 關鍵字以外，隱含運算式不能包含空格。

```csharp
<p>@await DoSomethingAsync()</p>
```

如果 C# 陳述式具有明確的結束字元，則可以混合空格：

```csharp
<p>@DoSomething(1, 2)</p>
```

隱含運算式**不能**包含 C# 泛型，因為括弧 (<>) 內的字元會解譯為 HTML 標籤。 下列程式碼無效：

```csharp
<p>@GenericMethod<int>()</p>
```

泛型方法呼叫必須包裝在明確的 Razor 運算式或程式 Razor 代碼區塊中。

### 明確 Razor 運算式

明確 Razor 運算式是由 @ 具有對稱括弧的符號所組成。

若要轉譯上周的時間，請 Razor 使用下列標記：

```csharp
<p>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))</p>
```

@() 括弧內的任何內容都會經過評估並轉譯成輸出。

也可以使用`{}`表示程式碼區塊如

```csharp
@{
    var joe = new Person("Joe", 33);
}

<p>Age@(joe.Age)</p>
```

若沒有明確運算式，`<p>Age@joe.Age</p>`會視為電子郵件地址，並轉譯 <p>Age@joe.Age</p>。當撰寫為明確運算式時，會轉譯 <p>Age33</p>。

您可以使用明確運算式，透過 .cshtml 檔案中的泛型方法轉譯輸出。下列標記會顯示如何修正稍早顯示的錯誤，此錯誤是由 C# 泛型的括弧所造成。 程式碼會撰寫為明確運算式：

```csharp
<p>@(GenericMethod<int>())</p>
```

### 程式碼區塊

在程式碼區塊中，使用標記宣告區域函式作為樣板化方法：

```csharp
@{
    void RenderName(string name)
    {
        <p>Name: <strong>@name</strong></p>
    }

    RenderName("Mahatma Gandhi");
    RenderName("Martin Luther King, Jr.");
}
```

程式碼會轉譯下列 HTML：

```csharp
<p>Name: <strong>Mahatma Gandhi</strong></p>
<p>Name: <strong>Martin Luther King, Jr.</strong></p>
```

雖然程式碼區塊中的預設語言是 C#，但是如果在區塊內使用 HTML 標籤，則會自動轉回 HTML：

```csharp
@{
    var inCSharp = true;
    <p>Now in HTML, was in C# @inCSharp</p>
}
```

若使用 HTML 標籤會破壞 HTML 結構，可以使用 `@:` 來進行單行轉換：

```csharp
@{
    var inCSharp = true;
    @:Now in HTML, was in C# @inCSharp
}
```

或使用 `<text>` 標籤來進行多行轉換：

```csharp
@{
    var inCSharp = true;
    <text>
        Now in HTML, was in C# @inCSharp
    </text>
}
```