# Server API

```csharp
namespace AltV.Net.Example
{
    public class SampleResource : IResource
    {
        public void OnStart()
        {
            Alt.On<string>("test", s => { Alt.Log("test=" + s); });
            
            Alt.On("test", args => { Alt.Log("args=" + args[0]); });
            
            Alt.Emit("test", "bla");
        }

        public void OnStop()
        {
        }
    }
}
```

## Events

## Vehicle

## Player

