# ZabbixSender.Core

ZabbixSender is a class library that allows you to send data to a Zabbix server.

## Sample to send a single value
```csharp
using System;
using Predes.ZabbixSender.Core;

namespace Predes.ZabbixSender.Samples
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var service = new SenderService("server.sample.com", 10051);
            var response = service.Send("monitored.sample.com", "metric", args[0]);

            Console.WriteLine($"Total: {response.Total} - Processed: {response.Processed} - Failed: {response.Failed}");
        }
    }
}
```

## Sample to send multiple values
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Predes.ZabbixSender.Core;

namespace Predes.ZabbixSender.Samples
{
    internal class Program
    {
        private static void SendList(Dictionary<string, string> values)
        {
            var service = new SenderService("server.sample.com", 10051);
            var data = values.Select(v => new SenderData {Host = "monitored.sample.com", Key = v.Key, Value = v.Value}).ToArray();
            var response = service.Send(data);

            Console.WriteLine($"Total: {response.Total} - Processed: {response.Processed} - Failed: {response.Failed}");
        }
    }
}
