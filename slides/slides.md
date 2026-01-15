---
marp: true
theme: custom
size: 16:9
footer: 'Andy Lech - Build Better Mobile Apps with ReactiveUI'
paginate: true
---

<!-- @@@ Talk Title @@@ -->

<!-- _footer: "" -->
<!-- _paginate: skip -->

<!-- _class: talk_title invert -->

# Build Better Mobile Apps with ReactiveUI

<p />

## Andy Lech

---

<!-- @@@ Sponsors @@@ -->

<!-- _footer: "" -->
<!-- _paginate: skip -->

![height:640px](./images/sponsors/2026-Code-Mash-Sponsors.png)

---

<!-- @@@ Orlando Code Camp @@@ -->

<!-- _footer: "" -->
<!-- _paginate: skip -->

![height:360px](./images/conferences/2026-Orlando-Code-Camp.png)

#### Seminole State College, Sanford, FL

[https://www.orlandocodecamp.com/](https://www.orlandocodecamp.com/)

---

<!-- @@@ Audience Questions @@@ -->

<!-- _footer: "" -->
<!-- _paginate: skip -->

<!-- _class: talk_topics -->

### Audience Polls

* Written a mobile or desktop app before?
* Used the MVVM pattern in their app?
* Used Reactive Extensions (Rx.NET) before?
* Used ReactiveUI (RxUI) or related libraries before?

---

<!-- @@@ Topics @@@ -->

<!-- _class: talk_topics -->

### Topics

* What is ReactiveUI?
* My Path to ReactiveUI
* Architecting for Smart Data Consumption
* How Reactive UI Helps

---

<!-- @@@ Section - What is ReactiveUI? @@@ -->

<!-- _class: section_title -->

## Part 1

<br />

### What is ReactiveUI?

---

<!-- @@@ History of ReactiveUI @@@ -->

<!-- _class: details_list -->

### ReactiveUI Ecosystem

- Reactive Extensions (Rx or Rx.NET) - [reactivex.io](https://reactivex.io/)
  An API for asynchronous programming with observable streams

- ReactiveUI (RxUI) - [www.reactiveui.net](https://www.reactiveui.net/)
  A composable Model-View-ViewModel framework for all .NET platforms!

- Dynamic Data - [github.com/reactivemarbles/DynamicData](https://github.com/reactivemarbles/DynamicData)
  A library for managing complex operation on collections through Rx.NET

- Refit - [reactiveui.github.io/refit](https://reactiveui.github.io/refit/)
  An automatic type-safe REST library for .NET Core, Xamarin and .NET

- Akavache - [github.com/reactiveui/Akavache](https://github.com/reactiveui/Akavache)
  An asynchronous Key-Value store for cross-platform applications

- Splat - [github.com/reactiveui/splat](https://github.com/reactiveui/splat)
  A cross-platform library for service location, unit testing, and logging

---

<!-- @@@ Reactive Extensions @@@ -->

<!-- _class: details -->

### Reactive Extensions

<div class="columns-two">

<div class="column">

<!-- _class: details_list -->

- Based on IObservable<T>
- Data is pushed to subscribers
- Subscribers hook into a pipeline
- Values can be processed like LINQ

</div>

<div>

```csharp
using System.Reactive.Linq;

IObservable<long> ticks =
  Observable.Timer(
    dueTime: TimeSpan.Zero(),
    period: TimeSpan.FromSeconds(1)
  );

ticks.Subscribe(
  tick => Console.WriteLine("$Tick {tick}");
)

Console.ReadLine();
```

</div>

</div>

---

<!-- @@@ ReactiveUI @@@ -->

<!-- _class: details -->

### ReactiveUI

<div class="columns-two">

<div class="column">

<!-- _class: details_list -->

- Light MVVM framework over Rx.NET
- Smart property-change notifications
- Control of thread scheduling
- Complex command functionality
- Supports ViewModel navigation
- Allow automatic data persistence

</div>

<div>

```csharp
this.WhenAnyValue(x => x.SearchQuery)
    .Throttle(TimeSpan.FromSeconds(0.8),
      RxApp.TaskpoolScheduler)
    .Select(query => query?.Trim())
    .DistinctUntilChanged()
    .Where(query =>
      !string.IsNullOrWhiteSpace(query))
    .ObserveOn(RxApp.MainThreadScheduler)
    .InvokeCommand(ExecuteSearch);
```

</div>

</div>

---

<!-- @@@ My Path to ReactiveUI @@@ -->

<!-- _class: details_list -->

### My Path to ReactiveUI

- 2009 - Reactive Extensions released by Microsoft

- Early 2011 - ReactiveUI created

- May 2014 - Xamarin.Forms launched

- August 2015 - Hired to create apps for Android, iOS, Windows Phone

- Late 2015 - Started using Refit for API mapping and Akavache for caching

- Early 2016 - Started using VM navigation library derived from ReactiveUI

- May 2020 - .NET MAUI announced

- September 2020 - Saw Michael Stonis talk on ReactiveUI

- October 2020 - Started using RxUI for VM navigation, testing, and more

- May 2022 - .NET MAUI released

---

<!-- @@@ Section 2 - Architecture @@@ -->

<!-- _class: section_title -->

## Part 2

<br />

### Architecting for Smart Data Consumption

---

<!-- @@@ Data and Testing Perspectives @@@ -->

<!-- _class: details -->

### Perspectives on Data and Testing

<!-- Images -->

<div class="columns-three">

<div class="column">

![width:400px](./images/houses/isometric-house-profile-concept/17395.jpg)

</div>

<div class="column">

![width:300px](./images/houses/plumbing-problems-solution-isometric-infographic-poster/17767.jpg)

</div>

<div class="column">

![width:400px](./images/houses/smart-home-energy-generation-isometric-poster/16696.jpg)

</div>

</div>

<!-- Labels -->

<div class="columns-three">

<div class="column">

#### User

</div>

<div class="column">

#### Web Site

</div>

<div class="column">

#### Mobile App

</div>

---

<!-- @@@ Mobile Architecture - Components @@@ -->

### Mobile Architecture - Components

<!-- _class: details -->

![width:1100px](./images/architecture/mobile-components.drawio.svg)

<div class="detail-summary">

- App handles interactivity, page layouts, local caching, and API calls
- API stack delivers only data or status codes in response to app requests
- App pages tend to be focused on single tasks that call the API selectively
- <b>Mobile/API devs focus more on reliable, just-in-time data delivery</b>

</div>

---

<!-- @@@ MVVM Architecture @@@ -->

<!-- _class: details -->

## MVVM Pattern - Theory

<br />

![width:1000px](./images/architecture/MVVM%20Pattern%20-%20Wikipedia.svg)

<div class="attribution">
    <a href="https://en.wikipedia.org/wiki/File:MVVMPattern.svg">
    Image from Wikipedia</a>
</div>

<br />

---

<!-- @@@ Mobile Architecture - Real World @@@ -->

<!-- _class: details -->

## Mobile Architecture - Real-world

| Component | Architecture | Purpose |
| - | - | - |
| Page Layouts | Views | Presentation |
| Navigation Logic | ViewModels | Navigation Router |
| Code Behind | ViewModels | Presentation Logic |
| Code Behind | ViewModels | Data Manipulation Logic |
| Local Caches | Data Service | Data Source Logic |
| Data Access | API Services | Data Translation Logic |
| Data Access | Models | Internal Data Definitions |
| Data Access | Data Transfer Objects | External Data Definitions |

---

<!-- @@@ Mobile Architecture - Network @@@ -->

<!-- _class: details -->

## Mobile Architecture - Network

<br />

![width:1100px](./images/architecture/mobile-real-world-network.drawio.svg)

---

<!-- @@@ Mobile Architecture - Solution @@@ -->

<!-- _class: details -->

## Mobile Architecture - Solution

<br />

![width:1100px](./images/architecture/mobile-real-world-solution.drawio.svg)

---

<!-- @@@ Section - What is ReactiveUI? @@@ -->

<!-- _class: section_title -->

## Part 3

<br />

### How Reactive UI Helps

---

<!-- @@@  @@@ -->

<!-- _class: details -->

### Login - XAML

```xml
    <VerticalStackLayout Grid.Row="1" Spacing="6">
      <Label Text="First Name" TextColor="{StaticResource PrimaryDarkText}" />
      <Entry x:Name="FirstName"
        TextChanged="Entry_OnTextChanged"
        TextColor="{StaticResource Primary}" />
    </VerticalStackLayout>
    <VerticalStackLayout Grid.Row="2" Spacing="6">
      <Label Text="Last Name" TextColor="{StaticResource PrimaryDarkText}" />
      <Entry x:Name="LastName"
        TextChanged="Entry_OnTextChanged"
        TextColor="{StaticResource Primary}" />
    </VerticalStackLayout>
    <Button x:Name="LoginButton"
      BackgroundColor="{StaticResource Tertiary}"
      Clicked="LoginButton_OnClicked"
      IsEnabled="False"
      Text="Login"
      TextColor="{StaticResource White}" />

```

---

<!-- @@@  @@@ -->

<!-- _class: details -->

### .NET - Event Handlers

```csharp
    private void Entry_OnTextChanged(object? sender, TextChangedEventArgs e)
    {
        LoginButton.IsEnabled =
            !IsNullOrWhiteSpace(FirstName.Text)
            && !IsNullOrWhiteSpace(LastName.Text);
    }

    private async void LoginButton_OnClicked(object? sender, EventArgs e)
    {
        var firstName = FirstName.Text;
        if (Users.TryGetValue(firstName, out var lastName))
        {
            if (lastName == LastName.Text)
            {
                UnauthenticatedMessage.IsVisible = false;
                var homePageRoute = $"home?firstName={firstName}&lastName={lastName}";
                await Shell.Current.GoToAsync(homePageRoute, animate: true);
            }
        }
        UnauthenticatedMessage.IsVisible = true;
    }
```

---

<!-- @@@  @@@ -->

<!-- _class: details -->

### ReactiveUI - Property Assignment

```csharp
public class ViewModel : ReactiveObject {
    [Reactive] public string FirstName { get; set; }
    [Reactive] public string LastName { get; set; }

    public string FormattedName { [ObservableAsProperty] get; }

    public BetterViewModel()
    {
      this.WhenAnyValue(
          vm => vm.FirstName,
          vm => vm.LastName,
          (first, last) => $"{last}, {first}")
        .ToPropertyEx(this, x => x.FormattedName);
    }
  }
```

---

<!-- @@@  @@@ -->

<!-- _class: details -->

### ReactiveUI - Commands

```csharp
ReactiveCommand
  .CreateFromTask(
    async () =>
    {
      this.Log().Info("Starting Login");
      var result = await ProcessLogin();
      this.Log().Info($"Finished Login");
      return result;
    },
    this.WhenAnyValue(x => x.Username, x => x.Password,
      (username, password) =>
        !string.IsNullOrWhiteSpace(username) &&
        !string.IsNullOrWhiteSpace(password)));
```

---

<!-- @@@ Dynamic Data @@@ -->

<!-- _class: details -->

### Dynamic Data

```csharp
ReadOnlyObservableCollection<TradeProxy> list;

var myTradeCache = new SourceCache<Trade, long>(trade => trade.Id);
var myOperation = myTradeCache.Connect()
  .Filter(trade=>trade.Status == TradeStatus.Live)
  .Transform(trade => new TradeProxy(trade))
  .Sort(SortExpressionComparer<TradeProxy>.Descending(t => t.Timestamp))
  .ObserveOnDispatcher()
  .Bind(out list)
  .DisposeMany()
  .Subscribe();
```

---

<!-- @@@ Refit @@@ -->

<!-- _class: details -->

### Refit

```csharp
public interface IGitHubApi
{
    [Get("/users/{user}")]
    Task<User> GetUser(string user,
      [Authorize("Bearer")] string token);
}

var gitHubApi = RestService.For<IGitHubApi>("https://api.github.com");

// Will add the header "Authorization: Bearer OAUTH-TOKEN}" to the request
var octocat = await gitHubApi.GetUser("octocat", "OAUTH-TOKEN");

```

---

<!-- @@@ Akavache @@@ -->

<!-- _class: details -->

### Akavache

```csharp
// Store an object
var user = new User { Name = "John", Email = "john@example.com" };
await CacheDatabase.UserAccount.InsertObject("current_user", user);

// Retrieve an object
var cachedUser =
  await CacheDatabase.UserAccount.GetObject<User>("current_user");

// Store with expiration
await CacheDatabase.LocalMachine.InsertObject("temp_data",
  someData, DateTimeOffset.Now.AddHours(1));

// Get or fetch pattern
var data =
  await CacheDatabase.LocalMachine.GetOrFetchObject("api_data",
    async () => await httpClient.GetFromJsonAsync<ApiResponse>(
      "https://api.example.com/data"));
```

---

<!-- @@@ Splat @@@ -->

<!-- _class: details -->

### Splat

- Service Locator

```csharp
// Register services at application startup
Locator.CurrentMutable.Register<IToaster>(() => new Toaster());
Locator.CurrentMutable.RegisterConstant<IConfiguration>(myConfig);
Locator.CurrentMutable.RegisterLazySingleton<ILogger>(() => new FileLogger());

// Resolve services anywhere in your application
var toaster = Locator.Current.GetService<IToaster>();
var config = Locator.Current.GetService<IConfiguration>();
```

---

<!-- @@@ Page - References @@@ -->

<!-- _class: references_list -->

### References

<div class="columns-two-5ths-4-1">

<div class="column-4-5ths">

##### Media

- [Rx.NET in Action](https://www.manning.com/books/rx-dot-net-in-action) by Tamir Dresher (Manning)

- [You, I, and ReactiveUI](https://kent-boogaart.com/you-i-and-reactiveui/) by Kent Boogart (self-published)

- Michael Stonis - Rx, RxUI, and Xamarin.Forms (2 PDFs)

  [github.com/TheEightBot/Reactive-Examples](https://github.com/TheEightBot/Reactive-Examples)

##### Frameworks

- Reactive Extensions (Rx) - [reactivex.io](https://reactivex.io/)

- ReactiveUI (RxUI) - [www.reactiveui.net](https://www.reactiveui.net/)

- Refit - [reactiveui.github.io/refit](https://reactiveui.github.io/refit/)

- Akavache - [github.com/reactiveui/Akavache](https://github.com/reactiveui/Akavache)

- Splat - [github.com/reactiveui/splat](https://github.com/reactiveui/splat)

- Dynamic Data - [github.com/reactivemarbles/DynamicData](https://github.com/reactivemarbles/DynamicData)

</div>

<div class="column-1-5th">

![height:240px](./images/books/Dresher-Rx.NET-in-ActionI.png)

![height:240px](./images/books/Boogart-You,%20I,%20and%20ReactiveUI.png)

</div>

<span class="break" />

</div>
