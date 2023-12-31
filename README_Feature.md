<!-- 
Everything in here is of course optional. If you want to add/remove something, absolutely do so as you see fit.
This example README has some dummy APIs you'll need to replace and only acts as a placeholder for some inspiration that you can fill in with your own functionalities.
-->
![](nuget.png)
# Plugin.Maui.Feature

`Plugin.Maui.Feature` provides the ability to do this amazing thing in your .NET MAUI application.

## プラグインをインストール / Install Plugin

[![NuGet](https://img.shields.io/nuget/v/Plugin.Maui.Feature.svg?label=NuGet)](https://www.nuget.org/packages/Plugin.Maui.Feature/)

Available on [NuGet](http://www.nuget.org/packages/Plugin.Maui.Feature).

Install with the dotnet CLI: `dotnet add package Plugin.Maui.Feature`, or through the NuGet Package Manager in Visual Studio.

### サポートする端末 / Supported Platforms

| 端末 / Platform | 最小バージョン要件 / Minimum Version Supported |
|----------|---------------------------|
| iOS      | 11+                       |
| macOS    | 10.15+                    |
| Android  | 5.0 (API 21)              |
| Windows  | 10(ビルド1809)以降, 11 / 11 and 10 version 1809+   |

## API利用 / API Usage

`Plugin.Maui.Feature` provides the `Feature` class that has a single property `Property` that you can get or set.

You can either use it as a static class, e.g.: `Feature.Default.Property = 1` or with dependency injection: `builder.Services.AddSingleton<IFeature>(Feature.Default);`

### 権限 / Permissions

Before you can start using Feature, you will need to request the proper permissions on each platform.

#### iOS

No permissions are needed for iOS.

#### Android

No permissions are needed for Android.

### 依存関係の追加 / Dependency Injection

You will first need to register the `Feature` with the `MauiAppBuilder` following the same pattern that the .NET MAUI Essentials libraries follow.

```csharp
builder.Services.AddSingleton(Feature.Default);
```

You can then enable your classes to depend on `IFeature` as per the following example.

```csharp
public class FeatureViewModel
{
    readonly IFeature feature;

    public FeatureViewModel(IFeature feature)
    {
        this.feature = feature;
    }

    public void StartFeature()
    {
        feature.ReadingChanged += (sender, reading) =>
        {
            Console.WriteLine(reading.Thing);
        };

        feature.Start();
    }
}
```

### 単純な利用 / Straight usage

Alternatively if you want to skip using the dependency injection approach you can use the `Feature.Default` property.

```csharp
public class FeatureViewModel
{
    public void StartFeature()
    {
        feature.ReadingChanged += (sender, reading) =>
        {
            Console.WriteLine(feature.Thing);
        };

        Feature.Default.Start();
    }
}
```

### 特徴 / Feature

Once you have created a `Feature` you can interact with it in the following ways:

#### イベント / Events

##### `ReadingChanged`

Occurs when feature reading changes.

#### 状態 / Properties

##### `IsSupported`

Gets a value indicating whether reading the feature is supported on this device.

##### `IsMonitoring`

Gets a value indicating whether the feature is actively being monitored.

#### 方法 / Methods

##### `Start()`

Start monitoring for changes to the feature.

##### `Stop()`

Stop monitoring for changes to the feature.

# 謝辞 / Acknowledgements

このプロジェクトは多くのプロジェクトによって成り立っています。ありがとうございます! / This project could not have came to be without these projects and people, thank you! <3
