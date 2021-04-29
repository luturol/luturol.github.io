---
layout: post
title: How to configure Application Insights in .Net 5
date:   2021-04-29 09:50:40
categories: 
- csharp
- azure
---

## How to configure Azure Applications Insights on .Net 5

Application insights is a wonderful tool to help you track log, see performance issues and application map. It's more like CloudWatch on AWS.


First you need to download two packages from nuget to start.

1. [Microsoft.ApplicationInsights.AspNetCore](https://www.nuget.org/packages/Microsoft.ApplicationInsights.AspNetCore)

1. [Microsoft.Extensions.Logging.ApplicationInsights](https://www.nuget.org/packages/Microsoft.Extensions.Logging.ApplicationInsights)

```bash
dotnet add package Microsoft.ApplicationInsights.AspNetCore --version 2.17.0
dotnet add package Microsoft.Extensions.Logging.ApplicationInsights --version 2.17.0
```

After that you need to initialize the configurations from application inights on Statup.cs and Program.cs


On Startup.cs, you need to add the service dependency.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddApplicationInsightsTelemetry();

    //others dependencies
}
```

On Program.cs, you need to set the Log Level and your Instrumentation Key.

```csharp
public static IHostBuilder CreateHosBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureLogging(logging =>
        {
            logging.AddApplicationInsights("your-instrumentation-key");
            logging.AddFilter<ApplicationINsightsLoggerProvider>("", LogLevel.Trace);
        })
        .ConfigureWebHostDefaults(webBuilder => 
        {
            webBuilder.UseStartup<Startup>();
        });
```

Now you can use ILogger to create logs on Azure Application Insights.


Don't forget to eat clean and drink water.

Peace!!

