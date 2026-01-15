---
marp: true
theme: custom
size: 16:9
footer: 'Andy Lech - Build Better Mobile Apps with ReactiveUI'
paginate: true
---

<!-- @@@ Page - Talk Title @@@ -->

<!-- _footer: "" -->
<!-- _paginate: skip -->

<!-- _class: talk_title invert -->

# Build Better Mobile Apps with ReactiveUI

<p />

## Andy Lech

---

<!-- @@@ Page - Sponsors @@@ -->

<!-- ![height:550px](./images/conferences/) -->

<!-- --- -->

<!-- @@@ Topics @@@ -->

<!-- _class: talk_topics -->

### Topics

- My Path to ReactiveUI
- Architecting for Smart Data Consumption
- How Reactive UI Helps
- References
- Questions

---

<!-- @@@ Section 1 @@@ -->

<!-- _class: section_title -->

## Part 1

<br />

### My Path to ReactiveUI

---

<!-- @@@ History of ReactiveUI @@@ -->

<!-- _class: details_list -->

### ReactiveUI Ecosystem

- Reactive Extensions (Rx or Rx.NET) - [reactivex.io](https://reactivex.io/)
  An API for asynchronous programming with observable streams

- ReactiveUI (RxUI) - [www.reactiveui.net](https://www.reactiveui.net/)
  A composable Model-View-ViewModel framework for all .NET platforms!

- Refit - [reactiveui.github.io/refit](https://reactiveui.github.io/refit/)
  An automatic type-safe REST library for .NET Core, Xamarin and .NET

- Akavache - [github.com/reactiveui/Akavache](https://github.com/reactiveui/Akavache)
  An asynchronous Key-Value store for cross-platform applications

- Splat - [github.com/reactiveui/splat](https://github.com/reactiveui/splat)
  A cross-platform library for service location, unit testing, and logging

- Dynamic Data - [github.com/reactivemarbles/DynamicData](https://github.com/reactivemarbles/DynamicData)
  A library for managing complex operation on collections through Rx.NET

---

<!-- @@@ My Mobile Background @@@ -->

<!-- _class: details_list -->

### A Mobile History

- 2008 or 2009 (?) - Reactive Extensions created by Microsoft

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

<!-- @@@ Section 2 @@@ -->

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

![width:400px](./images/isometric-house-profile-concept/17395.jpg)

</div>

<div class="column">

![width:300px](./images/plumbing-problems-solution-isometric-infographic-poster/17767.jpg)

</div>

<div class="column">

![width:400px](./images/smart-home-energy-generation-isometric-poster/16696.jpg)

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

<!-- @@@ Mobile Architecture - Simple @@@ -->

### Mobile Architecture - Simple

<!-- _class: details -->

![width:1100px](./images/mobile-apps-high-level.drawio.svg)

<div class="detail-summary">

- App handles interactivity, page layouts, local caching, and API calls
- API stack delivers only data or status codes in response to app requests
- App pages tend to be focused on single tasks that call the API selectively
- <b>Mobile/API devs focus more on reliable, just-in-time data delivery</b>

</div>

---

<!-- @@@ Mobile Apps - Components @@@ -->

<!-- _class: details -->

### Mobile Apps - Components

<div class="columns-two">

<div>

#### _App (Client)_

- Requests: API Calls
- State Management: ViewModels, Cache
- Data Mapping: API to App
- Caching: Platform, Local DB
- Resiliency: Network State
- <b>Dev Focus: Interactivity, Data Updates, Layouts, State, API Calls</b>
- <b>Data Goal: Smart Data Pipes (to API)</b>

</div>

<div>

#### _API (Server/Cloud)_

- Responses: Data (JSON/XML)
- State Management: Auth Tokens
- Data Mapping: Source to API
- Caching: Server/Cloud
- Resiliency: Server/Cloud, Services
- <b>Dev Focus: Data, Status Codes, Messages</b>
- <b>Data Goal: Smart Data Pipes (from App)</b>

</div>

</div>

---

<!-- @@@ Mobile Architecture - Real World (Network) @@@ -->

<!-- _class: details -->

## Mobile Architecture - Real-world

<div style="padding: 20px 0px;">

- ViewModels
  - Moving navigation out of the View allows ViewModels to be tested individually with frameworks like ReactiveUI (RxUI)
- Api Services
  - Individually testable to return app Models and not just Data Transfer Objects (DTOs)
- Data Service
  - Decides whether to call the local cache DB, the platform cache, an API endpoint, or a service based on the requested data and the app lifecycle

</div>

---

<!-- @@@ Mobile Architecture - MVVM @@@ -->

<!-- _class: details -->

## Mobile Architecture - MVVM

<br />

![width:1100px](./images/archtecture/MVVM%20Pattern%20-%20Wikipedia.svg)

---

<!-- @@@ Mobile Architecture - Network @@@ -->

<!-- _class: details -->

## Mobile Architecture - Network

<br />

![width:1100px](./images/mobile-apps-real-world-network.drawio.svg)

---

<!-- @@@ Mobile Architecture - Solution @@@ -->

<!-- _class: details -->

## Mobile Architecture - Solution

<br />

![width:1100px](./images/mobile-apps-real-world-solution.drawio.svg)

---

<!-- @@@ Mobile Architecture - Testing @@@ -->

<!-- _class: details -->

## Mobile Architecture - Testing

<br />

![width:1100px](./images/mobile-apps-real-world-testing.drawio.svg)

---

<!-- @@@ Section 3 @@@ -->

<!-- _class: section_title -->

## Part 3

<br />

### How ReactiveUI can Help

---

<!-- @@@ Mobile Architecture - Solution @@@ -->

<!-- _class: details -->

### Reactive Extensions

<br />

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

<!-- @@@  @@@ -->

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

<!-- @@@  @@@ -->

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

<!-- @@@  @@@ -->

<!-- _class: details -->

### Refit

```csharp
public interface IGitHubApi
{
    [Get("/users/{user}")]
    Task<User> GetUser(string user);
}

var gitHubApi = RestService.For<IGitHubApi>("https://api.github.com");
var octocat = await gitHubApi.GetUser("octocat");
```

---

<!-- @@@  @@@ -->

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

<!-- @@@ Section 5 @@@ -->

<!-- _class: section_title -->

## Part 4

<br />

### References

---

<!-- @@@ Page - References @@@ -->

<!-- _class: references_list -->

### References

<div class="columns-two-5ths-4-1">

<div class="column-4-5ths">

##### Presentations

- Michael Stonis - Rx, RxUI, and Xamarin.Forms (2 PDFs)

  [github.com/TheEightBot/Reactive-Examples](https://github.com/TheEightBot/Reactive-Examples)

##### Books

- [Rx.NET in Action](https://www.manning.com/books/rx-dot-net-in-action) by Tamir Dresher (Manning)

- [You, I, and ReactiveUI](https://kent-boogaart.com/you-i-and-reactiveui/) by Kent Boogart (self-published)

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

---

<!-- @@@ Section 5 @@@ -->

<!-- _class: section_title -->

## Part 5

<br />

### Questions?
